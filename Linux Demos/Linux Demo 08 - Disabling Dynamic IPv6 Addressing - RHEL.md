# Linux Demo 8

## Disabling Dynamic IPv6 Addressing in RHEL using *nmcli*

1. Connect and login to the RHEL desktop.
2. Open **Terminal**.
3. Run the `ip -6 address show ens3` command and observe the existing IPv6 configuration.

```console
[user@RHEL-10 ~]$ ip -6 a s ens3
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 state UNKNOWN qlen 1000
    inet6 ::1/128 scope host noprefixroute
       valid_lft forever preferred_lft forever
2: ens3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 state UP qlen 1000
    inet6 3fff:1d00:3001:1d33::100/64 scope global noprefixroute
       valid_lft forever preferred_lft forever
    inet6 3fff:1d00:3001:1d33::13/128 scope global dynamic noprefixroute
       valid_lft 41628sec preferred_lft 25428sec
    inet6 3fff:1d00:3001:1d33:b1b:ccb7:d675:8782/64 scope global temporary dynamic
       valid_lft 603228sec preferred_lft 14159sec
    inet6 3fff:1d00:3001:1d33:f1eb:905e:c405:8beb/64 scope global dynamic mngtmpaddr noprefixroute
       valid_lft 2591759sec preferred_lft 14159sec
    inet6 fe80::ec77:7a7a:f10d:b7b7/64 scope link noprefixroute
       valid_lft forever preferred_lft forever
```
4. Observe the configured IPv6 addresses:
   - The ::100 address is the static address manually configured from a previous lab.
   - The address configured with a /128 CIDR length is provided by DHCPv6. 
   - The **temporary** IPv6 address is labeled as such. This address has a randomized IID which will change periodically (based on the valid and preferred lifetime) and upon reboot.
   - The next address is a stable SLAAC address (as defined by RFC 7217). It also has a randomized IID, but one that will persist across reboots.

5. It may be undesirable operationally to keep the dynamically configured IPv6 addresses on a server once a static address has been defined. Generally this *static-only* operational model would be configured on the router/default gateway by modifying the Router Advertisements to set the A, M, and O flags to 0 and disable dynamic addressing for the entire segment.
   
    >   **Note:** For Linux nodes that are acting as desktop environments, dynamic addressing with privacy extensions enabled (the default configuration for RHEL/CentOS desktop installations) would likely be preferred and RAs for the segment would be configured accordingly.

6. Disabling dynamic addressing on the server side can be accomplished with the following commands: \
   `nmcli connection modify ens3 ipv6.method manual` \
   `nmcli connection up ens3`

7. Verify the configuration with the `ip -6 a s ens3` command:

```
[user@RHEL-10 ~]$ ip -6 a s ens3
2: ens3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    altname enp0s3
    altname enx500000080000
    inet6 3fff:1d00:3001:1d33::100/64 scope global noprefixroute
       valid_lft forever preferred_lft forever
    inet6 fe80::5200:ff:fe08:0/64 scope link noprefixroute
       valid_lft forever preferred_lft forever
