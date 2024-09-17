# IEEE MAC Sublayer
#### MAC Protocols
- Control access to shared medium
- Two types of channel allocation
	- Static
	- Dynamic
- General principle
	- *Static channel ....*

#### Channelization Protocols
- Employ and extend basic multiplexing techniques
- May be static or dynamic
- Three basic types

#### Channelization Protocols
- Three principal forms
	- Polling
		- Centralized controlled repeatedly polls stations and allows each to transmit one packet
	- Reservation
		- Stations submit a request for the next round of data transmission
		- Often used with satellite systems
			- Stations inform a controller if they have data to send
			- They have a huge delay so we definitely don't want to use polling
	- Token Passing
		- Stations circulate a token; each time it receives the token, a station transmits one packet
- All three have been used in practice

#### Example Random Access protocols
- ALOHA
	- Historic protocol used in an early radio network in Hawaii
	- Popular in textbooks and easy to analyze, but not used in real networks
- CSMA/CD
	- Carrier Sense Multi-Access with Collision Detection
	- The basis for the original Ethernet, and the most widely used random access protocol
- CSMA/CA
	- Carrier Sense Multi-Access with Collision Avoidance
	- The basis for Wi-Fi

#### Aloha
- Two carrier frequencies, *inbound* & *outbound*
- Central transmitter rebroadcast each incoming packet
- If inbound packets collide, sender receives a scrambled signal, waits a random time, and retransmits
- Channel utilization under 20%

#### CSMA/CD
- Used in original Ethernet (1973)
- Provides access to shared medium
- Principle features
	- Carrier Sense (CS)
		- Are there any signals on this wire?
	- Multiple Access (MA)
	- Collision Detection (CD)
- Uses binary exponential backoff
	- If a collision occurs during transmission, choose a random delay, and keep doubling this if another collision occurs

#### CSMA/CA
- Alternative to CSMA/CD
- Used in wireless networks (Wi-Fi)
- Needed because signals have limit distance $\delta$
- How do we avoid a collision
	- Neighbors delay transmission for 1 packet time
	- Communicating pair exchange RTS (ready to send) and CTS (clear to send) before packet transmission
	- In other words, an access point sends message saying that a given message is cleared to send that is received by everyone

#### Wired LAN technologies
