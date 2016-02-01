
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


OpenStack Infrastructure
========================

* General Overview

.. note::
    * OpenStack is software
    * We test it
    * 20k tests a day at peak times
    * Jobs, test, integration, docs, release, translate


VoxPupuli
=========

* "Voice of the Puppets"

.. note::
    * Community thing
    * PCCI
    * VPCI


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
    * if you own a github repo
    * if you depend on code in a github repo


Example
=======

.. figure:: _static/pcci_voting.png
   :align: center


.. note::

    * running live
    * 3 things you get from this
      ** code works better
      ** developers value my system, I get my bugs looked at
      ** I run their code in my environment so it wont regress my stuff


Pause for Audience Participation
================================

Pausing

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

Example
=======

.. figure:: _static/pcci_voting.png
   :align: center


.. note::

    * running live
    * 3 things you get from this
      ** code works better
      ** developers value my system, I get my bugs looked at
      ** I run their code in my environment so it wont regress my stuff


Example
=======

.. figure:: _static/cinder_ci.png
   :align: center


.. note::

    * running live
    * Environmental control
    * plugin configuration
    * selective testing

Example
=======

.. figure:: _static/k8s_code.png
   :align: center


.. note::

    * running live
    * Environmental control
    * plugin configuration
    * selective testing




Testing Order
=============

* 0th Order: my code, my test, my testing
* 1st Order: your code, your test, my testing
* 2nd Order: your code, your test, my environment, my testing
* 3rd Order: your code, my code, my test, my testing

.. note::

    * 0th order very classic testing
    * 1st order, what does that look like
    * 2nd order, super advanced
    * 3rd order crazypants



The Pitch
=========

More advisory third-party CI

.. note::

    * I want us to start setting this up all over the place
    * Code will break less
    * Devs will be happier
    * Breaking changes will be caught
    * Kylo during the puppet4 work would get in irc and ask general question like 'is anyone using this internalish api?'
    * third party ci provides a way to communicate your usage of the software
    * my hope is you will all build systems
    * not a pitch about using the things I made


Setting up a test for a library
===============================

1) Follow pull requests on that library
2) Pull library from git into test env
3) Pull code from a project that uses library, where the project is known to pass tests
4) Run the projects tests.
5) Report the results as CI information for library

.. note::

    * Really #2 is the magic

The Part where I give you things
================================

Functions to help set up git repos: http://git.openstack.org/cgit/openstack-infra/devstack-gate/tree/functions.sh
Functions to help set up installed libraries: http://git.openstack.org/cgit/openstack-dev/devstack/tree/functions-common


.. note::

    * OpenStack Devstack-gate
    * Super Test
    * becomes less about git clone, run tests
    * more about mix up a specific soup, then run entrypoint.sh


The Part where I give you things
================================

Github pull request follower: https://github.com/voxpupuli/vpci/blob/master/vpci/github_task_creator.py

.. note::

    * Need a list of things to do
    * Github post hooks insufficient
    * Pushes a list of pull requests on to a queue
    * Uses a database to keep track of what has and has not been updated

The Part where I give you things
================================

Github CI Ball Poster: https://github.com/voxpupuli/pcci/blob/master/comment.py

.. note::

    * Pops things off of a queue
    * Sets CI status
    * Requires pygithub from git master


Github Balls
============

.. code-block:: python

    if success == 0:
        status = 'success'
    else:
        status = 'failure'
    commit.create_status(
        status,
        target_url=log_path,
        description="PCCI Voting System",
        context="continuous-integration/pcci-{0}".format(nodeset))

.. note::

    * Pops things off of a queue
    * Sets CI status
    * Requires pygithub from git master


OpenStack CI Neat features
==========================


* Linearlized merge queue
* Gate collections
* Depends-On
* Docs only patches
* Releases
* Refs creation and server


References
==========

* https://wiki.openstack.org/wiki/Cinder/tested-3rdParty-drivers#How_do_I_run_my_CI_to_test_all_cinder_patches_with_my_driver_not_yet_merged.3F
* http://lists.openstack.org/pipermail/openstack-dev/2016-January/084042.html
* https://github.com/kubernetes/kubernetes/pull/17700
* https://github.com/voxpupuli/vpci
* https://github.com/voxpupuli/pcci
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



