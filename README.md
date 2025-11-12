TCPDump
============

`tcpdump` is a command-line tool used to capture and analyse network traffic
going through your system.

Example commands include:
 - `tcpdump -i <interface>`     - Captures packets on <interface>
 - `tcpdump -w <file>`          - Write captured packets to <file>
 - `tcpdump -r <file>`          - Read captured packets from <file>
 - `tcpdump -c <count>`         - Capture <count> packets
 - `tcpdump -n`                 - Don't resolve IP addresses
 - `tcpdump -nn`                - Don't resolve IP addresses and protocol numbers
 - `tcpdump -v`                 - Verbose display


# Filtering Expressions
The `man pcap-filter` page has a list of filtering expressions you can use with `tcpdump`.

## Filtering by Host
`tcpdump host <hostname>` will capture all packets with <hostname>. e.g. `tcpdump host example.com` will capture packets exchanged with `example.com`
You can further limit to packets sent from a source, or to a particular destination with `src host <hostname>` and `dst host <hostname>`.
Note the hostname can be the `IP` or `hostname`.

## Filtering by Port
`tcpdump -i <interface> (<src/dst>) port <portnum>`

## Filtering by Protocol
`tcpdump -i <interface> <protocol>`. This includes protocols like `ip`, `ip6`, `udp`, `tcp`, and `icmp`.

## Logical Operators
 - `and`        - `tcpdump host 1.1.1.1 and tcp`
 - `or`         - `tcpdump udp or icmp`
 - `not`        - `tcpdump not tcp`

##



Wireshark
===============

Wireshark is a packet analyser tool capable of sniffing and investigating live traffic and inspecting Packet CAPtures(PCAP).

*Note:* Wireshark is not an IDS and cannot modify packets

# Tool Overview
## PCAP Files
Packet details are shown in three panes.
- Packet List Pane - Summary of each packet (source & destination address, protocol, and packet info
- Packet Details Panel - Detailed protocol breakdown of the selected packet
- Packet Bytes Pane - Hex and decoded ASCII representation of the selected packet. Will highlight selected section from details pane

## Colouring Packets
*Colouring rules are managed in "View -> Colouring Rules"

## Traffic Sniffing
Started via the blue shark fin, stopped with red, and restarted with green.

## Merge PCAP Files
You can merge two pcap files with "File -> Merge".

## View File Details
You can view details (e.g. file hash, capture time, capture file comments, interface, and statistics) via "Statistics -> Capture File Properties", or using the pen and paper in the bottom left.


# Packet Dissection
Packet dissection, or protocol dissectino, investigates packet details by decoding available protocols and fields. You can use many different protocols, and can also write your own dissection scripts.

## Packet Details
Packets consist of 5 to 7 layers based on the OSI model.
- The Frame (Layer 1 - Physical Layer) - Shows what frame/packet you are looking at, and details specific to the Physical Layer
- Source [MAC] (Layer 2 - Data Link Layer) - Shows the source and destination MAC Addresses
- Source [IP] (Layer 3 - Network Layer) - Shows the source and destination IP Addresses
- Protocol (Layer 4 - Transport Layer) - Shows the details of the protocol used (TCP/UDP) and source and destination ports
- Application Protocol (Layer 5 - Session Layer) - Shows details specific to
the protocol used, such as HTTP, FTP, and SMB


# Packet Navigation
## Go To Packet
<Ctrl+G> or "Go" in the toolbar can be used to jump to a given packet.

## Find Packets
"Edit -> Find Packets" can be used dto make a search inside the packets for particular events of interest.
Searches are case insensitive by default, but can be toggled on.
You can search through the packet list, packet details, or packet bytes for hex values, strings, regex, or display filters.

## Mark Packets
<Ctrl+M> or "Edit -> Mark selected" can be used to mark packets, and will be
displayed in black.
Marked packets will be lost after closing the capture file!

## Packet Comments
<Ctrl+Alt+C> can be used to comment on particular packets, and will persist until removed.

## Export Packets
You can export packets via the "File" menu to help share only suspicious packages (decided scope), thus removing redundant information.

## Export Objects (Files)
You can export files transferred through the wire via the "File -> Export Objects" menu.

## Time Display Format
By default Wireshark displays Time as "Seconds Since Beginning of Capture". You can change this via "View -> Time Display Format"

## Expert Information
Expert info can provide groups of categories in different severities, helping to spot possible anomalies and problems.
Found via cirlce in the bottom left, or "Analyse -> Expert Information"


# Packet Filtering
Wireshark has two filtering approaches:
- Capture filters - "captures" only a specific part of the traffic based on the filter. This is not changeable during the capture.
        - The typical workflow is to capture everything, then filter afterwards so you don't accidentally filter out information you want
- Display filters - only "views" certain packets that fit the filter. It is changeable during the capture
        - You can find a filter reference at https://www.wireshark.org/docs/dfref/, a simpler one at "Analyse -> Display Filters", or a               comprehensive list at "Analyse -> Display Filter Expression".

## Apply as Filter
To filter for a selected field, select it and use "Analyse -> Apply as Filter" or "<Rclick> -> Apply as Filter"

## Conversation Filter
Conversation filters allow you to view only linked packets by focusing on IP
addresses and port numbers.

## Colourise Conversation
This is similar to conversation filters, except it highlights the linked packets without applying a display filter.

## Prepare as Filter
This will create a filter and paste it in the pane, but waits for the execution command.

## Apply as Column
This can be used to add columns to the packet list pane.

## Follow Stream
Wireshark displays everything in packets, but it's possible to reconstruct the streams and view the raw traffic as it's presented at the application level.
To do so, use "Analse -> Follow TCP/UDP/HTTP Stream". Packets originating rom the server are in blue, and packets from the client are red.

# Statistics
All of these are subsections of the "Statistics" menu.
The sections in here each display information related to specific information fields, such as converstions between endpoints, a list of all IPv4 & IPv6 addresses, all HTTP packets, and more.


# TRAFFIC ANALYSIS
## Nmap Scans
You can spot scan activity on a network by looking at network traffic and spotting patterns associated with typical network scans.

