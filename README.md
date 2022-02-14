# projectsimplot
Automatically exported from code.google.com/p/projectsimplot
SimPlot

SimPlot is a simple real time data visualization tool. This tool plots real time data from serial port. Check out the project home page for more information and video of the tool in action.

Automatically exported from code.google.com/p/projectsimplot

http://forum.arduino.cc/index.php/topic,58911.0.html http://web.archive.org/web/20140125023847/http://www.negtronics.com/simplot http://web.archive.org/web/20140125023847/http://arduino.cc/forum/index.php/topic,58911.0.html


http://web.archive.org/web/20140125023847/http://www.negtronics.com/simplot
SimPlot

The Why?
In my projects I needed a simple tool that could plot real time data from a microcontroller. There was no such tool available out there. There are various scripts using Processing and Python that can be used to plot the data, but nothing that is simple, easy to use and ready out of the box.

The What?
SimPlot is a simple plotting tool. This tool is used for visualization of real time data. The tool accepts data over serial port and plots it in real time on the screen.

Currently has following features
Plots data from serial port
4 Channels of data
16bit signed data type (Arduino int datatype)
User defined X axis length
User defined Y axis scale


The Where?
Download from: 

http://code.google.com/p/projectsimplot/

Forum thread for discussion and questions:
http://arduino.cc/forum/index.php/topic,58911.0.html

The How?
The tool expects data in a particular format. The data should be in little endian format (ie. first byte is LSB). The tool can plot from one to 4 channels data. Arduino code samples can be found here.

 Sample pseudo C code to generate and send proper data packet is given below

Packet format to send 1 channel of data

int16_t comPkt[130];     //Buffer to hold the packet, note it is 16bit data type

comPkt[0] = 0xCDAB;      //Packet Header, indicating start of packet.
comPkt[1] = 2;           //Size of data payload in bytes.
comPkt[2] = (int16_t) Channel1_data;    //Channel 1 data. 16bit signed integer
       
Serial_sendBuffer(USART1, (uint8_t *) comPkt, 6);

Packet format to send 4 channel of data

int16_t comPkt[130];   //Buffer to hold the packet, note it is 16bit data type

comPkt[0] = 0xCDAB;                     //Packet Header, indicating start of packet.
comPkt[1] = 8;                          //Size of data payload in bytes.
comPkt[2] = (int16_t) Channel1_data;    //Channel 1 data. 16bit signed integer
comPkt[3] = (int16_t) Channel2_data;    //Channel 2 data. 16bit signed integer
comPkt[4] = (int16_t) Channel3_data;    //Channel 3 data. 16bit signed integer
comPkt[5] = (int16_t) Channel4_data;    //Channel 4 data. 16bit signed integer

 Serial_sendBuffer(USART1, (uint8_t *) comPkt, 12);

Take care of endianess of your microcontroller. The PC is little endian and expects data in that format. The byte stream should look like this
 0xAB    	Header byte 1
 0xCD	Header byte 2 
 0x8    	 Size LSB
 0x00    	 Size MSB
 0x01	 Channel 1 LSB
 0x00	          Channel 1 MSB            
 0x05	 Channel 2 LSB
 0x00	  Channel 2 MSB

Comments and Suggestions
