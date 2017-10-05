Installing DockPanel Suite On Windows
=====================================

By `Lex Li`_

This page shows you how to install DockPanel Suite to your project on Windows. 

.. contents:: In this article:
  :local:
  :depth: 1

Install DockPanel Suite via NuGet
---------------------------------

The easiest way to get started building applications with DockPanel Suite is to install via NuGet in the latest version of Visual Studio 2015 (including the free Community edition). 

1. Install `Visual Studio 2015 <https://go.microsoft.com/fwlink/?LinkId=532606>`_ .

  Be sure to specify that you include the Windows and Web Development.

2. Install latest `NuGet Package Manager <https://docs.nuget.org/consume/installing-nuget>`_ . 
  
  This will install the latest NuGet tooling.

3. Open/create an empty Windows Forms project.
  
4. Install DockPanel Suite NuGet packages following `NuGet conventions <https://docs.nuget.org/Consume/Package-Manager-Dialog>`_ . 

  The latest packages can be found at,
  
  * `Main Library with VS2005 Theme <https://www.nuget.org/packages/DockPanelSuite/>`_ .
  * `VS2003 Theme <https://www.nuget.org/packages/DockPanelSuite.ThemeVS2003/>`_ .
  * (2.10) `VS2012 Light Theme <https://www.nuget.org/packages/DockPanelSuite.ThemeVS2012Light/>`_ .
  * (2.11+) `VS2012 Themes <https://www.nuget.org/packages/DockPanelSuite.ThemeVS2012/>`_ .
  * (2.10) `VS2013 Blue Theme <https://www.nuget.org/packages/DockPanelSuite.ThemeVS2013Blue/>`_ .
  * (2.11+) `VS2013 Themes <https://www.nuget.org/packages/DockPanelSuite.ThemeVS2013/>`_ .
  * `VS2005 Theme for Multiple UI Threads <https://www.nuget.org/packages/DockPanelSuite.ThemeVS2005Multithreading/>`_ .

  .. note:: ``VS2005MultithreadingTheme`` is not recommended for general usage.*

  .. warning:: Theme package version should match main library version whenever possible. Otherwise, there can be compatibility issues.

5. Create the ``DockPanel`` control in code and insert to the main form

.. code-block:: csharp

  public MainForm()
  {
      InitializeComponent();
      
      this.dockPanel = new WeifenLuo.WinFormsUI.Docking.DockPanel();
      this.dockPanel.Dock = System.Windows.Forms.DockStyle.Fill;
      this.Controls.Add(this.dockPanel); 
  }
  
6. Create other panels by creating a new ``Form`` or new ``UserControl`` in Visual Studio

.. code-block:: csharp

  public class NewForm : Form
  {
  
  }

Change the base type to ``WeifenLuo.WinFormsUI.Docking.DockContent``
  
.. code-block:: csharp
  
  public class NewDockContent : WeifenLuo.WinFormsUI.Docking.DockContent
  {
  
  }
  
7. Show the custom ``DockContent`` in ``DockPanel`` as a document

.. code-block:: csharp

  public void ShowDockContent()
  {
      var dockContent = new NewDockContent();
      dockContent.Show(this.dockPanel, DockState.Document);
  }
  
Install DockPanel Suite via Source Code
---------------------------------------
.. note:: This approach requires Visual Studio 2015 and above. Please switch to NuGet package approach if you use older VS releases.

DockPanel Suite source code can be directly used in your project. 

1. Download the source code from `GitHub <https://github.com/dockpanelsuite/dockpanelsuite/releases>`_ , or clone the repo directly.

2. Open/create a empty Windows Forms project in a solution.

3. Add WinFormsUI.csproj in ``WinFormsUI`` directory to your solution.

4. (optional) Add other theme projects such as ThemeVS2003.csproj to your solution.
 
5. Compile the solution and DockPanel Suite controls are automatically added to Toolbox panel.

6. Open main form of the empty project, and drag the ``DockPanel`` control from Toolbox on to it.

  This will let Visual Studio generate the necessary code.

7. Create other panels by creating new ``Form`` or new ``UserControl`` in Visual Studio

.. code-block:: csharp

  public class NewForm : Form
  {
  
  }

Change the base type to ``WeifenLuo.WinFormsUI.Docking.DockContent``
  
.. code-block:: csharp
  
  public class NewDockContent : WeifenLuo.WinFormsUI.Docking.DockContent
  {
  
  }
  
8. Show the custom ``DockContent`` in ``DockPanel`` as a document

.. code-block:: csharp

  public void ShowDockContent()
  {
      var dockContent = new NewDockContent();
      dockContent.Show(this.dockPanel, DockState.Document);
  }

Compile DockPanel Suite from Source Code
----------------------------------------
1. Download the source code from `GitHub <https://github.com/dockpanelsuite/dockpanelsuite/releases>`_ , or clone the repo directly.
2. Install .NET Framework 4.0 (or above) if it is not yet installed.
3. Install Visual Studio 2015 (like Community edition) or above.
4. Run ``all.bat`` in the source code to start compilation.

If everything works, then the binaries are in the ``bin`` folder.

Related Resources
-----------------

- :doc:`/getting-started/installing-in-visualstudio`
- :doc:`/getting-started/history`
- :doc:`/tutorials/basics`
- :doc:`/themes/existing-themes`
