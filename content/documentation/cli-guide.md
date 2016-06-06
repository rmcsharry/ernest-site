+++
date = "2016-06-06"
title = "CLI Guide"
category = "documentation"
showChildren=true
[menu.documentation]
  name = "CLI Guide"
  weight = -80
  identifier = "cli-guide"
  parent = "Introduction"
+++

# Using the CLI

## Connecting to Ernest

The first step is to specify the IP address of our Ernest Server:

```
$ ernest target https://<Ernest Server IP>
Target set

```

Now we should login to Ernest with the built-in admin account:

```
ernest login
Username: admin
Password: <admin default password>

```

and change the admin password:

```
$ ernest user list
NAME	ID					EMAIL
admin	<User ID>	<User Email>

$ ernest user password <User ID>
New Password: <new admin password>
Repeat new Password: <new admin password>

```

*Note when changing a user password you must identify the user by their User ID.*

Now we can create a user on Ernest:

```
$ ernest user create --user admin --password <admin password> <username> <password>
SUCCESS: Group <user> created
SUCCESS: User <user> created

```

*Note a group is also created with the same name as the user.*

Now we can login with our new user:

```
$ ernest logout
Log out succesful.

$ ernest login 
Username: <user>
Password: <password>
Log in succesful.

```

We can confirm our Ernest Server IP and user:

```
$ ernest info
Current target : https://<Ernest Server IP>
Current user : <user>

```

## Datacenters

Ernest uses the concept of a datacenter to specify an infrastructure service provider, the provider API endpoint, credentials to access the provider API, and information specific to certain provider types. An example of creating a datacenter in Ernest for a vCloud Director provider is:

```
$ ernest datacenter create --datacenter-user <vcloud user> --datacenter-password <vcloud password> --datacenter-org <vcloud org> <vcloud datacenter> <vcloud API endpoint> <vcloud external network>

```

## Services

**yaml, create/modify, history**

## Next Steps

See the [reference guide](/documentation/cli-cmds/) for a complete list of the commands available for the CLI.

See the provider-specific documentation for examples of how to use Ernest:

* [vCloud Director](/documentation/vcloud-into/)