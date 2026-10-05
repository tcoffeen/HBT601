# Linux Demo 4

## Add a temporary static IPv6 address in Debian server 

1. Connect and login to the Debian server.
2. Observe the current interface configuration with the `ip -6 address show ens3` command.
3. Add a new static IPv6 address with the command `sudo ip addr add 3fff:1d00:3001:1d33::100/64 dev ens3`
4. Verify that the static IPv6 address has been added to the interface (`ip -6 a s ens3`)

**Note:** Addresses and routes added by this method will not persist following a restart of the system.

#### Example 1:

```console
user@debian-13:~$ sudo ip addr add 3fff:1d00:3001:1d33::100/64 dev ens3
user@debian-13:~$ ip -6 a s ens3
2: ens3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    altname enp0s3
    altname enx5000000a0000
    inet6 3fff:1d00:3001:1d33::100/64 scope global
       valid_lft forever preferred_lft forever
    inet6 3fff:1d00:3001:1d33::1c/128 scope global dynamic noprefixroute
       valid_lft 40458sec preferred_lft 24258sec
    inet6 3fff:1d00:3001:1d33:80f0:3d44:f944:c15f/64 scope global temporary dynamic
       valid_lft 581858sec preferred_lft 14367sec
    inet6 3fff:1d00:3001:1d33:5200:ff:fe0a:0/64 scope global dynamic mngtmpaddr noprefixroute
       valid_lft 2591967sec preferred_lft 14367sec
    inet6 fe80::5200:ff:fe0a:0/64 scope link noprefixroute
       valid_lft forever preferred_lft forever
```
