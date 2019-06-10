# ocp4

This was a private repo for my own private lab, but I have opened it up in case there are some useful things.

Note that my internal domain is hard wired in places.

Assumed pre-requisites
1. You have RHEV 4.3
2. You have a web server to host the boot image and ignition files.
3. You have a dnsmasq server serving up DHCP and DNS
4. You have a rhel7_template to clone a machine from for haproxy

Driving playbook is 
```
ansible-playbook cluster_install/site.yml  -e cluster_name=<domain_prefix>
```
