Babel: An Untyped, Stack-based HLL
==================================

:Authors: Clayton Bauman
:Time: 10:20-10:50
:Session: https://thestrangeloop.com/sessions/babel-an-untyped-stack-based-hll
:Link: http://babelscript.net
:Slides:

Going to explain how it works, and demonstrate it using the reference
implementaiton. Began devleoping babel around 2006. In 2005 it was
revealed that the NSA was spying on US citizens. The security flaws
were made possible in some cases by backdoors inserted by NSA, et al.
Today the emphasis of ownership is on those of the designer. Babel
attempts to shift that to the rights of the user and the system owner.

Babel 1.0 will use public key crypto to verify that code is allowed --
by the user -- to execute. This means that the user decides who they
trust to write software.

Babel is a stack based, untyped langauge. It's not a "pure" language:
some (many?) actions can have side effects. Although Babel is untyped,
it does support tags, which allow you to assign string descriptors to
pointers.

The core babel data structure is called the ``bstruct``. This is the
underlying container for all data in Babel. Strings, integers,
unsigned, floats, are all stored as values in lfaf-arryas. No pointers
can be stored ina  leaf-array.

Ordeiinary pointers are stored in nitnerior-arrays: overy points in an
interior-array must be initialized and valid. No values can be stored
in an interior array.

[ overview of in memory data structure for Babel ]

Code is data in Babel.

[ example ]

And the following are equivalent::

  (val "Hello")
  (val 0x6c6c6548 0x6f 0xffffffff00)

The virtual machine, the BVM, is also a bstruct. There are three
stacks: the down stack (dstack), up stack (ustack), and managed stack
(rstack). Code-list is a linked list containing data operands, etc.

The Bable interpreter uses a small boostrap, which is also written in
Bable. This bootstrap loads and begins execution of your program. The
reference implementation is written in C, with a Perl front end
parser (based on sparse.pl). In the future it will have a built in
parser instead of using Perl, and include a wide selection of crypto
primitives (libtomcrypt).

[Lots of time spent discussing stack and memory internals of Babel.
This would be great for situations where I thought I might want to use
Babel and wanted to develop a deep understanding. Unfortunately not at
all clear to me when I might want to use Babel at the moment.]
