# Module 3 - Network Programming
#### Topics
- Internet services & communication paradigms
- Client-server model & alternatives
- Networking programming w/ a simplified API
- The socket API

## Internet Services and Communication Paradigms

#### General Principle: Intelligence at the Edge
- *The Internet does not provide services. Instead, the Internet only provides communication, and application programs provide all services.*
- The phone people disagreed because they wanted to control the service
	- Then they could bill for it
	- They thought this was going to fail
- Consequence
	- Every Internet communication, including voice and video teleconferencing, involves communication among application programs

#### Communication Paradigms
- The internet offers 2 communication paradigms

| Stream Paradigm              | Message Paradigm                  |
| ---------------------------- | --------------------------------- |
| Connection-oriented          | Connectionless                    |
| 1-to-1 communication         | Many-to-many communication        |
| Sequence of individual bytes | Sequence of individual messages   |
| Arbitrary length transfer    | Each message limited to 64 Kbytes |
| Used by most                 | Used for multimedia applications  |
| Built on TCP protocol        | Built on UDP protocol             |
- Stream paradigm banned by some service providers

#### Stream Paradigm (TCP)
- Transfers sequence of bytes
- Connection-oriented: data sent between 2 apps
- Bidirectional (one stream in each direction)
- No meaning attached to data and no boundaries inserted in data
- Surprising characteristic
	- *Although it delivers all bytes in sequence, the stream paradigm does not guarantee that the chunks of bytes passed to a receiving application correspond to the chunks of bytes transferred by the sending application*

#### Message Paradigm (UDP)
- Connectionless: network accepts and delivers individual messages
- If the sender places N bytes in a message, a receiver gets exactly N bytes incoming
	- Not buffered
- Paradigm allows unicast, multicast, or broadcast delivery
- Surprising characteristic
	- *Although it preserves boundaries, the message paradigm allows messages to be lost, duplicated, or delivered out-of-order; neither the sender nor receiver is informed when such errors occur.*

#### Stream Transport and Data Chunks
- The protocol system may
	- Divide the data from the sender into multiple segments and deliver a few bytes at a time to the receiver
	- Combine data from multiple transmissions into a single large chunk and deliver it to the receiver all at once
- Consequence
	- Receiving application cannot know exactly which pieces were sent
- Ways to determine when a transmission is "finished"
	- First, send the size of the message to be sent (in an integer for example). Then, send the message
		- The receiver will know by the integer read initially how long the message its waiting for should be
	- The sender closes the connection after message is sent
		- This leaves an EOF that the receiver will pick up on at the end of the message

#### Programming Hints
- When using the stream paradigm
	- Devise a way that the receiver knows where a message ends
	- Read from a socket until the entire message has been acquired
- When considering using the message paradigm
	- Don't (at least not yet)
	- Somewhat dangerous
	- You better know what you're doing
#### Identifying Individual Messages in a Stream
- Methods
	- Send one message followed by EOF
		- Cause on connection closure
	- Send multiple messages with an integer length before each message
	- Send multiple messages with a termination character (or sequence) following each message
- Notes
	- Any technique can be used as long as both sides agree
	- If sending a multi-byte length val or a multi-byte termination sequence, remember that the application may need multiple calls to receive all bytes of the length or the termination sequence

#### Buffering in the Stream Paradigm
- `push()` is equivalent to `flush()` for TCP
- On most Unix systems, `push()` is called for every `write()` operation
	- Thus you should not `write()` individual bytes as it is terribly in-efficient

#### Client-Server Model of Interaction
- One application acts as a server
	- Starts execution first
	- Awaits contact
- The other application becomes a client
	- Starts after server is running
	- Initiates contact

#### Characteristics of a Client
- Temporary
- Usually invoked by a user
- Actively initiates contact
- Usually is the one that terminates contact
- Can access multiple services as needed, but usually only contacts one remote server at a time
- Runs locally on a users device
- Does not require any powerful hardware

#### Characteristics of a Server
- Special purpose, privileged program dedicated to providing a service
- Usually handles multiple remote clients at the same time
	- *Complicates the design*
- Invoked automatically on system boot and executes through many sessions
- Waits passively for contact from arbitrary remote clients and then exchanged messages
- Requires powerful hardware and a sophisticated OS
- Runs on a large, powerful computer

#### Alternatives to Client-Server
- Broadcast
	- Sender broadcasts a message and all stations receive it
	- Does not scale well
	- Difficult to restrict data access
