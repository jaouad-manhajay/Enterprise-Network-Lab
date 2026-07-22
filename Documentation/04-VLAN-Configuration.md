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
