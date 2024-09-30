# Transport-Network-DataLink Layer

The **network layer** itself doesn't physically route the data but is responsible for providing the necessary **routing information** to guide packets from the source to the destination. Let's break this down in more detail.

### 1. **Role of the Network Layer**:
The **network layer** (Layer 3 in the OSI model) focuses on:
- **Addressing**: Assigning IP addresses to devices and packets.
- **Routing information**: Determining the best logical path for data to travel across multiple networks.
- **Packet forwarding**: Adding routing information to data packets so that they can reach their final destination, regardless of the intermediate networks or devices.

### What the Network Layer Does:
- **Encapsulates data**: The transport layer data (segments) is encapsulated into **packets** with **IP addresses** (source and destination) and other relevant routing information.
  
- **Determines the path**: Based on the destination IP address and the state of the network (e.g., available paths, congestion, etc.), the network layer **chooses the best route** for the packet to travel. It uses **routing tables** and protocols like **OSPF**, **BGP**, or **RIP** to decide this.

- **Packet forwarding**: The network layer passes the packet (which now includes all the routing and addressing information) to the **data link layer** (Layer 2) for forwarding to the next hop in the network.

### 2. **Physical Routing Happens at the Router Level**:
While the network layer adds the necessary **logical addressing and routing information** (IP addresses, routing decisions) to the packet, the **actual physical routing** is performed by **routers**.

- **Routers**, which operate primarily at the **network layer** and the **data link layer**, physically move packets across the network by examining the **IP addresses** in the packets and deciding the next network hop.
  
- When a packet reaches a router, the router examines the **destination IP address** in the packet and uses its **routing table** to determine the next hop (either another router or the destination device).
  
- The router then **forwards the packet** along the correct path. This process repeats at each router the packet encounters until it reaches its final destination.

### 3. **Network Layer and Routing Information**:
The network layer uses **IP addresses** and **routing protocols** to:
- **Create routing tables**: These tables hold information about how packets should be forwarded based on destination IP addresses.
- **Determine the best path**: Using routing protocols (e.g., **OSPF**, **BGP**), the network layer builds paths for data to take through the network. This is **logical routing** — it decides the next hop based on the destination but doesn’t physically move the data itself.

### 4. **Physical Routing and Forwarding Happens Below the Network Layer**:
After the network layer has provided the routing information and encapsulated the packet:
- The **data link layer** (Layer 2) handles **frame transmission** within a single network segment. It forwards the packet to the next device (router or end device) based on **MAC addresses**.
  
- The **physical layer** (Layer 1) is where the actual signals (electrical, optical, or wireless) are transmitted across the network's physical medium (e.g., cables, fibers, or airwaves).

### Summary:
- The **network layer** is responsible for adding **logical routing information** (IP addresses, path determination) to data packets, deciding the best route for the packet.
- The **physical routing and forwarding** of the packet happens at **routers** and the lower layers (data link and physical layers), where the actual transmission of the packet across the network takes place.

In short, the **network layer** doesn’t physically route packets but **provides the logical information and decisions** needed for the packets to be routed correctly by devices like routers.
