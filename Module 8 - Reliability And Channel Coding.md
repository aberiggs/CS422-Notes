# Reliability and Channel Coding
#### Sources of Errors and Types
- Error sources: interference, distortion, and attenuation
- Resulting error types
	- Single bit error
		- A single bit in a block of bits is changed and all the other bits in the block are unchanged
	- Burst errors
		- By far the most common
		- Multiple bits in a block of bits are changed
		- Often from longer-duration interference
	- Erasure (ambiguity)
		- Often from hardware not being good enough
		- Signal that arrives at a receiver is ambiguous
		- Does not clearly correspond to a logical 1 or 0
		- Results from distortion or interference

#### Concept of Forward Error Correction (FEC)
- Examples
	- Single parity bit
		- Set a bit to say if there are even or odd number of 1 bits
	- Row and column (RAC)
		- To send 12 bits, arrange them in a matrix, compute a parity for each row and column and send 20 bits
	- Cyclic redundancy check (CRC)

#### Hamming Distance
- Used to assess code's resistance to errors
- Defined to be number of bit changes to transform bit string $S_1$ into bit string $S_2$
- Can be computed as number of 1 bits in the exclusive or of $S_1$ and $S_2$
- To assess code's strength, compute Hamming distance among all possible pairs of codewords, and take the minimum
- If minimum Hamming distance is $n$, an error that changes fewer than $n$ bits will be detected

#### Internet Checksum Computation
- Given
	- Message, M, of arbitrary length
- Compute
	- 16-bit 1s complement checksum, C
- Method
	- Pad M to an exact multiple of 16 bits
	- Set a 32 bit checksum int, C, to zero
	- For every 16-bit group in M
		- Treat the 16 bits as an int and add to C
	- Extract high-order 16 bits of C and add to C
	- Checksum is inverse of the low-order 16 bits
	- If the checksum is zero, substitute all 1s

#### Cyclic Redundancy Code (CRC)
- Used with Ethernet and other high-speed networks
- Hardware solution
- Properties
	- Arbitrary length message
		- As with a checksum the size of a dataword is not fixed, which means a CRC can be applied to 
	- Excellent Error Detection
	- Fast Hardware Implementation

#### Question
- Is it possible to write a function that computes the 32-bit CRC used with Ethernet
	- We wouldn't not be able to move at gigabit speed if we had to compute CRC
	- It's fairly slow to do with software
	- We use hardware to compute the CRC