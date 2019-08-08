# ocp4

This was a private repo for my own private lab, but I have opened it up in case there are some useful things.

Note this is work in progress - there are still some environment specific things in the code

Assumed pre-requisites
1. You have RHEV 4.3
2. You have a web server to host the boot image and ignition files (we use ClearOS for this).
3. You have a dnsmasq server serving up DHCP and DNS (we use ClearOS for this)
4. You have a rhel7_template to clone a machine from for haproxy

Driving playbook is 
```
ansible-playbook cluster_install/site.yml  -e cluster_name=<domain_prefix>
```

## What does it do?

Look at the cluster_install/site.yml and the subsequent included files.

The cluster install uses in memory inventory as each of the machines is provisioned

For more details on each of the roles see the README at the root of the role directory.

Roughly this is what the installer does.
1. Provision from RHEL template an haproxy configured as a layer 4 load balancer. All provisioning includes setting DNS for the newly created machines.
2. Download the oc and oc installer, generate the ignition files and upload them to a web server (in this case ClearOS), download the metal BIOS boot image and make that available in the web server (ClearOS), download the initrd and kernel image and upload them via the rhvm using engine-iso-uploader so they can be used in RHV at iso:// url. Create a disk, and attach to a new image to boot from kernel and initrd setting bootparams to point to bootstrap ignition and bios image, update dns enable the bootstrap cluster.
3. Provision the masters asynchronously using the setup created in step 2. Update haproxy config based on in memory inventory
4. Provision the workers and then run the openshift installer to boostrap the cluster on the masters
5. Install the guest agent using rpm-ostree and reboot all machines
6. Remove the bootstrap machine, patch the registry to enable storage, run the openshift installer to wait for cluster to be up.
 
