+++
date = "2016-05-17"
cssid = "download"
type = "download"
description = "Ernest makes it easier to develop and deploy applications in the Cloud. Ernest supports full-stack application orchestration that allows you to drive software and infrastructure as a unified system."
+++

# Downloads

## Get Ernest

### Use Vagrant Box

This is the fastest way to get started with Ernest. You will need Vagrant and Virtual Box.

1. Clone the repo containing the Vagrantfile: `git clone https://github.com/ernestio/ernest.git`

2. Change to the cloned directory: `cd ernest`

3. Start the Ernest Vagrant Box: `vagrant up`

Once the box is up Ernest will be available on 10.50.1.11.

### Use OVF Template

### Build From Source

Ernest requires on Ubuntu 15.10. The minimum recommended spec is: 1 CPU, 2 GB RAM, 10 GB HD. You will need to create a user **ernest** configured with passwordless sudo.

All commands below are run as **root** user.

1. Update the package list: `apt-get update`

2. Install some required packages: `apt-get install -y wget git make ruby`

3. Download ChefDK: `wget https://opscode-omnibus-packages.s3.amazonaws.com/ubuntu/12.04/x86_64/chefdk_0.10.0-1_amd64.deb`

4. Install ChefDK: `dpkg -i chefdk_0.10.0-1_amd64.deb`

5. Clone the Ernest install repo: `git clone https://github.com/ernestio/ernest-vagrant.git`

6. Change to the Ernest install repo dir: `cd ernest-vagrant`

7. Switch to the **master** branch: `git checkout master`

8. Install Ernest: `make deploy`

## Get Ernest CLI

## Get VSE Creator Service
