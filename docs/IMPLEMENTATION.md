# 🛠️ Implementation

This project implements a virtualized enterprise network using Ubuntu Server, VirtualBox, and Cisco Packet Tracer.

## Infrastructure

The environment consists of:

- 5 Routers
- 3 HTTP Servers
- 2 DNS Servers
- 3 Client Machines

All virtual machines were connected through VirtualBox Internal Networks to simulate an enterprise infrastructure.

## Network Services

The following services were implemented:

- Dynamic routing with FRRouting (RIPv2)
- DNS using BIND9
- HTTP using Apache2
- Static IP addressing with Netplan

## Validation

The implementation was validated using connectivity and service tests, including:

- Ping
- nslookup
- curl
- RIP routing verification
