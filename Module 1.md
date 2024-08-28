#  Module 1 - Approaches To Networking, Open And Closed Systems, Protocols, And Layering
## Historic Approaches to Networking
#### Vendors
- Thought that they should create a network system that connects all PCs
- Create network equipment and the interface hardware to connect all computer to their network
- They built drivers for your OS
- The problem was that all the hardware was proprietary and had specific limitations (e.g. only served 300 devices when a client may need support for 400)

#### Researchers
- Rejected all the other approaches
- We don't want a vendor to tell us we can only connect computers that use their hardware
- Wanted to experiment with new technologies (short/long distance) and applications
	- We don't want one technology, we want the ability to use whichever technology is appropriate for a given application

#### Resulting Research Projects
- Xerox Palo Alto Research Center
	- Ethernet
- MIT and elsewhere
	- Token passing ring networks
- U.S. D.O.D.
	- ARPANET
	- SATNET
	- Packet radio net
	- The global Internet

#### Open Vs. Closed Networks
- Closed
	- "Vertical approach"
	- Vendor builds their own
	- Owned by vendor
	- Licensed to other groups
- Open
	- Competitive approach
	- Multiple groups collaborate to define a technology
	- To ensure interoperability, specs had to be written in ***standards*** docs that were public
	- Companies build products according to the standards

## Protocol Standards & Design
#### Companies Issuing Standards
- They sell compliance
	- You can't just put a stamp that says your device speaks WiFi
	- IEEE sells this type of "compliance" authentication
- They sell specifications

#### What do protocols do?
- Specify **Syntax**
	- Format each message
	- Representation of data items
	- Encoding of bits in electromagnetic signals
- Specify **Semantics**
	- The meaning of each message
	- Procedures used to exchange messages
		- Not a matter of just simple reply/response
		- E.g. interference mangles a message sent between two devices, so what do you do?
	- Actions to take when a message arrives or when an error occurs

#### Steps in Protocol Design
- Looks at facilities the underlying hardware provides
- Imagine the way the world should work (the communication mechanism as a user would like it to work)
- Design an efficient implementation
- **The key** - choose a good abstraction

#### What Make Protocol Design Difficult
- Multiple implementations of a protocol will exist
- Implementations will be created by multiple individuals/organizations
- Many details to consider
- Key tradeoff
- If you specify every detail, you've eliminated all possible innovation
	- Enough details so everyone agrees, but leave enough of it open for people to try new things
- The key tradeoff
	- Specify too many details - Stifles innovation
	- Specify too few details (spec is ambiguous) - Incompatible implementations

#### Maximizing Interoperability
- *Be conservative in what you send and be liberal in what you accept*
	- Each device has software to address the difference cases of packets sent
	- Microsoft is an example of such a company that is terrible at TCP/IP as their packets are formatted differently

## Protocol Layering and Layering Models
- There's a lot of false info thats provided by companies regarding this topic
- Wikipedia has incorrect info
#### Protocol Layering
- Needed b/c communication is complex
- Intended (mostly) for protocol designers
- Divides the communication into manageable pieces
- Provides a conceptual framework to help us understand protocols
- Ideally, layering is invisible once protocols have been designed
	- Unlike what companies try to convince you that they have products that will help you split apart layers
	- Remember, layering is intended for designers

#### Two Layering Models
- Internet protocols use a 5-layer reference model
- ISO and the ITU defined a 7-layer model

#### Internet Reference Model

| Layer 5 | Application       |
| ------- | ----------------- |
| Layer 4 | Transport         |
| Layer 3 | Internet          |
| Layer 2 | Network Interface |
| Layer 1 | Physical          |
- Descriptive model formed after TCP/IP protocols were devised
- Used in practice 

#### Physical Layer
- Electromagnetic energy and its use
- Associated hardware
- Representation of info in signals

#### Network Interface Layer
- Communication between a computer and network hardware
- Packet is a generic term for a piece of data being transferred

#### Internet Layer
- Communication between a pair of computers across the internet
- Internet packet format (datagram)
- Only gets data from one computer to the target computer

#### Transport Layer
- Communication between a pair of applications (end-to-end)
- Reliable delivery and retransmission
- Mechanisms to control data rate and avoid congestions

#### Application Layer
- Format and representation of data and messages that one app sends to another
- Meaning of messages exchanged
- Internet infra support mechanisms, such as routing and DNS

#### General Idea
- Message has to go down through the layers, exits the computer, goes up through the layers in the other computer
- Each given layer adds info and forms a packet

#### Packet Headers as a Packet Passes Across the Internet
- One header prepended by each layer when message sent
- Result: headers are nested with lowest-layer header appearing first

physical header (possible but not typical) <-> network interface header <-> internet header 
<-> transport header <-> message

#### Layering Principle
- Layered protocols enforce an invariant
	- *Layer N at the destination receives an exact copy of the message sent by layer N at the source. All headers and other modifications added by lower layers at the source must be removed by lower layers at the destination.*
- Allows protocol designers to focus on one layer at a time

#### Cross-Layer Communication
- Facts
	- A transport protocol selects the amount of data to send in each packet
- In practice TCP "cheats" by looking down to layer 3 even though its at layer 4

#### Layering In An Internet
- Our layering
- Routers only need layer 2 and layer 3 software to forward packets across the internet
	- An example that not all devices need all 5 layers
	- *In practice* most routers do more than just forwarding packets (e.g. management)

#### Technologies that Intertwine Layers
- Cross-layer functions
- Layer circularities
	- Tunneling can be used to send IPv6 or IPv4 (layer 3 protocols)

#### VPN
- Inserts itself below the internet layer
- Grabs the data, encrypts it, and then has to send it out

#### ISO 7-Layer Reference Model
- Formed before protocols were devised
- Created by committee vote

| Layer 7 | Application  |
| ------- | ------------ |
| Layer 6 | Presentation |
| Layer 5 | Session      |
| Layer 4 | Transport    |
| Layer 3 | Network      |
| Layer 2 | Data Link    |
| Layer 1 | Physical     |
- Was defined when data networks connected dumb terminals to large mainframes
	- Remote login for telephone companies
- Session layer
	- Need a way to form a connection
	- Much like dialing a telephone line to give your information
	- Handled details of login and control of send/receive
	- Provided opportunity for billing and accounting
- Presentation layer
	- Two main character sets: ASCII & EBCIDIC
	- Intention was to map character sets
- Both layers are now superfluous

#### An Alternative to Layering
- Get really smart people to have them design a single, large protocol that handles everything on its own
