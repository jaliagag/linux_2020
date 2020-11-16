# Networking CCENT

<https://dxc.skillport.com/skillportfe/main.action?path=browsecatalog/en-us/_fcpaths_L1NraWxsU29mdFNQOC9JVFNraWxsczEvT3Blcm5nU3lzcnZlcnMvTGludXgx_fcpathe_#browse/0ff16745-fc92-4c6d-8413-1b403d6bebd8>

Exam 100-105 ICND1

## The OSI Model

There werer propietary network communication models.

|layer | name | function | protocols | devices |
| ----- |----- |-------- |--------- |---------|
| L7 | Application | program that creates and opens the data received | http, https, smtp (mail)| user applications|
| L6 | Presentation | Formatting and encryption| .jpgs, ascii, .gifs, .tiffs |         |
| L5 | Session | Synchronization, Logical Ports | NFS, RPC, SQL, NetBIOS | logical ports |
| L4 | Transport | Segmentation | TCP, UDP, SPX | firewalls, network hosts devices |
| L3 | Network | Addressing - has information about the final destination |	IP, IPX, ARP, ICMP | rotuers||
| L2 | Data Link| Where data gets chained into - forwarding to the next device | Ethernet, Frame Relay, PPP, HDLC | NIC, L2 switches|
| L1 | Physical | Media Pathways - copper, radio...| | Cabling, connectors, lights, hubs|

- L5-7 --> Prepares data for **destination to understand** - it happens on a single computer. Usually application blok
- L1-4 --> Prepares the data for **network delivery** to the destination.

AllPeopleSeemtoNeedDataProcessor. PleaseDoNotThroughSausagePizzaAway

- L1 - physical



- L2 - data link
	- PPP: point to point protocol
	- HDLC

- L3



- L4 - transport

Data is broken down into smaller units of data that can be transported. Sequencing information so that information is rebuilt in order

- L5 - session

The information that the destination computer has for the receiving computer.

- L6



- L7 - application

Layer that the user interacts with. Using a browser. 
