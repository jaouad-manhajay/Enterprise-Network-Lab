# VLAN Configuration

## Objective

This document describes the VLAN implementation and trunk configuration for the enterprise network. It includes the configuration of the Core Switch and all Access Switches.

---

# Network VLANs

| VLAN ID | Name | Purpose |
|---------:|------|---------|
| 10 | IT | IT Department |
| 20 | HR | Human Resources |
| 30 | SERVERS | Servers |
| 99 | MANAGEMENT | Management & Device Administration |

---

# CORE-SW Configuration

## Objective

Configure the Core Switch, create VLANs and establish trunk links with all access switches.

### Basic Configuration

```cisco
hostname CORE-SW
no ip domain-lookup
service password-encryption

enable secret Lab@2026

username admin privilege 15 secret Admin@2026

ip domain-name enterprise.lab

crypto key generate rsa modulus 2048

ip ssh version 2

line console 0
 password Lab@2026
 login
 logging synchronous

line vty 0 15
 login local
 transport input ssh

banner motd #
Authorized Access Only!
#
```

### VLAN Configuration

```cisco
vlan 10
 name IT

vlan 20
 name HR

vlan 30
 name SERVERS

vlan 99
 name MANAGEMENT
```

### Trunk Configuration

#### Trunk to SW-IT

```cisco
interface GigabitEthernet0/0
 description Trunk to SW-IT
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,99
 no shutdown
```

#### Trunk to EDGE-R1

```cisco
interface GigabitEthernet0/1
 description Trunk to EDGE-R1
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,99
 no shutdown
```

#### Trunk to SW-HR

```cisco
interface GigabitEthernet0/2
 description Trunk to SW-HR
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,99
 no shutdown
```

#### Trunk to SW-SRV

```cisco
interface GigabitEthernet0/3
 description Trunk to SW-SRV
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,99
 no shutdown
```

### Verification

```cisco
show vlan brief
show interfaces trunk
show interfaces status
```

### Notes

- VLANs created successfully.
- IEEE 802.1Q trunks configured.
- SSH enabled.
- Password encryption enabled.

---

# SW-IT Configuration

## Objective

Configure the IT access switch.

### Basic Configuration

```cisco
hostname SW-IT
no ip domain-lookup
service password-encryption

enable secret Lab@2026

username admin privilege 15 secret Admin@2026

ip domain-name enterprise.lab

crypto key generate rsa modulus 2048

ip ssh version 2

line console 0
 password Lab@2026
 login
 logging synchronous

line vty 0 15
 login local
 transport input ssh

banner motd #
Authorized Access Only!
#
```

### Trunk Configuration

```cisco
interface GigabitEthernet0/0
 description Trunk to CORE-SW
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,99
 no shutdown
```

### Access Port

```cisco
interface GigabitEthernet0/1
 description PC-IT
 switchport mode access
 switchport access vlan 10
 spanning-tree portfast
 no shutdown
```

### Verification

```cisco
show interfaces trunk
show vlan brief
show interfaces status
```

### Notes

- Uplink configured as trunk.
- PC assigned to VLAN 10.

---

# SW-HR Configuration

## Objective

Configure the HR access switch.

### Basic Configuration

```cisco
hostname SW-HR
...
```

### Trunk Configuration

```cisco
interface GigabitEthernet0/2
 description Trunk to CORE-SW
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,99
 no shutdown
```

### Access Port

```cisco
interface GigabitEthernet0/1
 description PC-HR
 switchport mode access
 switchport access vlan 20
 spanning-tree portfast
 no shutdown
```

### Verification

```cisco
show interfaces trunk
show vlan brief
show interfaces status
```

### Notes

- PC assigned to VLAN 20.

---

# SW-SRV Configuration

## Objective

Configure the Server access switch.

### Basic Configuration

```cisco
hostname SW-SRV
...
```

### Trunk Configuration

```cisco
interface GigabitEthernet0/3
 description Trunk to CORE-SW
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,99
 no shutdown
```

### Access Port

```cisco
interface GigabitEthernet0/1
 description Windows Server
 switchport mode access
 switchport access vlan 30
 spanning-tree portfast
 no shutdown
```

### Verification

```cisco
show interfaces trunk
show vlan brief
show interfaces status
```

### Notes

- Windows Server assigned to VLAN 30.

---

# Validation Checklist

| Task | Status |
|------|--------|
| VLAN 10 Created | ✅ |
| VLAN 20 Created | ✅ |
| VLAN 30 Created | ✅ |
| VLAN 99 Created | ✅ |
| Trunks Configured | ✅ |
| Access Ports Configured | ✅ |
| SSH Enabled | ✅ |
| Running Configuration Saved | ✅ |

---

# Screenshots

- CORE-SW VLAN Table
- CORE-SW Trunk Status
- SW-IT VLAN Table
- SW-HR VLAN Table
- SW-SRV VLAN Table
- Trunk Verification
- Running Configuration

---

# Conclusion

The VLAN infrastructure has been successfully deployed. All switches are configured with secure management settings, VLAN segmentation, and IEEE 802.1Q trunk links. The network is now ready for the next phase: **Inter-VLAN Routing (Router-on-a-Stick)**.
