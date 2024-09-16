# basic-networking
IPv4, Subnetting, DNS, DHCP, IPv6, Routing and Switching

## Understanding, Implementing, and Troubleshooting IPv4

- Planning IPv4 addressing
- Configuring an IPv4 host.
- Managing and troubleshooting IPv4 network connectivity.

### Planning IPv4 addressing

#### What is an IPv4 address?

An IP version four address is always four sets of numbers separated by a decimal, for example:
- 192.168.1.1
- 10.45.58.97
- 20.8.49.251
- 172.16.89.189

An IP address, or Internet Protocol address, is a series of numbers that identifies any device on a network.
Computers use IP addresses to communicate with each other both over the internet as well as on other network.


Let's take an example: We have 
- PC1
  - IP Address: 192.168.1.47
  - Default Gateway: 192.168.1.1
- PC2
  - IP Address: 192.168.1.209
  - Default Gateway: 192.168.1.1
- Phone
  - IP Address: 192.168.1.135
  - Default Gateway: 192.168.1.1
- Printer
  - IP Address: 192.168.1.20
  - Default Gateway: 192.168.1.1
- Server
  - IP Address: 192.168.1.17
  - Default Gateway: 192.168.1.1

Notice, all of these have IP addresses directly assigned. So if we want to communicate between PC1 and PC2, we will communicate using these IP addresses.

But what connects the devices each other?? It's a SWITCH!!!
A switch will connect any network devices (such as computers, printer, wireless access point) in a network to each other, and allow to `talk` by exchanging data frames.

So if i am on PC1 and i want to access something on PC2 so i will first travel to switch it will route to PC2 to exchange the data.

There are many types of switches:
1. With 4 ports.
2. With 96 ports.
3. or 100 ports.
That may cost tens of thousands of dollars depends on the needs and it can be very configurable.

It's an hardware?? So how mobile/wireless device works??
Those device connects to an access point. Your access point is going to connect directly to the switch. So you are still passing data through the switch, even though you yourself are wireless, you are just connecting to it via an access point.

What is a router?
A network router connects devices on one network to devices on other networks(internet) by exchanging packets. Default gateways is always the IP address of a router. Sometimes it's called a router, business gateway or a cable modem.

So what happens is anytime I need to connect to a device that's on a different network, that data gets passed through the switch and up to the router and then it's routes on to the internet.

So for now, to think of a switch as connecting different devices on the same network to each other and a router connecting different networks to each other.

#### What is a MAC (Media Access Control) Address?
- A MAC address is a 12 character hexadecimal address
- It's assigned to the Network Interface Adapater (NIC).
- This can be wired or wireless.
- Also referred to as `physical address`
Example: FC-F8-AE-53-6D-8F.

How to get MAC address?
```
ifconfig -v
```

#### How MAC Address and IP address are related to each other?

Understanding ARP (address resolution protocol)

For devices on the same IP network:
ARP sends a broadcast directed to the IP address of the destination device. The destination device responds with it's MAC address

```
ARP -a # to get the list of all the IP's and MAC in ARP cache
ARP -d * # to delete all the IP's and MAC
```

#### OSI Model
- Layer 7: Application Layer
  - Network process to application
  - DNS,WWW/HTTP, P2P, EMAIL/POP, SMTP, Telnet, FTP
- Layer 6: Presentation Layer
  - Data representation and encryption
  - Recognizing data, HTML, DOC JPEG, MP3, AVI, Sockets.
- Layer 5: Session Layer
  - Interhost communication
  - Session establishment in TCP, SIP, RTP, RPC-Named pipes
- Layer 4: Transport
  - End to end connections and reliability
  - TCP, UDP, SCTP, SSL and TLS
- Layer 3: Network (Routers)
  - Path determination and logical addressing
  - IP, ARP, IPsec, ICMP, IGMP, OSPF
- Layer 2: Data Link (Switches)
  - Physical addressing
  - Ethernet, 802.11, MAC/LLC, VLAN, ATM, HDP, Fibre Channel, Frame Relay, HDLC, PPP, Q.921, Token Ring
- Layer 1: Physical 
  - Media, Signal, and binary transmission
  - RS-232, Rj45, V.24, 100BASE-1X, SDH, DSL, 802.11


#### Understanding Binary Code

Dotted decimal notations are based on the decimal number system, but computers use IP addresses in binary
- Within an 8-bit octet, each bit position has a decimal value:
  - A bit that is set to 0 always has a zero value
  - A bit that is set to 1 can be converted to a decimal value
  - The low-order bit represents a decimal value of 1
  - The high-order bit represents a decimal value of 128
- If all bits in an octet are set to 1, then the octets decimal value is 255, the highest possible value of an octet:
  128 + 64 + 32 + 16 + 8 + 4 + 2 + 1


#### Overview of IPv4 settings:

| 1 |  1 |  1 |  1 |  1 |  1 |  1 |  1 |   8 Bit Octet |  
|------|-------|-------|-------|-------|-------|-------|-------|-------|
| Bit 7 |  Bit 6 |  Bit 5 |  Bit 4 |  Bit 3 |  Bit 2 |  Bit 1 |  Bit 0 | |  
| 2<sup>7</sup> |  2<sup>6</sup> |  2<sup>5</sup> |  2<sup>4</sup> |  2<sup>3</sup> |  2<sup>2</sup> |  2<sup>1</sup> |  2<sup>0</sup> | Exponent |
| 128 |  64 |  32 |  16 |  8 |  4 |  2 |  1 | Decimal Value |

8 bits = 1 byte



- Each networked computer must be assigned a unique IPv4 address.
- Network communication for a computer is directed to the IPv4 address of the computer
- Each IPv4 address contains:
  - Network ID, identifying the network
  - Host ID, identifying the computer
- The subnet mask identifies which part of the IPv4 address is the network ID (255) and which is the host ID (0)

| IP Address | 172 | 16 | 0 | 10 |
| ----- |  ----- |  ----- |  ----- |  ----- |
| Subnet mask | 255 | 255 | 0 | 0 |
| Network ID | **172** | **16** | 0 | 0 |
| Host ID | 0 | 0 | **0** | **10** |


##### Classful IP addressing

**Class A**
- Starting with 1 - 126
- Subnet mask 255.0.0.0/8
- 10.1.5.89 here 10 is the net id and 1,5, and 89 is the host id
- 16777214 total IPs - 2<sup>24</sup> - 2

**Class B**
- Starting with 128-191
- Subnet mask 255.255.0.0/16
- 65,534 total IP's - 2<sup>16</sup> - 2

**Class C**
- Starting with 191-223
- Subnet mask 255.255.255.0/24
- 254 IP's - 2<sup>8</sup> - 2

> /8,/16/24 is called as CIDR

Number of IP's in the class = 2<sup>#0's in mask</sup> - 2

**Why we subtract it from 2 ??**
It's bcoz we have to IP's allready booked for net ID and Broadcast from mask.
For example: 
IP 10.0.0.0
NET ID: 10.0.0.0
Firt IP: 10.0.0.1
Last IP: 10.255.255.254
Broadcast: 10.255.255.255


#### Subnet Mask

| Binary | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 |
| ------ | ------ |  ------ |  ------ | ------ | ------ | ------ | ------ |  ------ |
| Decimal | 128 | 64 | 32| 16 | 8 | 4 | 2 | 1 |
| Subnet Mask | 128 | 192 | 224 | 240 | 248 | 252 | 254 | 255|

