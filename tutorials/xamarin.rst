Information on Xamarin.Android
==============================

By Edward Brey

This page shows how to automate Obfuscar for Xamarin.Android using MSBuild.
Integration for other Xamarin platforms is similar.

.. contents:: In this article:
  :local:
  :depth: 1

Nuget Package
----------------
Install the Obfuscar NuGet package into the Xamarin.Android project.

.. code-block:: powershell

  Install-Package Obfuscar

Project File
------------
In the Xamarin.Android project file (.csproj), add an ``AfterBuild`` target to
run the obfuscator.

The obfuscator runs from ``MonoAndroidIntermediateAssetsDir``, which is the
assets directory that gets bundled into the APK. An example of this directory
is ``obj\Release\90\android\assets``.

The obfuscator outputs to the target directory (e.g. ``bin\Release``) so that
the mapping file will go there. It then copies the obfuscated files to the
assets directory.

This is an example target for obfuscating a single assembly called
``MyAssembly.dll``:

.. code-block:: xml

  <Target Name="AfterBuild" Condition=" '$(Configuration)' == 'Release' ">
    <Exec WorkingDirectory="$(MonoAndroidIntermediateAssetsDir)" Command="$(Obfuscar) $(ProjectDir)obfuscar.xml" />
    <Copy SourceFiles="$(TargetDir)MyAssembly.dll" DestinationFolder="$(MonoAndroidIntermediateAssetsDir)" />
  </Target>

Obfuscar Configuration File
---------------------------
Create ``obfuscar.xml`` in the Xamarin.Android project. Configure it to output
to the target directory relative to the assets directory.

.. code-block:: xml

  <Obfuscator>
    <Var name="OutPath" value="..\..\..\..\..\bin\Release" />
    <Module file="MyAssembly.dll" />
  </Obfuscator>

Related Resources
-----------------

- :doc:`/getting-started/basics`
- :doc:`/getting-started/configuration`
- :doc:`/tutorials/basics`
- :doc:`/support/services`
