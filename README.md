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


Let's use Network: 172.16.0.0 Subet Mask: 255.255.252.0

Determine the number of Hosts IP addresses available per subnet
1. Convert the subnet mask to binary code
2. Count the 0s in the subnet mask
3. Using a calculator 2<sup>Number of 0s</sup>, then -2 = _____

   Example:
   1. 255.255.252.0 converted to binary is 11111111/11111111/11111100/00000000
   2. There are 10 zeros in the subnet mask
   3. On the calculator, 2<sup>10</sup> - 2  = 1022 IP address per subnet

Determine the number of Networks available
1. Convert the subnet mask to binary code.
2. Exclude the default subnet mask bits.
3. Count the remaining 1s in the subnet mask.
4. Use a calculator 2<sup>number of 1s remaining</sup> = _____
   Example:
   1. 255.255.252.0 converted to binary is 11111111/111111111/11111100/00000000
   2. There are 16 ones in the default subnet mask because addresses beginning with 172 are class B IP addresses, exclude those 11111111/11111111/`111111`00/00000000
   3. Count the remaing ones.
   4. 2<sup>6</sup> = 64 subnets

Class A example

IP: 10.0.0.0
Subnet: 255.255.248.0

Host IP calculation:
1. 11111111/11111111/11111000/00000000
2. 11 0s in the subnet mask
3. 2<sup>11</sup> = 2046 Host IP address per subnet

Number of Network available:
1. As it's a Class A
2. 111111111/`111111111`/`11111`000/000000000
3. 13 1s in the subnet mask.
4. 2<sup>13</sup> = 8192 subnets

Class B Example

IP Address: 172.16.244.0
Subnet Mask: 255.255.224.0

| Network ID | First IP address | Last IP address | Broadcast Address |
| ---------- |  ---------- |  ---------- | ---------- |
| 172.16.0.0 | 172.16.0.1 | 172.16.31.254 |  172.16.31.255 |
| 172.16.32.0 | 172.16.32.1 |172.16.63.254 |  172.16.63.255 |
| 172.16.64.0 | 172.16.64.1 | 172.16.95.254 |  172.16.95.255 |
| 172.16.96.0 | 172.16.96.1 |172.16.127.254 |  172.16.127.255 |
| 172.16.128.0 | 172.16.128.1 |172.16.191.254 |  172.16.191.255 |
| 172.16.192.0 | 172.16.192.1 |172.16.243.254 |  172.16.243.255 |
| 172.16.244.0 | 172.16.244.1 |172.16.255.254 |  172.16.255.255 |

### Public and private addresses

| Public | Private |
| ------ | ------- |
| Required by devices and hosts that connect directly to the intenet | Not routable on the internet eg 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16|
| Must be globally unique | Can be assigned locally by an organization |
| Routable on the Internet | must be translated to access the internet |
| Must be assigned by IANA | |

### Network address transaltion (NAT)

With NAT, my internet service provide will assign me a public IP address, let say 27.1.54.42. Now, i have no control over that, as it is assigned by whoever my ISP is and that IP address is actually on the internet side, sometimes called a wan wide area network, modem etc. They connect to your internal network to the public network.
Also it contains private IP 192.168.1.1. 
