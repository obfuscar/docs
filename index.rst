.. obfuscar documentation master file, created by
   sphinx-quickstart on Sat Nov 21 17:51:25 2015.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

.. _index:

Obfuscar Documentation
======================

.. attention:: Obfuscar 2.2 is now available on NuGet! Please read the
   :doc:`Getting Started <getting-started/index>` instructions for installing
   the latest version from NuGet.

.. warning::
   Environment-variable expansion inside Obfuscar configuration files is deprecated and will be removed in a future release. Please avoid using environment-variable syntax in project configuration files and consult the Getting Started guide for migration steps.

.. warning::
   Relative paths in Obfuscar configuration files are deprecated and future releases will require absolute paths. Update your configuration to use absolute paths and consult the Getting Started guide for examples.

General
-------
Obfuscar is a basic obfuscator for .NET assemblies. It uses massive
overloading to rename metadata in .NET assemblies (including the names of
methods, properties, events, fields, types and namespaces) to a minimal set,
distinguishable in most cases only by signature.

For example, if a class contains only methods that accept different
parameters, they can all be renamed 'A'. If another method is added to the
class that accepts the same parameters as an existing method, it could be
named 'a'.

It makes decompiled code very difficult to follow. The wiki has more details
about What It Does.

.. image:: _static/obfuscar.png

The current release is Obfuscar 2.x. This is a port of Obfuscar 1.5.4 to the
latest Mono.Cecil library. There were a lot of subtle changes in Cecil's new API
and patches merged from different sources.

.. note:: Since version 1.5 the attrib attribute is evaluated correctly. Be
   sure to check if there are any unintended attrib values from the example in
   your configuration file.

Its source code can be found at GitHub,

https://github.com/obfuscar/obfuscar

Obfuscar works its magic with the help of Jb Evain's fantastic Mono Cecil
library.

The documentation section includes the following topics,

.. toctree::
    :titlesonly:

    Visit Docs Home <https://docs.lextudio.com>
    getting-started/index
    tutorials/index
    support/index
    contribute/index
    privacy

Contribute to Documentation
---------------------------

The documentation on this site is the handiwork of our many contributors.

**We accept pull requests!** But you're more likely to have yours accepted if
you follow these guidelines:

Read the `Contributing Guide <https://github.com/obfuscar/docs/blob/master/CONTRIBUTING.md>`_.
