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

## Step 1 — Configure Router Interfaces

Each router interface was configured with IP addresses to enable connectivity between the routers.

Routers configured:

- Router R1
- Router R2
- Router R3

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
