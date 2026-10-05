# Linux Demo 2

## View IPv6 network configuration in Debian server 

1. Connect and login to the Debian server.
2. View the network configuration file with the `cat /etc/network/interfaces` command.

#### Example 1:

```console
user@debian-13:~$ cat /etc/network/interfaces
# This file describes the network interfaces available on your system
# and how to activate them. For more information, see interfaces(5).

source /etc/network/interfaces.d/*

# The loopback network interface
auto lo
iface lo inet loopback
allow-hotplug ens3
```
 