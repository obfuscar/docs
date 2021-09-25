Frequent Asked Questions
========================
By `Lex Li`_

This page shows you the common questions.

.. contents:: In this article
   :local:
   :depth: 1

How to understand the return code?
----------------------------------
The command line utility returns different codes in the following cases,

* 0,

  * when obfuscation finishes successfully.
  * when showing version number or help.
  * when no argument is provided.
* 1,

  * when any invalid argument is provided.
  * when any exception happens at runtime.

How to troubleshoot IOException?
--------------------------------
Typical exceptions might look like below,

.. code-block:: text

   System.IO.IOException: The process cannot access the file
   'xxxx\Mapping.txt' because it is being used by another process.

   System.IO.IOException: The process cannot access the file
   'xxxx\bin\Release\xxxx.exe' because it is being used by another process.

   System.IO.IOException: The process cannot access the file
   'xxxx\bin\x86\Debug\xxxx.pdb' because it is being used by another process.

Usually such exceptions happen because the output files try to overwrite input
files. Make sure to use a different output path and they should disappear.

How to troubleshoot ArgumentException?
--------------------------------------
Typical exceptions might look like below,

.. code-block:: text

   System.ArgumentException: Illegal characters in path.

Usually such exceptions happen when an invalid input path is used. Use a valid
path and they should disappear.

How to troubleshoot BadImageFormatException?
--------------------------------------------
Typical exceptions might look like below,

.. code-block:: text

   System.BadImageFormatException: Format of the executable (.exe) or library
   (.dll) is invalid.

Usually such exceptions happen when Mono Cecil cannot understand the input
assemblies. You might upgrade to a newer version of Obfuscar (if exists) or
skip such assemblies in obfuscation process (as usually they are already
obfuscated).

How to troubleshoot ResolutionException or AssemblyResolutionException?
-----------------------------------------------------------------------
Typical exceptions might look like below,

.. code-block:: text

   Mono.Cecil.ResolutionException: Failed to resolve xxx.dll

   Mono.Cecil.AssemblyResolutionException: Failed to resolve assembly: 'xxxx, Version=x.x.x.x, Culture=neutral, PublicKeyToken=xxxx'

Usually such exceptions happen when Obfuscar cannot locate dependent
assemblies. You might add `assembly search paths <https://docs.obfuscar.com/getting-started/configuration.html#assembly-search-path-2-2-5>`_
in configuration file.

How to troubleshoot NotSupportedException?
------------------------------------------
Typical exceptions might look like below,

.. code-block:: text

   System.NotSupportedException: The given path's format is not supported.

Usually such exceptions happen when the input path is invalid. Provide
a valid input path in configuration and then they should disappear.

.. code-block:: text

   System.NotSupportedException: Writing mixed-mode assemblies is not supported

Usually such exceptions happen when mixed-mode assemblies (from C++/CLI) are
being obfuscated. Mono Cecil does not support such. Please skip them.

How to troubleshoot UnauthorizedAccessException?
------------------------------------------------
Typical exceptions look like below,

.. code-block:: text

   System.UnauthorizedAccessException: Access to the path 'xxxx\xxxx.exe' is denied.

Such exceptions happen when Obfuscar has not enough permissions to access file
system. Modify file system permissions and try again.

How to troubleshoot TypeLoadException during reflection?
--------------------------------------------------------
After obfuscation, the application might not work and ``TypeLoadException`` is
quite common a case. One such case is

https://stackoverflow.com/questions/24058302/obfuscar-2-0-could-not-load-type-from-assembly

There can be other similar cases, where either explicitly or implicitly the
application code itself requires an instance to be initialized at runtime by
reflection.
Since reflection requires metadata, which obfuscation manipulates heavily,
such initialization could fail.

The workaround is to skip such types or methods in obfuscation, so that
reflection can still find them out.

.. note:: It is rarely a bug of Obfuscar.

How to troubleshoot TypeLoadException if a method does not have implementation?
----------------------------------------------------------------------------------
One such case is

https://github.com/obfuscar/obfuscar/issues/47

.. note:: It is very likely a bug of Obfuscar.

Obfuscar can mistakenly rename a virtual function, so that at runtime CLR
cannot find the expected method from the type.

The workaround is to skip such methods in obfuscation explicitly. A bug report
can also be fired at GitHub.

How to analyze exception call stack if obfuscated?
---------------------------------------------------
Obfuscation replaces class and method names so that exception call stacks
would be difficult to read. But there is
`a separate open source project called ObfuscarMappingParser <https://github.com/BrokenEvent/ObfuscarMappingParser>`_ to address the challenge.

Related Resources
-----------------

- :doc:`/getting-started/basics`
- :doc:`/getting-started/configuration`
- :doc:`/tutorials/basics`
