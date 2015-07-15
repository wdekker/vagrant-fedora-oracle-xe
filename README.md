Oracle XE 11g on Fedora 21 using Vagrant
=====
Get a simple Oracle XE up and running in minutes using Vagrant.

## Installation

* Clone this project:

        git clone https://github.com/wdekker/vagrant-fedora-oracle-xe.git

* Download [Oracle Database 11g Express Edition](http://download.oracle.com/otn/linux/oracle11g/xe/oracle-xe-11.2.0-1.0.x86_64.rpm.zip) for Linux x64. Place the file
  `oracle-xe-11.2.0-1.0.x86_64.rpm.zip` in the base directory (next to the Vagrantfile).

* *Optional:* Create a `postinstall.sh` script to do some custom stuff like creating a user and schema.

* Run `vagrant up` from the base directory of this project. The first time should take a couple of minutes.

## Connecting

You should now be able to
[connect](http://www.oracle.com/technetwork/developer-tools/sql-developer/downloads/index.html) to
the new database at `localhost:1521/XE` as `system` with password `oracle`. For example, if you
have `sqlplus` installed on the host machine you can do

    sqlplus system/oracle@//localhost:1521/XE

You can customize the password by editing the `xe.rsp` file before running `vagrant up`. 

## Copyright

Copyright © 2015 Willem Dekker
This work is free. You can redistribute it and/or modify it under the
terms of the Do What The Fuck You Want To Public License, Version 2,
as published by Sam Hocevar. See the COPYING file for more details.

## Warranty

This program is free software. It comes without any warranty, to the extent permitted by applicable law. You can redistribute it and/or modify it under the terms of the Do What The Fuck You Want To Public License, Version 2, as published by Sam Hocevar. See [http://www.wtfpl.net/](http://www.wtfpl.net/) for more details.