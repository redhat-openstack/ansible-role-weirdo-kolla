ansible-role-weirdo-kolla
-------------------------
This role provides an implementation of the
Kolla_ gate jobs for the WeIRDO_ project.

.. _Kolla: https://github.com/openstack/kolla
.. _WeIRDO: https://github.com/redhat-openstack/weirdo

Supported gate jobs
~~~~~~~~~~~~~~~~~~~

* gate-kolla-dsvm-build-centos-binary
* gate-kolla-dsvm-deploy-centos-binary

Role variables
~~~~~~~~~~~~~~

For default values, see `defaults/main.yml`_

* ``project``: Name of the project, analogous to the role name
* ``openstack_release``: Name of the OpenStack release to select which trunk repository to use by default
* ``version``: Version/tag/branch of Kolla to clone
* ``repository``: URL to the Kolla repository
* ``clone_path``: Path where Kolla will be cloned
* ``delorean_url``: URL to the delorean repository .repo file.
* ``delorean_deps_url``: URL to the delorean-deps repository .repo file.
* ``loopback_device``: Name of the loopback device for Docker block device
* ``required_packages``: Required packaged dependencies to install prior to running the tests
* ``base_pip_packages``: Required pip packages to install prior to running the tests

.. _defaults/main.yml: https://github.com/redhat-openstack/ansible-role-weirdo-kolla/blob/master/defaults/main.yml

Included tasks
~~~~~~~~~~~~~~

* ``packages``: Ensures required dependencies are installed
* ``setup``: Configures a block device for usage with Docker, clones the
  repository and installs the requirements.
* ``run``: Runs the integration tests

Dependencies
~~~~~~~~~~~~

`ansible-role-weirdo-common`_ to be installed as ``common``

.. _ansible-role-weirdo-common: https://github.com/redhat-openstack/ansible-role-weirdo-common

Example playbook
~~~~~~~~~~~~~~~~

.. code-block:: yaml

    - name: Run kolla build tests
      hosts: openstack_nodes
      force_handlers: True
      roles:
        - { role: "kolla", test: "build-centos-binary" }
