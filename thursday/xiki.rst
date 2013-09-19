====
Xiki
====

:Authors: Craig Muth
:Time: 15:00
:Session:
:Link: http://xiki.org
:Slides:

[Pre-show music makes me feel hostile towards presenter.]

Xiki is a langauge for creating UI languages. Muth has been involved
in Xiki for 10 years. Muth would argue that there aren't really simple
ways to create user interfaces, and there should be. These just aren't
interfaces for your users, but for yourself, as well.

Xiki doesn't try to solve all UI problems, but focuses on a single
problem: nested menus. Many user interfaces consist of vast lists of
choices.

Xiki consists of a web server, a ``xiki`` shell command, and editor
plugin[s?].

When we start thinking about new interfaces, a lot of times we start
with an indented list of items. Xiki uses that sort of indented list
as it's basic data structure::

  book flight/
    one way/
    round trip/
  check in/
  flight status/

[Shows demo of Xiki web server reading a file and generating a mobile
UI on the iPhone simulator.]

Any item that ends with a ``/`` is a menu item. Lines that don't end
in a slash are just plain text. You can also embed Ruby code for
simple dynamic generation.

The built-in web server allows you to also created new items through
the browser.

Xiki provides a command line interface, and generates a desktop GUI,
too. I still don't know why I'd use Xiki.

[Demonstrates using the Emacs editor plugin to pipe things back and
forth with the Xiki command line.]

Lots of capabilities for Xiki; Muth is obviously very well versed in
using it.
