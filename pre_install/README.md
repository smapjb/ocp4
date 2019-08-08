Pre_install
=========

The pre_install role is specific to OpenShift 4.1 on RHV
It automates the steps outlined in the baremetal install instructions.
See the tasks/main.yml

Requirements
------------

Requires a web server to upload the ignition files, and boot image to. Also requires a rhvm machine to upload to an ISO domain. (note that it should be possible to do that via the API - but that is not currently exposed by rhev)

Role Variables
--------------

See defaults/main.yml for variables that can be overridden

Dependencies
------------

There are no dependencies on other roles. This role is currently used by the bootstrap.yml in cluster_install.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

      roles:
        # Download the installation program and set up the boot resources and ignition config
        - pre_install

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
