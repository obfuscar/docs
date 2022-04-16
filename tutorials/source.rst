Compiling Source Code
=====================

By `Lex Li`_

This page shows you how to compile the source code of Obfuscar.

.. contents:: In this article:
  :local:
  :depth: 1

Source Structure
----------------
The Git repository contains most of the source files, except BAML parsing
files, which comes from a submodule of ILSpy.

Compilation Steps
-----------------
.. important:: Assume that you have latest Visual Studio installed.

#. Clone the Git repository from ``https://github.com/obfuscar/obfuscar.git``.
#. Make sure submodules are checked out.
#. Open Obfuscar.sln in Visual Studio and compile.

.. note:: Alternatively, run ``dist.pack.bat`` to compile via command line.

Related Resources
-----------------

- :doc:`/getting-started/basics`
- :doc:`/getting-started/configuration`
- :doc:`/support/faq`
- :doc:`/support/services`
