This is work in progress! It should work, however, it is not extensively tested. 


Requirements
------------

- VirtualBox 1.20+
- Vagrant 1.65+
  - [Git for Windows](https://msysgit.github.io/) (for `vagrant ssh`, make sure git/bin is in PATH)
- `vagrant plugin install vagrant-proxyconf`


Provision
---------
        vagrant up
        vagrant ssh ansible-master -- -t "cd /ansible && ansible-playbook -i hosts_vagrant site.yml"

Access
------
        URL:  http://192.168.0.20 (or http://liferay with vagrant-hostsupdater plugin)
        User: test@liferay.com 
        Pass: test

TODO
----

- Detailed documentation
- Fix few less important errors within liferay portal.
