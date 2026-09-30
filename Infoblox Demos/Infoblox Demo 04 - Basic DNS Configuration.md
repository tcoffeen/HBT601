# Infoblox Demo 4

## IPv6 Basic DNS Configuration in Infoblox NIOS 

1. After logging in to the GUI, select **Grid**.

![NIOS Web UI Dashboard](../images/NIOS_webUI_dashboard_grid.png)

2. The **Grid Manager** workspace appears. Verify that the **Services** tab is selected for **DNS** then check the box next to the grid member's name before clicking on the edit button.

![NIOS Web UI Grid Manager Services DNS](../images/NIOS_webUI_grid_mgr_serv_DNS.png)

3. The **Member DNS Properties** screen appears. Verify that IPv6 (along with IPv4) is enabled for the LAN1 interface.

![NIOS Web UI Grid Manager Services DNS Properties](../images/NIOS_webUI_grid_mgr_serv_DNS_prop.png)

   > In this lab example, the Infoblox nameserver is authoritative for only the hexabuild.net domain (and only within the confines of the lab network). The servers and clients are configured to use IPv4 and IPv6 addresses of infoblox.hexabuild.net as the only recursive DNS server. As a result, the nameserver needs to have forwarders configured to facilitate name resolution for Internet domain names.

4. To configure DNS forwarders, return to the *Grid -> Grid Manager -> Services* screen, click the service checkbox, then click **Edit** in the Toolbar on the right.

![NIOS Web UI Grid Manager Services DNS Grid Properties](../images/NIOS_webUI_grid_mgr_serv_DNS_grid_prop.png)

5. Note that two Internet-based external forwarders are already configured (provided by the open DNS service Quad9 in this instance).

![NIOS Web UI Grid Manager Services DNS Grid Properties 2](../images/NIOS_webUI_grid_mgr_serv_DNS_grid_prop2.png)

6. To add an additional forwarder, click the plus sign in the uppper right hand corner, then enter the IPv6 (or IPv4) address of the forwarder in the indicated field. (In this example, the IPv6 address for a Cloudflare DNS nameserver is used.) Click **Save & Close**.

![NIOS Web UI Grid Manager Services DNS Grid Properties 3](../images/NIOS_webUI_grid_mgr_serv_DNS_grid_prop3.png)

7. Restart the service.

![NIOS Web UI Services Restart](../images/NIOS_webUI_services_restart.png)