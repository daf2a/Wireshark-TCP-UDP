# Wireshark-TCP-UDP


| NRP | Name |
| --- | --- |
| 5025211015 | Muhammad Daffa Ashdaqfillah |

## Table of Contents
  - [TCP Problems](#tcp-problems)
  - [UDP Problems](#udp-problems)

## TCP Problems
1. What is the IP address and TCP port number used by the client computer (source) that is transferring the file to gaia.cs.umass.edu?

2. What is the IP address of gaia.cs.umass.edu? On what port number is it sending and receiving TCP segments for this connection?

3. What is the sequence number of the TCP SYN segment that is used to initiate the TCP connection between the client computer and gaia.cs.umass.edu? What is it in this TCP segment that identifies the segment as a SYN segment?Will the TCP receiver in this session be able to use Selective Acknowledgments?

4. What is the sequence number of the SYNACK segment sent by gaia.cs.umass.edu to the client computer in reply to the SYN? What is it in the segment that identifies the segment as a SYNACK segment? What is the value of theAcknowledgementfield in the SYNACK segment? How did gaia.cs.umass.edu determine that value?

5. What is the sequence number of the TCP segment containing the header of the HTTP POST command? How many bytes of data are contained in the payload (data) field of this TCP segment? Did all of the data in the transferred file alice.txt fit into this single segment?

6. Consider the TCP segment containing the HTTP “POST”as the first segment in the data transfer part of the TCP connection.
- At what time was the firstsegment(the onecontaining the HTTP POST) in the data-transfer part of the TCP connection sent?
- At what timewas the ACK for this firstdata-containing segment received?
- What is the RTT for this first data-containing segment?
- What is the RTT value the seconddata-carrying TCP segment and its ACK?
- What is the EstimatedRTTvalue (see Section 3.5.3, in the text) after the ACK for the second data-carryingsegmentis received?

7. What is the length (headerplus payload) ofeach ofthe first fourdata-carrying TCP segments?

8. What is the minimum amount of available buffer space advertised to the client by gaia.cs.umass.eduamong these first fourdata-carrying TCP segments7? Does the lack of receiver buffer space ever throttle the senderfor these first four data-carrying segments?

9. Are there any retransmitted segments in the trace file? What did you check for (in the trace) in order to answer this question?

10. How much data does the receiver typically acknowledgein an ACK among the first ten data-carrying segments sent from the client to gaia.cs.umass.edu? Can you identify cases where the receiver is ACKing every other received segment (see Table 3.2 in the text)among these first ten data-carrying segments?

11. What is the throughput (bytes transferred per unit time) for the TCP connection? Explain how you calculated this value.

12. Use the Time-Sequence-Graph(Stevens) plotting tool to view the sequence number versus time plot of segments being sent from the client to the gaia.cs.umass.edu server. Consider the “fleets”of packets sent around t= 0.025, t=0.053, t=0.082 and t=0.1. Comment on whether this looks as if TCP is in itsslow start phase, congestion avoidance phase or some other phase.Figure 6 shows a slightly different view of this data.

13. These “fleets”of segments appear to have some periodicity. What can you say about the period?

14. Answer each of two questions above for the trace that you have gathered when 
you transferred a file from your computer to gaia.cs.umass.edu

## UDP Problems
1. Select one UDP packet from your trace. From this packet, determine how many fields there are in the UDP header. (You shouldn’t look in the textbook! Answer these questions directly from what you observe in the packet trace.) Name these fields.

2. By consulting the displayed information in Wireshark’s packet content field for this packet, determine the length (in bytes) of each of the UDP header fields.

3. The value in the Length field is the length of what? (You can consult the text for this answer). Verify your claim with your captured UDP packet.

4. What is the maximum number of bytes that can be included in a UDP payload? (Hint: the answer to this question can be determined by your answer to 2. above)

5. What is the largest possible source port number? (Hint: see the hint in 4.)

6. What is the protocol number for UDP? Give your answer in both hexadecimal and decimal notation. To answer this question, you’ll need to look into the Protocol field of the IP datagram containing this UDP segment (see Figure 4.13 in the text, and the discussion of IP header fields).

7. Examine a pair of UDP packets in which your host sends the first UDP packet and the second UDP packet is a reply to this first UDP packet. (Hint: for a second packet to be sent in response to a first packet, the sender of the first packet should be the destination of the second packet). Describe the relationship between the port numbers in the two packets.