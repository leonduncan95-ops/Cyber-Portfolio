# Splunk + Sysmon (Windows Logging Lab)

## One-line summary
Built a Windows logging setup using Sysmon + Splunk and used searches to pull process, DNS, and network activity.

## Tools used
- Splunk Enterprise (local)
- Sysmon (Windows)
- Windows Event Logs

## What I did (high level)
1. Confirmed Sysmon logs were coming into Splunk
2. Checked which Sysmon Event IDs were showing up
3. Ran searches to pull useful fields (process name, command line, destination IP/port, DNS query)
4. Saved searches / made the results easy to read

## Why this matters
Splunk is used in security teams to search logs fast and spot suspicious activity. Sysmon gives detailed Windows event data that helps you answer questions like:
- What process ran?
- What did it try to connect to?
- What domains were queried?
## Evidence (Screenshots)

### Event ID and count
![Event ID count](./Event-ID-count.png)

### User and Command line
![User and Command line](./User-Command-line.png)

### Query Name
![Query Name](./Query-Name.png)

### Query name 2
![Query name 2](./Query-name-2.png)

### Destination IP and Port
![Destination IP Port](./DestinationIP-Port.png)

### Destination IP, Port, Protocol
![Destination IP Port Protocol](./Destination-IP-Port-Protocol.png)

### Raw screenshots (extra)
![Screenshot 66](./Screenshot%20(66).png)
![Screenshot 71](./Screenshot%20(71).png)
