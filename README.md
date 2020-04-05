# Percona XtraDB Cluster 8.0 (experimental)

This repo is to build an environment with PXC 8.0 (still experimental)

## Install

### Install VirtualBox.

Version 6.0.14 works. Download Virtualbox from [here](https://www.virtualbox.org/wiki/Downloads).

### Install Vagrant.

Version 2.2.6 works. Download Vagrant from [here](http://vagrantup.com/).

### Install Vagrant plugin hostmanager

This plugin will take care of dealing with the /etc/hosts file so we can use hostnames instead of IPs. https://github.com/devopsgroup-io/vagrant-hostmanager

To install it, just run:

```
vagrant plugin install vagrant-hostmanager
```

## Deploy

Just clone the repo and start the VMs:

- git clone https://github.com/nethalo/pxc8.git
- Vagrant up; vagrant hostmanager

You will end with a 3-node cluster using PXC8.0 plus an additional VM to run PMM, sysbench, etc
