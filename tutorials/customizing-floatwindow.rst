Customizing FloatWindow
=======================

By `Ryan Rastedt`_, `Lex Li`_

This page shows you how to customize ``FloatWindow``. 

.. contents:: In this article:
  :local:
  :depth: 1

Maximizable FloatWindow
-----------------------
Out of the box, a window that is undocked to a floating state lacks a maximize button. 
Utilizing the ``Extender`` functionality of ``DockPanel`` it's easy to customize the 
``FloatWindow`` class!

The first step is to create a custom class that extends ``FloatWindow``. By default, 
``FloatWindow`` has a ``FormBorderStyle`` of ``SizableToolWindow`` which will only provide 
a close button. To expose the maximize and minimize button, set ``FormBorderStyle`` of 
the custom window to ``Sizable``,

.. code-block:: csharp

  public class CustomFloatWindow : FloatWindow
  {
      public CustomFloatWindow(DockPanel dockPanel, DockPane pane)
          : base (dockPanel, pane)
      {
          FormBorderStyle = FormBorderStyle.Sizable;
      }

      public CustomFloatWindow(DockPanel dockPanel, DockPane pane, Rectangle bounds)
          : base (dockPanel, pane, bounds)
      {
          FormBorderStyle = FormBorderStyle.Sizable;
      }
  }

Next, create a factory class to create the ``CustomFloatWindow``. This is done by implementing 
the ``IFloatWindowFactory`` interface,

.. code-block:: csharp

  public class CustomFloatWindowFactory : DockPanelExtender.IFloatWindowFactory
  {
      public FloatWindow CreateFloatWindow(DockPanel dockPanel, DockPane pane, Rectangle bounds)
      {
          return new CustomFloatWindow(dockPanel, pane, bounds);
      }

      public FloatWindow CreateFloatWindow(DockPanel dockPanel, DockPane pane)
      {
          return new CustomFloatWindow(dockPanel, pane);
      }
  }

Lastly, attach the new factory to the ``DockPanel`` control,

.. code-block:: csharp

  this.dockPanel.Extender.FloatWindowFactory = new CustomFloatWindowFactory();

Alt+Tab Support
---------------
To enable Alt+Tab between your undocked forms and your main form add this to 
your ``CustomFloatWindow`` constructors,

.. code-block:: csharp

  ShowInTaskbar = true;
  Owner = null;

Overriding Double Clicking Behavior
-----------------------------------

.. note:: This requires DockPanel Suite version 2.8 and above.

By default, when a float window's title bar is double clicked it is redocked into 
the ``DockPanel``. This behavior can be disabled (and allow the Windows default 
behavior of maximizing/restoring the window) by setting the following property 
in your ``CustomFloatWindow`` constructor,

.. code-block:: csharp

  DoubleClickTitleBarToDock = false;

Positioning for Multiple Monitors
---------------------------------
When a dock content is set to float, the created ``FloatWindow`` might be at a 
secondary monitor (depending on WinForms underlying positioning).

To force the ``FloatWindow`` to appear on a desired monitor, a custom ``FloatWindow`` 
can be created. Then override its ``SetBoundsCore`` method to check the monitors based 
on the information exposed by the ``Screen`` class.

Top-Most FloatWindow
--------------------
To make the ``FloatWindow`` top-most, simply create a custom ``FloatWindow`` class and 
set its ``TopMost`` property to true.

Related Resources
-----------------

- :doc:`/getting-started/installing-on-windows`
- :doc:`/tutorials/basics`
- :doc:`/tutorials/customizing-dockcontent`
- :doc:`/tutorials/customizing-dockwindow`
- :doc:`/tutorials/customizing-persistence`
- :doc:`/themes/existing-themes`