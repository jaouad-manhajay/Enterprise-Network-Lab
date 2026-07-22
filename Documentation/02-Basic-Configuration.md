# Basic Configuration

## EDGE-R1

### Configure hostname

```cisco
hostname EDGE-R1
```

### Disable DNS lookup

```cisco
no ip domain-lookup
```

### Encrypt passwords

```cisco
service password-encryption
```

### Configure enable secret

```cisco
enable secret Lab@2026
```

### Create local administrator

```cisco
username admin privilege 15 secret Admin@2026
```

### Configure SSH

```cisco
ip domain-name enterprise.lab
crypto key generate rsa modulus 2048
ip ssh version 2
```

### Configure console access

```cisco
line console 0
password Lab@2026
login
logging synchronous
```

### Configure VTY

```cisco
line vty 0 4
login local
transport input ssh
```

### Configure MOTD banner

```cisco
banner motd #
Authorized Access Only!
#
```

### Save configuration

```cisco
write memory
```

## Verification Commands

```cisco
show running-config
show ip interface brief
show ip ssh
```
