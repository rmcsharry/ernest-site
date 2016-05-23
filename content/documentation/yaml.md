+++
date = "2016-05-17"
title = "YAML Structure"
category = "documentation"
showChildren=true
[menu.documentation]
  name = "YAML Structure"
  weight = -70
  identifier = "yaml"
  parent = "Documentation"
+++


# Ernest YAML Structure

Environments built and managed with Ernest are defined in YAML format.

## Example

```
---
name: demo
datacenter: examples
bootstrapping: salt

firewalls:
  - name: fw
    rules:
    - name: in_out_all
      source: internal
      from_port: any
      destination: external
      to_port: any
      protocol: any
      action: allow

    - name: out_in_22
      source: external
      from_port: any
      destination: internal
      to_port: '22'
      protocol: tcp
      action: allow

networks:
  - name: net
    subnet: 10.1.0.0/24

port_forwarding:
  - from_port: '22'
    to_port: '22'
    destination: 10.1.0.11

instances:
  - name: srv
    image: r3/ubuntu-1404
    cpus: 1
    memory: 1GB
    disks:
     - 10GB
    count: 1
    networks:
      name: net
      start_ip: 10.1.0.11
    provisioner:
      - exec:
        - 'uptime'
```

## Field Reference

### Service Options

```
name: demo
datacenter: examples
bootstrapping: salt
```

Service Options support the following fields:

* **name**
 * String that defines the name of the platform environment to build.
 * This field is mandatory.
 * This field cannot be null or empty.
 * The value of this field must be 50 characters maximum.

* **datacenter**
 * String that defines the name of the datacenter where the environment is built.
 * This field is mandatory.
 * This field cannot be null or empty.
 * The value of this field must 50 characters maximum.

* **bootstrapping**
 * String [salt, none] that defines if you’re going to be able to execute commands on the servers
 * This field is optional.
 * This field defaults to none.
 * The value of this is restricted to “salt” or “none”

### Firewalls

```
firewalls:
  - name: fw
    rules:
    - name: in_out_all
      source: internal
      from_port: any
      destination: external
      to_port: any
      protocol: any
      action: allow

    - name: out_in_22
      source: external
      from_port: any
      destination: internal
      to_port: '22'
      protocol: tcp
      action: allow
```

Firewalls support the following fields:

* **name**
 * String that defines the name of the platform environment to build.
 * This field is mandatory.
 * This field cannot be null or empty.
 * This field must be unique by user & manifest.
 * The value of this field can be 50 characters maximum.

* **source**
 * String the source of the network where this firewall acts
 * This field is mandatory.
 * Values can be: external | internal | any | named networks | CIDR

* **from_port**
 * Source port numbers
 * This field is mandatory.
 * Values can be:  an string ( valid port number, 1 - 65535 ) or any

* **destination**
 * String the destination of the network where this firewall acts
 * This field is mandatory.
 * Values can be:  external | internal | any | named networks | named lb groups | CIDR

* **to_port**
 * Destination port numbers
 * This field is mandatory.
 * Values can be:  an string ( valid port number, 1 - 65535 ) or any

* **protocol**
 * String with the protocol we are firewalling
 * This field is mandatory.
 * Values can be: tcp | udp | icmp | any | tcp & udp 


### Networks

```
networks:
  - name: net
    subnet: 10.1.0.0/24
```

Networks support the following fields:

* **name**
 * String that defines the name of the platform environment to build.
 * This field is mandatory.
 * This field cannot be null or empty.
 * The value of this field must be 50 characters maximum.

* **subnet**
 * String that defines the name of a network to add to this environment.
 * It must follow CIDR notation as described at: https://en.wikipedia.org/wiki/Classless\_Inter-Domain\_Routing 
 * This field is mandatory.
 * This field cannot be null or empty.
 * This field must be unique for this user & all the networks on the manifest.

### Port Forwarding

```
port_forwarding:
  - from_port: '22'
    to_port: '22'
    destination: 10.1.0.11
```

Port Forwarding supports the following fields:

* **from_port**
 * Source port numbers
 * Values can be:  an string ( valid port number, 1 - 65535 ) or any

* **to_port**
 * Destination port numbers
 * Values can be:  an string ( valid port number, 1 - 65535 ) or any

* **destination**
 * String the destination of the IPv4 Address to translate to
 * Values can be: IPv4

### Instances

```
instances:
  - name: srv
    image: r3/ubuntu-1404
    cpus: 1
    memory: 1GB
    disks:
     - 10GB
    count: 1
    networks:
      name: net
      start_ip: 10.1.0.11
    provisioner:
      - exec:
        - 'uptime'
```

Instances support the following fields:

* **name**
 * String that defines the name of the instance to build.
 * This field is mandatory.
 * This field cannot be null or empty.
 * This field must be unique by user & manifest.
 * The value of this field must be 50 characters maximum.

* **image**
 * String that defines the name of an image to install on the VM.
 * This field is mandatory.
 * This field cannot be null or empty.
 * This field is composed in two parts one for the “catalog” and another one for the “image” separated by a slash “/”
 * Both “catalog” and “image” are strings and can’t be null.

* **cpus**
 * Integer that defines how many CPUs will have the VM.
 * This field is mandatory.
 * This field cannot be null or empty.
 * This field must be greater or equal than 1

* **memory**
 * String that defines the name of a load balancer to add to this environment.
 * This field is mandatory.
 * This field cannot be null or empty.
 * This field must follow the Binary Prefix format:
 * https://en.wikipedia.org/wiki/Binary\_prefix#Computer\_memory 
 * The possible binary prefixes are MB, GB, TB, PB, YB

* **disks:**
 * A list of sizes of hard disks that belongs to the VM
 * This field can be an empty list
 * This field is a list of strings
 * Each element of the string must follow the Binary Prefix format:
 * https://en.wikipedia.org/wiki/Binary\_prefix#Hard\_disk\_drives 
 * The possible binary prefixes are MB, GB, TB, PB, YB

* **count**
 * Integer that defines the number of VM to be created.
 * This field is mandatory.
 * This field cannot be null or empty.
 * This field must be greater or equal that 1

* **network**
 * Network is a map with two fields

* **network:name**
 * String that defines the name of a network to attach this instance.
 * This field is mandatory.
 * This field cannot be null or empty.
 * The value of this field should exist on the networks section previously specified.

* **network:start_ip**
 * String that defines the starting IP to allocate the VMs to be built.
 * This field is mandatory.
 * This field cannot be null or empty.
 * This field must be a valid IP.
 * This IP should belong to the network already defined on the instance.

* **provisioner**
 * Array that contains provisioner types
 * Each provisioner type will be run in the order they are specified in the document
 * This field is optional
 * This field can be empty

* **provisioner - exec**
 * Array of strings, any command characters must be escaped with backslashes: (RFC7159, Section 7)
 * Each command in the exec array is concatenated together and delimited by a semicolon.
 * This field is optional
 * If specified as a provisioner type, this array field must contain at least one element
