Download Link: https://assignmentchef.com/product/solved-ece358-lab-3-encapsulation-and-network-utilities
<br>






<table width="590">

 <tbody>

  <tr>

   <td width="590"><strong> <u>Objective:</u></strong>After this project, students are expected to:i.                    Understand the format of standard frames and packet headers.ii.                  Use basic network utilities to monitor network traffic.</td>

  </tr>

 </tbody>

</table>




<h1>1.Overview</h1>

Refer to the textbook and the lecture notes for an introduction on the layered architecture (see Figure 1).




<h2>Figure 1</h2>

In this project, you will be asked to interpret all the encapsulated headers of captured Ethernet frames. You will also get an opportunity to use some network utilities to get an idea about the performances of the network. <em>If you have a Linux-based computer, you can run the utilities directly from your machine, otherwise, use one of the ECE Linux machines.</em>




<h1>2.Background Material</h1>

<h2>2.1  Ethernet Frame</h2>

Figure 2 shows the format of Ethernet frames sent and received by the MAC layer.

The preamble bits are not shown. If a frame is received without bit errors, the “Data” portion is passed on to the upper layer (network layer).




<h2>2.2  IP/TCP/UDP Header</h2>

The IP protocol is defined in RFC 791 (RFC: Request for Comment), and a summary of the IP header is given in Figure 3. The number on the top is the bit number and each row is   four –byte long.  Figures 4 and 5 show the format of the headers of TCP and UDP, respectively. They are defined in RFC 793 and RFC 768, respectively. All the RFCs can be found at   http://www.ietf.org/rfc.html. The numbers on top again represent the bit number and each row is four-byte (32-bits) long. You will also need to refer to the

ICMP protocol (RFC 792) and tell us what is the highest protocol (e.g., FTP, HTTP, etc.) .













<h2>2.3  Protocol Header Analysis</h2>




The analysis of a sample MAC frame is being shown below.







Ethernet header:




00 00 0c d9 fa 88: Ethernet destination address is 00 00 0c d9 fa 88 (unicast).

00 00 b4 a0 15 c1: Ethernet source address: 00 00 b4 a0 15 c1 (unicast).

08 00: The payload type is IP (0x0800). (Note: 0x0806 is ARP.)




IP header:




45: This is an IP version 4 datagram,

45: The header length is 5×4 = 20 bytes. (There is no <em>options</em> field in the given IP header).







00

(0 0 0 0 0 0 0 0 in binary): This datagram has routine precedence (the lowest). The IP Precedence field is used by some routers to determine which datagram to drop, therefore datagrams with the lowest precedence will be dropped first.




(0 0 0 0 0 0 0 0 in binary): the 3 type of service (ToS) bits

0 0 0 <em>Normal delay </em>

0 0 0 <em>Normal throughput </em>

0 0 0 <em>Normal Reliability </em>

(0 0 0 0 0 0 0 0 in binary): The last two bits must be zero (for future use).




00 28: Total length of the IP datagram is 40 (0x0028) bytes.

04 04: The identification of this datagram is 0x0404 (for fragmentation purpose).

40 00: (0 1 0 0 0 0 0 0 0 0 0 0 0 0 0 0):

1 Don’t Fragment flag set

0 More Fragment flag unset The Fragment offset is 0.

This means that the datagram cannot be fragmented, and there are no fragments after this datagram. With a fragment offset equals to zero, we know that this is the only fragment of a datagram.

80: Time to live = 128 (0x80), meaning the datagram may exist for <em>at most</em> 128 more hops.

06: The Protocol on top is TCP (0x06) (Note: 0x01 is ICMP and 0x11 is UDP).

42 a0: This is the checksum of the datagram.

80 d3 a0 3c: Source IP address is 128.211.160.60.

80 0a 13 14: Destination IP address is 128.10.19.20.




<strong>TCP header: </strong>




04 3a: The Source port is 1082, which is an arbitrarily port number assigned by the operating system.

00 15: The Destination port is 21, which is the well-known port for FTP (File Transfer Protocol).

54 f1 f2 09: The Seq. no. is 1425142281. d6 7d df 9d: The Ack no. is 3598573469.

50: Data offset is 20 (5 x 4) bytes. This is the length of the TCP header.

10 (0 0 0 1 0 0 0 0):

Flags:              URG  0                        ACK  1                         PSH  0

RST  0                         SYN  0                         FIN  0

Only the ACK flag is set, meaning that the value carried in the acknowledgement field is valid. <strong>(You should comment on all the flags that are set, i.e., equal to </strong>

<h2>1)</h2>

