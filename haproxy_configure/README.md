HAPROXY Configure
=========

This role works on a clean rhel 7 machine and installs and configures haproxy suitable for bootstrapping and running an openshift 4.1 cluster.

Requirements
------------

Requires a rhel7 machine, requires details for subscribing rhel to RHN
Uses in memory inventory built up from the provisioner role.

This role is designed to be used in conjunction with the provisioner role. 
The provisioner role builds up the inventory that is used to build the configuration for haproxy.

Role Variables
--------------

See defaults/main.yml

Dependencies
------------

Designed to be used in conjunction with the provision role.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    # Now that all the machines have been provisioned we can configure haproxy (validation of the config will fail if machines are not set up correctly)
    - name: Install and configure haproxy
      hosts: "haproxy.{{ cluster_name }}.{{ domain_name }}"
      remote_user: root
    
      roles:
          # Role to install haproxy and configure it for the openshift cluster - requires in memory inventory from provisioning play above
        - haproxy_configure

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
