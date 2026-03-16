# VPN Site-to-Site Tunnel Configuration

## Project Overview

This project demonstrates the configuration of a secure Site-to-Site VPN tunnel between two routers to allow secure communication between two different internal networks.

The lab involved configuring routing, testing connectivity, and establishing an encrypted tunnel between routers.

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

## Step 2 — Configure Default Routing

Routing entries were added to allow traffic to reach remote networks.

Example configuration:

ip route 192.168.2.0 255.255.255.0 172.16.1.2

This route directs traffic destined for the 192.168.2.0 network through the gateway.

---

## Step 3 — Connectivity Testing

Connectivity between routers was tested using ping commands.

Tests performed included:

- Router3 pinging Router2
- Router2 pinging Router3
- Router3 pinging external addresses

These tests confirmed that the routing configuration was working.

---

## Step 4 — VPN Tunnel Configuration

A VPN tunnel was configured between:

- Router R1
- Router R3

Both routers were configured with the required parameters to establish encrypted communication.

---

## Step 5 — Tunnel Verification

Connectivity tests were performed again after the VPN tunnel configuration.

Ping tests confirmed successful communication between Router R1 and Router R3.

---

## Step 6 — Routing Through the Tunnel

Additional routes were configured to ensure traffic flows through the VPN tunnel.

Example configuration:

R1(config)# ip route 192.168.2.0 255.255.255.0 172.16.1.2

R3(config)# ip route 192.168.1.0 255.255.255.0 172.16.1.0

---

## Result

The VPN tunnel was successfully established between Router R1 and Router R3, allowing secure communication between the two networks.

---

## Skills Demonstrated

- Network routing
- Router configuration
- VPN implementation
- Network troubleshooting
- Secure network communication
