

### Learn Systemd

Init Boot Sequence 'CentSO'

1. boot partition find from boot loader
2. Kernel and initial RAM disk are loaded
3. Kernel pull initial drivers and set up tools from RAM disk
4. The Kernel hands the system over to /sbin/init
5. Init performs some system maintenance task from /etc/rc.d/rc.sysinit
6. Init has read the initdefault line in /etc/inittab and is entering runLevel 7.  System is read to use


    rc = runcommnds

    Redhat : /etc/rc.d
    Debian : /etc/init.d

    rc.local : sys admins can use for run their requirment


#### Basic of unit files

1. init and parts of upstart rely on Bash shell script
2. Systemd replaces the functionality of the shell script with complied C code
3. Still compatible with older System V init script

##### Unit files

1. Provided by package installation

    /usr/lib/systemd/system

2. Unit file location for system administrations

    /usr/systemd/system

3. Runtime location

    /run/systemd/system

4. view all unit file on a system

    systemctl list-unit-files
5. All unit file follow the INI file format

#### Modification Unit file

1. Modification must be in /ect/systemd/system
2. Two main methods of using custom unit files
  * copying an exsiting unit from /usr/bin64/systemd/system to /etc/systemd/system and edit this file
  * create a drop-in unit within /etc/systemd/system

##### Drop in unit files

1. create a directory named in the format of <iunit>.d with in the /ect/systemd/system directory
  * eg : modifying the HTTP service : /etc/systemsd/system/httpd.serice.d/

2. Create a .conf file that contains your change and place in this directory

  * Add a ExecStart= line to your new way of starting httpd into
    /etc/system/system/httpd.service.d/my-httpd.conf

3. the best way to create drop-in unit is to use the systemctl edit command

  * this command will create the necessary directory structure and conf file you
  * To create a full replacement (not just snippet of a unit file )use

  systemctl edit --full <unit>

4. Run the systemd-delta command to view modified unit files
5. after ANY modification to a unit file, you must run th following command to reload daemon.

    systemctl daemon-reload


#### Target types

1. multi-user.target - muti-user system runlevel 3 Provided
2. graphical.target - muti-user system with a desktop enviroment
3. rescue.target - pull in a basic system and file system mounts and provides a recurse shell
4. basic.target  basic system, used during the boot process before anther target takes over
5. sysinit.target

  systemctl isolate <target> : will chaneg the running state of the system form the current target to a different target
  systemctl rescue : almost identical to  the system V init single-user mode
  systemctl reboot : will run the reboot target
  systemctl poweoff : will perform a complete shutdown

### Service unit file

1. service unit files have following config

* [service] - denotes this is a service
* [install] - contains information about the service install
* man 5 systemd.service

    systemclt list-units -t service
    systmectl enable <daemon.service>
    systemctl disable <daemon.service>
    systmectl is-enabled <daemon.service>
