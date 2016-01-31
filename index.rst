
.. Secure Peer Networking with TINC slides file, created by
   hieroglyph-quickstart on Sun Nov 15 21:40:13 2015.


=======================
Advisory Third Party CI
=======================

.. figure:: _static/config_mgmt_camp_logo.png
   :align: left
   :width: 300px

Spencer Krum, IBM

Feb 1, 2016

@nibalizer

http://spencerkrum.com


.. note::

   * Who am I
   * What do I work on
   * github


Portland
========

.. figure:: _static/mt_hood.jpg
   :align: center


Agenda
======


* Introduction
* Basic Idea
* Audience Participation
* More examples
* Call to action



.. note::

   * Not a super new idea


Other People
============

* Jim Blair
* Anita Kuno
* Mike Perez
* Hunter Haugen
* Bryan Jen
* Emilien Macchi
* Daniele Sluijters
* Many More

.. note::

   * Not a super new idea

CI Definition
=============

Good idea: Run tests

Better idea: Run tests for every pull request

Best idea: Don't merge code unless tests pass


Topic
=====

Advisory Third Party CI


.. note::

    * one word at a time


Example
=======

#TODO picture of pcci voting on puppetlabs-haproxy

.. note::

    * running live


An average day
==============

D1: All the tests are failing

D2: Yep, fog released and now everything is bad

D1: ...


Why do this
===========

"Not using a local repo is like having unprotected sex with the internet"

-ACS

Sysadmins
=========

"Why would you upgrade anything EVER?!?!?"

-James Mickens


The Point
=========

Code you use will break less

The Point
=========

Code you use will break, *you* less


Setting up a test for a library
===============================

1) Follow pull requests on that library
2) Pull library from git into test env
3) Pull code from a project that uses library, where the project is known to pass tests
4) Run the projects tests.
5) Report the results as CI information for library



Testing Order
=============

* 1st Order: my code, my test, my testing
* 2nd Order: your code, your test, my testing
* 3rd Order: my code, my other code, my test, my testing
* 4th Order: your code, my code, my test, my testing

.. note::

    * 1st order very classic testing
    * 2nd order, what does that look like
    * 3rd order, super advanced
    * 4th orger crazypants


1st Order
=========

* Already doing this

.. note::

    * Describe the steps
    * Particularly around gem install or puppet module install


2nd Order
=========

* Already doing this


3rd Order
=========

* Already doing this

4th Order
=========

* Already doing this



OpenStack Infrastructure
========================

* General Overview

.. note::
    * OpenStack is software
    * We test it
    * 20k tests a day at peak times
    * Jobs, test, integration, docs, release, translate


OpenStack CI Neat features
==========================


* Linearlized merge queue
* Gate collections
* Depends-On
* Docs only patches
* Releases



Thank You
=========

.. figure:: _static/spencer_face.jpg
   :align: left

Spencer Krum

IBM

@nibalizer

nibz@spencerkrum.com

https://github.com/nibalizer/talk-thirdpartyci



