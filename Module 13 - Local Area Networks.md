# Local Area Networks: Packets, Frames, And Topologies
#### Networks
- Distinct from physical communication systems
- Attach multiple endpoints 
- Two broad categories 
	- Circuit switched 
	- Packet switched

#### Circuit Switched Networks
- Provide point-to-point communication between pairs of endpoints
- Hardware establishes a circuit (path) between sender and receiver
- Separate steps for circuit creation, use, and termination
- Circuit can be
	- Permanent/provisioned
	- Switched (created on demand)
- *Concept* - user leases piece of underlying infrastructure for a time period 

#### Packet Switched Networks
- From the basis for the internet
- Multiplex communication over shared media
- All data divided into packets (with max size fixed)
- After sending a packet, sender allows others a chance to transmit before sending the next
- Arbitrary, async communication supported
- No set-up required before communication begins
- Performance varies due to statistical multiplexing
	- If every user "enters" at the same time to send packets, there will be delay since its shared
- *Concept* - underlying infrastructure is shared among users

#### Categories of Packet Switched Networks
- **LAN**
	- Local Area Network
	- Spans a single room or single building
- **MAN**
	- Metropolitan Area Network
	- Spans a major city or metroplex
- **WAN**
	- Wide Area Network
	- Spans sites in multiple cities
- PAN
	- Personal Area Network
	- Spans area around individual (used for headphones for example)
- SAN
	- Storage Area Network
	- Spans distance between a disk farm and processors in a data center
- CAN
	- Chip Area Network
	- Spans a single chip and connections processor, memories, etc.

#### IEEE 802 Model and Standards
- Project 802
- LAN/MAN standards
- Focuses on layer 1 and layer 2 standards
- Divides layer 2 into two sublayers
	- Logical Link Control
	- Media Access Control
- Organized in 1980
	- This is when ethernet was created
	- They wanted to standardize ethernet

#### Token Ring
- Intel, Microsoft, and other PC people were supporting something call token ring
- Ethernet ended up wiping out token ring

#### Standards Define
- Network topology (shape)
- Endpoint addressing scheme
- Frame (packet) format
- Media access mechanism
- Physical layer aspects and wiring

#### The Four LAN Topologies
- Bus
- Rung
- Star
- Mesh

#### IEEE Standard for Addressing
- **Formal name** - IEEE Media Access Control address (MAC address)
- Informally called an *Ethernet address*
- Each address is 48 bits long
- Assigned to Network Interface card (NIC) when device manufactured
- Divided into subfields
	- 3-byte Organizationally Unique ID (*IOU*)
	- 3-byte Network Interface Controller (*NIC*)
- Address types
	- *Unicast*
		- Destination is a single computer
		- Only that computer should receive a copy of the packet
	- *Broadcast*
		- Destination is all computers on a network
		- All of these computers should receive a copy of the packet
	- *Multicast*
		- A subset of computers on a network should receive a copy of the packet

#### Frame Format
- Layer 2 packet is called a frame
- General layout of a frame
	- Optional *prelude*
	- *Header*
	- *Payload*
	- Optional *postlude*

#### Framing and Serial Communications Systems
- Consider sending packets over a leased circuit
- Circuit hardware either provides a stream of bits or a stream of bytes (characters)
- We will consider hardware that provides a byte stream
	- No frame boundary
	- Any 8-bit value can appear in the data
- How can we send packets over such a system
- **Answer** - Sender and receiver must agree on framing

#### Example Framing Used With a Leased Circuit
- Use SOH and EOT characters to mark the start and end of a frame
- Use byte stuffing within the payload
	- *SOH* is the byte in payload
		- *ESC A* is the sequence sent
	- *EOT* is the byte in the payload
		- *ESC B* is the sequence sent
	- *ESC* is the byte in payload
		- *ESC C* is the sequence sent

