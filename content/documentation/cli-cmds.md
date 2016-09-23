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
   --user value      User credentials
   --password value  Password credentials
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
    $ ernest user create <username> <password>

   You can also add an email to the user with the flag --email

   Example:
    $ ernest user create --email username@example.com <username> <password>
  

OPTIONS:
   --email value  Email for the user
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
   --user value      Admin user credentials
   --password value  Admin password credentials
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
   --user value      Admin user credentials
   --password value  Admin password credentials
```

`ernest group delete`

```
NAME:
   ernest group delete - Deletes a group.

USAGE:
   ernest group delete

DESCRIPTION:
   Deletes a group.

    Example:
      $ ernest group delete <group-id>
```

`ernest group create`

```
NAME:
   ernest group create - Create a group.

USAGE:
   ernest group create

DESCRIPTION:
   Create a group.

   Example:
    $ ernest group create <name>
```

`ernest group add-user`

```
NAME:
   ernest group add-user - Adds a user to a group.

USAGE:
   ernest group add-user

DESCRIPTION:
   Adds a user to a group.

    Example:
      $ ernest group add-user <user-name> <group-name>
```

`ernest group remove-user`

```
NAME:
   ernest group remove-user - Removes an user from a group.

USAGE:
   ernest group remove-user

DESCRIPTION:
   Removes an user from a group.

    Example:
      $ ernest group remove-user <user-id> <group-id>
```

`ernest group add-datacenter`

```
NAME:
   ernest group add-datacenter - Adds a datacenter to a group.

USAGE:
   ernest group add-datacenter

DESCRIPTION:
   Adds a datacenter to a group.

    Example:
      $ ernest group add-datacenter <datacenter-id> <group-id>
```

`ernest group remove-datacenter`

```
NAME:
   ernest group remove-datacenter - Removes a datacenter from a group.

USAGE:
   ernest group remove-datacenter

DESCRIPTION:
   Removes an datacenter from a group.

    Example:
      $ ernest group remove-datacenter <datacenter-id> <group-id>
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

`ernest datacenter create aws`

```
NAME:
   ernest datacenter create aws - Create a new aws datacenter.

USAGE:
   ernest datacenter create aws [command options] <datacenter-name>

DESCRIPTION:
   Create a new AWS datacenter on the targeted instance of Ernest.

  Example:
   $ ernest datacenter create aws --region region --token token --secret secret my_datacenter
   

OPTIONS:
   --region value  Datacenter region
   --token value   AWS Token
   --secret value  AWS Secret
   --fake          Fake datacenter
```

`ernest datacenter create vcloud`

```
NAME:
   ernest datacenter create vcloud - Create a new vcloud datacenter.

USAGE:
   ernest datacenter create vcloud [command options] <datacenter-name> <vcloud-url> <network-name>

DESCRIPTION:
   Create a new vcloud datacenter on the targeted instance of Ernest.

   Example:
    $ ernest datacenter create vcloud --datacenter-user username --datacenter-password xxxx --datacenter-org MY-ORG-NAME --vse-url http://vse.url mydatacenter https://myernest.com MY-PUBLIC-NETWORK
  

OPTIONS:
   --datacenter-user value      User to be configured with the datacenter
   --datacenter-password value  Password related with user
   --datacenter-org value       vCloud Organization name
   --vse-url value              VSE URL
   --fake                       Fake datacenter
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
   --build value  Build ID
```

`ernest service info`

```
NAME:
   ernest service info - $ ernest service info <my_service> --build <specific build>

USAGE:
   ernest service info [command options] <service_name>

DESCRIPTION:
   Will show detailed information of the last build of a specified service.
  In case you specify --build option you will be able to output the detailed information of specific build of a service.

   Examples:
    $ ernest service definition myservice
    $ ernest service definition myservice --build build1
  

OPTIONS:
   --build value  Build ID
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
