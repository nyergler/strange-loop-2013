Axiomatic Language
==================

:Authors: Walter Wilson
:Time: 14:15
:Session: https://thestrangeloop.com/sessions/axiomatic-language
:Link: http://axiomaticlanguage.org/
:Slides:

Axiomatic has four goals:

* Pure specification -- what, not how
* Minimal but extensible -- as small as possible
* Metalanguage -- able to imitate other languages
* Beautiful

Speificiation by Enumeration: a program can be specific by an infinite
set of symbolic epxressions that enumerate all possible inputs or
sequences of inputs along with the corresponding outputs.
Additionally, you could create a syntax for describing programs in
terms of the input and output files. But what about interactive
programs? This is a specialization of the previous case: instead of a
single input specification and a single output specification, the
enumeration interleaves input and output, again exhausitvely.

If you accept the premise that this enumeration is a specification,
then what you need is a way to formally describe the enumerations.
Axiomatic syntax supports atoms, expressions, strings, and sequences.
The *axiom* construct is a conclusion (output) and some set of
conditions. In the core language, the program generates expressions if
all the conditions of an axiom instances are valid (true).
