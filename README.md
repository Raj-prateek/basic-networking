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
ARP -a # to get the list of all the IP's and MAC
ARP -d * # to delete all the IP's and MAC
```

