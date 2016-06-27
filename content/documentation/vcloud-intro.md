+++
date = "2016-06-06"
title = "Introduction"
category = "documentation"
showChildren=true
[menu.documentation]
  name = "Introduction"
  weight = -100
  identifier = "vcloud-intro"
  parent = "vCloud Director"
+++

# vCloud Director

[vCloud Director (vCD)](https://www.vmware.com/products/vcloud-director/) is cloud management tool from VMWare that acts as an overlay on top of vSphere, providing users with a self-service GUI and API. vCloud Director enables service providers to offer Infrastructure as a Service to their customers by providing users with direct control of virtual machine provisioning, and some aspects of networking.

## Network Limitations

vCD most network functionality is delivered by the VMWare vShield Edge (vSE) virtual appliance. Unfortunately certain key network operations can only be performed by the service provider and are not available to users. The include:

* deploying a vSE

* connecting a vSE to an external network

* sub-allocating external IP addresses to a vSE

All other common network operations are accesible to users, however many of them are limited to users with the [Organization Administrator](https://pubs.vmware.com/vca/index.jsp?topic=%2Fcom.vmware.vcloud.api.doc_56%2FGUID-BC504F6B-3D38-4F25-AACF-ED584063754F.html) role assigned to them.

## Supported Configurations

Due to the network limitations Ernest supports 2 different options for vCloud Director:

1. **normal** (your service provider has not deployed the VSE Creator Service)

2. **enhanced** (your service provider has deployed the VSE Creator Service)

<small>*The VSE Creator Service is an optional service that can give users the ability to create their own vSE and assign an IP to it. The VSE Creator Service is installed and operated by the service provider.*</small>

You can see more information about each option by reviewing the examples of [normal](/documentation/vcloud-normal/) and [enhanced](/documentation/vcloud-enhanced/) configurations.

You can also find a reference YAML for vCloud Director [here](/documentation/vcloud-yaml/).