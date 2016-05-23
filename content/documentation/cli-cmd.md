+++
date = "2016-05-17"
title = "CLI Commands"
category = "documentation"
showChildren=true
[menu.documentation]
  name = "CLI Commands"
  weight = -80
  identifier = "cli-cmd"
  parent = "Documentation"
+++


# CLI Commands

## Info

```
NAME:
   ernest info - Display system-wide information.

USAGE:
   ernest info

DESCRIPTION:
   Displays ernest instance information.

   Example:
    $ ernest info
```

## Target

```
NAME:
   ernest target - Configure Ernest target instance.

USAGE:
   ernest target <ernest_url>

DESCRIPTION:
   Sets up ernest instance target.

   Example:
    $ ernest target https://myernest.com
```

## Login

```
NAME:
   ernest login - Login with your Ernest credentials.

USAGE:
   ernest login [command options]

DESCRIPTION:
   Logs an user into Ernest instance.

   Example:
    $ ernest login

   It can also be used without asking the username and password.

   Example:
    $ ernest login --user <user> --password <password>
	

OPTIONS:
   --user 	User credentials
   --password 	Password credentials
```

## Logout

```
NAME:
   ernest logout - Clear local authentication credentials.

USAGE:
   ernest logout

DESCRIPTION:
   Logs out an user from Ernest instance.

   Example:
    $ ernest logout
```

## Apply

```
NAME:
   ernest apply - Builds or changes infrastructure.

USAGE:
   ernest apply <file.yml>

DESCRIPTION:
   Sends a service YAML description file to Ernest to be executed.
   You must be logged in to execute this command.

   If the file is not provided, ernest.yml will be used by default.

   Example:
    $ ernest apply myservice.yml
```

## Destroy

```
NAME:
   ernest destroy - Destroy a service.

USAGE:
   ernest destroy <service_name>

DESCRIPTION:
   Destroys a service by its name.

   Example:
    $ ernest destroy myservice
```

## History

```
NAME:
   ernest history - Shows the history of a service, a list of builds

USAGE:
   ernest history <service_name>

DESCRIPTION:
   Shows the history of a service, a list of builds and its status and basic information.

   Example:
    $ ernest history myservice
```

## Reset

```
NAME:
   ernest reset - Reset a service.

USAGE:
   ernest reset <service_name>

DESCRIPTION:
   Reseting a service creation may cause problems, please make sure you know what are you doing.

   Example:
    $ ernest reset myservice
```

## Status

```
NAME:
   ernest status - Show the current status of a service by its name

USAGE:
   ernest status [command options] <service_name>

DESCRIPTION:
   Show the current status of a service by its name getting the definition about the build.

   Example:
    $ ernest status myservice
	

OPTIONS:
   --build 	Build ID
```

## Upgrade

```
NAME:
   ernest upgrade - Upgrade the Ernest client.

USAGE:
   ernest upgrade

DESCRIPTION:
   Upgrades the Ernest client to the latest version available.

   Example:
    $ ernest upgrade
```

## Monitor

```
NAME:
   ernest monitor - Monitor a service.

USAGE:
   ernest monitor <service_id>

DESCRIPTION:
   Monitors a service while it is being built by its service id.

   Example:
    $ ernest monitor F94034CE-1A57-4A66-AF49-E1E99C5010A2
```

## List

### List Datacenters

```
NAME:
   ernest list datacenters - List available datacenters.

USAGE:
   ernest list datacenters

DESCRIPTION:
   List available datacenters.

   Example:
    $ ernest list datacenters
```

### List Services

```
NAME:
   ernest list services - List available services.

USAGE:
   ernest list services

DESCRIPTION:
   List available services and shows its most relevant information.

   Example:
    $ ernest list services
```

### List Users

```
NAME:
   ernest list users - List available users.

USAGE:
   ernest list users

DESCRIPTION:
   List available users.

   Example:
    $ ernest list users
```

### List Groups

```
NAME:
   ernest list groups - List available groups.

USAGE:
   ernest list groups

DESCRIPTION:
   List available groups.

   Example:
    $ ernest list groups
```

## Create

### Create Datacenters

```
NAME:
   ernest create datacenter - Create a new datacenter.

USAGE:
   ernest create datacenter [command options] <datacenter-name> <vcloud-url> <network-name>

DESCRIPTION:
   Create a new datacenter on the targeted instance of Ernest.

   Example:
    $ ernest create datacenter --datacenter-user username --datacenter-password xxxx --datacenter-org MY-ORG-NAME mydatacenter https://myernest.com MY-PUBLIC-NETWORK
	

OPTIONS:
   --datacenter-user 		User to be configured with the datacenter
   --datacenter-password 	Password related with user
   --datacenter-org 		vCloud Organization name
```

### Create User

```
NAME:
   ernest create user - Create a new user.

USAGE:
   ernest create user [command options] <username> <password>

DESCRIPTION:
   Create a new user on the targeted instance of Ernest.

   Example:
    $ ernest create user --user admin --password xxxx username xxxxxx

   You can also add an email to the user with the flag --email

   Example:
    $ ernest create user --user admin --password xxxx --email username@example.com username xxxxxx
	

OPTIONS:
   --user 	Admin user credentials
   --password 	Admin password credentials
   --email 	Email for the user
```

### Create Group

```
NAME:
   ernest create group - Create group.

USAGE:
   ernest create group [arguments...]

DESCRIPTION:
   Create a group of users.
```
