
# Wireshark Network Traffic Analysis Lab

## Overview

In this lab, I used Wireshark to capture and analyze network traffic. I practiced identifying DNS queries and responses, examining a TCP three-way handshake, inspecting unencrypted HTTP traffic, and following a TCP stream to view a conversation between a client and server.

This project documents my hands-on practice with network troubleshooting and packet analysis as I build my skills for IT support roles.

## Video Walkthrough

I recorded a walkthrough demonstrating the lab exercises.

[Watch my Wireshark lab walkthrough on YouTube](https://www.youtube.com/watch?v=iVjSRkhIkow)

## Tools Used

- Wireshark
- Command Prompt / terminal
- `nslookup`
- Web browser
- HTTP test login form with test credentials

## Lab Objectives

- Capture traffic on an active network interface.
- Use display filters to isolate relevant packets.
- Identify DNS queries and their corresponding responses.
- Recognize the TCP three-way handshake.
- Demonstrate how unencrypted HTTP can expose submitted credentials.
- Reassemble a conversation using Follow TCP Stream.
- Save and export packet captures for later analysis.

## Lab Steps

### 1. Capture Network Traffic

I opened Wireshark, selected the active network interface, and started a capture. I generated traffic by browsing a website, then stopped the capture to examine the packets.

I used the packet list and packet details pane to inspect protocols, source and destination addresses, and packet information.

### 2. Apply Display Filters

I used display filters to narrow the packet list without removing packets from the underlying capture.

| Filter | Purpose |
| --- | --- |
| `dns` | Show DNS queries and responses |
| `tcp` | Show TCP traffic |
| `http` | Show traffic Wireshark identifies as HTTP |
| `tcp && ip.addr == <server-ip>` | Isolate TCP traffic involving a selected IPv4 address |
| `http.request.method == "POST"` | Locate HTTP POST requests |

Replace `<server-ip>` with the actual server IPv4 address before applying the filter.

### 3. Capture a DNS Lookup

With a capture running, I used the following command in a separate terminal:

```text
nslookup google.com
```

I stopped the capture and applied the `dns` filter. I examined the query for `google.com` and the corresponding response, including the returned A record information. I compared the returned IPv4 addresses with the terminal output.

This exercise showed how DNS translates a domain name into an IP address that a client can use to connect to a service.

### 4. Examine the TCP Three-Way Handshake

I captured traffic while opening `http://example.com` and used `nslookup example.com` to identify a server address. I filtered the TCP traffic involving that address and located the handshake packets within the same connection.

| Packet | Meaning |
| --- | --- |
| SYN | The client requests a connection |
| SYN, ACK | The server acknowledges the request and sends its own SYN |
| ACK | The client acknowledges the server's SYN, completing the handshake |

This exercise helped me understand how TCP establishes a connection before application data is exchanged.

### 5. Inspect Cleartext HTTP Credentials

I captured a test login submitted over HTTP using test credentials. After stopping the capture, I applied:

```text
http.request.method == "POST"
```

I inspected the POST request and its form data to see how a username and password can appear in plaintext when transmitted without encryption.

This exercise demonstrated why login forms need HTTPS to protect data in transit. The exercise used a test environment and test credentials.

### 6. Follow a TCP Stream

I selected an HTTP packet and opened **Follow → TCP Stream**. Wireshark reassembled the connection's captured data so I could read the HTTP request and response together.

This made it easier to understand the conversation than examining individual packet fragments alone.

### 7. Save and Export Captures

I practiced saving captures in `.pcapng` format for later analysis. The lab also covered exporting displayed packets after applying a filter and reopening saved captures in Wireshark.

## Skills Practiced

- Live packet capture and protocol identification
- DNS analysis and name-resolution troubleshooting
- TCP connection analysis
- Filtering traffic by protocol and IP address
- Inspecting HTTP requests and form data
- TCP stream reconstruction
- Saving packet captures for review

## What I Learned

Wireshark helps connect network concepts to observable traffic. DNS packets show how a name is resolved, handshake packets show how a TCP connection starts, and HTTP streams show the data exchanged by a client and server.

These skills provide a foundation for investigating website access problems, DNS failures, and connection issues in IT support. This lab also reinforced the importance of encryption when transmitting sensitive information.
