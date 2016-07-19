+++
date = "2016-06-06"
title = "Bootstrapping with Salt"
category = "documentation"
showChildren=true
[menu.documentation]
  name = "Bootstrapping with Salt"
  weight = -60
  identifier = "salt-boot"
  parent = "Introduction"
+++

# Bootstrapping with Salt

Once we have created our servers we may want to install and configure software on them (bootstrap them). We can use Ernest to bootstrap the servers for us.

Ernest uses [Salt](https://saltstack.com/) for bootstrapping. When you enable Salt bootstrapping in an environment Ernest deploys a small footprint Salt Master into the environment. Ernest then instructs the Salt Master to install the Salt Minion on each server, and have each server register themselves with the Salt Master.

Once the servers have been registered we can securely communicate with them from Ernest, and execute remote commands on them. These commands can be included in the YAML that defines the environment. You can find an example of bootstrapping [here](/documentation/vcloud-normal-examples/).

If you wish to use Salt bootstrapping the supported OS versions and OS-specific requirements are shown in the following table:

| OS | Windows | CentOS | Ubuntu |
|:---:|:---:|:---:|:---:|
| Supported Versions | 2012r2 and newer | 6.5 and newer | 14.04 and newer |
| Installation Method | WinRM | SSH | SSH |
| Username | ernest | ernest | ernest |
| Password | b00tStr4pp3rR | b00tStr4pp3rR | b00tStr4pp3rR |
| Privilege Level | local administrator | passwordless sudo | passwordless sudo |
| Notes | - | disable sudo tty req | disable sudo tty req |

You can download the salt-master appliance from the [Download page](/download).