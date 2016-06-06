+++
date = "2016-06-06"
title = "CLI Command Reference"
category = "documentation"
showChildren=true
[menu.documentation]
  name = "CLI Command Reference"
  weight = -70
  identifier = "cli-cmds"
  parent = "Introduction"
+++


# CLI Command Reference

`ernest target`

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

`ernest info`

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

`ernest login`

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
   --user   User credentials
   --password   Password credentials
```

`ernest logout`

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

`ernest user list`

```
NAME:
   ernest user list - List available users.

USAGE:
   ernest user list

DESCRIPTION:
   List available users.

   Example:
    $ ernest user list
```

`ernest user create`

```
NAME:
   ernest user create - Create a new user.

USAGE:
   ernest user create [command options] <username> <password>

DESCRIPTION:
   Create a new user on the targeted instance of Ernest.

   Example:
    $ ernest user create --user <adminuser> --password <adminpassword> <username> <password>

   You can also add an email to the user with the flag --email

   Example:
    $ ernest user create --user <adminuser> --password <adminpassword> --email username@example.com <username> <password>
  

OPTIONS:
   --user   Admin user credentials
   --password   Admin password credentials
   --email  Email for the user
```

`ernest user password`

```
NAME:
   ernest user password - Change password of available users.

USAGE:
   ernest user password [command options] <user-id>

DESCRIPTION:
   Change password of available users.

   Example:
    $ ernest user password <user-id>

    or changing a password by being admin:

    $ ernest user password --user <adminuser> --password <adminpassword> <user-id>
  

OPTIONS:
   --user   Admin user credentials
   --password   Admin password credentials
```

`ernest user disable`

```
NAME:
   ernest user disable - Disable available users.

USAGE:
   ernest user disable [command options] <username>

DESCRIPTION:
   Disable available users.

  Example:
   $ ernest user disable --user <adminuser> --password <adminpassword> <user-id>
 

OPTIONS:
   --user   Admin user credentials
   --password   Admin password credentials
```

`ernest group list`

```
NAME:
   ernest group list - List available groups.

USAGE:
   ernest group list

DESCRIPTION:
   List available groups.

   Example:
    $ ernest group list
```

`ernest datacenter list`

```
NAME:
   ernest datacenter list - List available datacenters.

USAGE:
   ernest datacenter list

DESCRIPTION:
   List available datacenters.

   Example:
    $ ernest datacenter list
```

`ernest datacenter create`

```
NAME:
   ernest datacenter create - Create a new datacenter.

USAGE:
   ernest datacenter create [command options] <datacenter-name> <vcloud-url> <network-name>

DESCRIPTION:
   Create a new datacenter on the targeted instance of Ernest.

   Example:
    $ ernest datacenter create --datacenter-user username --datacenter-password xxxx --datacenter-org MY-ORG-NAME --vse-url http://vse.url mydatacenter https://myernest.com MY-PUBLIC-NETWORK
  

OPTIONS:
   --datacenter-user    User to be configured with the datacenter
   --datacenter-password  Password related with user
   --datacenter-org     vCloud Organization name
   --vse-url      VSE URL
```

`ernest service list`

```
NAME:
   ernest service list - List available services.

USAGE:
   ernest service list

DESCRIPTION:
   List available services and shows its most relevant information.

   Example:
    $ ernest service list
```

`ernest service apply`

```
NAME:
   ernest service apply - Builds or changes infrastructure.

USAGE:
   ernest service apply <file.yml>

DESCRIPTION:
   Sends a service YAML description file to Ernest to be executed.
   You must be logged in to execute this command.

   If the file is not provided, ernest.yml will be used by default.

   Example:
    $ ernest apply myservice.yml
```

`ernest service destroy`

```
NAME:
   ernest service destroy - Destroy a service.

USAGE:
   ernest service destroy [command options] <service_name>

DESCRIPTION:
   Destroys a service by its name.

   Example:
    $ ernest destroy myservice
  

OPTIONS:
   --yes, -y  Force destroy command without asking for permission.
```

`ernest service history`

```
NAME:
   ernest service history - Shows the history of a service, a list of builds

USAGE:
   ernest service history <service_name>

DESCRIPTION:
   Shows the history of a service, a list of builds and its status and basic information.

   Example:
    $ ernest history myservice
```

`ernest service reset`

```
NAME:
   ernest service reset - Reset an in progress service.

USAGE:
   ernest service reset <service_name>

DESCRIPTION:
   Reseting a service creation may cause problems, please make sure you know what are you doing.

   Example:
    $ ernest reset myservice
```

`ernest service definition`

```
NAME:
   ernest service definition - Show the current definition of a service by its name

USAGE:
   ernest service definition [command options] <service_name>

DESCRIPTION:
   Show the current definition of a service by its name getting the definition about the build.

   Example:
    $ ernest service definition myservice
  

OPTIONS:
   --build  Build ID
```

`ernest service monitor`

```
NAME:
   ernest service monitor - Monitor a service.

USAGE:
   ernest service monitor <service_id>

DESCRIPTION:
   Monitors a service while it is being built by its service id.

   Example:
    $ ernest monitor F94034CE-1A57-4A66-AF49-E1E99C5010A2
```
