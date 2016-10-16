+++
date = "2016-06-06"
title = "vCloud Examples"
category = "documentation"
showChildren=true
[menu.documentation]
  name = "vCloud Examples"
  weight = -90
  identifier = "vcloud-examples"
  parent = "vCloud Director"
+++

# vCloud Director Examples

If you would like to try Ernest but do not have access to vCloud you can request a demo vCloud account [here](/vcloud-account).

Before we get started we will need the following information:

* Ernest IP address (31.210.241.221)
* Ernest username/password (user1/xxxxxx)
* vCloud URL (myvdc.carrenza.net)
* vCloud organisation (r3labs-development)
* vCloud datacenter (r3-jreid2)
* vCloud network (DVS-VCD-EXT-665)
* vCloud username/password (jreid/xxxxxx)
* vCloud router name (test1)
* vCloud sub-allocated IP (195.3.186.42)

*The values in brackets are what we will use for this example. Your service provider can provide you with the vCloud information.*

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
Welcome back user1

```

Once we have logged in to Ernest we can setup the vCloud datacenter and credentials that Ernest will use to create our infrastructure:

```
$ ernest datacenter create vcloud --user jreid --password xxxxxx --org r3labs-development --vcloud-url https://myvdc.carrenza.net --public-network DVS-VCD-EXT-665 r3-jreid2
Datacenter 'r3-jreid2' successfully created

```

Now that we have our datacenter created in Ernest we can start building stuff. Below we will show examples for:

* creating infrastructure only
* creating infrastructure and configuring the servers
* creating the servers only

### Infrastructure Only

For our example we will deploy a single Ubuntu server from a catalog image (image: r3/ubuntu-1404) and configure our networking to permit SSH access to the server. Our YAML for this example is:

```
---
name: demo1
datacenter: r3-jreid2
bootstrapping: none
service_ip: 195.3.186.42

routers: 
  - name: test1
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
      - source: 195.3.186.42
        from_port: '22'
        to_port: '22'
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

```

Now that we have defined our infrastructure we are ready to apply our definition:

```
$ ernest service apply demo1.yml
Environment creation requested
Ernest will show you all output from your requested service creation
You can cancel at any moment with Ctrl+C, even the service is still being created, you won't have any output
Starting environment creation
Creating networks:
 - r3-jreid2-demo1-web
   IP     : 10.1.0.0/24
   Status : completed
Networks successfully created
Creating instances:
 - r3-jreid2-demo1-web-1
   IP        : 10.1.0.11
   Status    : completed
Instances successfully created
Updating instances:
 - r3-jreid2-demo1-web-1
   IP        : 10.1.0.11
   Status    : completed
Instances successfully updated
Creating firewalls:
 - r3-jreid2-demo1-test2
   Status    : completed
Firewalls created
Creating nats:
 - r3-jreid2-demo1-test2
   Status    : completed
Nats created
SUCCESS: rules successfully applied
Your environment endpoint is: 195.3.186.42

```
Congratulations! You have built your first infrastructure with Ernest. You can now SSH to the server on IP 195.3.186.42 to install and configure your software.

If you wish to change the infrastructure update your YAML to show how you want the infrastructure to look, then re-apply the YAML. Ernest will make the appropriate changes to the infrastructure.

For example if we increase the 'web' instance count from 1 to 2 and re-apply the YAML a new server is created:

```
$ ernest service apply demo1.yml
Environment creation requested
Ernest will show you all output from your requested service creation
You can cancel at any moment with Ctrl+C, even the service is still being created, you won't have any output
Starting environment creation
Creating instances:
 - r3-jreid2-demo1-web-2
   IP        : 10.1.0.12
   Status    : completed
Instances successfully created
Updating instances:
 - r3-jreid2-demo1-web-2
   IP        : 10.1.0.12
   Status    : completed
Instances successfully updated
SUCCESS: rules successfully applied
Your environment endpoint is: 195.3.186.42

```

We can list the services we created:

```
$ ernest service list
NAME  UPDATED       STATUS  ENDPOINT
demo1 2016-05-29 14:52:13 +0100 BST done  195.3.186.42

```

For a given service we can see the history:

```
$ ernest service history demo1
NAME  BUILD ID                                                              UPDATED             STATUS
demo1 488249c2-63c2-484e-b6e0-c690ba859dab-8c22343f8f9d3dfb68e41cc033e7b492 2016-05-29 14:52:13 done
demo1 6799e858-0484-42cb-bbb1-c1bc5f61e500-8c22343f8f9d3dfb68e41cc033e7b492 2016-05-29 14:39:56 done

