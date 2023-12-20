# ACL Part 3

When you use ACLs for traffic filtering, they can operate inbound or outbound. The direction determines at which point packets are tested against the ACL as they pass through the router.

1. Outbound ACLs: Incoming packets are routed to the outbound interface and then are processed through the outbound ACL. If packets match a permit statement, they are forwarded through the interface. If packets match a deny statement or if there is no match, they are discarded.

2. Inbound ACLs: Incoming packets are processed by the ACL before they are routed to an outbound interface. An inbound ACL is efficient because it saves the overhead of routing lookups if the filtering tests deny the packet and it is discarded. If the tests permit the packet, it is processed for routing.


Apply ACL 1 on the interface as an outbound filter.
```
Branch(config-if)# ip access-group 1 out
```
Apply ACL 2 on the interface as an inbound filter.
```
Branch(config-if)# ip access-group 2 in
```
## Example Standart ACL
```
Branch(config) # access-list 1 deny host 10.1.1.101 
Branch(config)# access-list 1 permit 10.1.1.0 0.0.0.255 
Branch(config)# interface GigabitEthernet 0/1 
Branch(config-if)# ip access-group 1 out
```
## Example Extended ACL
```
Branch(config)# access-list 101 deny ip host 10.1.1.101 any 
Branch(config)# access-list 101 permit ip 10.1.1.0 0.0.0.255 any 
Branch(config)# interface GigabitEthernet 0/0 
Branch(config-if)# ip access-group 101 in
```
