+++
date = "2016-06-06"
title = "Installation"
category = "documentation"
showChildren=true
[menu.documentation]
  name = "Installation"
  weight = -90
  identifier = "install"
  parent = "Introduction"
+++

# Installating Ernest

## The Server

The Ernest Server can be [downloaded](/download/) as a pre-packaged OVF or VirtualBox image. It can also be built from source by following the instructions on [GitHub](https://github.com/r3labs/ernest).

## The CLI

The Ernest CLI is distributed as a binary package for all supported platforms and architectures. It can also be built from source by following the instructions on [GitHub](https://github.com/r3labs/ernest-cli).

### Installation

To install Ernest CLI, find the [appropriate package](http://artefact.r3labs.io/ernest/) for your system and download it. Ernest CLI is packaged as an executable.

After downloading Ernest CLI, move it to a directory that is on the PATH. See [this page](http://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux) for instructions on setting the PATH on Linux and Mac. [This page](http://stackoverflow.com/questions/1618280/where-can-i-set-path-to-make-exe-on-windows) contains instructions for setting the PATH on Windows.

### Verification

After installing Ernest CLI, verify the installation worked by opening a new terminal session and checking that ernest is available. By executing ernest you should see help output similar to that below:

```
$ ernest
NAME:
   ernest - Command line interface for Ernest

USAGE:
   ernest [global options] command [command options] [arguments...]
   
VERSION:
   0.14
   
COMMANDS:
    target  Configure Ernest target instance.
    info  Display system-wide information.
    login Login with your Ernest credentials.
    logout  Clear local authentication credentials.
    user  User related subcommands
    group Group related subcommands
    datacenter  Datacenter related subcommands
    service Service related subcommands

GLOBAL OPTIONS:
   --help, -h   show help
   --version, -v  print the version

```

If you get an error that ernest could not be found, then your PATH environment variable was not setup properly. Please go back and ensure that your PATH variable contains the directory where Ernest CLI was installed.

Otherwise, Ernest CLI is installed and ready to go.

## Next Steps

Now that we have the Server and CLI installed we can [start working with the CLI](/documentation/cli-guide/).