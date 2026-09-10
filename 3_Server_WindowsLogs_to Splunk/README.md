# Project Objective
Set up the server to send Windows Event alerts to Splunk in order to verify how the messages appear before creating a dashboard to monitor for specific events.

For screenshots of the issue and network topology, please refer to the folder 3_Server_Splunk_config.

#Technology Used
HPE ProLiant DL360 Gen10

# Quick Topology
Splunk Laptop: 10.147.62.10/28
Server: 10.147.64.30/27
Splunk Port: 9997

# Troubleshooting Issues
Issue 1: Testing Port 9997
After verifying network connectivity, I confirmed that the server could successfully ping the Splunk laptop. However, for Splunk to operate correctly, the server must be able to communicate with Splunk over TCP port 9997, which was configured in the Splunk Universal Forwarder.

Troubleshooting
- I opened PowerShell on the server and performed a Test-NetConnection (TNC) to the Splunk IP address on port 9997:

- Test-NetConnection 10.147.62.10 -Port 9997

- The connection test continued to fail on port 9997. I then checked the configuration documentation and ran the netstat -a command on the server to get a better understanding of which ports were actively listening.

- The server was not listening for connections on port 9997.

- I then performed a Wireshark packet capture to monitor traffic on port 9997. At this point, traffic was being sent to the port, but there was no TCP acknowledgment from the server.

- For a successful TCP connection, I expected to see a SYN → SYN/ACK → ACK handshake.

Fix: 
I opened Windows Firewall on the server and created an inbound rule to allow TCP port 9997.

After allowing the port through the firewall, Wireshark showed a valid TCP handshake and acknowledgment.

I then ran netstat -a on the server again and was able to see the Splunk IP address communicating over port 9997.

Validation
After resolving the network issue with port 9997, I created Windows events that Splunk could receive and verified them using the Search & Reporting application in Splunk.

To generate test events, I started and stopped the DHCP and DNS services on the server. The corresponding Windows events successfully appeared in Splunk.

Project completed and successfully validated.
