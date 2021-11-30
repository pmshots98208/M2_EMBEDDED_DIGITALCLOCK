### The five components of a data communication network are:
1. Data
2. Sender
3. Receiver
4. Transmission Medium
5. Protocol

# SOURCE CODE

The code for the microcontroller section is written in embedded C and compiled using AVR-GCC (WinAVR) .
Hex code is  uploaded into Atmega328p with AVRDUDE using USBasp Programmer. 

### Asynchronous Communication:

The asynchronous communication there is no need for any clock line.

In some cases the sender and receiver agree upon some predefined clock period and generate their own clock pules and use them for extracting the information from the bit stream and in others the sender sends the data at a fixed rate and the receiver has the ability to measure the duration of each pulse to determine the length of each bit.

### Synchronous Communication:

In the synchronous type, one of the devices indulging in the communication has to generate the clock pulse and source it to the other devices in the the bus.

Typically the device that generated the clock is called the Master and it starts the conversation. The clock pulse sent out by the master is used by the slaves to determine the length of each bit in the coming data stream.

# Hardware Connection Setup  

We are using a 32 pin TQFP version of the ATmega328p microcontroller .If you are using the 28 pin DIP version,please make sure that the pin numbers  match by referring to the data sheet of ATmega328p.

TXD of ATmega328 is connected to RXD of USB to Serial Converter THEN, RXD of ATmega328 is connected to TXD of USB to Serial Converter.

In our case we are using the 8N1 setup ie 

1 Start Bit
8 Data Bits
No Parity 
1 Stop Bit

USART Control and Status Register 0 B or UCSR0B contains the bits for configuring the USART as Transmitter,Receiver or Both.

1. Enabling TXEN0 bit configures USART as  Transmitter
2. Enabling RXEN0 bit configures USART as Receiver 


 
