---
layout: post
title: Working with compiler
---

### Building and testing

Learning how to build compiler is the first step of studying OCaml compiler
source code. When developing compiler locally, we may need to build and try out different compilers. So, we suggest using OPAM together with Gabriel Scherer's
script to build and test compilers.


1. First, install Gabriel Scherer's [opam-compiler-conf](https://github.com/gasche/opam-compiler-conf) script.
 Make sure

2. Do the following to compile and install your experimental compiler. Switch to new compiler environment accordingly

  ```
  $ opam compiler-conf configure
  $ make -j world.opt
  $ opam compiler-conf install
  ```

  Note that enabling parallel building with ``-j`` flag can make building
  become unstable and fail.

3. Do the following to test your compiler after some change

   ```
   $ make -j world.opt
   $ opam compiler-conf reinstall
   ```

   Note that one may need to do ``make clean`` to clear all compiled interface to make sure building succeed.

### Using Merlin when reading source code

When studying compiler source code, it is very convenient to have Merlin enabled. One can
easily get the type of variables and functions, or jump to the definition site of a function.
To make sure Merlin can understand your compiler source code, we need to install Merlin with the compiler you built. After installing your own compiler according to steps above, we switch to the new compiler using ``opam switch`` and install Merlin.

Note that using Merlin to read compiler source code does not work all the time. Strange errors may happen,
mostly because of digest mismatch. Digest mismatch happens when one makes changes in the interface since
the last compilation. The reason is that merlin is using the switch managed standard libraries, while
your local compiler is built against its own set of libraries. The fix is to change the path of standard library
library to source code's ``stdlib/`` (``export OCAMLSTDLIB=...``).
