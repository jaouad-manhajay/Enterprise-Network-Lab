# VLAN Configuration

## Objective

Create VLANs for the enterprise network.

## Configuration

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

## Verification

```cisco
show vlan brief
```
---

# Trunk Configuration

## Objective

Configure trunk links between the CORE-SW and the access switches.

## CORE-SW

### GigabitEthernet0/0 (SW-IT)

```cisco
interface GigabitEthernet0/0
description Trunk to SW-IT
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan 10,20,30,99
no shutdown
```

### GigabitEthernet0/2 (SW-HR)

```cisco
interface GigabitEthernet0/2
description Trunk to SW-HR
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan 10,20,30,99
no shutdown
```

### GigabitEthernet0/3 (SW-SRV)

```cisco
interface GigabitEthernet0/3
description Trunk to SW-SRV
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan 10,20,30,99
no shutdown
```

## Verification

```cisco
show interfaces trunk
```
---

# SW-IT Configuration

## Objective

Configure the SW-IT access switch with a trunk uplink to the CORE-SW and assign the user port to VLAN 10.

## Basic Configuration

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

## Trunk Configuration

```cisco
interface GigabitEthernet0/0
description Trunk to CORE-SW
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan 10,20,30,99
no shutdown
```

## Access Port Configuration

```cisco
interface GigabitEthernet0/1
description PC-IT
switchport mode access
switchport access vlan 10
spanning-tree portfast
no shutdown
```

## Verification

```cisco
show interfaces trunk
show vlan brief
show interfaces status
```

## Notes

- Uplink configured as an IEEE 802.1Q trunk.
- User access port assigned to VLAN 10.
- PortFast enabled on the access interface connected to the end device.

---

# SW-HR Configuration

## Objective

Configure the SW-HR access switch with a trunk uplink to the CORE-SW and assign the user port to VLAN 20.

## Basic Configuration

```cisco
hostname SW-HR
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

## Trunk Configuration

```cisco
interface GigabitEthernet0/2
description Trunk to CORE-SW
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan 10,20,30,99
no shutdown
```

## Access Port Configuration

```cisco
interface GigabitEthernet0/1
description PC-HR
switchport mode access
switchport access vlan 20
spanning-tree portfast
no shutdown
```

## Verification

```cisco
show interfaces trunk
show vlan brief
show interfaces status
```

## Notes

- Uplink configured as an IEEE 802.1Q trunk.
- User access port assigned to VLAN 20.
- PortFast enabled on the access interface.


---

# SW-SRV Configuration

## Objective

Configure the SW-SRV access switch with a trunk uplink to the CORE-SW and assign the server port to VLAN 30.

## Basic Configuration

```cisco
hostname SW-SRV
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

## Trunk Configuration

```cisco
interface GigabitEthernet0/3
description Trunk to CORE-SW
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan 10,20,30,99
no shutdown
```

## Access Port Configuration

```cisco
interface GigabitEthernet0/1
description Windows Server
switchport mode access
switchport access vlan 30
spanning-tree portfast
no shutdown
```

## Verification

```cisco
show interfaces trunk
show vlan brief
show interfaces status
```

## Notes

- Uplink configured as an IEEE 802.1Q trunk.
- Server port assigned to VLAN 30.
- PortFast enabled on the server access interface.
