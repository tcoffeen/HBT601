# Linux Demo 1

## View IPv6 and IPv4 addresses configured on the interface in Linux with the `ip address show` command

1. Connect and login to a dual-stack Linux node.
2. In the console or terminal type the `ip address show` (can be abbreviated to `ip a s`) command and view the results. To view only the IPv6 addresses use `ip -6 address show`.
3. What is the source of the various configured IP addresses (DHCP, DHCPv6, SLAAC, etc.)?
4. What are the IPv6 address types configured (GUA, Link-local, etc)?
5. What are the configured IPv6 address Interface Identifier (IID) types (EUI-64, temporary/random, DHCPv6 pool, etc.)?

#### Example 1 (Debian-13):

```console
user@debian-13:~$ ip a show
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute
       valid_lft forever preferred_lft forever
2: ens3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 50:00:00:0a:00:00 brd ff:ff:ff:ff:ff:ff
    altname enp0s3
    altname enx5000000a0000
    inet 192.168.51.19/24 brd 192.168.51.255 scope global dynamic noprefixroute ens3
       valid_lft 42249sec preferred_lft 42249sec
    inet6 3fff:1d00:3001:1d33::1c/128 scope global dynamic noprefixroute
       valid_lft 38927sec preferred_lft 22727sec
    inet6 3fff:1d00:3001:1d33:c708:8698:8a19:acfe/64 scope global temporary dynamic
       valid_lft 582234sec preferred_lft 14292sec
    inet6 3fff:1d00:3001:1d33:5200:ff:fe0a:0/64 scope global dynamic mngtmpaddr noprefixroute
       valid_lft 2591892sec preferred_lft 14292sec
    inet6 fe80::5200:ff:fe0a:0/64 scope link noprefixroute
       valid_lft forever preferred_lft forever
```
