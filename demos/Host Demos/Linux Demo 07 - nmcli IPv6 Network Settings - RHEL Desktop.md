# Linux Demo 7

## Use *nmcli* to Review and Configure IPv6 Settings in RHEL 

1. Connect and login to the RHEL desktop.
2. Open **Terminal**.
3. Run the `ip -6 address show ens3` command and observe the existing IPv6 configuration.
4. Without hitting enter, type the command `nmcli connection modify ens3 ipv6.`
5. Hit the tab key twice for context sensitive help to display all of the IPv6 configuration options available for the interface.

```console
[user@RHEL-10 ~]$ nmcli connection modify ens3 ipv6.
ipv6.addresses                ipv6.ignore-auto-routes
ipv6.addr-gen-mode            ipv6.ip6-privacy
ipv6.auto-route-ext-gw        ipv6.may-fail
ipv6.dhcp-duid                ipv6.method
ipv6.dhcp-hostname            ipv6.mtu
ipv6.dhcp-hostname-flags      ipv6.never-default
ipv6.dhcp-iaid                ipv6.ra-timeout
ipv6.dhcp-pd-hint             ipv6.replace-local-rule
ipv6.dhcp-send-hostname       ipv6.required-timeout
ipv6.dhcp-send-hostname-v2    ipv6.routed-dns
ipv6.dhcp-send-release        ipv6.route-metric
ipv6.dhcp-timeout             ipv6.routes
ipv6.dns                      ipv6.route-table
ipv6.dns-options              ipv6.routing-rules
ipv6.dns-priority             ipv6.temp-preferred-lifetime
ipv6.dns-search               ipv6.temp-valid-lifetime
ipv6.gateway                  ipv6.token
ipv6.ignore-auto-dns
[user@RHEL-10 ~]$ nmcli connection modify ens3 ipv6.
``` 
6. Add a static IPv6 address with the command `nmcli connection modify ens3 ipv6.addresses "3fff:1d00:3001:1d33::100/64"`
7. Confirm the modification with the command `nmcli connection show ens3 | grep ipv6.addresses`

```console
[root@RHEL-10 user]# nmcli connection show ens3 | grep ipv6.addresses
ipv6.addresses:                         3fff:1d00:3001:1d33::100/64
```
8. Apply the change with the command `nmcli connection up ens3` and confirm with `ip -6 a s ens3`

```console
[user@RHEL-10 ~]$ ip -6 a s ens3
2: ens3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 state UP qlen 1000
    inet6 3fff:1d00:3001:1d33::100/64 scope global noprefixroute
       valid_lft forever preferred_lft forever
    inet6 3fff:1d00:3001:1d33::13/128 scope global dynamic noprefixroute
       valid_lft 42907sec preferred_lft 26707sec
    inet6 3fff:1d00:3001:1d33:a2be:6a17:f5c4:b630/64 scope global temporary dynamic
       valid_lft 604506sec preferred_lft 14196sec
    inet6 3fff:1d00:3001:1d33:f1eb:905e:c405:8beb/64 scope global dynamic mngtmpaddr noprefixroute
       valid_lft 2591796sec preferred_lft 14196sec
    inet6 fe80::ec77:7a7a:f10d:b7b7/64 scope link noprefixroute
       valid_lft forever preferred_lft forever
```
**Note:** Addresses added with this method will persist across reboots.

