
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
    * Heavy CI/CD culture, everything goes through git, delpoy - grafana

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


Example of where we were at
==========================

.. code-block:: shell

    if [ -n "$NODEPOOL_SSH_KEY" ] ; then
        puppet_install_users="install_users => false,
    ssh_key => '$NODEPOOL_SSH_KEY',"
    else
        puppet_install_users=""
    fi

    cat >/tmp/local.pp <<EOF
    class {'openstack_project::single_use_slave':
      sudo => $SUDO,
      thin => $THIN,
      install_resolv_conf => false,
      $puppet_install_users
    }
    EOF

    puppet apply /tmp/local.pp

.. note::
    * Some but not all of the terribleness has been preserved
    * run this in prod


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


Need basic orchestration
========================

.. code-block:: shell

    commit b55ed05a274e5da40b567ad127a3d1c5808e48c6
    Author: Monty Taylor <mordred@inaugust.com>
    Date:   Mon Mar 17 04:01:33 2014 -0400

        Drive puppet from the master over ssh
        
        We'd like to be able to control sequencing of how and when puppet
        runs across our machines. Currently, it's just a set of agents
        that run kinda whenever they run. At times they hang and we don't
        know about it. Also, cross-server sequencing is impossible to
        achieve.
        
        Change the operation away from agents running on the machine as
        daemons, and instead ssh from the master to each machine.
        
        Change-Id: I76e41e63c6d0825e8735c484ba4580d545515e43

.. note::
    * /opt/config/production/run_all.sh
    * 'override hosts'
    * gave us limited Do X before Y
    * create repos in git slaves before creating them in the git master
    * replication in the git-master is a bit derpy
    * "this allows creation of git repos on the git slaves before creation of the master repos on the gerrit server"


Need basic orchestration
========================

.. code-block:: shell

    commit 034f37c32aed27d8000e1dc3a8a3d36022bcd12a
    Author: Monty Taylor <mordred@inaugust.com>
    Date:   Tue Apr 15 17:41:45 2014 -0700

        Use ansible instead of direct ssh calls
        
        Instead of a shell script looping over ssh calls, use a simple
        ansible playbook. The benefit this gets is that we can then also
        script ad-hoc admin tasks either via playbooks or on the command
        line. We can also then get rid of the almost entirely unused
        salt infrastructure.
        
        Change-Id: I53112bd1f61d94c0521a32016c8a47c8cf9e50f7

.. note::
    * Yes there was a ancient salt infra crusting


Puppet Inventory
================

.. code-block:: shell

    import json
    import subprocess

    output = [
        x.split()[1][1:-1] for x in subprocess.check_output(
            ["puppet","cert","list","-a"]).split('\n')
        if x.startswith('+')
    ]

    data = {
        '_meta': {'hostvars': dict()},
        'ungrouped': output,
    }
    print json.dumps(data, sort_keys=True, indent=2)



References
==========

* All infra repos: http://git.openstack.org/cgit/openstack-infra/
* Main Control repo: http://git.openstack.org/cgit/openstack-infra/system-config
* Apply test: http://git.openstack.org/cgit/openstack-infra/system-config/tree/tools/apply-test.sh
* OpenStack CI http://docs.openstack.org/infra/openstackci/


References: shas
================

* Drive puppet from ssh edaa31ebbda09fb03baf1d18b64f5fa996188745
* Move from ssh to ansible: 034f37c32aed27d8000e1dc3a8a3d36022bcd12a



Thank You
=========

.. figure:: _static/spencer_face.jpg
   :align: left

Spencer Krum

IBM

@nibalizer

nibz@spencerkrum.com

https://github.com/nibalizer/talk-thirdpartyci



