# Module 4 - Application Layer Protocols
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

#### Mail Access Protocols
- Two standards protocols
	- Post Office Protocol version 3 (POP3)
	- Internet Mail Access Protocol (IMAP)
- Functionality
	- Provide access to a user's mailbox
	- Permit user to view headers, download, delete, or send individual messages
	- Client runs on user's personal computer
	- Server runs on a computer that stores user's mailbox

#### RFC2822 Mail Message Format
- Email representation standard
- Name derived from the Internet standard in which it is defined
- Specifies
	- Email message consists of text file
	- Blank line separates header from the body
	- Header lines have the form
		- Keyword: information
- Some keywords have defined meanings:
	- From:
		- Is not verified - results in the ability to impersonate others
	- To:
	- Subject:
	- Cc:
- Keywords starting with uppercase X have no effect

#### Multimedia Email
- SMTP was limited to transferring plain text messages
- How can SMTP be used to transfer images and the like?
	- We encode arbitrary binary items in plain text (think of a hex dump)
	- Sender can specify content type and encoding
	- Standard includes Base64 encoding

#### Examples of Mime Headers
- Mime header lines added to other RFC2822 headers

Example:
---xyz123
Content-Type: image/jpeg

^ Important. Blank line ends header

## Domain Name System
#### DNS
- Important piece of Internet infrastructure
- Runs at the application layer
- Translates human-readable names into the binary addresses used by the Internet Protocol

#### DNS Terminology
- Names are hierarchical
- Each name divided into segments by a period character
- Most significant segment is on the right
- Rightmost segment known as the top-level domain (TLD)
- Client program known as a resolver
	- "The DNS client"
	- Used by web browser, email, etc.

#### DNS Servers
- Names are divided among a hierarchy of servers; each is an authority for some names
- Multiple groupings possible

#### Name Resolution and Caching
- Resolver
	- Acts as a client
	- Is configured w/ address of local DNS server
	- Contacts local server first
	- Socket library resolves is gethostbyname
- Caching
	- Follows locality of reference principle
	- Each DNS server caches results
	- Cached item never kept when stale

#### DNS Server Algorithm Pt. 1
- Given
	- Request message form a DNS name resolver
- Provide
	- Response message that contains address

##### Method
```
extract name N from request
if (server is authority for N) {
	Form and send auth response to requester
} else if (answer for N is in cache) {
	Form and send a nonauthoritative response to the requester
} else {
	if (authority server for N is known) {
		send request to authority server
	} else {
		Send request to root server
	}
	Receive response and place in cache
	Form and send response to the requester
}
```
