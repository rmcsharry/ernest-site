+++
date = "2016-06-06"
title = "AWS YAML Reference"
category = "documentation"
showChildren=true
[menu.documentation]
  name = "AWS YAML Reference"
  weight = -60
  identifier = "aws-yaml"
  parent = "Amazon Web Services"
+++

# Amazon Web Services YAML Reference

Environments built and managed with Ernest are defined in YAML format.

## Example

```
---
name: demo
datacenter: vpc-abcdef01

networks:
  - name: web
    subnet: 10.0.10.0/24
    public: true
  - name: db
    subnet: 10.0.11.0/24
    public: false
    nat_gateway: db-nat

nat_gateways:
  - name: db-nat
    public_network: web

security_groups:
  - name: web-sg
    egress:
      - ip: 0.0.0.0/0
        protocol: any
        from_port: '0'
        to_port: '65535'
    ingress:
      - ip: 10.0.0.0/16
        protocol: any
        from_port: '0'
        to_port: '65535'
      - ip: 52.211.19.211/32
        protocol: tcp
        from_port: '22'
        to_port: '22'
  - name: db-sg
    egress:
      - ip: 0.0.0.0/0
        protocol: any
        from_port: '0'
        to_port: '65535'
    ingress:
      - ip: 10.0.0.0/16
        protocol: any
        from_port: '0'
        to_port: '65535'
      - ip: 52.211.19.211/32
        protocol: tcp
        from_port: '22'
        to_port: '22'

instances:
  - name: web
    elastic_ip: true
    type: t2.micro
    image: ami-ed82e39e
    network: web
    start_ip: 10.0.10.11
    count: 1
    key_pair: web-key
    security_groups:
      - web-sg

  - name: db
    type: t2.micro
    image: ami-ed82e39e
    network: db
    start_ip: 10.0.11.11
    count: 1
    key_pair: db-key
    security_groups:
      - db-sg

```

## Field Reference

### Service Options

```
name: demo
datacenter: vpc-abcdef01

```

Service Options support the following fields:

* **name**
 * String that defines the name of the service to build.
 * This field is mandatory.
 * This field cannot be null or empty.
 * The value of this field must be 50 characters maximum.

* **datacenter**
 * String that defines the name of the datacenter where the service is built.
 * This field is mandatory.
 * This field cannot be null or empty.
 * The value of this field must 50 characters maximum.

### Networking

```
networks:
  - name: web
    subnet: 10.0.10.0/24
    public: true
  - name: db
    subnet: 10.0.11.0/24
    public: false
    nat_gateway: db-nat

nat_gateways:
  - name: db-nat
    public_network: web

```

Networking supports the following fields:

**networks**

A network is a subnet that our instances can connect to. This is what allows us to network/isolate VM’s together.

* **name**
 * String that defines the name of the subnet to build.
 * This field is mandatory.
 * This field cannot be null or empty.
 * The value of this field must be 50 characters maximum.

* **subnet**
 * String that defines the IP address range of the subnet.
 * It must follow CIDR notation as described at: https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing 
 * This field is mandatory.
 * This field cannot be null or empty.
 * This field must be unique for this user & all the networks on the manifest.

* **public**
 * String that defines if the subnet will be public or private.
 * This field is optional.
 * Values can be: “true“ or “false“.
 * This field will default to “false“.

* **nat_gateway**
 * String that defines the name of the NAT gateway to use for this subnet.
 * This field is optional.
 * This field can be empty.

**nat_gateways**

NAT gateways enable instances in a private subnet to connect to the Internet or other AWS services, but prevent the Internet from initiating a connection with those instances.

* **name**
 * String that defines the name of the NAT gateway to build.
 * This field is mandatory.
 * This field cannot be null or empty.
 * The value of this field must be 50 characters maximum.

* **public_network**
 * String that defines the name of the public network the NAT gateway will reside.
 * This field is mandatory.
 * This field cannot be null or empty.
 * The value of this field must be 50 characters maximum.

### Security Groups

```
security_groups:
  - name: web-sg
    egress:
      - ip: 0.0.0.0/0
        protocol: any
        from_port: '0'
        to_port: '65535'
    ingress:
      - ip: 10.0.0.0/16
        protocol: any
        from_port: '0'
        to_port: '65535'

```

Security Groups support the following fields:

* **name**
 * String that defines the name of the security group to build.
 * This field is mandatory.
 * This field cannot be null or empty.
 * The value of this field must be 50 characters maximum.

**egress**

Security group egress rules.

* **ip**
 * String that defines the IP address range for this rule.
 * It must follow CIDR notation as described at: https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing 
 * This field is mandatory.
 * This field cannot be null or empty.

* **protocol**
 * String that defines the protocol for this rule.
 * This field is mandatory.
 * This field cannot be null or empty.
 * Values can be: tcp | udp | icmp | any

* **from_port**
 * Starting port-range number.
 * This field is mandatory.
 * Values can be: 0 - 65535.

* **to_port**
 * Ending port-range number.
 * This field is mandatory.
 * Values can be: 0 - 65535.

**ingress**

Security group ingress rules.

* **ip**
 * String that defines the IP address range for this rule.
 * It must follow CIDR notation as described at: https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing 
 * This field is mandatory.
 * This field cannot be null or empty.

* **protocol**
 * String that defines the protocol for this rule.
 * This field is mandatory.
 * This field cannot be null or empty.
 * Values can be: tcp | udp | icmp | any

* **from_port**
 * Starting port-range number.
 * This field is mandatory.
 * Values can be: 0 - 65535.

* **to_port**
 * Ending port-range number.
 * This field is mandatory.
 * Values can be: 0 - 65535.

### Instances

```
instances:
  - name: web
    elastic_ip: true
    type: t2.micro
    image: ami-ed82e39e
    network: web
    start_ip: 10.0.10.11
    count: 1
    key_pair: web-key
    security_groups:
      - web-sg

```

Instances support the following fields:

* **name**
 * String that defines the name of the instance to build.
 * This field is mandatory.
 * This field cannot be null or empty.
 * This field must be unique by user & manifest.
 * The value of this field must be 50 characters maximum.

* **elastic_ip**
 * String that defines if the instance will be assigned an elastic IP.
 * This field is optional.
 * Values can be: “true“ or “false“.
 * This field will default to “false“.

* **type**
 * String that defines the instance size.
 * This field is mandatory.
 * This field cannot be null or empty.
 * This field must be a valid AWS EC2 size.

* **image**
 * String that defines the name of an AMI to install.
 * This field is mandatory.
 * This field cannot be null or empty.

* **network:**
 * String that defines the name of a network to attach this instance.
 * This field is mandatory.
 * This field cannot be null or empty.
 * The value of this field should exist on the networks section previously specified.

* **start_ip:**
 * String that defines the starting IP to allocate the VMs to be built.
 * This field is mandatory.
 * This field cannot be null or empty.
 * This field must be a valid IP.
 * This IP should belong to the network already defined on the instance.

* **count**
 * Integer that defines the number of instances to be created.
 * This field is mandatory.
 * This field cannot be null or empty.
 * This field must be greater or equal that 1

* **key_pair**
 * String that specifies the key pair to be used to login to the instances.
 * This field is optional.
 * This field cannot be null or empty.

* **security_groups**
 * Array that contains security groups that will be applied to the instances.
 * This field is optional.
 * This field can be empty.