40 5a: the receiver window size is 16474 (0x405a) bytes.   b9 e8: Checksum of the whole TCP segment.

00 00: Urgent pointer (Not used in this segment).




Data: none




<strong>Overall comment on the given frame:</strong> The given example frame contained a pure TCP ACK (no data). We observe a lot of those when we monitor the Internet. There may be data in a frame, so you just need to highlight the data portion without analyzing it. You should try to include as much information about the frame as possible. Do not try to analyze the TCP options (see Figure 4).

<strong> </strong>

<h3>2.4  Network Utilities</h3>




In this project, you will use the following network utilities:

<ul>

 <li>arp</li>

 <li>ifconfig</li>

 <li>nslookup</li>

 <li>netstat</li>

 <li>ping</li>

 <li>traceroute (tracert)</li>

</ul>




Detailed information about each utility can be obtained from the Internet.  Also, you can find information about the utilities by using the <strong><em>man</em></strong> command on Unix/Linux machines.

<strong> </strong>

<ol start="3">

 <li><strong><u>Questions</u></strong><strong>: </strong></li>

</ol>

To do questions 2 to 7, the student should try the commands on different machines/locations and keep the most interesting results. Note that in some environments, the output to the commands might be more difficult to interpret.

<strong> </strong>

<h3>3.1  Protocol Header Analysis</h3>




<strong><u>Question 1:</u></strong> Obtain two frames in from the folder “frames” under “Lab Manuals” in LEARN (please download the frames according to the last digit of your student ID, i.e., if last digit of ID = <em>i</em>, do frame <em>i</em> and frame <em>i+10</em>.  Using the example given in section 2.3 as a template, parse the frames in a human readable format and comment.   For example, write an IP address in the dotted decimal notation and header length as a positive integer. Also, color (or, underline) the different parts of the frames to indicate their layers: 2, 3, 4, or app data and indicate the name of the highest layer protocol.

<strong> </strong>

<h3>3.2  Network Utilities</h3>




In the manual, we tell you to use the network utilities using a command of the type /sbin/command. This only applies if you use one of the ECE Linux machines, otherwise use the command directly. You might get more interesting results by logging to an ECE Linux machine.

<strong> </strong>

<h3>Question 2: (arp)</h3>

<ul>

 <li>Explain the functions of the utility.</li>

 <li>Use the command /sbin/arp –a to see the ARP table of the machine on which you are logged in. Include the output of the command in your report and explain it.</li>

</ul>




<h3>Question 3: (ifconfig)</h3>

<ul>

 <li>Explain the functions of the utility.</li>

 <li>Use the command /sbin/ifconfig –a. Include the output in your report and explain it.</li>

</ul>




<h3>Question 4: (netstat)</h3>

<ul>

 <li>Explain the functions of the utility.</li>

 <li>Use the command netstat -in. Change –in to –s to get some statistics. Include the output in your report and explain it.</li>

 <li>Use the command netstat -r. Include the output in your report and explain it.</li>

</ul>




<h3>Question 5: (nslookup)</h3>

<ul>

 <li>Explain, in your own words, what the utility does.</li>

 <li>Use the command to obtain the IP addresses of the following hosts and explain what you get.

  <ol>

   <li>uwaterloo.ca (do it twice)</li>

   <li><a href="https://web.mit.edu/">mit.edu</a></li>

   <li><a href="https://www.gmail.com/">gmail.com</a></li>

   <li>facebook.com</li>

  </ol></li>

</ul>




<h3>Question 6: (ping)</h3>

<ul>

 <li>Explain the functions of the utility.</li>

 <li>Use ping –c10 <em>hostname </em>to estimate the average round-trip-time from the machine on which you are logged in to the following hosts. Include the output in your report and explain what you get.

  <ol>

   <li>ualberta.ca</li>

   <li>lemonde.fr</li>

   <li>ucla.edu</li>

  </ol></li>

</ul>




Check if each host above is up by using a web browser to connect to the hosts.




<strong><u>Question 7:</u></strong> (traceroute)

<ul>

 <li>Explain the functions of the utility.</li>

 <li>Use /usr/sbin/traceroute <em>hostname </em>to find out how many hops there are between the machine on which you are logged in and the following hosts. Include the outputs in your report and explain what you get.

  <ul>

   <li>uwaterloo.ca</li>

   <li><a href="https://www.youtube.com/">youtube.com</a></li>

   <li><a href="https://www.nytimes.com/">nytimes.com</a></li>

  </ul></li>

</ul>