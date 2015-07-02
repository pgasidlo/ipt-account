# Installation #

To install **ipt\_account** module you must first download [software](Software.md) that supports your kernel/iptables. Then, depending what distribution you use the installation may differ.

## Debian/Ubuntu ##

  * check what kernel version you are currently running
```
# uname -a
Linux psyche 2.6.20-16-generic #2 SMP Thu Jun 7 20:19:32 UTC 2007 i686 GNU/Linux
```
  * install linux-headers package matching your kernel version
```
# sudo apt-get install linux-headers-2.6.20-16-generic
```
  * kernel headers can be found in /usr/src
```
# ls -la /usr/src/
...
drwxr-xr-x  4 root root     4096 2007-07-22 01:31 linux-headers-2.6.20-16-generic
```
  * unpack downloaded **ipt\_acount** software package (filename may be different):
```
# tar xvfj ipt_account.tar.gz
```
  * build kernel module (KERNEL\_DIR variable is full path to kernel headers):
```
# cd kernel
# make KERNEL_DIR=/usr/src/linux-headers-2.6.20-generic
# make install
# depmod -Ae
# cd ..
```
  * build iptables module
```
# cd iptables
# make 
# make KERNEL_DIR=/usr/src/linux-headers-2.6.20-generic
# make install
# cd ..
```
  * if everything went ok, you should have iptables binary working with new ipt\_account match:
```
# /sbin/iptables -V
iptables v1.3.6
# /sbin/iptables -m account -h
iptables v1.3.6
...
account v1.3.6 options:
--aaddr network/netmask
        defines network/netmask for which make statistics.
--aname name
        defines name of list where statistics will be kept. If no is
        specified DEFAULT will be used.
--ashort
       table will colect only short statistics (only total counters
       without splitting it into protocols.
```

## Other ##
<sup>thanks to Jind<C5><99>ich Vrba for writting this chapter</sup>

  * you need source code for your linux kernel and iptables

  * both linux kernel and iptables should be compiled and installed
> > You can find kernel compiling howto for example here: http://www.cyberciti.biz/tips/compiling-linux-kernel-26.html
> > For iptables it is enough: make; make install
> > Optionally, if you are using any distribution based on packages:
> > > Use your distribution specific method of kernel compiling.
> > > For iptables, use checkinstall instead of make install.

  * unpack downloaded ipt\_account software package (filename may be different):
```
# cd /usr/src
# tar -xjf ipt_account.tar.gz
```
  * build kernel module (KERNEL\_DIR variable is full path to kernel source; DESTDIR\_ROOT variable is root path to kernel modules):
```
# cd kernel
# make KERNEL_DIR=/usr/src/linux-2.6.22.4
# make install KERNEL_DIR=/usr/src/linux-2.6.22.4/ DESTDIR_ROOT=/lib/modules/2.6.22.4/
# depmod -Ae 2.6.22.4
# cd ..
```
  * build iptables module (IPTABLES\_LIB\_DIR is full path to iptables libraries - "# whereis iptables | xargs -n1 | grep lib" should help you):
```
# cd iptables
# make
# make install IPTABLES_LIB_DIR=/usr/local/lib/iptables
```
  * if you are running another kernel right now, reboot your computer into the new kernel
  * if everything went ok, you should have iptables binary working with new ipt\_account match:
```
# /sbin/iptables -V
iptables v1.3.8
# /sbin/iptables -m account -h
iptables v1.3.8
...
account v1.3.8 options:
--aaddr network/netmask
        defines network/netmask for which make statistics.
--aname name
        defines name of list where statistics will be kept. If no is
        specified DEFAULT will be used.
--ashort
      table will collect only short statistics (only total counters
      without splitting it into protocols.
```