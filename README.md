Cross platform Liferay deploy using Docker & Ansible. 

**NOTE**: This is a work in progress.

Requirements
============

For development
---------------

- VirtualBox 1.20+
- Vagrant 1.65+
  - If on Windows: [Git for Windows](https://msysgit.github.io/) (req. for `vagrant ssh` to work on Windows, make sure .../Git/bin is in the PATH)
- If you have proxy: `vagrant plugin install vagrant-proxyconf`


For production server
---------------------

- Ubuntu Utopic
- SSH with root ssh access for provisioning
- Ansible-master server to execute playbooks (you can also use the provided virtual machine)

Install
=======

    git clone https://github.com/majkinetor/liferay-server.github
    cd liferay-server

    vagrant up
    vagrant ssh ansible-master -- -t "cd /ansible && ansible-playbook -i hosts_vagrant site.yml"

Usage
======

 - **URL**: http://192.168.0.20 (or http://liferay with vagrant-hostsupdater plugin)
 - **User**: test@liferay.com 
 - **Pass**: test

Administration basics
---------------------

```sh
sudo su

# Show running images (should list mysql & liferay)
docker ps 

# Enter liferay images
docker exec -it liferay /bin/bash

# Inside docker container go to liferay dir
cd /opt/liferay-portal-6.2-ce-ga2/
cd /var/liferay-home
```

TODO
====

- Detailed documentation
- Fix few less important errors within liferay portal.
