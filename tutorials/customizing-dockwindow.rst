Customizing DockWindow
======================

By `Lex Li`_

This page shows you how to customize ``DockWindow``. 

.. contents:: In this article:
  :local:
  :depth: 1

Change DockWindow Z-Order
-------------------------
There are four ``DockWindow`` instances created in ``DockPanel`` control, where later new ``DockContent`` instances
can be inserted to. By changing their Z-order, the layout style can be controlled.

.. code-block:: csharp

  this.dockPanel.UpdateDockWindowZOrder(DockStyle.Right, true);

Related Resources
-----------------

- :doc:`/getting-started/installing-on-windows`
- :doc:`/tutorials/basics`
- :doc:`/tutorials/customizing-dockcontent`
- :doc:`/tutorials/customizing-floatwindow`
- :doc:`/tutorials/customizing-persistence`
- :doc:`/themes/existing-themes`