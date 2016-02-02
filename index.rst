
.. Secure Peer Networking with TINC slides file, created by
   hieroglyph-quickstart on Sun Nov 15 21:40:13 2015.


===================================
Better Together: Puppet and Ansible
===================================

.. figure:: _static/config_mgmt_camp_logo.png
   :align: left
   :width: 300px

Spencer Krum, IBM

Feb 2, 2016

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


Other People
============

* OpenStack Infra Team
* Jim Blair
* Monty Taylor
* Colleen Murphy
* Hunter Haugen
* Many More

.. note::

   * Team effort


OpenStack Infrastructure
========================

* General Overview

.. note::
    * OpenStack is software
    * We test it
    * 20k tests a day at peak times
    * Jobs, test, integration, docs, release, translate

History
=======

* Started 5 years ago
* Open Source

.. note::
    * pleia jim/monty sitck figures
    * pre ansible (python shop)
    * tried chef, hard
    * went with puppet

Primary Services
================

* Code Review (gerrit)
* CI (zomg complexity)
* Code hosting (haproxy/cgit farm)
* Mailing lists(mailman)

.. note::
    * These are the things that we really need to be up
    * Our CI system is home grown and awesome

Secondary Services
==================

* wiki
* ask.openstack.org
* mailing lists
* afs/kerberos
* irc bots
* paste
* etherpad
* elk
* zanata
* graphite/grafana/grafyaml

.. note::
    * These are the things that got set up
    * Lot of community involvment here


Basics
======

* 30 'pets'
* 12 x jenkins masters
* 20 x package mirrors
* 8 x git mirrors
* ~30 elk cluster
* infinity test vms

.. note::
    * These are the things that got set up
    * Lot of community involvment here

Basics
======

* All infrastructure runs on OpenStack clouds
* Clouds donated by companies <3
* Rackspace and HPCloud at first
* Now involving BlueBox, OVH, Internap and more

.. note::
    * Maybe yours
    * HP has donated a blob of physical gear which we are clouding


References
==========

* http://git.openstack.org/cgit/openstack-infra/


Thank You
=========

.. figure:: _static/spencer_face.jpg
   :align: left

Spencer Krum

IBM

@nibalizer

nibz@spencerkrum.com

https://github.com/nibalizer/talk-thirdpartyci



