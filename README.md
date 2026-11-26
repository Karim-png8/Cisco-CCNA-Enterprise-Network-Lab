# Cisco-CCNA-Enterprise-Network-Lab    
# Network Lab: 3 Routers, 2 PCs (Cisco Packet Tracer)

A CCNA lab connecting two LANs through three routers using static routing.

## Topology

- PC1 -> SW1 -> R1 (LAN 192.168.1.0/24)
- R1 <-> R2 (link 192.168.12.0/24)
- R2 <-> R3 (link 192.168.13.0/24)
- R3 -> SW2 -> PC2 (LAN 192.168.3.0/24)

## Addressing Table

| Device | Interface | IP Address | Subnet Mask | Default Gateway |
|---|---|---|---|---|
| PC1 | Fa0 | 192.168.1.1 | 255.255.255.0 | 192.168.1.254 |
| R1 | Gig0/1 | 192.168.1.254 | 255.255.255.0 | n/a |
| R1 | Gig0/0 | 192.168.12.1 | 255.255.255.0 | n/a |
| R2 | Gig0/1 | 192.168.12.2 | 255.255.255.0 | n/a |
| R2 | Gig0/0 | 192.168.13.1 | 255.255.255.0 | n/a |
| R3 | Gig0/1 | 192.168.13.2 | 255.255.255.0 | n/a |
| R3 | Gig0/0 | 192.168.3.254 | 255.255.255.0 | n/a |
| PC2 | Fa0 | 192.168.3.1 | 255.255.255.0 | 192.168.3.254 |

## Key Ideas

- **ip address**: gives an interface its own address. Each side of a link gets a different host number on the same network.
- **ip route**: tells a router how to reach a remote network. Format: `ip route <remote network> <subnet mask> <next hop>`.
- **Remote network**: any network the router is not directly connected to.
- **Next hop**: the neighbor router's address on the shared link, never the router's own address.
- If you change a host number, change it everywhere it is used, including in ip route commands.

## R1 Configuration

```
enable
configure terminal
hostname R1
interface gigabitEthernet 0/1
ip address 192.168.1.254 255.255.255.0
no shutdown
exit
interface gigabitEthernet 0/0
ip address 192.168.12.1 255.255.255.0
no shutdown
exit
ip route 192.168.13.0 255.255.255.0 192.168.12.2
ip route 192.168.3.0 255.255.255.0 192.168.12.2
end
write memory
```

R1 is directly connected to networks 1 and 12, so it only needs routes to networks 13 and 3, both reached through R2 (192.168.12.2).

## R2 Configuration

```
enable
configure terminal
hostname R2
interface gigabitEthernet 0/1
ip address 192.168.12.2 255.255.255.0
no shutdown
exit
interface gigabitEthernet 0/0
ip address 192.168.13.1 255.255.255.0
no shutdown
exit
ip route 192.168.1.0 255.255.255.0 192.168.12.1
ip route 192.168.3.0 255.255.255.0 192.168.13.2
end
write memory
```

R2 has two neighbors: R1 (192.168.12.1) leads to network 1, and R3 (192.168.13.2) leads to network 3.

## R3 Configuration

```
enable
configure terminal
hostname R3
interface gigabitEthernet 0/1
ip address 192.168.13.2 255.255.255.0
no shutdown
exit
interface gigabitEthernet 0/0
ip address 192.168.3.254 255.255.255.0
no shutdown
exit
ip route 192.168.1.0 255.255.255.0 192.168.13.1
ip route 192.168.12.0 255.255.255.0 192.168.13.1
end
write memory
```

R3 reaches networks 1 and 12 through R2 (192.168.13.1).

## Testing

1. From PC1, open Command Prompt and run `ping 192.168.3.1`.
2. From PC2, run `ping 192.168.1.1`.
3. On any router, run `show ip route` to see static routes marked with S.

## Troubleshooting Notes

- If a ping fails, check that every interface is up with `show ip interface brief`.
- If the router seems stuck after a typo, wait for the domain lookup to time out, or press Ctrl+Shift+6. Prevent it with `no ip domain-lookup`.
- Make sure each PC's default gateway matches its router interface address.

## Files

- `CCNA Lab 2.pkt`: the Packet Tracer project file.
