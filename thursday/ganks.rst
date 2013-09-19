=======================================
Tracking MMs of Ganks in Near Real Time
=======================================

:Authors: Garrett Eardly
:Time: 9:50
:Session:
:Link:
:Slides:


Working on distributed backend system for the past two years. For the
past 18 months working on stats platform for League of Legends.

Riot Games aspires to be a player focused game company: this means
ensuring that players can continue to play, without down time. League
of Legends provides lots of post game stats for users.

The initial stats system (2009) was built with a short development
window, and consciously incured technical debt. The system used a
single database (MySQL) with a caching layer. There was a low
concurrency target, and the database was a single point of failure for
the entire game. When database upgrades needed to happen, the game was
down, as well.

An interim step (2012) was sharding the database to achieve some
horizontal scalability. At this time they were treating MySQL largely
like a key-value store: in order to avoid expensive schema changes,
blobs of unstructured data were stored as values (ie, JSON blobs).
Eight different regions worldwide to support players, and the
deployments are non-homogenous.

Today they're supporting 30+ regions, with more cache and faster
databases (SSD, etc), but fundamentally still the same problems.
Additionally, new data heavy features are extremely difficult to
develop.

The challenges they needed to solve were:

* remove single point of failure
* remove need for downtime during software upgrades
* allow for horizontal scaling.
* enable development of data heavy features

The new system utilizes Riak as its datastore.

There is not single point of failure. Rolling upgrades are possible
(Basho has committed to compatibility between versions). Additionally,
Riak supports hot rebalancing when you add a new node.

Riak works differently than their caching layer over MySQL did. So
what does GET/PUT look like? The request arrives at any one of the
nodes, and is delegated to the nodes that have the data, and when the
threshold number respond, the response is returned. This allows for
tunable eventual consistency. [I wonder how this differs from
Cassandra?]

Challenges:

* Conflict resolution
* Idempotent operations:
  When processing a game repeatedly, you don't want to corrupt the
  stats.
* Balancing # of Gets vs Object size

In order to deal with these, they developed some data patterns. Single
game stats are the simplest case: the last write always wins, and
encapsulates the stats for the entire game. There are no modifications
after write.

A player's match history is more complicatied: you have 1 player and N
games. The matchlist is stored as a single document, so the pattern is
read-update-write [looks like adding a key to a dict]. In this case
the set of games only ever increases, so when there's a conflict, you
simply take the union of the two conflicting documents.

Aggregate stats and counters are more complicated: they're sets of
counters mutating as players play the game. For example, incrementing
the number of kills or deaths over the lifetime of play. In that case,
if there are conflicting siblings, you can't simply union. You *can*
store a sequence of deltas with the object, which allows you to use
union to resolve concurrent write conflicts. Doing that naively,
however, can lead to very large object sizes, which slows down
performance considerably. The solution is to store a rolled-up,
truncated value, along with a set of "recent games" deltas. This isn't
a perfect solution: it's still susceptible to network partitions
during aggregation, but it's something they've decided is managable.

The system is currently live but dark, not deployed worldwide yet.
They are able to begin doing gameplay analysis using the data at this
point.
