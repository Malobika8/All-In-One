## How does the communication happen between computers?

There are 2 ways
- Guided Way: There's a set of paths already defined. Example: 2 computers connected with a wire.
- Unguided Way: Communication happens but there's no one single path. Example: WiFi, Bluetooth

When we talk to someone from a different country, we send a request to the ISP, the ISP sends it to the country & the country gives it back.

```
In India, tier-1 service provider is Tata. Tier 2 is Airtel and others.
```

### How are our countries connected?

They have wires running across the ocean from one country to another. 

```
There's a website where we can see that - https://www.submarinecablemap.com/
```

<img width="1439" alt="Screenshot 2024-07-30 at 11 33 25 AM" src="https://github.com/user-attachments/assets/74d8ed37-66ab-47d5-8d3a-0937ae8b8de0">

Submarine cables

<img width="799" alt="Screenshot 2024-07-30 at 11 37 30 AM" src="https://github.com/user-attachments/assets/5d0d178b-0afb-493e-95e3-bb86d851e7c1">
<img width="952" alt="Screenshot 2024-07-30 at 11 38 31 AM" src="https://github.com/user-attachments/assets/0ea6a4b7-fc0e-48f3-aa6b-691de54e3d63">

<img width="1113" alt="Screenshot 2024-07-30 at 11 39 47 AM" src="https://github.com/user-attachments/assets/a38e200a-4c63-43dc-81da-28f8798f9a4a">

##### Why can't we use satellites instead of cables? 

- It's faster than satellites.
  
## How are things connected?

- *LAN*: Small hubs/Office. Via Ethernet cable, wifi
- *MAN*: Across the city.
- *WAN*: Across countries. Via Optical Fibre cables.
  - *SONET*: Synchronous optical networking. It carries data using optical fiber cables and hence can cover larger distances.
  - *Frame Relay*: a way to connect LAN to WAN.

The Internet is a collection of all these. LANs are connected to each other using MAN that are in turn connected using WAN.

## Modem & Router
- A Modem is used to convert digital signals to analog/electrical signals & vice-versa.
- A Router is a device that routes data packets based on IP Addresses.

### Note:
*Modem, router, and WiFi are different components that work together to provide internet access in your home or office. A modem (Modulator-Demodulator) connects your device to the 
internet via a broadband connection, such as cable or fiber. A router directs traffic between devices on your network, ensuring they can communicate with each other. WiFi, on the other 
hand, is a wireless technology that allows devices to connect to the router without the use of cables. While they serve distinct purposes, they often work together to provide a 
seamless internet experience.* 

## Topologies

- Bus: Every system is connected like a backbone. If the link gets broken, the entire network is spoilt. Only 1 person can send data at a particular time.
  
  <img width="1116" alt="Screenshot 2024-07-30 at 12 13 34 PM" src="https://github.com/user-attachments/assets/8cccb85c-3994-4106-ac12-ec4dcb9566f1">

- Ring: Connected in a ring. Every system communicates with one another. If one of the cables breaks, it becomes impossible to transfer data. A lot of unnecessary calls are being made.

  <img width="750" alt="Screenshot 2024-07-30 at 12 14 15 PM" src="https://github.com/user-attachments/assets/43daf211-4c5b-4492-939b-e311b8d23652">

- Start: One controlling/central device connected to all computers. Every system communicates via a centralized device. If central fais, the network goes down.

  <img width="861" alt="Screenshot 2024-07-30 at 12 15 21 PM" src="https://github.com/user-attachments/assets/69242abb-a65d-42b7-88d2-2c9a3770383e">

- Tree: It is a combination of bus and star topology.

  <img width="1096" alt="Screenshot 2024-07-30 at 12 16 20 PM" src="https://github.com/user-attachments/assets/d766a1db-c383-47e6-8e41-8cd2de8cd9ee">

- Mesh: Every single computer gets connected to every other computer. It's expensive. Scalability issue.

  <img width="792" alt="Screenshot 2024-07-30 at 12 17 02 PM" src="https://github.com/user-attachments/assets/8ccfa18c-f9f4-4eac-b052-f38c57c9f181">

























