1_SPLUNK_Cisco-Syslog

# Project Objective

Configure Splunk Enterprise to receive and analyze syslog messages from a Cisco Layer 3 switch.

The lab uses UDP port 514 for syslog communication between the Cisco device and the Splunk server. The Cisco switch is configured to forward logging messages to Splunk, and the network is verified to allow UDP/514 traffic.

Validation

To validate the configuration:

Shut down SVI VLAN 700 on the Cisco Layer 3 switch to generate an interface down syslog event.
Bring VLAN 700 back up to generate the corresponding interface up event.
Use Wireshark to verify that UDP/514 syslog traffic is being transmitted across the network.
Search the received events in Splunk Enterprise to confirm successful log ingestion.
This lab demonstrates the complete syslog flow from Cisco device → network → Splunk, including packet-level and application-level verification.
