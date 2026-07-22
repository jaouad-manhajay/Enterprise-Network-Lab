# WAN Configuration

## Objective

Configure the WAN link between ISP-R1 and EDGE-R1.

## ISP-R1

```cisco
interface GigabitEthernet0/0
description WAN Link to EDGE-R1
ip address 203.0.113.1 255.255.255.252
no shutdown
```

## EDGE-R1

```cisco
interface GigabitEthernet0/0
description WAN Link to ISP-R1
ip address 203.0.113.2 255.255.255.252
no shutdown
```

## Verification

```cisco
show ip interface brief
ping 203.0.113.2
ping 203.0.113.1
```
