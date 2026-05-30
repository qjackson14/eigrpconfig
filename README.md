<p align="center">




<h1>Video Demonstration</h1>

- ### [YouTube: Day 25 EIGRP Configuration](https://www.youtube.com/watch?v=PINz_4R3oO4)

<h2>Environments and Technologies Used</h2>

- Jeremy's IT Lab Youtube Channel
- Cisco Packet Tracer
  

  
<h2>Operating Systems Used </h2>

- Cisco IOS


<h2>Step-by-Step</h2>
- 🟢 <b>Step 1: Configure Basic Settings (Prerequisite)</b>


Set hostname:

hostname R1

Configure IP addresses on all interfaces

Enable interfaces:

no shutdown

- 🟢 <b>Step 2: Configure Loopback Interfaces</b>

On Each Router (R1–R4)

Example (R1)

enable

conf t

interface loopback 0

ip address 1.1.1.1 255.255.255.255

Repeat:

R2 → 2.2.2.2 /32

R3 → 3.3.3.3 /32

R4 → 4.4.4.4 /32

🔍 Verify

show ip interface brief

✅ Loopback should be:

up/up

Always active unless manually shut down

- 🟢 <b>Step 3: Configure EIGRP</b>

🔹 On R4 (Quick Method – Lab Shortcut)

router eigrp 100

network 0.0.0.0 255.255.255.255

no auto-summary

passive-interface g0/0

passive-interface loopback0

🔹 On R3 (Precise Method)

router eigrp 100

network 10.0.13.0 0.0.0.3

network 10.0.34.0 0.0.0.3

network 3.3.3.3 0.0.0.0

no auto-summary

passive-interface loopback0

🔹 On R2

router eigrp 100

network 10.0.12.0 0.0.0.3

network 10.0.24.0 0.0.0.3

network 2.2.2.2 0.0.0.0

no auto-summary

passive-interface loopback0

🔹 On R1

router eigrp 100

network 10.0.12.0 0.0.0.3

network 10.0.13.0 0.0.0.3

network 1.1.1.1 0.0.0.0

no auto-summary

passive-interface loopback0

- 🟢 <b>Step 4: Verify EIGRP Configuration</b>

Check protocols

show ip protocols

Check neighbors

show ip eigrp neighbors

Check routing table

show ip route eigrp

Check topology table

show ip eigrp topology

🧠 Key Concepts (Important for CCNA)

📊 EIGRP Metric (Simplified)

Based on:

Bandwidth (slowest link)

Delay (sum of all links)

👉 Think:

Metric ≈ Bandwidth + Delay

📚 EIGRP Terminology

Feasible Distance (FD)

→ This router’s best metric to destination

Reported Distance (RD)

→ Neighbor’s metric to destination

Successor

→ Best route (lowest FD)

Feasible Successor

→ Backup route that meets condition:

RD < Successor FD

- 🟢 <b>Step 5: Configure Unequal-Cost Load Balancing</b>

Default behavior:

Only equal-cost paths used

Enable unequal-cost load balancing

On R1:

router eigrp 100

variance 2

What this does:

Allows routes with higher metric to be used

Condition:

Feasible Successor FD ≤ (Successor FD × Variance)

🧪 Verification After Variance

show ip route

✅ You should now see:

Multiple routes to same destination

Load balancing across unequal paths