```

For a given service and build ID we can see the definition we applied:

```
$ ernest service definition demo1
---
name: demo1
datacenter: r3-jreid2
bootstrapping: none
service_ip: 195.3.186.42

routers: 
  - name: test1
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
      - source: 195.3.186.42
        from_port: '22'
        to_port: '22'
        destination: 10.1.0.11

instances:
  - name: web
    image: r3/ubuntu-1404
    cpus: 1
    memory: 1GB
    count: 2
    networks:
      name: web
      start_ip: 10.1.0.11

```

### Infrastructure and Server Configuration

In the above example the task of installing and configuring software was left to the user to do. In this example we will bootstrap the servers and install our software directly from the YAML.

The new YAML is shown here:

```
---
name: demo2
datacenter: r3-jreid2
bootstrapping: salt
service_ip: 195.3.186.42
ernest_ip:
  - 31.210.241.221
  - 31.210.240.161

routers: 
  - name: test1
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
      - source: 195.3.186.42
        from_port: '80'
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
$ ernest service apply demo2.yml
Environment creation requested
Ernest will show you all output from your requested service creation
You can cancel at any moment with Ctrl+C, even the service is still being created, you won't have any output
Starting environment creation
Creating networks:
 - r3-jreid2-demo2-salt
   IP     : 10.254.254.0/24
   Status : completed
 - r3-jreid2-demo2-web
   IP     : 10.1.0.0/24
   Status : completed
Networks successfully created
Creating instances:
 - r3-jreid2-demo2-salt-master
   IP        : 10.254.254.100
   Status    : completed
 - r3-jreid2-demo2-web-1
   IP        : 10.1.0.11
   Status    : completed
Instances successfully created
Updating instances:
 - r3-jreid2-demo2-salt-master
   IP        : 10.254.254.100
   Status    : completed
 - r3-jreid2-demo2-web-1
   IP        : 10.1.0.11
   Status    : completed
Instances successfully updated
Creating firewalls:
 - r3-jreid2-demo2-test2
   Status    : completed
Firewalls created
Creating nats:
 - r3-jreid2-demo2-test2
   Status    : completed
Nats created
Running bootstraps:
 - Bootstrap r3-jreid2-demo2-web-1
   Status    : completed
Bootstrap ran
Running executions:
 - Execution web 1
   Status    : completed
Executions ran
SUCCESS: rules successfully applied
Your environment endpoint is: 195.3.186.44

```

Notice that Ernest has automatically created a SALT instance for us on network 10.254.254.0/24. It has also trigged the bootstrapping process that installs the SALT minion on each of our servers, and then run the commands we specified in the provisioner section of each instance defined in the YAML.

You should be able to browse to http://195.3.186.42. Congratulations! 

If you wish to change the platform update your YAML to show how you want the platform to look, then re-apply the YAML. Ernest will make the appropriate changes to the platform.

> The SALT image can be downloaded from [here](/downloads/r3-salt-master.ova). For the current version of Ernest (1.0) it is not possible to specify the catalog name that Ernest will get the SALT image from, you will need to place the image in a catalog named 'r3'.

### Servers Only

If your vCloud account does not have the Organization Administrator assigned to it most of the network related configuration in the above examples will be impossible. You will be limited to the creation and modification of virtual machines only. An example YAML for this scenario is:

```
---
name: demo3
datacenter: r3-jreid2

instances:
  - name: web
    image: r3/ubuntu-1404
    cpus: 1
    memory: 1GB
    count: 1
    networks:
      name: r3-jreid2-test3-web
      start_ip: 10.1.0.11

```

And applying it gives:

```
$ ernest service apply demo3.yml
Environment creation requested
Ernest will show you all output from your requested service creation
You can cancel at any moment with Ctrl+C, even the service is still being created, you won't have any output
Starting environment creation
Creating instances:
 - r3-jreid2-demo3-web-1
   IP        : 10.1.0.11
   Status    : completed
Instances successfully created
Updating instances:
 - r3-jreid2-demo3-web-1
   IP        : 10.1.0.11
   Status    : completed
Instances successfully updated
SUCCESS: rules successfully applied
Your environment endpoint is:

```

## Next Steps

Take a look at the [vCloud YAML reference](/documentation/vcloud-yaml/).