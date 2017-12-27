Frequent Asked Questions
========================

By `Lex Li`_

This page shows you where to find the answers.

.. contents:: In this article:
  :local:
  :depth: 1

How to troubleshoot TypeLoadException during reflection?
--------------------------------------------------------
After obfuscation, the application might not work and TypeLoadException is quite common a case. One such case is 

http://stackoverflow.com/questions/24058302/obfuscar-2-0-could-not-load-type-from-assembly

There can be other similar cases, where either explicitly or implicitly the application code itself requires an instance to be initialized at runtime by reflection. Since reflection requires metadata, which obfuscation manipulates heavily, such initialization could fail.

The workaround is to skip such types or methods in obfuscation, so that reflection can still find them out.

.. note:: It is rarely a bug of Obfuscar.

How to troubleshoot TypeLoadException if a method does not have an implementation?
----------------------------------------------------------------------------------
One such case is 

https://github.com/lextm/obfuscar/issues/47

It is very likely a bug of Obfuscar, where it mistakenly renames a virtual function, so that at runtime CLR cannot find the expected method from the type.

The workaround is to skip such methods in obfuscation explicitly. A bug report can also be fired at GitHub.

GitHub FAQ List
---------------
We use `GitHub <https://github.com/lextm/obfuscar/issues?q=label%3A%22faq+candidate%22+is%3Aclosed>`_ to manage the list.

StackOverflow
-------------
You might also want to check out existing discussions at `StackOverflow <http://stackoverflow.com/questions/tagged/obfuscar>`_ .

Related Resources
-----------------

- :doc:`/getting-started/basics`
- :doc:`/getting-started/history`
- :doc:`/tutorials/basics`
- :doc:`/support/services`
