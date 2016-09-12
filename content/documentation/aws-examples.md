+++
date = "2016-06-06"
title = "AWS Examples"
category = "documentation"
showChildren=true
[menu.documentation]
  name = "AWS Examples"
  weight = -90
  identifier = "aws-examples"
  parent = "Amazon Web Services"
+++

# Amazon Web Services Examples

First YAML:

```
---
name: demo
datacenter: vpc-abcdef01

networks:
  - name: public
    subnet: 10.0.10.0/24
    public: true

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

```

First YAML apply:

```
$ ernest service apply demo.yml 
Environment creation requested
Ernest will show you all output from your requested service creation
You can cancel at any moment with Ctrl+C, even the service is still being created, you won't have any output
Starting environment creation

Creating networks:
  - 10.0.10.0/24
Networks successfully created

Setting up firewalls:
Firewalls Created

Creating instances:
   - vpc-abcdef01-demo-public-1
Instances successfully created

SUCCESS: rules successfully applied
Your environment endpoint is: 

```

First YAML list:

```
$ ernest service list
NAME  UPDATED         STATUS  ENDPOINT
demo  2016-09-12 15:57:46.195942 +0000 UTC  done

```

First YAML info:

```
$ ernest service info demo
Name : demo
Datacenter : vpc-abcdef01

Networks:
+---------------------------+-----------------+
|           NAME            |       ID        |
+---------------------------+-----------------+
| vpc-abcdef01-demo-public  | subnet-defabc01 |
+---------------------------+-----------------+

Instances:
+-----------------------------+---------------------+---------------+------------+
|            NAME             |         ID          |   PUBLIC IP   | PRIVATE IP |
+-----------------------------+---------------------+---------------+------------+
| vpc-abcdef01-demo-public-1  | i-abcdef01abcdef011 | 52.210.179.96 | 10.0.10.11 |
+-----------------------------+---------------------+---------------+------------+

NAT gateways (empty)

Security groups:
+------------------------------+-------------+
|             NAME             |  GROUP ID   |
+------------------------------+-------------+
| vpc-abcdef01-demo-public-sg  | sg-01234567 |
+------------------------------+-------------+

```

First YAML history:

```
$ ernest service history demo
NAME  BUILD ID                UPDATED         STATUS
demo  89389b76-cc25-4add-55e5-b7647217b4b1-abf663d6c173d4af98e3ff20bb7e8dde 2016-09-12 15:57:46.195942 +0000 UTC  done

```

First YAML definition:

```
$ ernest service definition demo --build 89389b76-cc25-4add-55e5-b7647217b4b1-abf663d6c173d4af98e3ff20bb7e8dde
---
name: demo
datacenter: vpc-abcdef01

networks:
  - name: public
    subnet: 10.0.10.0/24
    public: true

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

```

Second YAML:

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

Second YAML apply:

```
$ ernest service apply demo.yml 
Environment creation requested
Ernest will show you all output from your requested service creation
You can cancel at any moment with Ctrl+C, even the service is still being created, you won't have any output
Starting environment creation

Creating networks:
  - 10.0.11.0/24
Networks successfully created

Setting up firewalls:
Firewalls Created

Creating instances:
   - vpc-abcdef01-demo-private-1
Instances successfully created

Configuring nats
Nats Created

SUCCESS: rules successfully applied
Your environment endpoint is: 

```

First YAML list:

```
$ ernest service list
NAME  UPDATED         STATUS  ENDPOINT
demo  2016-09-12 15:57:46.195942 +0000 UTC  done

```

Second YAML info:

```
$ ernest service info demo
Name : demo
Datacenter : vpc-abcdef01

Networks:
+---------------------------+-----------------+
|           NAME            |       ID        |
+---------------------------+-----------------+
| vpc-abcdef01-demo-public  | subnet-defabc01 |
| vpc-abcdef01-demo-private | subnet-defabc02 |
+---------------------------+-----------------+

Instances:
+-----------------------------+---------------------+---------------+------------+
|            NAME             |         ID          |   PUBLIC IP   | PRIVATE IP |
+-----------------------------+---------------------+---------------+------------+
| vpc-abcdef01-demo-public-1  | i-abcdef01abcdef011 | 52.210.179.96 | 10.0.10.11 |
| vpc-abcdef01-demo-private-1 | i-abcdef01abcdef012 |               | 10.0.11.11 |
+-----------------------------+---------------------+---------------+------------+

NAT gateways:
+-------------------------------+-----------------------+
|             NAME              |       GROUP ID        |
+-------------------------------+-----------------------+
| vpc-abcdef01-demo-private-nat | nat-abcdef01abcdef013 |
+-------------------------------+-----------------------+

Security groups:
+------------------------------+-------------+
|             NAME             |  GROUP ID   |
+------------------------------+-------------+
| vpc-abcdef01-demo-public-sg  | sg-01234567 |
| vpc-abcdef01-demo-private-sg | sg-89012345 |
+------------------------------+-------------+

```

Second YAML history:

```
$ ernest service history demo
NAME  BUILD ID                UPDATED         STATUS
demo  72c1306c-c6ee-4d9b-4230-617d0e969ea9-abf663d6c173d4af98e3ff20bb7e8dde 2016-09-12 16:03:40.235144 +0000 UTC  done
demo  89389b76-cc25-4add-55e5-b7647217b4b1-abf663d6c173d4af98e3ff20bb7e8dde 2016-09-12 15:57:46.195942 +0000 UTC  done

```

Second YAML definition:

```
$ ernest service definition demo --build 72c1306c-c6ee-4d9b-4230-617d0e969ea9-abf663d6c173d4af98e3ff20bb7e8dde
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