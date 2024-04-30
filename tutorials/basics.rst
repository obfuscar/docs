Basic Example
=============

This page shows you the basics about Obfuscar.

Folder Structure
----------------
The example has been moved to a separate repository `at GitHub <https://github.com/obfuscar/example>`_ .

Technical Details
-----------------
.. note:: The example assumes you have Visual Studio 2017 installed.

The example consists of a solution that includes an executable and a dll.

The final executable project adds Obfuscar NuGet package from NuGet.org, and
uses it in post build event to perform obfuscation.

The obfuscation settings are stored in an XML file (``obfuscar.xml``), and is
copied to output directory by MSBuild.

Related Resources
-----------------

- :doc:`/getting-started/basics`
- :doc:`/getting-started/configuration`
- :doc:`/tutorials/xamarin`
- :doc:`/support/faq`
- :doc:`/support/services`
