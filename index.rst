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
   Obfuscar configuration files must use absolute paths for ``InPath``, ``OutPath``, and ``LogFile``. Relative paths are rejected.

.. warning::
   Obfuscar does not expand environment variables or ``$(...)`` placeholders in configuration files. Provide explicit values.

.. note::
   It is recommended to *generate* the Obfuscar XML configuration file as part of your build or CI pipeline. Expand environment variables and resolve relative paths during generation so the produced XML contains only absolute paths and explicit values.

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

The current release is Obfuscar 2.x. The project historically used the Mono.Cecil
library for metadata handling. With the upcoming v3 release Obfuscar has been
refactored to use System.Reflection.Metadata (SRM)-backed readers and mutable
metadata abstractions; v3 will not have a runtime dependency on Mono.Cecil for
its core obfuscation pipeline. See the developer notes for migration details.

.. note:: Since version 1.5 the attrib attribute is evaluated correctly. Be
   sure to check if there are any unintended attrib values from the example in
   your configuration file.

Its source code can be found at GitHub,

https://github.com/obfuscar/obfuscar

Obfuscar previously relied on Jb Evain's Mono.Cecil for low-level metadata
manipulation. The codebase has since moved to SRM/mutable adapters and uses
abstractions to avoid a direct runtime dependency on Mono.Cecil in the main
projects and tests.

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
