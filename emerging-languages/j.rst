The J Programming Language
==========================

:Authors: Tracy Harms @kaleidic
:Time: 15:50 - 16:20
:Session: https://thestrangeloop.com/sessions/the-j-programming-language
:Link: http://www.jsoftware.com/
:Slides:

Tracy didn't create J, but he's here to talk about it. J is the
product of Kenneth E. Iverson adn Roger Hui. J was first released
in 1990.

What sort of problem does J fit well? Subtraction. Specifically image
subtraction: removing a shadow from an image.

[Shows the source, fits on one slide.]

When reading a J program, it's often best to start at the end: that's
the punch line. And then start back at the top to see *how* it gets
there.

[Walks through image subtraction program.]

J favors an interactive approach, assuming the "operator" is at the
console.

In J, data is called a *noun*, and a *noun* is a collection. Nouns are
regular. Scalar data is the exception, rather than the rule. A *verb*
(function) applies across

J has had over fifty years of refinement, starting on chalkboards in
1957 with Iverson at Harvard. In 1962, there was a book published on
it: "A Programming Language". A paper followed in 1964, desribing the
System/360 architecture. The interpreter, APL, was released in 1966:
before then verification and changes happened *manually*, with pencil
and paper.

Even though APL was critically important, Iverson had a sense that it
could have been better had he known more starting out. In the 1980's
he released its successor, **J**.

[Shows some J interaction.]

In J you can factor verbs that take common nouns out into a *verb
train*. If you give that train a name, you've defined a new verb.

::

  average =: +/ % #

allows you to do::

  average MyList

And is equivalent to::

  (+/MyList) % (#MyList)

(The sum of the list divided by the number of elements.)

Verb Trains are higher order functions, denoted by placing verbs
adjacent to one another.

[Shows numeronym example.]
