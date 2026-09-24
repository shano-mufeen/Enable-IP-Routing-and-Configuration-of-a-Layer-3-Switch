# 🌐 Layer 3 Switch – Basic Routing Configuration | Cisco Packet Tracer

## 📌 Project Overview

This lab demonstrates the basic configuration of a **Cisco Layer 3 switch** using Cisco Packet Tracer.

A Layer 3 switch combines the functionality of a traditional Layer 2 switch with **Layer 3 routing capabilities**. By default, the switch operates primarily as a Layer 2 device, so **IP routing must be enabled** before it can perform routing functions.

In this lab, two Cisco Layer 3 switches are connected to a router. The switches are configured with Layer 3 interfaces, IP routing is enabled, and connectivity is verified using ICMP ping tests.

---

## 🎯 Objectives

The main objectives of this lab are to:

* Understand the purpose of a Layer 3 switch
* Configure a Cisco 3650 Layer 3 switch
* Power on a modular Layer 3 switch in Packet Tracer
* Connect the network devices
* Enable IP routing on Layer 3 switches
* Convert Layer 2 switch ports into Layer 3 routed interfaces
* Assign IPv4 addresses to Layer 3 interfaces
* Configure IP addresses on router interfaces
* Verify connectivity between switches and the router
* Understand the difference between Layer 2 switch ports and Layer 3 routed ports

---

## 🗺️ Network Topology

The topology consists of:

* 2 × Cisco 3650 Layer 3 Switches
* 1 × Cisco Router
* Ethernet/Gigabit connections between the devices

### Logical Topology

```text
        Layer 3 Switch 1
        192.168.1.2/30
               |
               |
        192.168.1.1/30
             Router
        192.168.2.1/30
               |
               |
        192.168.2.2/30
        Layer 3 Switch 2
```

---

## 🧰 Devices Used

| Device         | Model               | Role                 |
| -------------- | ------------------- | -------------------- |
| Layer 3 Switch | Cisco 3650          | Routing + Switching  |
| Layer 3 Switch | Cisco 3650          | Routing + Switching  |
| Router         | Cisco Router        | Layer 3 Connectivity |
| Simulator      | Cisco Packet Tracer | Network Simulation   |

---

## 📝 IP Addressing Scheme

| Device      | Interface | IP Address    | Subnet Mask       |
| ----------- | --------- | ------------- | ----------------- |
| L3 Switch 1 | Gi1/0/1   | `192.168.1.2` | `255.255.255.252` |
| Router      | Gi0/0     | `192.168.1.1` | `255.255.255.252` |
| Router      | Gi0/1     | `192.168.2.1` | `255.255.255.252` |
| L3 Switch 2 | Gi1/0/1   | `192.168.2.2` | `255.255.255.252` |

> The exact interface numbering may vary depending on the Packet Tracer device model.

---

# 🔧 Configuration Steps

## 1. Select the Layer 3 Switch

For this lab, the **Cisco 3650** Layer 3 switch is used.

In Cisco Packet Tracer:

```text
Network Devices
   ↓
Switches
   ↓
Cisco 3650
```

The 3650 supports both Layer 2 switching and Layer 3 routing functionality.

---

## 2. Power On the Layer 3 Switch

Some modular switches in Packet Tracer require a power supply to be installed manually.

Open the **Physical** tab of the switch and install the AC power supply.

Repeat the process for the second Layer 3 switch.

```text
Physical Tab
      ↓
Install AC Power Supply
      ↓
Power On
```

> Depending on the Packet Tracer version and device model, the power-on behavior may differ.

---

# 3. Connect the Devices

Connect the Layer 3 switches to the router using the appropriate Ethernet/Gigabit interfaces.

Example:

```text
L3 Switch 1 Gi1/0/1
        |
        |
     Router Gi0/0

     Router Gi0/1
        |
        |
L3 Switch 2 Gi1/0/1
```

---

# 4. Enable IP Routing

By default, the Layer 3 switch can operate as a Layer 2 switch.

To enable Layer 3 routing capabilities:

### Layer 3 Switch 1

```cisco
Switch1(config)# ip routing
```

### Layer 3 Switch 2

```cisco
Switch2(config)# ip routing
```

### Why is this important?

The command:

```cisco
ip routing
```

enables the switch to perform **Layer 3 routing**.

Without IP routing enabled, the switch cannot function as a router between Layer 3 networks.

---

# 5. Convert the Switch Port to a Layer 3 Interface

By default, physical switch ports operate as Layer 2 switchports.

To use a physical port as a routed Layer 3 interface, remove its switchport functionality.

### Switch 1

```cisco
Switch1(config)# interface gigabitEthernet 1/0/1
Switch1(config-if)# no switchport
```

The command:

```cisco
no switchport
```

converts the interface from a Layer 2 switchport into a **Layer 3 routed interface**.

---

# 6. Assign an IP Address to the Layer 3 Interface

After converting the interface into a Layer 3 interface, an IPv4 address can be assigned.

```cisco
Switch1(config-if)# ip address 192.168.1.2 255.255.255.252
Switch1(config-if)# no shutdown
```

---

## 7. Configure the Second Layer 3 Switch

On the second switch:

```cisco
Switch2(config)# interface gigabitEthernet 1/0/1
Switch2(config-if)# no switchport
Switch2(config-if)# ip address 192.168.2.2 255.255.255.252
Switch2(config-if)# no shutdown
```

---

# 8. Configure the Router Interfaces

The router provides Layer 3 connectivity between the two networks.

### Router Interface Gi0/0

```cisco
Router(config)# interface gigabitEthernet 0/0
Router(config-if)# ip address 192.168.1.1 255.255.255.252
Router(config-if)# no shutdown
```

### Router Interface Gi0/1

```cisco
Router(config)# interface gigabitEthernet 0/1
Router(config-if)# ip address 192.168.2.1 255.255.255.252
Router(config-if)# no shutdown
```

---

# 🧪 9. Test Connectivity

After configuring the interfaces, connectivity can be tested using ICMP.

### From Layer 3 Switch 1

```cisco
Switch1# ping 192.168.1.1
```

Expected result:

```text
Success rate is 100 percent
```

### From Layer 3 Switch 2

```cisco
Switch2# ping 192.168.2.1
```

Expected result:

```text
Success rate is 100 percent
```

Successful ping responses confirm that the Layer 3 interfaces and directly connected networks are operational.

---

# 🔍 Verification Commands

### Check Interface Status

```cisco
show ip interface brief
```

This command can be used to verify:

* Interface status
* IP addresses
* Administrative state
* Protocol status

---

### Verify IP Routing

```cisco
show ip route
```

This displays the routing table of the Layer 3 switch.

---

### Verify Interface Configuration

```cisco
show running-config
```

This can be used to review the current configuration.

---

### Test Connectivity

```cisco
ping <destination-ip>
```

Example:

```cisco
ping 192.168.1.1
```

---

# 🧠 Key Concepts Learned

### Layer 3 Switch

A Layer 3 switch provides both:

```text
Layer 2 Switching
        +
Layer 3 Routing
```

This allows the device to switch traffic within Layer 2 networks and route traffic between Layer 3 networks.

---

### `ip routing`

Enables Layer 3 routing functionality on the switch.

```cisco
ip routing
```

---

### `no switchport`

Converts a physical switch interface from a Layer 2 switchport into a Layer 3 routed interface.

```cisco
interface gigabitEthernet 1/0/1
no switchport
```

---

### Routed Port

A routed port behaves similarly to a router interface.

Instead of being associated with a VLAN, it directly receives an IP address.

```cisco
interface gigabitEthernet 1/0/1
no switchport
ip address 192.168.1.2 255.255.255.252
```

---

# 📊 Layer 2 vs Layer 3 Interface

| Feature                      | Layer 2 Switchport | Layer 3 Routed Port |
| ---------------------------- | ------------------ | ------------------- |
| VLAN membership              | Yes                | No                  |
| IP address directly assigned | No                 | Yes                 |
| Uses `switchport`            | Yes                | No                  |
| Uses `no switchport`         | No                 | Yes                 |
| Can route IP traffic         | No                 | Yes                 |
| Layer                        | Layer 2            | Layer 3             |

---

# 🛠️ Important Commands

```cisco
ip routing
```

```cisco
interface gigabitEthernet 1/0/1
```

```cisco
no switchport
```

```cisco
ip address 192.168.1.2 255.255.255.252
```

```cisco
no shutdown
```

```cisco
show ip interface brief
```

```cisco
show ip route
```

```cisco
ping <destination-ip>
```

---

# ✅ Verification Results

| Test                     | Expected Result |
| ------------------------ | --------------- |
| L3 Switch 1 → Router     | ✅ Successful    |
| L3 Switch 2 → Router     | ✅ Successful    |
| Layer 3 interface status | ✅ Up/Up         |
| IP routing enabled       | ✅               |
| Routed ports configured  | ✅               |
| IP addressing configured | ✅               |

---

# 📚 Skills Demonstrated

**Networking**

`Layer 3 Switching` · `IPv4 Addressing` · `Routing` · `Layer 2 Switching` · `Routed Ports` · `Subnetting`

**Cisco IOS**

`ip routing` · `no switchport` · `show ip route` · `show ip interface brief` · `ping`

**Tools**

`Cisco Packet Tracer` · `Cisco IOS CLI`

---

# 🚀 Key Takeaway

This lab provides a foundation for understanding **Layer 3 switching and routing**.

The key configuration workflow is:

```text
Select Layer 3 Switch
        ↓
Power On
        ↓
Connect Devices
        ↓
Enable IP Routing
        ↓
Convert Switchport → Routed Port
        ↓
Assign IP Address
        ↓
Configure Router Interfaces
        ↓
Verify Connectivity
```

The most important commands demonstrated in this lab are:

```cisco
ip routing
```

and

```cisco
no switchport
```

Together, these allow the Layer 3 switch to perform routing functions in addition to traditional Layer 2 switching.

---

## 📁 Project Structure

```text
Layer-3-Switch-Basic-Routing/
│
├── README.md
├── Layer-3-Switch.pkt
└── screenshots/
    ├── topology.png
    ├── switch-configuration.png
    ├── ip-routing.png
    └── connectivity-test.png
```

---

## 🏷️ Tags

`Cisco` `CCNA` `PacketTracer` `Layer3Switch` `Routing` `Switching` `IPv4` `CiscoIOS` `Networking` `NetworkEngineering`
