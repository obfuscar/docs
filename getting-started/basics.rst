What does Obfuscar do?
======================

By `Lex Li`_

Basically, Obfuscar scrambles the metadata in a set of assemblies. It renames
everything to the minimal set of names that can be used to identify them,
given signatures and type information. Since these new names are shorter than
the old ones, it also dramatically shrinks executable size.

.. contents:: In this article:
  :local:
  :depth: 1

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
               this.A();
               this.a.Text = new A.A("Some Text").A();
       }

It's a simple example, but it scales...For example, given a reasonably sized
code base, one could easily run into a class named A (in the namespace A) with
7 methods, 4 properties, and 5 fields named A, with several more methods,
properties, and fields named a.

To try it out, see Basic Example.

Caveat
------
It makes debugging / reverse engineering very difficult, but wouldn't stop
someone who really wants to reverse engineer it. It would at least slow them
down, and would deter casual observers.

Deobfuscators such as `de4dot <https://bitbucket.org/0xd4d/de4dot>`_ make it
easy to reverse most protection a commercial obfuscator might set. But note
that the names obfuscated by Obfuscar still remains useful, as what's lost
cannot be restored.

Related Resources
-----------------

- :doc:`/getting-started/history`
- :doc:`/tutorials/basics`
