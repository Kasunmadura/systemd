

### Learn systemd


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


    Lec : init
