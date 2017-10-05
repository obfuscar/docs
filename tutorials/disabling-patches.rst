Disabling Patches (2.11+)
=========================

By `Lex Li`_

This page shows you how to disable certain community patches of DockPanel Suite. 

.. contents:: In this article:
  :local:
  :depth: 1

Community Patches
-----------------
DockPanel Suite has a very strong developer community where people fork and refine this library with bug fixes and new features. As
maintainers, instead of waiting for pull requests we evaluate such commits from time to time and merge them if they are mature and 
really useful.

However, it would be difficult to assert the quality of such patches, especially when we cannot easily contact the original developers 
or fully understand the code base.

Patch Controller Design
-----------------------
In order to make patch evaluation more efficient, a mechanism called Patch Controller is designed for 2.11+.

This allows us to ship selected patches and turn them on by default, which gives a bigger audience opportunities to play with the patches. 
It would be more likely that we receive bug reports and feedbacks on such patches. Of course, this mechanism also allows users to disable 
the patches individually.

To disable all patches, the following code can be used,

.. code-block:: csharp

  PatchController.EnableAll = false;

To disable all patches without modifying source code, the following custom section can be used in ``app.config`` or ``web.config``,

.. code-block:: xml

  <?xml version="1.0" encoding="utf-8" ?>
  <configuration>
    <configSections>
      <section name="dockPanelSuite" type="WeifenLuo.WinFormsUI.Docking.Configuration.PatchSection, Tests3"/>
    </configSections>
    <dockPanelSuite enableAll="false" />
  </configuration>

To disable a patch in code, such as the HiDPI patch, the following code can be used,

.. code-block:: csharp

  PatchController.EnableHighDpi = false;

To disable a patch such as the HiDPI patch without modifying source code, the following section can be used in ``app.config`` or 
``web.config``,

.. code-block:: xml

  <?xml version="1.0" encoding="utf-8" ?>
  <configuration>
    <configSections>
      <section name="dockPanelSuite" type="WeifenLuo.WinFormsUI.Docking.Configuration.PatchSection, Tests3"/>
    </configSections>
    <dockPanelSuite enableHighDpi="false" />
  </configuration>

To disable a patch such as the HiDPI patch via environment variable, please set "DPS_EnableHighDpi" to "false".

To disable a patch such as the HiDPI patch via registry key, please create a key named "Software\DockPanelSuite", and create a string 
value named "EnableHighDpi" which should be set to "false".

Current Patches in Testing
--------------------------
There are several patches included in 2.11 for testing. They are,

* `GitHub #155 a focus lost fix <https://github.com/dockpanelsuite/dockpanelsuite/issues/321>`_
* `GitHub #291 an exception fix <https://github.com/dockpanelsuite/dockpanelsuite/issues/291>`_
* `GitHub #318 a flicker fix <https://github.com/dockpanelsuite/dockpanelsuite/issues/318>`_
* `GitHub #320 a HiDPI fix <https://github.com/dockpanelsuite/dockpanelsuite/issues/320>`_
* `GitHub #321 a memory leak fix <https://github.com/dockpanelsuite/dockpanelsuite/issues/321>`_

More might be added in the next few weeks before the final release.

The magic words to disable them can be found in `this source file <https://github.com/dockpanelsuite/dockpanelsuite/blob/master/WinFormsUI/Docking/PatchController.cs>`_ .
