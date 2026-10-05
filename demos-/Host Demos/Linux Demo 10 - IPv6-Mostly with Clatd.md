# Linux Demo 10

## IPv6-Mostly with Clatd

1. Log in to a host on the network segment configured for IPv6-mostly

2. Run the `ip address show` command and observe the output.

   - What is the globally scoped IPv6 address of the primary interface?
   - How was it learned?
   - Which interface has an IPv4 address and what is it?

2. Run the `ip route show` command and observe the output.

   - Is there a default IPv4 route?
   - What interface does it point to?

3. Try pinging an IPv4 address; e.g., `ping 1.1.1.1`.

   - Was the ping successful?

4. Now try pinging and IPv4-only domain; e.g., `ping github.com`

   - Was the ping successful?

5. Traceroute to the same IPv4-only domain; e.g., `traceroute github.com`

   - What is the address of the first hop?

6. Review the log for the clatd service on the IPv6-mostly host by running the command `journalctl -u clatd.service`

   - How did clatd learn the NAT64 prefix?
   - What does Tayga do?

```console
[user@CentOS-9-v6-m ~]$ journalctl -u clatd.service
Jan 18 23:14:08 CentOS-9-v6-m systemd[1]: Started 464XLAT CLAT daemon.
Jan 18 23:14:08 CentOS-9-v6-m systemd[1]: Stopping 464XLAT CLAT daemon...
Jan 18 23:14:08 CentOS-9-v6-m systemd[1]: clatd.service: Deactivated successfully.
Jan 18 23:14:08 CentOS-9-v6-m systemd[1]: Stopped 464XLAT CLAT daemon.
Jan 18 23:14:08 CentOS-9-v6-m systemd[1]: Started 464XLAT CLAT daemon.
Jan 18 23:14:10 CentOS-9-v6-m clatd[1188]: Starting clatd v2.1.0 by Tore Anderson <tore@fud.no>
Jan 18 23:14:10 CentOS-9-v6-m clatd[1188]: Performing DNS64-based PLAT prefix discovery (cf. RFC 7050)
Jan 18 23:14:10 CentOS-9-v6-m clatd[1188]: Using PLAT (NAT64) prefix: 2001:db8:3001:1dff::/96
Jan 18 23:14:20 CentOS-9-v6-m clatd[1188]: Device facing the PLAT: ens3
Jan 18 23:14:20 CentOS-9-v6-m clatd[1188]: Using CLAT IPv4 address: 192.0.0.1
Jan 18 23:14:20 CentOS-9-v6-m clatd[1188]: Using CLAT IPv6 address: 3fff:1d00:3001:1d35:5200:ff:fe0c:0
Jan 18 23:14:20 CentOS-9-v6-m clatd[1188]: Checking if this system already has IPv4 connectivity in 10 sec(s)
Jan 18 23:14:20 CentOS-9-v6-m clatd[1188]: Enabling IPv6 forwarding
Jan 18 23:14:20 CentOS-9-v6-m clatd[1188]: Creating and configuring up CLAT device 'clat'
Jan 18 23:14:20 CentOS-9-v6-m clatd[2087]: Created persistent tun device clat
Jan 18 23:14:20 CentOS-9-v6-m clatd[1188]: Adding clatd nftable, using conntrack mark 49575
Jan 18 23:14:20 CentOS-9-v6-m clatd[1188]: Adding IPv4 default route via the CLAT
Jan 18 23:14:20 CentOS-9-v6-m clatd[1188]: Starting up TAYGA, using config file '/tmp/5IT_T2_xhA'
Jan 18 23:14:20 CentOS-9-v6-m tayga[2107]: starting TAYGA 0.9.2
Jan 18 23:14:20 CentOS-9-v6-m tayga[2107]: Using tun device clat with MTU 1500
Jan 18 23:14:20 CentOS-9-v6-m tayga[2107]: TAYGA's IPv4 address: 192.0.0.2
Jan 18 23:14:20 CentOS-9-v6-m tayga[2107]: TAYGA's IPv6 address: 2001:db8:3001:1dff::c000:2
Jan 18 23:14:20 CentOS-9-v6-m tayga[2107]: NAT64 prefix: 2001:db8:3001:1dff::/96
```
