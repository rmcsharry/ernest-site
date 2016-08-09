+++
date = "2016-06-06"
title = "vCloud Enhanced Examples"
category = "documentation"
showChildren=true
[menu.documentation]
  name = "vCloud Enhanced Examples"
  weight = -80
  identifier = "vcloud-enhanced-examples"
  parent = "vCloud Director"
+++

# vCloud Director Enhanced Examples

If you would like to try Ernest but do not have access to vCloud you can request a demo vCloud account [here](/vcloud-account).

Before we get started we will need the following information:

* Ernest IP address (31.210.241.221)
* Ernest username/password (user1/xxxxxx)
* vCloud URL (myvdc.carrenza.net)
* vCloud organisation (r3labs-development)
* vCloud datacenter (r3-jreid2)
* vCloud network (DVS-VCD-EXT-665)
* vCloud username/password (jreid/xxxxxx)
* VSE Creator Service URL (https://vse-creator-service.carrenza.net)

*The values in brackets are what we will use for this example. Your service provider can provide you with the vCloud and VSE Creator Service information.*

The first step is to set the IP address of Ernest:

```
$ ernest target https://31.210.241.221
Target set

```

Next we login to Ernest:

```
$ ernest login
Username: user1
Password: ******
Log in succesful.

```

Once we have logged in to Ernest we can setup the vCloud datacenter and credentials that Ernest will use to create our infrastructure:

```
$ ernest datacenter create --datacenter-user jreid --datacenter-password xxxxxx --datacenter-org r3labs-development --vse-url https://vse-creator-service.carrenza.net r3-jreid2 https://myvdc.carrenza.net DVS-VCD-EXT-665
SUCCESS: Datacenter r3-jreid2 created

```

Now that we have our datacenter created in Ernest we can start building stuff. Below we will show examples for:

* creating infrastructure only
* creating infrastructure and configuring the servers

### Infrastructure Only

For our example we will deploy a single Ubuntu server from a catalog image (image: r3/ubuntu-1404) and configure our networking to permit SSH access to the server. Our YAML for this example is:

```
---
name: demo4
datacenter: r3-jreid2
bootstrapping: none

routers: 
  - name: demo4
    rules:
    - name: in_out_any
      source: internal
      from_port: any
      destination: external
      to_port: any
      protocol: any
      action: allow

    - name: out_in_22
      source: any
      from_port: any
      destination: internal
      to_port: '22'
      protocol: tcp
      action: allow

    networks:
      - name: web
        subnet: 10.1.0.0/24
        dns:
          - 8.8.8.8
          - 8.8.4.4

    port_forwarding:
      - from_port: '22'
        to_port: '22'
        destination: 10.1.0.11

instances:
  - name: web
    image: r3/ubuntu-1404
    cpus: 2
    memory: 8GB
    count: 1
    networks:
      name: web
      start_ip: 10.1.0.11

```

Note that we have not specified the service IP, or the source IP for port-forwarding. This is because the VSE Creator Service will automatically assign these IPs and configure the vSE as necessary.

Now that we have defined our infrastructure we are ready to apply our definition:

```
$ ernest service apply demo4.yml
Environment creation requested
Ernest will show you all output from your requested service creation
You can cancel at any moment with Ctrl+C, even the service is still being created, you won't have any output
Starting environment creation

Creating routers:
  195.3.186.66
Routers successfully created

Creating networks:
  - 10.1.0.0/24
Networks successfully created

Creating instances:
   - r3-jreid2-demo4-web-1
Instances successfully created

Updating instances:
   - r3-jreid2-demo4-web-1
Instances successfully updated

Setting up firewalls:
Firewalls Created

Configuring nats
Nats Created

SUCCESS: rules successfully applied
Your environment endpoint is: 195.3.186.66

```
Congratulations! You have built your first infrastructure with Ernest. You can now SSH to the server on IP 195.3.186.66 to install and configure your software.

If you wish to change the infrastructure update your YAML to show how you want the infrastructure to look, then re-apply the YAML. Ernest will make the appropriate changes to the infrastructure.

For example if we increase the 'web' instance count from 1 to 2 and re-apply the YAML a new server is created:

```
$ ernest service apply demo4.yml 
Environment creation requested
Ernest will show you all output from your requested service creation
You can cancel at any moment with Ctrl+C, even the service is still being created, you won't have any output
Starting environment creation

Creating instances:
   - r3-jreid2-demo4-web-2
Instances successfully created

Updating instances:
   - r3-jreid2-demo4-web-2
Instances successfully updated

SUCCESS: rules successfully applied
Your environment endpoint is: 195.3.186.66

```

We can list the services, view their histories and definitions, and modify them in exactly the same way we did for the normal examples.

### Infrastructure and Server Configuration

In the above example the task of installing and configuring software was left to the user to do. In this example we will bootstrap the servers and install our software directly from the YAML.

The new YAML is shown here:

```
---
name: demo5
datacenter: r3-jreid2
bootstrapping: salt
ernest_ip:
  - 31.210.241.221

routers: 
  - name: demo5
    rules:
    - name: in_out_any
      source: internal
      from_port: any
      destination: external
      to_port: any
      protocol: any
      action: allow

    - name: out_in_80
      source: any
      from_port: any
      destination: internal
      to_port: '80'
      protocol: tcp
      action: allow

    networks:
      - name: web
        subnet: 10.1.0.0/24
        dns:
          - 8.8.8.8
          - 8.8.4.4
          
    port_forwarding:
      - from_port: '80'
        to_port: '80'
        destination: 10.1.0.11

instances:
  - name: web
    image: r3/ubuntu-1404
    cpus: 1
    memory: 1GB
    count: 1
    networks:
      name: web
      start_ip: 10.1.0.11
    provisioner:
      - exec:
        - 'sudo apt-get update'
        - 'sudo apt-get install apache2 -y'

```

The first thing to notice is that we have changed 'bootstrapping' from 'none' to 'salt'. This will result in Ernest deploying a SALT instance that we can use to manage our environment. Note that the 'bootstrapping' option must be specified when an environment is created and cannot be changed for that environment.

The next thing we have changed are the firewall and port-forwarding configuration. We have removed the sections needed for SSH access to the server since we are now able to run commands directly from the YAML.

Finally, we have added a provisioner section to the instance that will install the Apache HTTP Server.

Now that we have defined our platform we are ready to create it:

```
$ ernest service apply demo5.yml
Environment creation requested
Ernest will show you all output from your requested service creation
You can cancel at any moment with Ctrl+C, even the service is still being created, you won't have any output
Starting environment creation

Creating routers:
  195.3.186.48
Routers successfully created

Creating networks:
  - 10.254.254.0/24
  - 10.1.0.0/24
Networks successfully created

Creating instances:
   - r3-jreid2-demo5-salt-master
   - r3-jreid2-demo5-web-1
Instances successfully created

Updating instances:
   - r3-jreid2-demo5-salt-master
   - r3-jreid2-demo5-web-1
Instances successfully updated

Setting up firewalls:
Firewalls Created

Configuring nats
Nats Created

Bootstrapping
Instances bootstrapped

Running executions
Executions ran

SUCCESS: rules successfully applied
Your environment endpoint is: 195.3.186.48

```

Notice that Ernest has automatically created a SALT instance for us on network 10.254.254.0/24. It has also trigged the bootstrapping process that installs the SALT minion on each of our servers, and then run the commands we specified in the provisioner section of each instance defined in the YAML.

You should be able to browse to http://195.3.186.48. Congratulations! 

If you wish to change the platform update your YAML to show how you want the platform to look, then re-apply the YAML. Ernest will make the appropriate changes to the platform.

> The SALT image can be downloaded from [here](/downloads/r3-salt-master.ova). For the current version of Ernest (1.0) it is not possible to specify the catalog name that Ernest will get the SALT image from, you will need to place the image in a catalog named 'r3'.

## Next Steps

Take a look at the [vCloud YAML reference](/documentation/vcloud-yaml/).