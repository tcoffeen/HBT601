# Infoblox Demo 3

## Configuring network settings in the Infoblox NIOS GUI 

1. Login to the web UI. 

![NIOS Web UI Login](../images/NIOS_webUI_login_2.png)

2. Select **Grid**.

![NIOS Web UI Dashboard](../images/NIOS_webUI_dashboard_grid.png)

3. The **Grid Manager** workspace appears. Verify that the **Members** tab is selected then check the box next to the grid member's name before clicking on the edit button.  

![NIOS Web UI Grid Manager](../images/NIOS_webUI_grid_mgr.png)

4. The **Grid Member Properties Editor** screen appears. Select **Network** from the configuration tabs to the left.  

![NIOS Web UI Grid Manager Properties](../images/NIOS_webUI_grid_mgr_prop.png)

5. Observe the options for the type of network connectivity. In most deployments, **IPv4 and IPv6** will be the desired choice. Note also the existing IPv6 and IPv4 addressing and gateways from the earlier, initial CLI configuration of NIOS.

![NIOS Web UI Grid Manager Properties Network](../images/NIOS_webUI_grid_mgr_prop_net.png)

6. Scroll down to **Communication Protocol Settings and Preferences** and observe that IPv6 and IPv4 are transport options for the Grid services listed under **Customized Settings**. Note that these features offer IPv6 feature parity with IPv4 and permit enhanced Infoblox grid function in an IPv6-only environment.

![NIOS Web UI Grid Manager Properties Network 2](../images/NIOS_webUI_grid_mgr_prop_net2.png)