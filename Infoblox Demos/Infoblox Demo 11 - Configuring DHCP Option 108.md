# Infoblox Demo 11

## Configuring DHCP Option 108 to Support IPv6-Mostly

1. After logging in to the UI, navigate to *Data Management -> DHCP -> DHCP Options* then select the checkbox for **DHCP** and click the pencil/edit icon.

![NIOS Web UI Data Management DHCP Option Spaces](../images/NIOS_webUI_data_mgmt_DHCP_options.png)

2. The **DHCP (Option Space)** configuration panel appears. Click the plus sign next to options to add a new DHCP option.

![NIOS Web UI Data Management DHCP Option Spaces 2](../images/NIOS_webUI_data_mgmt_DHCP_options2.png)

3. Scroll to the bottom of the list of options where a new blank one should appear. Click in the area under the **Name** column heading and enter a descriptive name. In this example, *ipv6-mostly* is entered.

![NIOS Web UI Data Management DHCP Option Spaces 3](../images/NIOS_webUI_data_mgmt_DHCP_options3.png)

4. Next, click in the area under the **Code** column heading and enter a value. In this example, *108* for DHCP Option 108.

![NIOS Web UI Data Management DHCP Option Spaces 4](../images/NIOS_webUI_data_mgmt_DHCP_options4.png)

5. Next, click in the area under the **Type** column heading and select a value from the pull-down menu. In this example, *32-bit Unsigned Integer* is selected

![NIOS Web UI Data Management DHCP Option Spaces 5](../images/NIOS_webUI_data_mgmt_DHCP_options5.png)

6. Verify that the new option has all the correct values then click **Save & Close**.

![NIOS Web UI Data Management DHCP Option Spaces 6](../images/NIOS_webUI_data_mgmt_DHCP_options6.png)

7. Next click on **Grid DHCP Properties** in the toolbar.
   
![NIOS Web UI Data Management DHCP Option Spaces 7](../images/NIOS_webUI_data_mgmt_DHCP_options7.png)

8. On the **(Infoblox) Grid DHCP Properties** configuration panel that appears, select **IPv4 DHCP Options** in the left column, then scroll down to the **Custom DHCP Options** item.
   
![NIOS Web UI Grid DHCP Properties](../images/NIOS_webUI_grid_DHCP_prop.png)

9. Click the **Custom DHCP Options** pull-down menu and select the desired option. In this example, *ipv6-mostly (108) 32-bit unsigned integer*.
   
![NIOS Web UI Grid DHCP Properties 2](../images/NIOS_webUI_grid_DHCP_prop2.png)

10. The second field for **Custom DHCP Options** accepts a value associated with the configured option type. In this example, this is the number of seconds (1800 seconds, or 30 minutes) that DHCP will signal to the IPv6-mostly host not to configure an IPv4 lease. Click **Save & Close** and restart the service.
   
![NIOS Web UI Grid DHCP Properties 3](../images/NIOS_webUI_grid_DHCP_prop3.png)

11. The proper configuration of the new DHCP option can be validated in different ways. In this example, a Wireshark packet capture of DHCP traffic to an IPv6-mostly host indicates the presence of DHCP Option 108 in the ACK from the DHCP server along with the configured type value.

![Wireshark DHCP Option 108](../images/Wireshark_DHCP_Option108.png)