Basic Example
=============

By `Lex Li`_

This page shows you the basics about Obfuscar.

.. contents:: In this article:
  :local:
  :depth: 1

Folder Structure
----------------
The example has been moved to a separate repository `at GitHub <https://github.com/lextm/obfuscar_example>`_ .

Technical Details
-----------------
.. note:: The example assumes you have Visual Studio 2017 installed.

The example consists of a solution that includes and executable and a dll. The test.bat script builds the solution, copies the output to a temporary input path. The files are then obfuscated into a temporary output path. After obfuscation, the files are copied along with the map file to their final output path.

The reason for this indirection is safety. The release process should be as follows:
1. Files that will not be obfuscated should be copied directly to the final output path.
1. Files to be obfuscated should be copied to a temporary location (Obfuscator_Input, in the example), along with their dependencies.
1. Files to be obfuscated should be obfuscated from the first location (Obfuscator_Input) to a different location (Obfuscator_Output, in the example).
1. Obfuscated files should be copied from the obfuscation output location (Obfuscator_Output) to the final output path.
1. Package files in final output path (beyond the scope of this document).

In the event that the obfuscator fails, an in-place obfuscation could allow files to enter the release without being obfuscated. Having the obfuscator explicitly save to a different location and using files from that location means that failure results in missing files.

Related Resources
-----------------

- :doc:`/getting-started/basics`
