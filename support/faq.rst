Frequent Asked Questions
========================

This page shows you the common questions.

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

Usually such exceptions happen when Mono.Cecil (legacy) cannot understand the input
assemblies. You might upgrade to a newer version of Obfuscar (if exists) or
skip such assemblies in obfuscation process (as usually they are already
obfuscated).

However, if you are obfuscating a .NET project, make sure your config file
points to the right assemblies (``*.dll``), not the native executable added by
.NET CLI (``*.exe``). Please use a tool like ILSpy to verify if a file is .NET
managed or native.

How to troubleshoot ResolutionException or AssemblyResolutionException?
-----------------------------------------------------------------------
Typical exceptions might look like below,

.. code-block:: text

   Mono.Cecil.ResolutionException: Failed to resolve xxx.dll

   Mono.Cecil.AssemblyResolutionException: Failed to resolve assembly: 'xxxx, Version=x.x.x.x, Culture=neutral, PublicKeyToken=xxxx'

Usually such exceptions happen when Obfuscar cannot locate dependent
assemblies. You might add `assembly search paths <https://docs.lextudio.com/obfuscar/getting-started/configuration.html#assembly-search-path-2-2-5>`_
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
being obfuscated. Mono.Cecil (legacy) does not support such. Please skip them.

Why does Obfuscar reject relative paths or $(...) placeholders?
---------------------------------------------------------------
Typical exceptions might look like below,

.. code-block:: text

   Obfuscar.ObfuscarException: InPath must be an absolute path: '$(InPath)'
   Obfuscar.ObfuscarException: OutPath must be an absolute path: 'bin\\Release'

**Why?** Obfuscar 3.0 requires absolute paths for ``InPath``, ``OutPath``, ``LogFile``, and ``AssemblySearchPath`` and does not expand environment variables or ``$(...)`` placeholders. This prevents ambiguity and path resolution errors.

**How to fix it:**

1. **If using a build system (MSBuild, PowerShell, bash):** Generate the Obfuscar XML configuration as part of your build process with expanded absolute paths:

   .. code-block:: bash

      # macOS/Linux example
      INPATH=$(realpath ./bin/Release)
      OUTPATH=$(realpath ./obfuscated)
      cat > /tmp/obfuscar.xml <<EOF
      <?xml version="1.0"?>
      <Obfuscator>
        <Var name="InPath" value="${INPATH}" />
        <Var name="OutPath" value="${OUTPATH}" />
        <Module file="${INPATH}/MyApp.exe" />
      </Obfuscator>
      EOF

   .. code-block:: powershell

      # Windows example
      $inPath = Resolve-Path ".\bin\Release" -Absolute
      $outPath = Resolve-Path ".\obfuscated" -Absolute
      @"
      <?xml version="1.0"?>
      <Obfuscator>
        <Var name="InPath" value="$inPath" />
        <Var name="OutPath" value="$outPath" />
        <Module file="$inPath\MyApp.exe" />
      </Obfuscator>
      "@ | Out-File -FilePath "obfuscar.xml" -Encoding UTF8

2. **If manually editing XML:** Always use full absolute paths:

   - macOS/Linux: ``/Users/you/project/bin/Release`` or ``/home/user/project/bin``
   - Windows: ``C:\Users\you\project\bin\Release`` (forward slashes ``C:/Users/you/project/bin/Release`` also work)

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

.. important:: In general, it is impossible to obfuscate a lot of classes and
   their members due to .NET itself or the frameworks used in the project.

   For example, there are,

   * Weak references used in XAML/AXML (used in WPF/UWP/Xamarin)
   * Names used in dependency injection
   * Names used in reflection (used a lot in ASP.NET MVC for example)
   * Names used in ``DebuggerDisplayAttribute`` or similar attributes
   * Things used in ``dynamic`` context
   * Setting names used in .NET configuration system
   * Names used in plug-in framework like Microsoft Extension Framework or
     Mono.Addins
   * and many more.

   Thus, if the obfuscated program does not work for you, try to add items to
   obfuscation in small batches, so that you can quickly find out what items
   should be included or excluded.

.. note:: Obfuscar intentionally skips many classes used in WPF/XAML. However,
   due to limitation of the ILSpy maintained BAML library, there can still be
   a lot of names not skipped properly, which requires extra skip rules to be
   added to configuration file.

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
You can refer to :doc:`/getting-started/ecosystem` to learn about
ObfuscarMappingParser.

Related Resources
-----------------

- :doc:`/getting-started/basics`
- :doc:`/getting-started/configuration`
- :doc:`/getting-started/ecosystem`
- :doc:`/tutorials/basics`
