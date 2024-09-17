# Information Sources And Signals
#### Sources of Information
- An input signal can arise from
	- A transducer such as a microphone
	- Receiver such as an Ethernet interface
- We use the term signal processing to describe the recognition and transformation of signals

#### Fourier Analysis 
- Multiple sine waves can be added together
	- Result is known as a composite wave
	- Corresponds to combining multiple symbols (e.g. playing two musical tones at the same time)
- Mathematician named Fourier discovered how to decompose an arbitrary composite wave into individual sine waves
- Fourier analysis provides the mathematical basis for signal processing
- Bad news: according to Fourier, a digital wave decomposes into an infinite set of sine waves

#### Sine Wave Characteristics
- Three important characteristics of a sine waved are used in networks
	- Frequency
	- Amplitude
	- Phase

#### Definition of Analog Bandwidth
- Decompose a signal into a set of sine waves and take the difference between the highest and lowest frequency
- Easy to compute from a frequency domain plot
- Example signal with a bandwidth of 4 Kilohertz (KHz)
![[analog_bandwidth.png]]

#### Digital Signals and Signal Levels
- A digital signal can represent multiple bits
- Hard for the data to be preserved with all the kinds of interference when there is many different levels

#### Maximum Data Rate
- We define a baud rate of a signal to be the number of times it changes per second
- At each change a sender chooses from K variants (K voltage levels for example)
- The maximum data rate for such a transmission is given by
	- data rate in bits/second = baud rate * floor(log_2(K))

#### Converting Digital to Analog
- Approximate a digital signal with a composite of several sine waves
- Mathematically the bandwidth of a digital signal is infinite

#### Converting Analog to Digital
- Steps taken to convert analog to digital 
	- analog signal
	- sampling
	- quantization
	- encoding
	- digital data

#### Sampling Rate and Nyquist Theorem
- How many samples should be taken per second?
- Mathematician named Nyquist discovered the answer
	- sampling rate = 2 * max frequency

#### Nonlinear Encoding
- Linear sampling doesn't work well for voice
- Researchers created nonlinear sampling algorithms that modify dynamic range to reproduce sounds to which the human ear is sensitive
- Mu-law
- A-law

#### Synchronization Errors
- Occurs when receiver and sender disagree about bit boundaries (clocks differ)
- Line coding techniques prevent synchronization errors

#### Example Line Coding
- Manchester Encoding
	- Used with Ethernet
	- Synchronizes receiver with sender
	- Transition in the middle of a bit time indicates the value
		- Low-to-high represents 1
		- High-to-low represents 0
- Differential Manchester Encoding
	- Transition at the beginning of the bit time indicates the value
		- No transition represents 1
		- Transition represents 0