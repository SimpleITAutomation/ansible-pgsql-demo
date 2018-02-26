# ansible-pgsql-demo

An Ansible playbook to deploy postgresql in a master - slave replication configuration on [Exoscale](https://www.exoscale.com/) cloud, including continous wal archiving in Exoscale [S3 compatible object store](https://www.exoscale.com/object-storage/) using wal-e [wal-e](https://github.com/wal-e/wal-e).

The goal of this playbook is to demonstrate how fast & easy it can be to deploy applications with high availability into the cloud using Ansible.

## Setup

### Prerequisites

```
apt-get update && apt-get install -y git python-pip python-dev build-essential
git clone https://github.com/exoscale/ansible-pgsql-demo
cd ansible-pgsql-demo
make
```

### API Key setup

You need to setup your API keys. The Key & secret can be found within your [portal](https://portal.exoscale.com) under the account section.

```
cat $HOME/.cloudstack.ini
[cloudstack]
endpoint = https://api.exoscale.ch/compute
key = Your API Key here
secret = Your secret key here
```

### SSH key setup

Your SSH RSA public key must be present at the following location: '~/.ssh/id_rsa.pub'

### Variable setup

A few variables must be setup prior executing this playbook. These variables are located in the following file:

```
defaults/main.yml
```

The following variables needs be edited:

* aws_key: "mykey"
* aws_secret: "mysecret"
* aws_bucket: "s3://mybucket/directory/or/whatever"

The bucket must be created prior running the playbook. [s3cmd](http://s3tools.org/s3cmd) or any S3 compatible tool may be used for this purpose.

## Running the playbook 

To run the playbook:

```
ansible-playbook -v role.yml 
```

## Notice

This playbook has been tested only on Ubuntu 14.04.

It is inspired from [this] (https://github.com/lesovsky/ansible-postgresql-on-el6) playbook.
