+++
date = "2016-05-17"
cssid = "download"
type = "download"
description = "Ernest makes it easier to develop and deploy applications in the Cloud. Ernest supports full-stack application orchestration that allows you to drive software and infrastructure as a unified system."
+++

# Downloads

## Get Ernest

### The Vagrant Box

This is the fastest way to get started with Ernest. You will need Vagrant and Virtual Box.

1. Clone the repo containing the Vagrantfile: `git clone https://github.com/ernestio/ernest.git`

2. Change to the cloned directory: `cd ernest`

3. Start the Ernest Vagrant Box: `vagrant up`

Once the box is up Ernest will be available on 10.50.1.11.

### The Appliance

You can download the OVF appliance [here](http://download.ernest.io/ernest.zip).

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

The Ernest CLI is distributed as a binary package for all supported platforms and architectures. It can also be built from source by following the instructions on [GitHub](https://github.com/ernestio/ernest-cli).

To install Ernest CLI, find the newest version of the [appropriate package](https://github.com/ErnestIO/ernest-cli/releases) for your system and download it.

After downloading Ernest CLI, unzip it and move the binary to a directory that is on the PATH. See [this page](http://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux) for instructions on setting the PATH on Linux and Mac. [This page](http://stackoverflow.com/questions/1618280/where-can-i-set-path-to-make-exe-on-windows) contains instructions for setting the PATH on Windows.

After installing Ernest CLI, verify the installation worked by opening a new terminal session and checking the CLI version:

```
$ ernest --version
ernest version 1.4.0

```

## Get Salt

The Salt image can be downloaded from [here](http://download.ernest.io/r3-salt-master.zip). For the current version of Ernest (1.0) it is not possible to specify the vCloud catalog name that Ernest will get the Salt image from, you will need to place the image in a catalog named 'r3'.