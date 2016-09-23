+++
date = "2016-06-06"
title = "Quickstart"
category = "documentation"
showChildren=true
[menu.documentation]
  name = "Quickstart"
  weight = -95
  identifier = "quickstart"
  parent = "Introduction"
+++

# Quickstart Guide

In this quickstart guide we will build a simple environment consisting of a public server and private server on AWS, and allow SSH access from our IP. You will need a working copy of Ernest and the Ernest CLI, your AWS Access Key and Secret Key, and an AWS VPC.

## Get Ernest

Follow the instructions [here](/download/) to get Ernest and the Ernest CLI.

## Setup Your User

Target your Ernest instance:

```
$ ernest target https://10.50.1.11
Target set

```

10.50.1.11 is the IP address Ernest will be on if you are using the Vagrant Box. If you download the OVF or build Ernest from source then Ernest may be run of a different IP.

Login to Ernest as admin:

```
$ ernest login --user admin --password w4rmR3d
Log in succesful.

```
Create a user:

```
$ ernest user create user1 abc123
SUCCESS: User user1 created

```

Create a group:

```
$ ernest group create group1
SUCCESS: Group group1 created

```

Add the user to the group:

```
$ ernest user list
NAME	ID
admin	1
user1	2

$ ernest group list
NAME	ID
admin	1
group1	2

$ ernest group add-user user1 group1
SUCCESS: Added user1 to group1

```

## Setup Your Datacenter

Login as the user:

```
$ ernest login --user user1 --password abc123
Log in succesful.

```

Configure the datacenter on Ernest using your Access Key, Secret Key, and VPC ID:

```
$ ernest datacenter create aws --region eu-west-1 --token XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX --secret YYYYYYYYYYYYYYYYYYYY vpc-abcdef01
SUCCESS: Datacenter vpc-abcdef01 created

```

## Create Your Environment

We will use this YAML (demo.yml) to create our environment:

```
---
name: demo
datacenter: vpc-abcdef01

networks:
  - name: public
    subnet: 10.0.10.0/24
    public: true
  - name: private
    subnet: 10.0.11.0/24
    public: false
    nat_gateway: private-nat

nat_gateways:
  - name: private-nat
    public_network: public

security_groups:
  - name: public-sg
    egress:
      - ip: 0.0.0.0/0
        protocol: any
        from_port: '0'
        to_port: '65535'
    ingress:
      - ip: 52.211.19.211/32
        protocol: tcp
        from_port: '22'
        to_port: '22'
  - name: private-sg
    egress:
      - ip: 0.0.0.0/0
        protocol: any
        from_port: '0'
        to_port: '65535'
    ingress:
      - ip: 10.0.0.0/16
        protocol: tcp
        from_port: '22'
        to_port: '22'

instances:
  - name: public
    elastic_ip: true
    type: t2.micro
    image: ami-ed82e39e
    network: public
    start_ip: 10.0.10.11
    count: 1
    key_pair: my-key
    security_groups:
      - public-sg

  - name: private
    type: t2.micro
    image: ami-ed82e39e
    network: private
    start_ip: 10.0.11.11
    count: 1
    key_pair: my-key
    security_groups:
      - private-sg

```

Now we can apply our YAML:

```
$ ernest service apply demo.yml 
Environment creation requested
Ernest will show you all output from your requested service creation
You can cancel at any moment with Ctrl+C, even the service is still being created, you won't have any output
Starting environment creation

Creating networks:
	- 10.0.10.0/24
	- 10.0.11.0/24
Networks successfully created

Setting up firewalls:
Firewalls Created

Creating instances:
	 - vpc-abcdef01-demo-public-1
	 - vpc-abcdef01-demo-private-1
Instances successfully created

Configuring nats
Nats Created

Configuring nats
Nats Updated

SUCCESS: rules successfully applied
Your environment endpoint is: 

```

Congratulations you have built something with Ernest!

## Next Steps

Find out how to use the CLI [here](/documentation/cli-guide/). Then dive into the detailed examples for the supported providers:

* [Amazon Web Services](/documentation/aws-intro/)
* [vCloud Director](/documentation/vcloud-intro/)
