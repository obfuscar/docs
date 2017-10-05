Customizing DockContent
=======================

By `Ryan Rastedt`_, `Lex Li`_

This page shows you how to customize ``DockContent``. 

.. contents:: In this article:
  :local:
  :depth: 1

Bring a DockContent to Front
----------------------------
Simply call ``DockContent.Activate``. This is usually used to show a tab as active tab in code. 

Prevent The DockContent From Being Closed
-----------------------------------------
To prevent a ``DockContent`` from every being closed, utilize the ``CloseButton`` property. 
You can also utilize the ``CloseButtonVisible`` property to hide the close button when docked 
in the ``DockPanel`` control,

.. code-block:: csharp
  
  public CustomContent : DockContent
  {
      public CustomContent()
      {
          InitializeContent();

          // Prevent this content from being closed
          CloseButton = false;

          // Hide the close button so the user isn't even tempted
          CloseButtonVisible = false;
      }
  }
  
You can also use the ``OnFormClosing`` method to prevent the user from closing under certain 
conditions that cannot be determined until runtime (for example, showing a dialog box asking 
the user if they are really sure they wish to close the tab),

.. code-block:: csharp

  public CustomContent : DockContent
  {
      protected override void OnFormClosing(FormClosingEventArgs e)
      {
          bool cancel = /* add your closing validation here */;
          e.Cancel = cancel;
          base.OnFormClosing(e);
      }
  }
  
Controlling Default Height or Width When Set to Auto-Hide
---------------------------------------------------------
The property ``DockContent.AutoHidePortion`` controls the auto-hide behaviors.

A value greater than 1 indicates a pixel size, while a value less than 1 indicates a percentage 
size (as a percentage of the ``DockPanel``).

Dismissing Visible Auto-Hide Panel
----------------------------------
Usually by double clicking the the tab of an auto-hide panel it will be dismissed. Below shows how to do it in code,

.. code-block:: csharp
  
  this.dockPanel.ActiveAutoHideContent = null;
  
Switching Among Documents
---------------------------
It is possible to add keyboard shortcuts to enable switching among document tabs, not yet part of the default code base,

1. Derive from ``DockContent``.
2. Override ``ProcessCmdKey``.
3. Find the next ``DockContent`` in ``DockPanel.Documents``.
4. Call its ``Activate`` method.

Remove a DockContent From DockPanel
-----------------------------------
To release a ``DockContent`` from ``DockPanel``, simply set ``DockContent.DockHandler.DockPanel`` to ``null``.

.. code-block:: csharp

  dockContent.DockHandler.DockPanel = null;

Related Resources
-----------------

- :doc:`/getting-started/installing-on-windows`
- :doc:`/tutorials/basics`
- :doc:`/tutorials/customizing-dockwindow`
- :doc:`/tutorials/customizing-floatwindow`
- :doc:`/tutorials/customizing-persistence`
- :doc:`/themes/existing-themes`