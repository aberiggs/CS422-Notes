# Wired LAN Technology

#### Technologies
- There were a whole lot of wired technologies
- Only one remains and it completely dominates the market
	- This is Ethernet

#### Ethernet Technology
- Invented at Xerox PARC in 1973
- Standardized by Digital, Intel, and Xerox (DIX) in 1978
- Frame has a 14-byte header followed by payload of 46 to 1500 bytes
- Frame format and addressing have survived virtually unchanged
![[ethernet_frame_format.png]]

#### Ethernet Address Filtering
- Recall: station accepts a copy of the frame if *destination address* matches 
	- The stations unicast address
	- The broadcast address (all 1s)
	- A multicast address to which station is listening

#### Frame Type Field
- Set by sender to identify contents of frame
- Used by receiver to determine how to process the frame
- Values are standardized
- Examples:
	- Type `0x0800` used for IPv4 datagram
	- Type `0x86DD` used for IPv6 datagram
	- Type `0x0806` used for ARP

#### Frame Demultiplexing
- Performed when frame arrives
- Usually handled by protocol software
- Frame type field examined and frame passed to appropriate protocol module
		- Unrecognized types are discarded

#### IEEE's Version of Ethernet
- Header *type* field reinterpreted as a frame length
- Eight bytes of payload occupied by LLC SNAP header
- Never really caught on (everyone still uses the original DIX version)

#### Ethernet Wiring
- Three generations
	- Thicknet
	- Thinnet
	- Twisted Pair