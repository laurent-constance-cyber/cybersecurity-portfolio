# VPN Site-to-Site Tunnel Configuration

> **Project Type:** Network Security Lab  
> **Environment:** Cisco Packet Tracer  
> **Difficulty:** Intermediate Networking

## Project Overview

This project demonstrates the configuration of a secure Site-to-Site VPN tunnel between two routers to allow secure communication between two different internal networks.

The lab involved configuring routing, testing connectivity, and establishing an encrypted tunnel between routers.

---

## Tools Used

- Cisco Packet Tracer
- Router CLI (Cisco IOS)
- ICMP Ping for connectivity testing
- Static routing configuration
- Tunnel interface configuration

---

## Table of Contents

1. [Lab Environment](#lab-environment)
2. [Network Topology](#network-topology)
3. [Host Configuration](#host-configuration)
4. [Router Configuration](#router-configuration)
5. [Default Routing](#step-2--configure-default-routing)
6. [Connectivity Testing](#step-3--connectivity-testing)
7. [VPN Tunnel Configuration](#step-4--vpn-tunnel-configuration)
8. [Tunnel Verification](#step-5--tunnel-verification)
9. [Routing Through the Tunnel](#step-6--routing-through-the-tunnel)
10. [VPN Tunnel Testing](#step-7--vpn-tunnel-testing)
11. [Result](#result)
12. [Skills Demonstrated](#skills-demonstrated)

---

## Lab Environment

Routers used:

- Router R1
- Router R2
- Router R3

Network ranges used in the lab:

| Router | Network |
|------|------|
| R1 | 192.168.1.0 |
| R3 | 192.168.2.0 |

Router R2 acted as the intermediate router between the two networks.

---

## Network Topology

The network topology used in this lab consists of three routers and two internal networks connected through an intermediate router. The VPN tunnel is created between Router R1 and Router R3 to securely connect the two networks.

![VPN Network Topology](vpn-topology.png)

---

## Host Configuration

Before configuring the routers and VPN tunnel, the end devices were configured with appropriate IP addresses so they could communicate with their respective local routers.

### PC0 Configuration

PC0 was configured with the following network settings:

- IP Address: 192.168.1.2
- Default Gateway: 192.168.1.1

![PC0 Configuration](pc0-config.png)

### PC1 Configuration

PC1 was configured with the following network settings:

- IP Address: 192.168.2.2
- Default Gateway: 192.168.2.1

![PC1 Configuration](pc1-config.png)

---

## Step 1 — Configure Router Interfaces

Each router interface was configured with IP addresses to enable connectivity between the routers.

Routers configured:

- Router R1
- Router R2
- Router R3

---

## Router Configuration

After configuring the end hosts, the routers were configured with IP addressing and interfaces to enable communication between networks.

### Router R1 Configuration

Router R1 connects the internal network 192.168.1.0 to the intermediate router.

Key configuration tasks included:

- Accessing router configuration mode
- Configuring the FastEthernet interface
- Assigning IP addresses
- Activating the interface

Example configuration steps:

enable  
configure terminal  
interface fastethernet0/1  
ip address 1.0.0.1 255.0.0.0  
no shutdown  

![Router R1 Configuration](router-r1-configuration.png)

---

### Router R2 Configuration

Router R2 acts as the intermediate router between Router R1 and Router R3. It is responsible for forwarding traffic between the two routers and ensuring proper network connectivity.

Configuration tasks included:

- Assigning IP addresses to router interfaces
- Enabling interfaces
- Allowing routing between connected networks

Example configuration steps:

enable  
configure terminal  
interface fastethernet0/0  
ip address 1.0.0.2 255.0.0.0  
no shutdown  

interface fastethernet0/1  
ip address 2.0.0.1 255.0.0.0  
no shutdown  

![Router R2 Configuration](router-r2-configuration.png)

---

### Router R3 Configuration

Router R3 connects the second internal network (192.168.2.0) to the intermediate router R2.

Configuration tasks included:

- Assigning IP addresses to interfaces
- Enabling router interfaces
- Preparing the router for VPN tunnel configuration

Example configuration commands:

enable  
configure terminal  
interface fastethernet0/1  
ip address 2.0.0.2 255.0.0.0  
no shutdown  

interface fastethernet0/0  
ip address 192.168.2.1 255.255.255.0  
no shutdown  

![Router R3 Configuration](router-r3-configuration.png)

---

## Step 2 — Configure Static Routing

After configuring the router interfaces, static routes were added to allow communication between the two internal networks.

Static routes were configured on Router R1 and Router R3 so that traffic destined for the remote network could be forwarded through the intermediate router.

### Static Route on Router R1

Router R1 was configured with a route directing traffic for the 192.168.2.0 network toward the intermediate router.

Example command used:

ip route 192.168.2.0 255.255.255.0 172.16.1.2

![Static Route on Router R1](default-route-router1.png)

---

### Static Route on Router R3

Router R3 was configured with a route directing traffic for the 192.168.1.0 network back toward Router R1 through the intermediate router.

Example command used:

ip route 192.168.1.0 255.255.255.0 172.16.1.0

![Static Route on Router R3](default-route-router3.png)

---

## Step 3 — Connectivity Testing

Connectivity between routers was tested using ping commands.

Tests performed included:

- Router3 pinging Router2
- Router2 pinging Router3
- Router3 pinging external addresses

These tests confirmed that the routing configuration was working.

---

### Router3 Ping Test

Router3 was used to test connectivity by sending ICMP ping requests to another network address.  
The successful replies confirmed that routing between the routers was working correctly.

![Router3 Ping Test](router3-ping-test.png)

---

### Router2 to Router3 Communication

Connectivity between Router2 and Router3 was verified using ICMP ping commands.

Successful responses confirmed that traffic could travel between the routers through the configured routing paths.

![Router2 to Router3 Test](router2-router3-test-1.png)

![Router2 to Router3 Test](router2-router3-test-2.png)

---

### Additional Connectivity Verification

Additional packet tests were performed in the Packet Tracer simulation environment to confirm successful routing across the network.

![Connectivity Test](connectivity-test-1.png)

![Connectivity Test](connectivity-test-2.png)

## Step 4 — VPN Tunnel Configuration

After verifying that basic connectivity and routing were functioning correctly, a VPN tunnel was created between Router R1 and Router R3 to securely connect the two remote networks.

The tunnel was configured on both routers using tunnel interfaces and appropriate IP addressing.

### VPN Tunnel Configuration on Router R1

Router R1 was configured with a tunnel interface that points to Router R3 as the tunnel destination.

![VPN Tunnel Configuration on Router R1](vpn-tunnel-on-router-R1.png)

---

### VPN Tunnel Configuration on Router R3

Router R3 was configured with a corresponding tunnel interface that points back to Router R1.

![VPN Tunnel Configuration on Router R3](vpn-tunnel-on-router-R3.png)

---

## Step 5 — Tunnel Verification

After configuring the VPN tunnel, connectivity tests were performed to verify that the tunnel was successfully established.

### Initial Test (Before Tunnel Fully Established)

An initial connectivity test from Router R1 to Router R3 resulted in packet loss, indicating that the tunnel was not yet fully operational.

![Initial Ping Failure](Router-r1-and-ping-with-router-r3-error.png)

---

### Successful Tunnel Communication

After completing the configuration, the routers were able to communicate successfully through the VPN tunnel.

![Successful Ping Test](Router-r1-and-ping-with-router-r3-sucessful.png)

---

### Router R3 Connectivity Test

Router R3 successfully communicated with Router R1 across the VPN tunnel, confirming that the encrypted connection was functioning correctly.

![Router R3 Ping Test](Router-r3-and-test-network-by-pinging-router-r1-interface-succesful1.png)

![Router R3 Ping Test](Router-r3-and-test-network-by-pinging-router-r1-interface-succesful2.png)

---

## Step 6 — Routing Through the Tunnel

Additional static routes were configured on both routers to ensure that traffic between the two internal networks travels through the VPN tunnel.

### Static Route on Router R1

Example configuration command:

R1(config)# ip route 192.168.2.0 255.255.255.0 172.16.1.2

![Routing Configuration on Router R1](R1config.png)

---

### Static Route on Router R3

Example configuration command:

R3(config)# ip route 192.168.1.0 255.255.255.0 172.16.1.0

![Routing Configuration on Router R3](R3config.png)

---

## Step 7 — VPN Tunnel Testing

Further tests were performed to confirm that the VPN tunnel was functioning correctly.

### Router R1 Tunnel Verification

Router R1 was used to verify that the VPN tunnel interface was successfully created and operational.

![Router R1 Tunnel Test](RouterR1-and-test-VPN-Tunnel-Creation.png)

---

### Router R3 Tunnel Verification

Router R3 also confirmed successful tunnel creation and communication.

![Router R3 Tunnel Test](RouterR3-and-test-VPN-Tunnel-Creation.png)

---

### Packet Flow Through Tunnel

Simulation mode in Packet Tracer was used to trace the packet flow through the VPN tunnel and verify that traffic was being routed correctly.

![Tunnel Packet Trace](trace-vpn-tunnel.png)

---

## Result

The VPN tunnel was successfully established between Router R1 and Router R3, allowing secure communication between the two networks.

---

## Key Learning Outcomes

This lab demonstrated how VPN tunnels can securely connect remote networks across an intermediate routing infrastructure.

The project also reinforced the importance of:

- proper routing configuration
- verifying connectivity before implementing security mechanisms
- validating tunnel functionality after deployment

---

## Skills Demonstrated

- Cisco router configuration using CLI
- Static routing configuration
- Site-to-Site VPN tunnel implementation
- Network troubleshooting and connectivity testing
- Packet flow verification using Packet Tracer simulation
- Secure network communication between remote networks


