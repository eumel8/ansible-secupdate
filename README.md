# Welcome to FAUP - Fully Automatic Update Processor

As part on an internal workflow to upgrade Ubuntu VMs in an OpenStack 
environment here are some ansible playbooks to do this:

Preconditions for OpenStack usage:

* OpenStack API access
* apt-get install ansible python-shade


## Update VMs (dynamic inventor is using the *internal* ip-address!)

```
    . ops.openrc
    export OS_TENANT_NAME=frank.test
    ansible-playbook -i openstack.py update.yml
```

for some mission critical VMs might this command useful:

```
    ansible-playbook -i openstack.py update.yml --limit vpn
    ansible-playbook -i openstack.py update.yml --limit dbserver
```

## Update LXD container (via ssh, needs ssh key deployed)

```
    ansible-playbook -i lxd.py lxd-update-ssh.yml

```

## Update LXD container (via lxc, make snapshots before)

```
    ansible-playbook -i lxd.py lxd-update-lxc.yml

```

Note: lxd.py is under deployment and will be implemented in the next ansible versions

Hints for install requirements for openstack.py inventory:

```
    apt-get install -y --force-yes build-essential libssl-dev libffi-dev python-dev libxml2-dev libxslt1-dev libpq-dev python-pip
    pip install -r requirements.txt
    pip install -U pyOpenSSL

```



