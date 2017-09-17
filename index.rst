.. obfuscar documentation master file, created by
   sphinx-quickstart on Sat Nov 21 17:51:25 2015.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.
   
.. _index:

Obfuscar Documentation
======================

.. attention:: Obfuscar 2.2.9 is now available on NuGet! Please read the :doc:`Getting Started <getting-started/index>` instructions for installing the latest version from NuGet.

General
-------
Obfuscar is a basic obfuscator for .NET assemblies. It uses massive overloading to rename metadata in .NET assemblies (including the names of methods, properties, events, fields, 
types and namespaces) to a minimal set, distinguishable in most cases only by signature.

For example, if a class contains only methods that accept different parameters, they can all be renamed 'A'. If another method is added to the class that accepts the same parameters 
as an existing method, it could be named 'a'.

It makes decompiled code very difficult to follow. The wiki has more details about What It Does.

.. image:: _static/obfuscar.png

The current release is Obfuscar 2.x. This is a port of Obfuscar 1.5.4 to the latest Mono.Cecil library. By using this new library Obfuscar now supports .NET 4.0 assemblies. 
Because there are a lot of subtle changes in Cecil's new API and patched merged from different sources, this release of Obfuscar must be considered unstable.

.. note:: Since version 1.5 the attrib attribute is evaluated correctly. Be sure to check if there are any unintended attrib values from the example in your configuration file.

Its source code can be found at GitHub,

https://github.com/lextm/obfuscar

Obfuscar works its magic with the help of Jb Evain's fantastic Mono Cecil library.

The documentation section includes the following topics,

.. toctree::
    :titlesonly:

    getting-started/index
    tutorials/index
    support/index
    contribute/index

Contribute to Documentation
---------------------------

The documentation on this site is the handiwork of our many contributors.

**We accept pull requests!** But you're more likely to have yours accepted if you follow these guidelines:

Read the `Contributing Guide <https://github.com/lextm/obfuscar_docs/blob/master/CONTRIBUTING.md>`_.
