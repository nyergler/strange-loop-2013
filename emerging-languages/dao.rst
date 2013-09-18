Dao Programming Language for Scripting and Computing
====================================================

:Authors: Limin Fu
:Time: 13:40
:Session: https://thestrangeloop.com/sessions/dao-programming-language-for-scripting-and-computing
:Link: http://daovm.net/
:Slides:

Dao is a language Fu developed in his spare time. It was initially
motivated by frustration with Perl. That frustration made him curious
about language design and implementation. Around the same time he
wanted a better language for bioinformatics, and Dao was a way to get
that. Since then the goal has evolved to providing a general purpose
language with some advanced features in a small runtime. Dao
emphasizes consistent and reasonable syntax, simple interface for
extending and embedding, good numeric efficiency, and good support for
multiple cores.

Dao supports:

* optional type annotations, with type inference and static type
  checking,
* BNF-like syntax macros for adding new language features,
* and anonymous functions,

among others (slides list more complete features).

::

   tup = ( 123, 'abc' )
   tup : tuple<int, string> = (123, 'abc')

Because Dao does some type inferencing and compile time checks, it
does some interesting things at compile time: if you call a function
in two places, once with a string and once with an int, you get two
specialized copies in the copmiled output: one for ints and one for
strings.

[Demonstrates lots of Dao features, including concurrency primitives.]

The Dao JIT  backend is based on LLVM. It only supports a subset of
the Dao VM instructions, so some programs won't be sped up with the
current implementation.

ClangDao provides an easy way to bind C/C++ libraries into Clang.
