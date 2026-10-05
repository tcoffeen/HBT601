# Infoblox Demo 6

## Enabling IPv6 DDNS

1. After logging in to the GUI, navigate to *Data Management -> DNS -> Zones (default)* and observe the configured zones.

![NIOS Web UI Data Management DNS Zones](../images/NIOS_webUI_data_mgmt_DNS_zones.png)

2. Select the zone that DDNS updates will apply to. In this example, the authoritative **hexabuild.net** zone is selected by clicking on the hexabuild.net link from the list of zones.

![NIOS Web UI Data Management DNS Zone hexabuild.net](../images/NIOS_webUI_data_mgmt_DNS_zones_hb-net.png)

3. Observe the list of resource records of differing types for the selected zone. Note that none of the records are marked *Dynamic*, indicating that DDNS is likely not enabled for either IPv6 or IPv4.

![NIOS Web UI Data Management DNS Zone hexabuild.net Records](../images/NIOS_webUI_data_mgmt_DNS_zones_hb-net_records.png)

4. Navigate to the *DHCP* tab under *Data Management* and click *Grid DHCP Properties* in the toolbar.

![NIOS Web UI Data Management DHCP Grid Properties](../images/NIOS_webUI_data_mgmt_DHCP_grid_prop.png)

5. On the *Grid DHCP Properties* panel that appears, select *IPv6 DDNS* from the left-hand column. Next, check the box to enable *DDNS Updates* and enter the *DDNS Domain Name* (in this example, **hexabuild.net**). Change the *DDNS Update Method* to **Standard** and near the bottom check the *Lease Renewal Update* box. Click **Save & Close**.

![NIOS Web UI Data Management DHCP Grid Properties IPv6 DDNS](../images/NIOS_webUI_data_mgmt_DHCP_grid_prop_v6_DDNS.png)

6. Restart the service.

![NIOS Web UI Services Restart](../images/NIOS_webUI_services_restart.png)

7. Once there are new leases or the existing leases have renewed, return to *Data Management -> DNS -> Zones (default) hexabuild.net* and click on **Show Filter**.

![NIOS Web UI Data Management DNS Zones hexabuild.net Show Filter](../images/NIOS_webUI_data_mgmt_DNS_zones_hb-net_filter.png)

8. Configure the filter by choosing *Record Source* for the first field. The operator should be *equals*, then select *Dynamic* for the third field. Click **Apply** then observe the three IPv6 leases below for which DNS has been dynamically updated with learned hostnames for the hexabuild.net forward zone.

![NIOS Web UI Data Management DNS Zones hexabuild.net Show Filter 2](../images/NIOS_webUI_data_mgmt_DNS_zones_hb-net_filter2.png)