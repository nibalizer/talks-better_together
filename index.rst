
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


Codesearch
==========

.. figure:: _static/codesearch.png
   :align: center

* http://codesearch.openstack.org

.. note::
    * codesearch.openstack.org
    * hound from etsy
    * deployed by outreachy intern
    * use our puppet module!
    * wicked fast

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
    * Run our services on the public internet

Puppet circa 2014
=================

* 2.7 Master
* Passenger
* Generated certs, w/ push
* CI/CD
* install_modules.sh
* puppet-lint test
* some public modules
* single puppet repo

.. note::
    * Single puppetmaster
    * launch_node.py would build a machine w/ openstack apis and push in a puppet cert
    * near-perfect cd
    * install_modules.sh was sortof r10kish
    * public modules were all really old versions
    * public internet, rouge puppet certs


Upgrades to the puppet setup
============================

* 3.x
* PuppetDB + PuppetBoard
* Modules split out
* Started using newer public modules
* Upgraded apache

.. note::
    * 3.x happened right as 2.7 Eol'd for the last time
    * launch_node.py would build a machine w/ openstack apis and push in a puppet cert
    * near-perfect cd
    * install_modules.sh was sortof r10kish
    * public modules were all really old versions

Upgrades to the puppet setup: Apply test
========================================

* Apply test http://git.openstack.org/cgit/openstack-infra/system-config/tree/tools/apply-test.sh

.. code-block:: shell

    file=$1
    fileout=${file}.out
    echo "##" > $fileout
    cat $file > $fileout
    sudo puppet apply --noop --verbose --debug $file >/dev/null 2>> $fileout
    ret=$?
    cat $fileout
    exit $ret

.. note::
    * 3.x happened right as 2.7 Eol'd for the last time
    * launch_node.py would build a machine w/ openstack apis and push in a puppet cert
    * near-perfect cd
    * install_modules.sh was sortof r10kish
    * public modules were all really old versions

Upgrades to the puppet setup: OpenStackCI
=========================================

* Control Repo Indirector
* Puppet module

.. note::
    * Open Source when you release
    * Open source when you get users
    * Wraps Daemons and configuration
    * All-in-one node deployment



References
==========

* All infra repos: http://git.openstack.org/cgit/openstack-infra/
* Apply test: http://git.openstack.org/cgit/openstack-infra/system-config/tree/tools/apply-test.sh
* OpenStack CI http://docs.openstack.org/infra/openstackci/


Thank You
=========

.. figure:: _static/spencer_face.jpg
   :align: left

Spencer Krum

IBM

@nibalizer

nibz@spencerkrum.com

https://github.com/nibalizer/talk-thirdpartyci



