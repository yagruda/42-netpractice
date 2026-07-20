<h1 align="center">Net_Practice — 42cursus</h1>

<p align="center">
  A compact guide to the networking fundamentals used in the <b>net_practice</b> project:
  IPv4 addressing, subnet masks (CIDR), switching, routing, and building correct routing tables.
</p>

<p align="center">
  <a href="#overview">Overview</a> •
  <a href="#key-topics">Key topics</a> •
  <a href="#core-concepts">Core concepts</a> •
  <a href="#level-strategy-1-10">Level strategy (1–10)</a> •
  <a href="#troubleshooting-checklist">Troubleshooting checklist</a>
</p>

<hr/>

## Overview

**Net_Practice** is the first networking-focused project in the **42** curriculum.  
It consists of **10 exercises** where the goal is to configure small network diagrams so devices can communicate correctly using **TCP/IP addressing** and **static routing**.

What you configure throughout the project:
- IPv4 addresses and subnet masks
- router interfaces (multiple networks, no overlaps)
- routing tables (destination + next hop)

---

## Key topics

- IPv4 (binary thinking, ranges, usable hosts)
- Subnet masks & **CIDR** notation
- **Reserved** addresses: network + broadcast
- LAN communication through a **switch**
- Inter-network communication through a **router**
- Static routes and the meaning of a **default route** (`0.0.0.0/0`)
- Return-path logic (packets must be able to come back)

---

## Core concepts

### 1) Network, nodes, packets
A **network** is a set of devices (*nodes*) that can exchange data. Data travels as **packets**.

### 2) TCP vs IP address
- **IP**: addressing + routing (where packets go)
- **TCP**: reliable delivery (splitting, retransmitting, reordering)

### 3) IPv4 format
An IPv4 address is **32 bits**, displayed as four octets:

- `a.b.c.d` with `0 ≤ a,b,c,d ≤ 255`

### 4) Subnet masks (CIDR)
A subnet mask selects the **network prefix**.  
Examples:

- `/24` → `255.255.255.0`
- `/25` → `255.255.255.128`
- `/30` → `255.255.255.252`

**Mask rule:** in binary, masks are continuous `1`s followed by continuous `0`s.

### 5) Reserved addresses inside a subnet
In most subnets:
- first address = **network address** (reserved)
- last address = **broadcast address** (reserved)

Usable hosts are usually: `total - 2`.

### 6) Switch
A **switch** connects multiple devices inside the *same subnet*. It doesn’t route between networks.

### 7) Router
A **router** connects different networks.
- each router interface belongs to a different subnet
- subnets on the same router must **not overlap**

### 8) Routing tables (net_practice model)
Each route contains:
- **Destination**: network as `IP/CIDR` (or default `0.0.0.0/0`)
- **Next hop**: where to forward traffic next (typically a router interface IP)

---

## Level strategy (1–10)

A consistent way to solve every level:

### Level 1 — Basic pairs
Ensure each communicating pair is placed in the same subnet (same prefix + mask).

### Level 2 — Same subnet, tighter constraints
Keep masks consistent and be careful with small subnets (like `/30`).

### Level 3 — Switch with multiple hosts
All hosts connected by the switch must share the same subnet and mask.

### Level 4 — Router with multiple interfaces
Pick masks/IPs so each router interface subnet is distinct (no overlap).

### Level 5 — First static routes
Add routes so hosts can reach remote networks via their router.

### Level 6 — Internet node appears
Use default routes outward, and ensure there is a valid route back toward internal subnets.

### Level 7 — Multiple routers
Identify each link as its own subnet, then build routes so traffic can traverse routers in both directions.

### Level 8 — Constrained address block
Work inside the allowed destination range, subnet it cleanly, assign interfaces, then set default routes on hosts.

### Level 9 — Mixed scenario
Combine all previous rules: subnet design + routing design + return path validation.

### Level 10 — Mostly prefilled
Focus on overlap prevention and consistent routing within the allowed range.

---

## Troubleshooting checklist

When something doesn’t work, verify in this order:

1. **Subnets**: which links are separate networks?
2. **Mask consistency**: same subnet → same mask
3. **Prefix match**: devices that should be local must share the same network address
4. **Reserved addresses**: avoid network/broadcast
5. **Overlap**: router interfaces must not share address ranges
6. **Default routes**: needed when the destination is “outside”
7. **Return route**: replies must also have a valid path back

<hr/>

<p align="center">
  42cursus • Net_Practice • Networking fundamentals (IPv4, subnetting, routing)
</p>
