# Linux Demo 5

## Add a permanent static IPv6 address in Ubuntu server 

1. Connect and login to the Ubuntu server.
2. Observe the current interface configuration with the `ip -6 address show` command.
3. Open the network configuration file with the `sudo vi /etc/netplan/50-cloud-init.yaml` command; (if preferred, use `sudo nano /etc/netplan/50-cloud-init.yaml`).
4. Add static IPv6 configuration (see Example 1) and save the file.
5. Apply the configuration changes with the command `sudo netplan apply`
6. Verify that the static IPv6 address has been added to the interface (`ip -6 a s`) 

#### Example 1:

```console
# Static IPv6/IPv4 configuration
network:
  version: 2
  ethernets:
    ens3:
      dhcp4: no
      dhcp6: no
      addresses:
        - 3fff:1d00:3001:1d33::100/64
        - 192.168.51.100/24
      accept-ra: no
      nameservers:
        addresses:
          - 1.1.1.1
          - 2620:fe::fe
      routes:
          - to: "::/0"
            via: "FE80::5200:FF:FE05:1"
          - to: "0.0.0.0/0"
            via: "192.168.51.1"
```
