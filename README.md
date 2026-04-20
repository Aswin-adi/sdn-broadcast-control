# SDN-Based Broadcast Traffic Control using Mininet

## 1. Introduction

In modern networks, broadcast traffic plays an important role in communication protocols such as ARP. However, excessive broadcast traffic can lead to network congestion, reduced performance, and broadcast storms. This project demonstrates a Software Defined Networking (SDN) approach to control broadcast traffic using a centralized controller.

## 2. Objective

The objective of this project is to design and implement an SDN-based mechanism that detects and controls broadcast traffic in a network using Mininet and a POX controller.

## 3. Technologies Used

* Mininet (Network Emulator)
* POX Controller (Python-based SDN Controller)
* OpenFlow Protocol
* Python Programming Language

## 4. System Design

The network topology consists of a single OpenFlow switch connected to multiple hosts. The switch communicates with the controller using the OpenFlow protocol. The controller inspects incoming packets and applies control logic.

### Working Principle:

* When a packet arrives at the switch, it is forwarded to the controller (PacketIn event).
* The controller examines the destination address of the packet.
* If the packet is identified as broadcast, it is dropped.
* If the packet is unicast (normal communication), it is forwarded to the appropriate destination.

## 5. Implementation

### Controller Logic

The controller is implemented using POX. It listens for PacketIn events and applies the following logic:

* Detect broadcast packets using destination MAC address.
* Block broadcast packets to prevent unnecessary flooding.
* Allow normal packets by forwarding them using OpenFlow actions.

## 6. Execution Steps

### Terminal 1 (Controller)

cd ~/pox
python3 pox.py broadcast_control

### Terminal 2 (Mininet)

sudo mn -c
sudo mn --topo single,4 --controller remote

## 7. Testing and Results

### Test Case 1: Normal Communication

Command:
h1 ping h2

Result:
Successful communication between hosts, indicating that normal traffic is allowed.

### Test Case 2: Broadcast Communication

Command:
h1 ping -b 10.0.0.255

Result:
Broadcast packets are blocked, and no response is received. The controller logs indicate detection and blocking of broadcast traffic.

## 8. Observations

* Broadcast traffic is effectively controlled by the SDN controller.
* Normal communication is not affected.
* The system reduces unnecessary network traffic and improves efficiency.

## 9. Conclusion

This project successfully demonstrates the use of SDN for broadcast traffic control. By implementing logic in the controller, broadcast traffic can be filtered, thereby preventing congestion and improving overall network performance.

## 10. References

* Mininet Documentation: https://mininet.org
* POX Controller Documentation: https://noxrepo.github.io/pox-doc/html/
* OpenFlow Specification
