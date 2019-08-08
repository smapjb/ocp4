Role Name
=========

This role will provision single and multiple machines suitable for installing an openshift cluster using the baremetal install method. It manages inventory in memory and maintains a datastructure suitable for constructing
hosts file entries. 
The role also updates a dnsmasq style service.

Requirements
------------

The provisioner is for RHV 4.3, and also requires a ClearOS gateway that provides DHCP and DNS to the provisioned machines. clearos.com
ClearOS has a rest API where we can query what IP has been given to a machine early in the boot cycle. This allows us to set up the DNS correctly which is a 
hard requirement for an openshift cluster.

Role Variables
--------------

See default/main.yml

Dependencies
------------

Not dependent on any other roles

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - name: Provision the permanent cluster master machines and haproxy
      hosts: localhost
      gather_facts: False
    
      roles:
        # Cannot asyncronously loop over an include or role - and looping over a role include is about as many lines of code for the number of machines that we are provisioning
        # Best option is to add async directly into the provision role and pass a sequence start / end variables
        - role: provision
          single_machine: False
          sequence_start: 0
          sequence_end: 2
          host_memory: 16
          sockets: 4
          disk_size: 40
          machine_type: rhcos
          node_type: master
          hostname_prefix:
            - master0
            - etcd-


License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
