..
 This work is licensed under a Creative Commons Attribution 3.0 Unported
 License.

 http://creativecommons.org/licenses/by/3.0/legalcode

========================
Neutron-vpnaas Scorecard
========================

Neutron integration
-------------------

.. _N0:

* N0. Does the project use the Neutron REST API or relies on proprietary backends?

  Yes. Neutron-vpnaas implements its own set of Neutron API extensions on top of
  the Neutron core framework and it does so by using the service plugin model.
  The API exposed has open source implementations, and it provides a pluggable
  mechanism for proprietary backends.

.. _N1:

* N1. Does the project integrate/use neutron-lib?

  Yes. The migration report shows that there are currently 598 total imports.
  Neutron is imported 112 times and Neutron-lib 77 times, for a migration
  percentage of 40.7400%.

.. _N2:

* N2. Do project members actively contribute to help neutron-lib achieve its
  goal?

  No. None of the project core members have merged anything meaningful into neutron-lib
  (source: https://review.openstack.org/#/q/project:openstack/neutron-lib+status:merged,75).

.. _N3:

* N3. Do project members collaborate with the core team to enable subprojects
  to loosely integrate with the Neutron core platform by helping with the definition
  of modular interfaces?

  Yes.

  * https://github.com/openstack/neutron-vpnaas/commit/7c10c41376f10898347cbc644d8d504b8258c99c

.. _N4:

* N4. How does the project provide networking services? Does it use modular interfaces
  as provided by the core platform?

  Yes, for the most part, but as far as the agent side is concerned, the project relies
  on the use of a VPN agent that specializes the base L3 agent, this is prone to breakage,
  and leads to deployment complications when VPN and L3 services are deployed together.
  This problem has been filed as a bug to track the work. And it is being working slowly.

  * https://github.com/openstack/neutron-vpnaas/blob/master/neutron_vpnaas/services/vpn/agent.py#L46
  * https://bugs.launchpad.net/neutron/+bug/1692128
  * https://review.openstack.org/#/c/488247/

.. _N5:

* N5. If the project provides new API extensions, have API extensions been discussed
  and accepted by the Neutron drivers team? Please provide links to API specs, if
  required.

  VPNaaS API was initially created by the neutron core team, and so implicitly had been
  agreed upon by previous core team.


Documentation
-------------

.. _D1:

* D1. Does the project have a doc tox target, functional and continuously
  working? Provide proof (links to logs.openstack.org).

  Yes.

  * https://github.com/openstack/neutron-vpnaas/blob/master/tox.ini
  * http://docs-draft.openstack.org/09/480809/2/gate/gate-neutron-vpnaas-docs-ubuntu-xenial/8209306//doc/build/html/

.. _D2:

* D2. If the project provide API extensions, does the project have an
  api-ref tox target, functional and continously working? Provide proof
  (links to logs.openstack.org).

  Yes. There is an API reference and is being confirmed its accuracy, see:

  * https://review.openstack.org/#/c/447345/

  * http://developer.openstack.org/api-ref/networking/
  * https://github.com/openstack/neutron-lib/blob/master/api-ref/source/v2/vpnaas.inc

.. _D3:

* D3. Does the project have a releasenotes tox target, functional and
  continously working? Provide proof.

  Yes.

  * https://github.com/openstack/neutron-vpnaas/blob/master/tox.ini
  * http://docs.openstack.org/releasenotes/neutron-vpnaas/
  * http://docs-draft.openstack.org/74/483374/2/check/gate-neutron-vpnaas-releasenotes/f8f42ee//releasenotes/build/html/

.. _D4:

* D4. Describe the types of documentation available: developer, end user,
  administrator, deployer.

  Yes. These documentations are going to be published, see:

  * https://review.openstack.org/#/c/482510/
  * https://review.openstack.org/#/c/446835/

  * http://docs-draft.openstack.org/26/303226/26/check/gate-neutron-vpnaas-docs-ubuntu-xenial/3776f6d//doc/build/html/
  * http://docs-draft.openstack.org/10/482510/1/check/gate-neutron-docs-ubuntu-xenial/9a5a443//doc/build/html/admin/vpnaas-scenario.html


Continuous Integration
----------------------

.. _C1:

* C1. Does the project have a Grafana dashboard showing historical trends of
  all the jobs available? Provide proof (links to grafana.openstack.org).

  Yes.

  * http://grafana.openstack.org/dashboard/db/neutron-vpnaas-failure-rates

.. _C2:

* C2. Does the project have CI for unit coverage? Provide proof (links to
  logs.openstack.org)

  Yes.

  * http://status.openstack.org/openstack-health/#/g/project/openstack~2Fneutron-vpnaas

.. _C3:

* C3. Does the project have CI for functional coverage? If so, does it include
  DB migration and sync validation?

  Yes. We have gate-neutron-vpnaas-dsvm-functional-sswan-ubuntu-xenial for
  functional coverage and DB migration tests are running as a part of it.

  * http://status.openstack.org/openstack-health/#/job/gate-neutron-vpnaas-dsvm-functional-sswan-ubuntu-xenial

.. _C4:

* C4. Does the project have CI for fullstack coverage?

  No. We consider it as lower priority and it has none at the moment.

.. _C5:

* C5. Does the project have CI for Tempest coverage? If so, specify nature
  (API and/or Scenario).

  Yes.

  * http://logs.openstack.org/89/475289/1/gate/gate-neutron-dsvm-tempest-vpnaas-ubuntu-xenial/4096e05/testr_results.html.gz

.. _C6:

* C6. Does the project require CI for Grenade coverage?

  Yes. But it has none.

.. _C7:

* C7. Does the project provide multinode CI?

  No. But it is needed to support L3-HA (and/or DVR) and unnecessary until then.

.. _C8:

* C8. Does the project support Python 3.x? Provide proof.

  Yes.

  * http://status.openstack.org/openstack-health/#/job/gate-neutron-vpnaas-python35

Release footprint
-----------------

.. _R1:

* R1. Does the project adopt semver?

  Yes.

.. _R2:

* R2. Does the project have release deliverables? Provide proof as available
  in the `release repo <http://git.openstack.org/cgit/openstack/releases/tree/>`_.

  Yes.

  * https://tarballs.openstack.org/neutron-vpnaas/neutron-vpnaas-10.0.0.tar.gz

.. _R3:

* R3. Does the project use upper-constraints?

  Yes.

  * https://github.com/openstack/neutron-vpnaas/blob/master/tox.ini#L10

.. _R4:

* R4. Does the project integrate with OpenStack Proposal Bot for requirements updates?

  * Yes.

  * https://github.com/openstack/requirements/commit/1d545edbebfff2e8983d6cab24a92c32636dd6bf


Stable backports
----------------

.. _S1:

* S1. Does the project have stable branches and/or tags? Provide history of
  backports.

  Yes. For example: https://git.openstack.org/cgit/openstack/neutron-vpnaas/log/?h=stable/ocata


Client library
--------------

.. _L1:

* L1. If the project requires a client library, how does it implement CLI and
  API bindings?

  Yes. There are Neutron CLI and API bindings. OSC is going to be done, see:

  * https://review.openstack.org/#/c/439978/


Scorecard
---------

+---------------+
| Scorecard     |
+===============+
| N0_ |    Y    |
+---------------+
| N1_ |    Y    |
+---------------+
| N2_ |    N    |
+---------------+
| N3_ |    Y    |
+---------------+
| N4_ |    N    |
+---------------+
| N5_ |    Y    |
+---------------+
| D1_ |    Y    |
+---------------+
| D2_ |    Y    |
+---------------+
| D3_ |    Y    |
+---------------+
| D4_ |    Y    |
+---------------+
| C1_ |    Y    |
+---------------+
| C2_ |    Y    |
+---------------+
| C3_ |    Y    |
+---------------+
| C4_ |    N    |
+---------------+
| C5_ |    Y    |
+---------------+
| C6_ |    N    |
+---------------+
| C7_ |    N    |
+---------------+
| C8_ |    Y    |
+---------------+
| R1_ |    Y    |
+---------------+
| R2_ |    Y    |
+---------------+
| R3_ |    Y    |
+---------------+
| R4_ |    Y    |
+---------------+
| S1_ |    Y    |
+---------------+
| L1_ |    Y    |
+-----+---------+


Final remarks
-------------

At the time of writing the project scores changed to positively if compared
with the last assessment [1]_ [2]_ for following 6 criteria: N3_, D2_, D4_,
C1_, C5_, L1_. It makes the project scores positively in 19 out of 24 criteria.
The subproject does not seem to lack the resources recently and the remaining
gaps can be focused to make timely progress when required.


References
----------
.. [1] https://specs.openstack.org/openstack/neutron-specs/specs/stadium/ocata/neutron-vpnaas.html#scorecard
.. [2] https://specs.openstack.org/openstack/neutron-specs/specs/stadium/ocata.html#summary
