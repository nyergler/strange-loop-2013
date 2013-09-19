======================================
Functional Reactive Programming in Elm
======================================

:Authors: Evan Czaplicki
:Time: 13:00
:Session:
:Link:
:Slides:

Functional graphics

How do we make graphics simple and declarative? Graphics meaning text
and links, layout, or free-form graphics. So the question was how do
you make text and links flow correctly, how do you design something
for layout (vertical centering, etc), and finally how do you draw
something completely irregular? And how do you do it in a functional
manner?

Quick example::

  words : Element
  words = [markdown|

  # Hello StrangeLoop!

  Thanks for coming :)
  |]

  img = image 200 200 "/yogi.jpg"

  main : Element
  main = asText 42
  main = words
  main = flow down [ words, img ]

So Elm lets you declare elements and then begin to flow them in a
simple manner.

Elm also has special elements for free form drawing::

  main = collage 200 200
         [ fillled blue (ngon 5 50)
         , outlined (dashed red) (circle 70)
         ]

That's all well and good: it's declarative and it's functional, but
it's just static.

But what if values changed over time? Turns out others had asked this
question ("Functional Reactive Animation", Elliott and Hudak, 1997).

Elements are things that are in the scene.

Signals are values that change over time, which increment in discrete
units. So the mouse position isn't just a pair of integers, it's a
signal that reports how it changes.

The ``lift`` function takes a signal and applies a function to it's
value as it changes. But lift only knows about the present: it doesn't
remember what happened in the past. You can imagine that's problematic
if you're trying to handle text input.
