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
