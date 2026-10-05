# Infoblox Demo 2

## Verify NIOS network settings using the CLI 

1. Connect to the Infoblox NIOS console and login at the prompt with the username `admin` and the password `infoblox`

```console
Disconnect NOW if you have not been expressly authorized to use this system.
login: admin
Local password:

               Infoblox NIOS Release 9.0.3-50212-ee11d5834df9 (64bit)
     Copyright (c) 1999-2023 Infoblox Inc. All Rights Reserved.

                   type 'help' for more information


Infoblox >
```

2. View the basic network settings with the command `show network`

```console
Infoblox > show network
Current LAN1 Network Settings:
  IPv4 Address:               192.168.50.53
  Network Mask:               255.255.255.0
  Gateway Address:            192.168.50.1
  VLAN Tag:                   Untagged
  IPv6 Address:               3fff:1d00:3001:1d32::53/64
  IPv6 Gateway Address:       automatic
  IPv6 VLAN Tag:              Untagged
  HA enabled:                 false
  Grid Status:                Master of Infoblox Grid

Note: Additional addresses configured can be viewed through "show interface" command
```
3. Use the `show interface lan1` command for interface details.

```console
Infoblox > show interface lan1
LAN1:
           IP Address:  192.168.50.53    MAC Address: 50:00:00:06:00:01
           Mask:        255.255.255.0    Broadcast:   192.168.50.255
           MTU:         1500             Metric:      1
           IPv6 Address:       3fff:1d00:3001:1d32::53
           IPv6 Link:          fe80::5200:ff:fe06:1
           IPv6 Status:        Enabled
           Negotiation: Disabled
           Speed:       unknown          Duplex:      unknown
           Status:      UP,BROADCAST,RUNNING,MULTICAST

           Statistics Information
             Received
                    packets:  10408        bytes:    1804440 (1.8 MB)
                    errors:   0            dropped:  1
                    overruns: 0            frame:    0
             Transmitted
                    packets:  13165        bytes:    10839774 (10.8 MB)
                    errors:   0            dropped:  0
                    overruns: 0            carrier:  0
             Collisions: 0                Txqueuelen:  1000

Enter <return> for next page or q<return> to cancel the command.
```
4. To view the routing table, run `show routes`.

```console
Infoblox > show routes
From LAN1:
  IPv4 route table:
192.168.50.0/24 dev eth1 scope link
default via 192.168.50.1 dev eth1

  IPv6 route table:

From anycast route table:
192.168.50.0/24 dev eth1 scope link

From IPv4 main route table:
default via 192.168.50.1 dev eth1 proto static
169.254.251.0/24 dev docker0 proto kernel scope link src 169.254.251.1 linkdown
192.168.50.0/24 dev eth1 proto kernel scope link src 192.168.50.53
From IPv6 main route table:
3fff:1d00:3001:1d32::/64 dev eth1 proto kernel metric 256 pref medium
fe80::/64 dev eth1 proto kernel metric 256 pref medium
default via fe80::5200:ff:fe02:1 dev eth1 proto ra metric 1024 expires 1795sec hoplimit 64 pref medium
Infoblox >
```
5. Verify basic connectivity by pinging the default gateway, in this instance the link-local learned via the Router Advertisement (enabled by the *automatic* configuration setting for the default gateway).

```console
Infoblox > ping fe80::5200:ff:fe02:1 count 5
pinging fe80::5200:ff:fe02:1
PING fe80::5200:ff:fe02:1(fe80::5200:ff:fe02:1) from :: eth1: 56 data bytes
64 bytes from fe80::5200:ff:fe02:1%eth1: icmp_seq=1 ttl=64 time=0.465 ms
64 bytes from fe80::5200:ff:fe02:1%eth1: icmp_seq=2 ttl=64 time=0.372 ms
64 bytes from fe80::5200:ff:fe02:1%eth1: icmp_seq=3 ttl=64 time=0.795 ms
64 bytes from fe80::5200:ff:fe02:1%eth1: icmp_seq=4 ttl=64 time=0.532 ms
64 bytes from fe80::5200:ff:fe02:1%eth1: icmp_seq=5 ttl=64 time=0.384 ms

--- fe80::5200:ff:fe02:1 ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 4063ms
rtt min/avg/max/mdev = 0.372/0.509/0.795/0.154 ms
Infoblox >
```
Note that because there is only the LAN1 interface configured with IPv6, no outgoing interface interface is specified or needed for the link-local ping.

6. Observe the IPv6 neighbor discovery cache with the command `show ipv6_neighbor lan1`.

```console
Infoblox > show ipv6_neighbor lan1
3fff:1d00:3001:1d32::80 lladdr 50:00:00:0b:00:00 STALE
fe80::5200:ff:fe06:1  FAILED
fe80::5200:ff:fe02:1 lladdr 50:00:00:02:00:01 router STALE
fe80::5200:ff:fe0b:0 lladdr 50:00:00:0b:00:00 STALE
Infoblox >
```