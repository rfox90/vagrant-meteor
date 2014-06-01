vagrant-meteor
==============

[Vagrant](http://www.vagrantup.com/) configuration for a [virtual machine](http://en.wikipedia.org/wiki/Virtual_machine)
that can run [Meteor](https://www.meteor.com/) apps. Can be used on Windows, Mac OS X or Linux.

## How to use

The following instructions are optimized for Windows users.
If you have questions or problems after reading and doing the following instructions please open an issue and I will
try to address your issue.

If you find this useful I would appreciate a [Gittip](https://www.gittip.com/Sanjo/).

### Installation

1. [Download this repository](https://github.com/Sanjo/vagrant-meteor/archive/master.zip) and unpack the downloaded zip file.
2. Install [Cygwin](http://www.cygwin.com/install.html) with the packages `openssh` and `rsync`.
3. Add the `<CYGWIN_INSTALL_DIR>/bin` folder to your [PATH](http://geekswithblogs.net/renso/archive/2009/10/21/how-to-set-the-windows-path-in-windows-7.aspx).
4. Install [VirtualBox](https://www.virtualbox.org/wiki/Downloads).
5. Install [Vagrant](http://www.vagrantup.com/downloads.html) (1.6.1 or newer is needed).

### File Synchronisation

The folder is synchronised two times. This is necessary because Meteor doesn't like the shared folders of
VirtualBox that are usually used.

#### Rsync - one way synchronisation for starting the Meteor app

The folder is synchronised with [Rsync](http://docs.vagrantup.com/v2/synced-folders/rsync.html) to the guest folder `/vagrant`.
You must use this folder to start the Meteor app.
Don't change files in the `/vagrant` folder.

#### Shared Folder - two way synchronisation for file editing

The folder is also synchronised with the [VirtualBox shared folder feature](https://www.virtualbox.org/manual/ch04.html#sharedfolders) to the guest folder `/vagrant2`.
Use this folder to make changes in the guest. For example by using Meteorite.
But don't use this folder to start the Meteor app because Meteor has currently problems with this type of synchronisation that will cause a high CPU usage.

### Start the Vagrant VM

Just run start.bat. First, it will start the VM. Then it will open a SSH connection to the VM and start the automatic file synchronisation.

### Stop the Vagrant VM

First close the terminals that were opened by start.bat. Then run stop.bat. It will [suspend](https://docs.vagrantup.com/v2/cli/suspend.html) your VM.

### Create a new app

Do the following steps in the SSH terminal that was opened by `start.bat`.

1. `cd /vagrant2`
2. Create a new app with `mrt create <name>` (see [Meteorite documentation](https://github.com/oortcloud/meteorite/)).
   You can also use the `meteor` tool if you want.

### Use an existing app

Move your app folder into the downloaded `vagrant-meteor-master` folder.

### Start your app

1. Change to the app directory in the virtual machine (`cd /vagrant/<MY_APP>`)
2. Start your app with `mrt` (or `meteor`).
5. You can access the app on your host machine with `http://localhost:3000/`.

### Debugging

1. Start `debug.bat`.
2. Start your app with `NODE_OPTIONS=--debug=5858 mrt`.
3. After this you can connect to the app with the IP 127.0.0.1 and the port 5858.
