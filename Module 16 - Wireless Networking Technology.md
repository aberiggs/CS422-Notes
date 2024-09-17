# Wireless Networking Technology
#### Wireless Networks
- Many types exist
- Technologies differ in
	- Distance spanned
	- Data rates
	- Physical characteristics of electromagnetic energy
		- Ability to permeate obstructions like walls
		- Susceptibility to interference
	- Isolated channel vs. shared channel
		- Isolated - your cell phone connected to a cell tower
		- Shared channel - Devices connecting to a network via Wi-Fi

#### Personal Area Network (PAN)
- Terminology used primarily with wireless networks
- Spans short distances
- Dedicated to single user (not shared)
- Examples
	- Bluetooth
	- InfraRed
	- ZigBee

#### ISM Wireless Bands
- ISM stands for *Industrial, Scientific, and Medical*
- Consists of regions of the EM spectrum available for use without license
- Used for wireless LANs and PANs (e.g., cordless phones)
- Three separate bands

#### Wireless LANs and Wi-Fi
- Vendors moved to open standards in 1990's
- IEEE provided most of the standards under 802.11
- Every 5 years or so there will be another advancement

#### Spread Spectrum Transmission
- Uses multiple frequencies for a single channel
- Can increase performance or provide immunity to noise
	- If one frequency that gets clobbered (like another device causing problems or the way the building is constructed), you can still get through
- Major spread spectrum techniques
	- Direct Sequence Spread Spectrum (DSSS)
	- Frequency Hopping Spread Spectrum (FHSS)
	- Orthogonal Frequency Division Multiplexing (OFDM)
		- *Considered the best now*

#### Wireless LAN Architecture
- IEEE defines two possible modes for wireless LAN communication
- Infrastructure mode
	- What everyone uses
	- Wireless devices communicate through an *access point* (AP)
	- AP's connect to each other and (usually) the Internet
	- Typical uses: corporate wireless LAN, Internet Cafe, etc.
- Ad hoc mode
	- Direct communication among wireless devices
	- Forwarding possible
	- Seldom used

#### Infrastructure Mode Wireless LAN
- Basic Service Set (BSS) for an AP is defined as a set of devices that can hear the AP
- APs interconnect through wired network
- Practical considerations
	- In practice BSSs can overlap (given wireless device can hear more than one AP)
	- To solve the problem, each device associates with one AP at any time

#### Practical Considerations: Wi-Fi Channels
- 11 channels defined for North American in 2.4 GHz range
- **Bad News** - 22 MHz bandwidth means that channels overlap
- **Good news** - Channels 1, 6, and 11 can operate simultaneously with no interference
	- Can also use wireless backhaul

#### Addresses in 802.11 Frame Format
- 802.11 frame is **NOT** the same as an Ethernet frame
- Each 802.11 frame includes four MAC addresses
	- Source
	- Destination AP
	- Router along the path to the Internet
	- Extra address for ad hoc mode

![[802.11_frame_format.png]]

#### Coordination Among Access Points
- Coordinated approach
	- Initial design
	- Similar to cellular telephone
	- APs communicate to achieve smooth handoff
- Uncoordinated approach
	- Later alternative
	- APs don't communicate
	- Wireless device changes association when communication with an AP lost
	- Lower overall cost

#### Cellular Telephones and Data Networking
- Call phone providers have switch to use Internet protocols
- There are more cell phones in the world than computers
- The smart phone is now the network interface of choice protocols

#### Current Cellular System Architecture
- Cell tower that connects to mobile switch system
- Each mobile switching system connects to PSTN or Internet
- Handoff decision made by infrastructure

#### Cell Size and Expected Cell Phone Density
- In practice, cell size is based on the expected number of cell phones
- Smaller cells used in high-population areas
- Larger cells used in rural areas

#### Frequency Assignment
- Goal: minimize interference
- Principle
	- *Interference can be minimized if an adjacent pair of cells do not use the same frequency*
- Method: devise an assignment of frequencies such that two adjacent cells are not assigned the same frequency
- Technique: create a pattern that can be repeated
- Known as a cluster approach (mathematicians use the term tessellation)

#### Cellular Technologies
- Many competing standards
- European Conference of Postal and telecommunications Administrators chose a TDMA technology known as Global System for Mobile Communications (GSM) for Europe
- In US, each carrier created its own standards
	- Motorola created iDEN using TDMA
	- Others adopted IS-95A which uses CDMA
- Japan chose PDC< which uses TDMA
- 5G pushes everyone to adopt the same standard; a GSM variant

