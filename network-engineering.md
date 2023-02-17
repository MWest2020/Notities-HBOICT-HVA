# Network Engineering

## TCP test questions (week 1)

## Termination of TCP connections

- Host A send a sgment witht he FIN f;ag set to 1
- Host B awknowledges
- Host B send its own segment with FIN flag set to 1
- Host A awknowledges

## What event causes the congestion protocol to increase speed?

answer: The aceptance of AWK proving segments are received.

NOT the RTT

---

## DNS test questions (week 2)

### What is the difference between a DNS server and a DNS client?

- A DNS server is a server that responds to DNS queries
- A DNS client is a client that sends DNS queries

### What is the difference between a DNS resolver and a DNS client?

- A DNS resolver is a program that sends DNS queries
- A DNS client is a client that sends DNS queries

### What is the difference between a DNS resolver and a DNS server?

- A DNS resolver is a program that sends DNS queries
- A DNS server is a server that responds to DNS queries

### What is the difference between a DNS resolver and a DNS proxy?

- A DNS resolver is a program that sends DNS queries
- A DNS proxy is a server that responds to DNS queries

### What is the difference between a DNS resolver and a DNS forwarder?

- A DNS resolver is a program that sends DNS queries
- A DNS forwarder is a server that responds to DNS queries

### How does DNSsec work?

- DNSsec uses public key cryptography to sign DNS records

## Routing algorithms

Reminder between forwarding and routing:

- Forwarding is the process of determining the next hop for a packet
- Routing is the process of determining the path for a packet

There are two routing algotirhms:

- Distance vector routing (decentralized routing)
- Link state routing (centralized routing)

### Distance vector routing (Bellman-Ford algorithm)

- Each router maintains a table of the distance to each neighbor
- Each router sends its distance vector to its neighbors
- Each router updates its distance vector based on the distance vectors it receives from its neighbors

#### Bellman-Ford algorithm

### Link state routing (Dijkstra's algorithm)

- Each router maintains a table of the distance to each destination
- Each router sends its link state to its neighbors
- Each router broadcasts least costpaths form one node to all other nodes (forwarding table)

#### Dijkstra's algorithm

- Dijkstra's algorithm is used to determine the least cost path from one node to all other nodes
- step 1: initialize the distance to all nodes to infinity
- step 2: set the distance to the source node to 0
- step 3: repeat until all nodes have been visited
  - step 3.1: find the node with the smallest distance that has not been visited
  - step 3.2: update the distance to all neighbors of the node found in step 3.1
  - step 3.3: mark the node found in step 3.1 as visited

### What is the difference between distance vector routing and link state routing?

- Distance vector routing uses a distance vector to determine the next hop
- Link state routing uses a link state to determine the next hop

## Autonomous systems

- An autonomous system is a collection of routers under the control of a single entity

## Routing protocols

- Routing protocols are used to exchange routing information between routers

### What is the difference between a routing protocol and a routing algorithm?

- A routing protocol is used to exchange routing information between routers
- A routing algorithm is used to determine the next hop for a packet

## Intra-AS routing

- Intra-AS routing is the process of determining the path for a packet within an autonomous system

## Inter-AS routing

- Inter-AS routing is the process of determining the path for a packet between autonomous systems

## Why different routing protocols are used for intra-AS routing and inter-AS routing?

- Scale hierachical routing saves table size, reduced update traffic
- Policy inter admin control, intra single admin no policy decisions needed
- Performance: intra is focused on performance (inter policy may dominate)

---

## BGP (Border Gateway Protocol)

- BGP is a inter-domain routing protocol used to exchange routing information between autonomous systems
- glue that holds the internet
- uses path vector routing

### BGP provides the following features to ASes

- eBGP: obtain subnet reachability information from neighboring ASes (gateway)
- iBGP: obtain reachability information to all AS-internal routers (internal and gateway)
- determines the best path to a destination based of reachibility and policy

### BGP Path attributes and BGP routes

- BGP path attributes are used to describe (advertise) the path to a destination
  - AS-PATH: list of ASes that the packet has traversed
  - NEXT-HOP: IP address of the next hop AS

This can be done through policy-based routing (never go through the same AS twice or AS Y)
Route selection :

- local preference based on policy
- shortest AS-PATH
- closest NEXT-HOP
- additional criteria (read more)

## BGP Hijacking

- BGP hijacking is the process of taking control of a BGP session
- can happen by mistake

## BGP specific questions

- **Explain how BGP uses the AS_PATH attribute to detect and prevent routing loops**

The AS_PATH attribute is a list of AS numbers that the prefix has traversed to reach the router advertising it. Each time the prefix is advertised by a new AS, the AS number of the advertising AS is added to the end of the list. When a router receives an update for a prefix, it compares the AS_PATH length (the number of ASes in the path) of the prefix with its own knowledge of the same prefix. If the AS_PATH length of the prefix received is shorter than its own, the router updates its information and re-advertises the prefix.

However, if the AS_PATH length is the same or longer, the router discards the update and does not re-advertise the prefix. *This prevents a routing loop from occurring because it ensures that the prefix is only advertised by the AS closest to the source of the prefix*.

In conclusion, BGP uses the AS_PATH attribute to detect and prevent routing loops by keeping track of the path a prefix has taken and ensuring that the prefix is only advertised by the AS closest to the source. This helps maintain a consistent and stable routing table, ensuring that packets are delivered to their intended destination

- **Will a BGP router always choose the route with the shortest AS_PATH length?
Explain your answer**

No, a BGP router will not always choose the route with the shortest AS_PATH length. The AS_PATH length is just one of several attributes that BGP routers use to determine the best route to a destination. Other factors, such as the next-hop IP address, the origin code, the Multi-Exit Discriminator (MED), local preference, and the weight attribute, are also considered when selecting the best route.

---

## OSPF

- OSPF is a routing protocol used to exchange routing information within an autonomous system
- publicly available
- uses link state routing
- uses Dijkstra's algorithm
- uses a 32-bit AS number carried over IP
