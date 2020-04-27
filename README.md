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

# Launch the cluster

Now that the VMs are running, the next step is to get a fully functional PXC cluster running.

Worth to mention that PXC8 now comes with the variable `pxc-encrypt-cluster-traffic` which enforce SSL encryption for the SST/IST traffic. To use that option, one has to configure the usage of the certificates automatically or manually.

Also, one can override the SSL and disable `pxc-encrypt-cluster-traffic` for testing purpose. This is the case in this repo.

## Disable SELinux

PXC still requires to disable SELinux

[ pxc1/2/3 ] `sudo setenforce 0`

## Bootstrap the cluster

[ pxc1 ] `sudo systemctl start mysql@bootstrap.service`

## Change temp root password

[ pxc1 ] `cat /var/log/mysqld.log | grep password`

[ pxc1 ] `mysql -uroot -p`

[ pxc1 ] `SET SESSION sql_log_bin=0; ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'myawesomepass'; flush privileges;`

## Set credentials file

[ pxc1/2/3 ] `sudo echo -e "[client]\nuser=root\npassword=myawesomepass" > /root/.my.cnf`

## Add nodes to the cluster

[ pxc2/3 ] `service mysql start`
