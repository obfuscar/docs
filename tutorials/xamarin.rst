Information on Xamarin.Android
==============================

By Edward Brey and Ronan Burke

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

It is a good idea to `place this near the bottom <https://stackoverflow.com/a/40348862/3991315>`_ of your project file after all other targets to ensure it is run.

Obfuscar Configuration File
---------------------------
Create ``obfuscar.xml`` in the Xamarin.Android project. Configure it to output
to the target directory relative to the assets directory.

.. code-block:: xml

  <Obfuscator>
    <Var name="OutPath" value="..\..\..\..\..\bin\Release" />
    <Module file="MyAssembly.dll" />
  </Obfuscator>

Troubleshooting
---------------
To more effectively troubleshoot issues, you can use the following tools/methods:

- Temporarily change the ``AfterBuild`` target mentioned above to be for the 'Debug' configuration. Add a debug message to the configuration so you can confirm the task is being run:

.. code-block:: xml

  <Target Name="AfterBuild" Condition=" '$(Configuration)' == 'Debug' ">
    <Message Importance="High" Text="Obfuscar task has been called." />
    <Exec WorkingDirectory="$(MonoAndroidIntermediateAssetsDir)" Command="$(Obfuscar) $(ProjectDir)obfuscar.xml" />
    <Copy SourceFiles="$(TargetDir)MyAssembly.dll" DestinationFolder="$(MonoAndroidIntermediateAssetsDir)" />
  </Target>

Update ``obfuscar.xml`` to output to the Debug folder:

.. code-block:: xml

    <Var name="OutPath" value="..\..\..\..\..\bin\Debug" />

- Run your application in Debug mode. In Visual Studio, go to ``Debug > Windows > Exception Settings``. Enable ``Common Language Runtime Exceptions``. When your app runs, this will allow you to see if you are getting any new exceptions when obfuscation is enabled.
- If your app crashes on startup with no obvious exceptions, go to ``Tools > Android > Device Log...`` and use the messages from Logcat to diagnose/research the errors you get.

Linking issues
**************

With linking enabled, you may get this error message:

::

	XALNK7000: Java.Interop.Tools.Diagnostics.XamarinAndroidException: error XA2006: Could not resolve reference to ' . '
	...
	When the scope is different from the defining assembly, it usually means that the type is forwarded. ---> Mono.Cecil.ResolutionException: Failed to resolve  .

With linking disabled, you may get this error message:

::

	JAVAC0000:  error: illegal character: '\u2006' xamarin forms

The above two errors can be resolved by using this property in ``obfuscar.xml``:

.. code-block:: xml

   <Var name="UseUnicodeNames" value="false" />

AndroidX issues
***************

Using Obfuscar can reveal issues with an improper AndroidX migration in Xamarin. If you get an error like this:

::

	System.InvalidCastException: Unable to convert instance of type 'Google.Android.Material.Internal.CheckableImageButton' to type 'AndroidX.AppCompat.Widget.Toolbar'
	
You should update "android.support.v7.widget.Toolbar" to "androidx.appcompat.widget.Toolbar" in ``Toolbar.xml``. You should rename the file to ``Toolbar.axml``. You should update "android.support.design.widget.TabLayout" to "com.google.android.material.tabs.TabLayout" in ``Tabbar.xml``. You should rename the file to ``Tabbar.axml``.

The `Xamarin.Forms team recommend removing these files altogether
<https://docs.microsoft.com/en-us/xamarin/xamarin-forms/troubleshooting/questions/forms5-migration#remove-axml-files>`_
, but you may encounter other issues when running your Android app after doing this. 

Dependency injection errors
***************************

If you are using dependency injection and are getting dependency injection
errors, ensure public items are kept in ``obfuscar.xml``:

.. code-block:: xml

   <Var name="KeepPublicApi" value="true" />

Related Resources
-----------------

- :doc:`/getting-started/basics`
- :doc:`/getting-started/configuration`
- :doc:`/tutorials/basics`
- :doc:`/support/services`
