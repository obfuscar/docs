What does Obfuscar do?
======================

Basically, Obfuscar scrambles the metadata in a set of assemblies. It renames
everything to the minimal set of names that can be used to identify them,
given signatures and type information. Since these new names are shorter than
the old ones, it also dramatically shrinks executable size.

An Example
----------
The following method is from the example included in the release:

.. code-block:: csharp

       public ExampleUI( )
       {
               InitializeComponent( );

               ClassX cx = new ClassX( "Some Text" );

               displayText.Text = cx.DisplayText;
       }

The code can be decompiled (via `ILSpy <http://ilspy.net/>`_) to:

.. code-block:: csharp

       public ExampleUI()
       {
               this.InitializeComponent();
               this.displayText.Text = new ClassX("Some Text").get_DisplayText();
       }

After obfuscation, the code can be decompiled (via ILSpy) to:

.. code-block:: csharp

       public A()
       {
               this.a();
               this.a.Text = new A.A("Some Text").A();
       }

It's a simple example, but it scales...For example, given a reasonably sized
code base, one could easily run into a class named A (in the namespace A) with
7 methods, 4 properties, and 5 fields named A, with several more methods,
properties, and fields named a.

To try it out, see :doc:`/tutorials/basics`. The sample project demonstrates
how to use Obfuscar NuGet package in your .NET Framework projects to perform
obfuscation.

Caveat
------
It makes debugging / reverse engineering very difficult, but wouldn't stop
someone who really wants to reverse engineer it. It would at least slow them
down, and would deter casual observers.

Deobfuscators such as `de4dot <https://github.com/0xd4d/de4dot>`_ make it
easy to reverse most protection a commercial obfuscator might set. But note
that the names obfuscated by Obfuscar still remains useful, as what's lost
cannot be restored.

.NET Core Global Tools
----------------------
Starting from .NET Core 2.1 SDK, Microsoft has introduced the concept of
global tools. Global tools are .NET Core applications that are installed
system-wide and can be run from any command prompt. This is similar to
traditional command-line tools, but with the added benefit of being able to
use the .NET Core runtime to run them.

Obfuscar can be used as a global tool since its 2.2.15 release. This allows
you to install Obfuscar as a global tool and run it from any command prompt.

#. To install Obfuscar as global tool execute: ``dotnet tool install --global Obfuscar.GlobalTool``
#. Once installed, you can call ``obfuscar.console`` to run Obfuscar.

Visit `the NuGet page <https://www.nuget.org/packages/Obfuscar.GlobalTool/>`_ for more information.

.. important::

   Due to the short life cycle of .NET Core SDK, latest Obfuscar release won't
   work with end-of-life releases. You need to read Microsoft documentation to
   find out which SDK versions are supported.

.. important::

   If you are working on .NET Core/.NET projects, using this global tool is
   highly recommended than using the NuGet package.

Related Resources
-----------------

- :doc:`/getting-started/history`
- :doc:`/getting-started/ecosystem`
- :doc:`/tutorials/basics`
