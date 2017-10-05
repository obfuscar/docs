Customizing Persistence
=======================

By `Lex Li`_

This page shows you how to customize persistence. 

.. contents:: In this article:
  :local:
  :depth: 1
  
Layout File Format
------------------
``DockPanel.Persistor.SaveAsXml`` is the method who saves current layout to an XML file.

It is not recommended to manually edit the generated layout file, as its syntax is complicated.

To achieve customization, it is recommended to override the persistent string.

Overriding Persistent String
----------------------------
As the sample project shows, by default when current layout is saved to disk only class 
name is persisted. As a result, in delegate ``IDockContent DeserializeDockContent(string persistString)`` 
only class name is used to reconstruct the layout.

The current design gives you flexibility to control what other information about each dock 
items to be persisted, as the method ``DockContent.GetPersistString()`` can be overridden 
by derived classes. By properly overriding it, extra data (such as custom data about the 
internal components of a dock item) can be appended to the string. Thus, when the layout 
is reconstructed, the extended persist string can be analyzed and extra data can be extracted and used.

Related Resources
-----------------

- :doc:`/getting-started/installing-on-windows`
- :doc:`/tutorials/basics`
- :doc:`/tutorials/customizing-dockcontent`
- :doc:`/tutorials/customizing-dockwindow`
- :doc:`/tutorials/customizing-floatwindow`
- :doc:`/themes/existing-themes`