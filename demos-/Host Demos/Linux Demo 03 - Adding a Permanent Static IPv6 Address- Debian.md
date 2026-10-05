# Linux Demo 3

## Add a permanent static IPv6 address in Debian server 

1. Connect and login to the Debian server.
2. Observe the current interface configuration with the `ip -6 address show` command.
3. Open the network configuration file with the `sudo vi /etc/network/interfaces` command; (if preferred, use `sudo nano /etc/network/interfaces`).
4. Add static IPv6 configuration (see Example 1) and save the file.
5. Reboot the system with the command `sudo reboot` (Note: Restarting networking with the `systemctl restart networking` command or disabling and reenabling the interface with `ip link set ens3 down ; ip link set ens3 up` will not remove the dynamically learned IPv6 addresses.)
6. Verify that the static IPv6 address has been added to the interface (`ip -6 a s`) 

#### Example 1:

```console
# Static IPv6 configuration
iface ens3 inet6 static
   autoconf 0
   address 3fff:1d00:3001:1d33::100
   netmask 64
   gateway 3fff:1d00:3001:1d33::1
   dns-nameservers 2620:fe::fe

# Optional Static IPv4 configuration    
iface ens3 inet static
   address 192.168.51.100
   netmask 24
   gateway 192.168.51.1
   dns-nameservers 192.168.50.53
```
