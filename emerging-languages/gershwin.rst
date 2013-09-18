Gershwin: Stack-based Concatenative Clojure
===========================================

:Authors: Daniel Gregoire
:Time: 9:00 - 9:30
:Session: https://thestrangeloop.com/sessions/gershwin-stack-based-concatenative-clojure
:Link: https://github.com/gershwin/gershwin
:Slides:

Why Gershwin? What's wrong with Clojure? That's the first question a
language designed gets asked. Because there's an itch. He wanted to
get a deeper understanding of  Clojure, and explore stack based
languages.

Gerwshin is not emergent, but Clojure is (and has emergerd), and
Gershwin is an extension of Clojure. So what does it mean for a
language to be extensible, and how far can we take that until we break
it? I sdon't think Gershwin breaks Clojure, but you (theaudience) be
the judge.

When studiying a language as humands, the first thing we learn
(usually) is phonestics.  In programming languages, the syntax is the
first thing we look at.

[brief overview of Clojure syntax]

So what does Gershwin add to Clojure? Gershwin is an addative
extension to Clojure; it can compile anythign that Clojure 1.6 can
compile.

First, it's stack based, so no parens are needed to call/invoke.

Functionas are called "words", and ":" is used to define words.

Anonymous functions are called quotations

Use #[] to write quotations (reader macro)

Words and Clojure fucntions can share names in the same namespace,
since they behave differently

Gershwin adds a couple of additions to the LispReader-- reader macros
for quotations, etc. Also, parsing ":" followed by a space.
Additionally, it modifies the pubshback reader buffer.

The next thing you usually learn in spoken languaegs are
words/phrases; in progrmaming, it's primatives: functions, types, etc.


Gershin words:

::

   2 2 +
   ;; 4

   :foo {:foo "bar"} get
   ;; "bar"

   :foo {:foo "bar"} apply
   ;; "bar"

   {:foo "bar"} :foo apply
   ;; "bar

   [:a 1 :b 2] hash-map*
   ;; {:a 1, :b 2}

   [1 2 3 4] #[ 2 * ] map
   ;; (2 4 6 8)    -- this uses a quotation (function)

Most concatenative languges don't include variables: they're point
free. But they're useful, so Gershwin exposes Clojure's variables

::

   (def my-data (atom 42))
   :times-2 [n -- n] 2 * .

   4 times-2
   ;=> 8

In the times-2 declaration, the "[n -- n]" tells Gershwin what to expect this
quotation to do to the stack.

So when you're wriitng Gershwin, it's usually just backwards from Clojure.

Conditionals in Gershwin:

::

   answer 42 =
   #[ :ok ]
   #[ :bad ] if

The "=" operator puts the boolean on the stack. The next two lines
("ok", "bad") put two quotations on the stack, and then the if word
takes a boolean and two quotations off the stack. This implies that
"if" isn't special -- *it's just another quotation*. This is one of
the exciting things about stack based langauges.

Gershwin adds a couple of extensions to the Clojure compiler.

gershwin.main is the entry point for REPL, loading files. The REPL
prints the stack instead of the return values.

clojure.lang.Compiler has a few changes. Compiler.load() takes one
exta argument, to indicate whether it's in clojure mode or gershwin
mode. When Gershwin encouters parenthesis, it assumes you're intermixing Clojure.

When it comes to evaluation, it's clojure function-turtles all the way
down: words wrap to invoke, not words wrap to conf onto stack.

The Stack uses a Clojure Vector under teh converes. It's stored as a
dynamic var in gershwin.core namespace. This means you can rebind it
and ensure that you have, for example, one stack per thread.

Why a stack based approach?

Functions ar enever explicitly passed arguments: it's data data data
word data data word. This means that it's an implicit stack,
maintained by the language (WAT?). But this means that there are
levels of succinctness you can achieve. This is enabled through
"vigorous factoring of words in to smaller words". Stack manipulation
primitves signal the need for factoring, because they're dififcult to
reason about.

Gershwin providese four dataflow combinators

Preserving combinators tempoaraily hides values from the stack: dip
and keep.

Cleave combinators

::

   user => 2 3{ 2 * ] #[ 3 * ] bi
   --- Data Stack:
   4
   6

So bi (and tri) allow you to apply multiple quotations to to elements
on the stack.

Spread combinators

Apply combinators

::

   bi&, tri&

These combinators are brought from Factor_.

So when would you use Gershwin? Gershwin (and other stack based
languages) are a lot like the arrow macro in Clojure. In cases like
that Gershwin can be very effective.

Clojure is a hosted langauge, which means that you can easily apply
your existing knowledge of the JVM or CLR to Clojure. And it's easy to
grow and extend: core.async, core.logic, and core.typed are all
extensions, along with cascalog and Gershwin.

"If your programming language isn't a tool, then you're the tool".
-- Michael Fogus
