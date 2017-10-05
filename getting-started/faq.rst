Frequent Asked Questions
========================
By `Lex Li`_

This page shows you the common questions.

.. contents:: In this article
   :local:
   :depth: 1

How to troubleshoot TypeLoadException during reflection?
--------------------------------------------------------
After obfuscation, the application might not work and ``TypeLoadException`` is quite common a case. One such case is 

http://stackoverflow.com/questions/24058302/obfuscar-2-0-could-not-load-type-from-assembly

There can be other similar cases, where either explicitly or implicitly the application code itself requires an instance to be initialized at runtime by reflection. 
Since reflection requires metadata, which obfuscation manipulates heavily, such initialization could fail.

The workaround is to skip such types or methods in obfuscation, so that reflection can still find them out.

.. note:: It is rarely a bug of Obfuscar.

How to troubleshoot TypeLoadException if a method does not have an implementation?
----------------------------------------------------------------------------------
One such case is 

https://github.com/lextm/obfuscar/issues/47

.. note:: It is very likely a bug of Obfuscar.

Obfuscar can mistakenly rename a virtual function, so that at runtime CLR cannot find the expected method from the type.

The workaround is to skip such methods in obfuscation explicitly. A bug report can also be fired at GitHub.

How to analyze exceptioni call stack if obfuscated?
---------------------------------------------------
Obfuscation replaces class and method names so that exception call stacks would be difficult to read. But there is 
`a separate open source project called ObfuscarMappingParser <https://github.com/BrokenEvent/ObfuscarMappingParser>`_ to address the challenge.

Related Resources
-----------------

- :doc:`/getting-started/basics`
- :doc:`/tutorials/basics`
