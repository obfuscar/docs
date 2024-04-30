Project History
===============

The popularity of managed programming languages and their ease of
decompilation introduce a common issue, "How can I protect my binaries?" [1]_.
Obfuscation has been invented to add some protection. But most of obfuscator
products are commercial and really expensive.

Started by Ryan
---------------
Ryan Williams (@drcforbin) announced the first release of an open source
obfuscator named obfuscar on May 3, 2007 [2]_ , while the initial checkin on
Google Code occurred in late April [3]_ .

It started to gain popularity and soon the following releases were published,

* 1.0.1 on May 10, 2007 [4]_
* 1.1.0 on May 18, 2007 [5]_
* 1.3.0 on Jul 12, 2007 [6]_
* 1.3.1 on Sep 12, 2007 [7]_

Resumed by Werner
-----------------
Werner (@webbie) first contributed an important patch to the project on June
19, 2007 [8]_ . He seemed to be taking care of the project since April 2009,
and made the following releases,

* 1.4.0 on Apr 24, 2009 [9]_
* 1.5.0 on Nov 06, 2009 [10]_
* 1.5.2 on Nov 20, 2009 [11]_
* 1.5.4 on ??

He was trying to upgrade the project to work with latest Cecil at that moment
under 2.0 branch, but that work was not finished.

Przemysław Rajpold(@rejpon) contributed two patches on July 29, 2010 [12]_
[13]_ . @mikael.hansen.idevio also contributed one patch on May 26, 2009.

Various Forks After 2010
------------------------
Carlo Kok from RemObjects has participated in the project since around Oct 8,
2009 [14]_ . RemObjects releases a commercial obfuscator called Oxfuscator in
early 2010, which is based on Obfuscar [15]_ . However, RemObjects still keeps
an open source version available [16]_ .

Calvin Rien (@darktable) created a fork on BitBucket on Oct 24, 2012 and
included his changes [17]_ .

Emil Johansen (@AngryAnt) forked Calvin's fork, and hosted it on GitHub [18]_ .

Inherited by Lex Li
-------------------
Lex Li was working on his commercial project
`#SNMP Pro <https://sharpsnmp.com/>`_ in Apr 2013, and came across Emil's
fork. He soon created a new fork and started to merge various patches he could
find from the Internet to this fork [19]_ .

Gradually Lex gained enough knowledge about Cecil and Obfuscar and started to
heavily change the obfuscation process so as to better serve his own needs.

Carlo from RemObjects also contributes to this new fork, since Jan 2014. The
collaboration aims to keep the two forks in sync in all possible ways, though
due to the varied needs and design goals of two parties the forks still
present significant differences.

The `project homepage <https://www.obfuscar.com>`_ is now launched, and the
latest release is 2.2.*.

.. rubric:: Footnotes

.. [1] http://en.wikipedia.org/wiki/Obfuscation_(software)
.. [2] https://groups.google.com/forum/#!topic/obfuscar/2QL0ObML40o
.. [3] https://code.google.com/p/obfuscar/source/list?num=25&start=10
.. [4] https://groups.google.com/forum/#!topic/obfuscar/ctAN-hUaIB8
.. [5] https://groups.google.com/forum/#!topic/obfuscar/SrPG1BDZgrM
.. [6] https://groups.google.com/forum/#!topic/obfuscar/aH6I8v9Q_uI
.. [7] https://groups.google.com/forum/#!topic/obfuscar/554b9QOYsx4
.. [8] https://groups.google.com/forum/#!topic/obfuscar/__vjzvP9m1o
.. [9] https://groups.google.com/forum/#!topic/obfuscar/TLyU9ybfsKg
.. [10] https://groups.google.com/forum/#!topic/obfuscar/o61if_nFeog
.. [11] https://groups.google.com/forum/#!topic/obfuscar/vsVCfSMYk3U
.. [12] https://groups.google.com/forum/#!topic/obfuscar/PYs0KNps8mk
.. [13] https://groups.google.com/forum/#!topic/obfuscar/2LY3WoU72IQ
.. [14] https://groups.google.com/forum/#!topic/obfuscar/Fy0wFMVpA9Y
.. [15] https://blogs.remobjects.com/2010/10/29/oxfuscator-introduction/
.. [16] http://code.remobjects.com/p/obfuscar
.. [17] https://bitbucket.org/darktable/obfuscar/wiki/Home
.. [18] https://github.com/AngryAnt/obfuscar
.. [19] https://github.com/obfuscar/obfuscar

Related Resources
-----------------

- :doc:`/getting-started/basics`
- :doc:`/tutorials/basics`