- Rendezvous point
	- Often used with consumer IoT
	- Intermediary that connects communicating applications
	- In essence, there are two clients and a server
	- Rendezvous point can become a bottleneck
- Peer-To-Peer
	- Designed to avoid central server bottleneck
	- Data divided among N computers
	- Each computers acts as a server for its data and as a client for other data
	- Given computer receives 1/N of the traffic

## A Simplified API
#### Network Programming
- General term that refers to the creation of client and server apps that communicate over a network
- Programmer uses an API
	- Set of functions
	- Include control as well as data transfer functions (e.g. establish and terminate communication)
- Defined by the OS; not part of the Internet standards
- Socket API has become a de facto standard
#### The Simplified API
- General Idea
	- Server is identified by pair (computer, application)
	- Server starts first and waits for contact
	- Client specifies server's location
	- Once a connection is established, client and server can exchange data
- Only seven functions


| Operation         | Meaning                                                                  |
| ----------------- | ------------------------------------------------------------------------ |
| await_contact     | Used by a server to wait for contact from a client                       |
| make_contact      | Used by a client to contact a server                                     |
| appname_to_appnum | Used to translate a program name to an equivalent internal binary value  |
| cname_to_comp     | Used to translate a computer name to an equivalent internal binary value |
| send              | Used by either client or server to send data                             |
| recv              | Used by either client or server to receive data                          |
| send_eof          | Used by both client and server after they have finished sending data     |

## The Socket API
#### Sockets
- AT&T defined an alternative named TLI (Transport Layer Interface), but TLI is now extinct
- Almost every OS includes an implementation
- MS Windows chose to make minor changes
	- This is annoying
- Super generalized
	- Have to specify protocol type
		- E.g. internet protocols
	- Have to specify address type
		- E.g. internet addresses

#### Socket Characteristics
- You can do anything with a socket
	- Connectionless communication (UDP message)
	- Connection-oriented communication (TCP stream)
- The API contains many functions
- General approach
	- Create a socket
	- Make many function calls to specify the type of communication, remote computer's address, port number to be used, etc.
	- Use socket to send/receive data
	- Close the socket

#### Terminology
- Availability of an application protocol
	- **Closed** - Vendor defines a protocol for their products
	- **Open** - Standardized and available for all vendors
- What application protocols specify
	- **Data Representation** - Message and data formats
	- **Data Transfer** - Procedures for exchanging messages and handling unexpected/error conditions
- Notes
	- The term *Transfer* in a protocol title indicates the latter
	- An application may define separate protocol for each type

#### Defining an Application Layer Protocol
- Programmer specifies a representation
	- Format of each message and data item
	- Meaning of each item in a message
- Programmer specifies transfer (interaction and message exchange)
	- What side sends first
	- Which side closes the connection first
	- What to do if one side crashes unexpectedly

#### State in an Application Protocol
- **Big Decision** - should state information be kept?
- A *stateful* protocol keeps info from previous requests
- A *stateless* protocol assumes each request is independent
- Example of a stateful interaction
	- Request 1 says "read 129 bytes from file X"
	- Request 2 says "read the next 128 bytes"
- Example of stateless interaction
	- Request 1 specifies "read bytes 0-127 from file X"
	- Request 2 specifies "read bytes 129-255 from file X"

#### Application-Layer Protocols for the Web
- HTML
- URL
- HTTP
#### HTTP Header Format
- Uses CRLF (carriage return line feeds)
	- Someone just put it into the standard since thats what their device used at the time
	- If they had been using one of the more modern computers at the time, things would be different

#### Original End-To-End Email Paradigm
- Each computer runs
	- An email server to accept incoming email
	- An email client to send outgoing email
- Incoming mail is deposited in a user's mailbox
- Outgoing mail placed in queue
- User interface to read or compose messages is separate from transfer applications

#### Current Email Paradigm
- Users mailbox located on a separate computer (usually at an ISP)
- Mail transfer application deposits message in mailbox
- User interface app accesses remote mailbox
	- Web browser may be used as an access mechanism
	- Special-purpose applications also exist
- Thus we need two protocols
	- An access protocol
	- A transfer protocol

#### Simple Mail Transfer Protocol (SMTP)
- Standard for email transfer
- Follows a stream paradigm
	- Through TCP
- Uses textual control messages
- Only transfers text messages
- Terminates with: \<CR> \<LF>. \<CR> \<LF>
	- Therefore, you can't send a message that has a line that contains just a period
- Allows sender to specify recipients' names and checks all names
- Sends only one copy of the message to a computer, even if destined to multiple recipients on the computer