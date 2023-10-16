# Wireshark-TCP-UDP

| NRP        | Name                        |
| ---------- | --------------------------- |
| 5025211015 | Muhammad Daffa Ashdaqfillah |

## Table of Contents

- [TCP Problems](#tcp-problems)
- [UDP Problems](#udp-problems)

## TCP Problems

1. What is the IP address and TCP port number used by the client computer (source) that is transferring the file to gaia.cs.umass.edu?

   - Pertama, dapatkan dulu ip dari `gaia.cs.umass.edu` dengan cara `ping gaia.cs.umass.edu` di terminal
     ![ping](/img/0.png)
   - Filter packet with ip `gaia.cs.umass.edu` : ip.addr == 128.119.245.12
   - Result :
     ![soal1](/img/1.png)
   - Dari data trace file di atas, dapat dilihat bahwa IP address dari client computer adalah `192.168.86.68` dan menggunakan port `55639`

2. What is the IP address of gaia.cs.umass.edu? On what port number is it sending and receiving TCP segments for this connection?

   - Dari hasil ping `gaia.cs.umass.edu` sebelumnya didapatkan IP address `128.119.245.12`
   - Dan dari hasil filter di soal sebelumnya, dapat dilihat bahwa port yang digunakan adalah `80`

3. What is the sequence number of the TCP SYN segment that is used to initiate the TCP connection between the client computer and gaia.cs.umass.edu? What is it in this TCP segment that identifies the segment as a SYN segment?Will the TCP receiver in this session be able to use Selective Acknowledgments?

   - Pada packet initial, dapat dilihat seperti ini :
     ![soal3](/img/3.png)
   - Didapatkan untuk sequence number of the TCP SYN segment adalah `seq = 0` atau `seq (raw) = 4236649187`
   - Di dalam packet tersebut terdapat flag `SYN: Set` yang menandakan bahwa packet tersebut adalah SYN segment, sehingga bisa digunakan sebagai selective acknowledgments

4. What is the sequence number of the SYNACK segment sent by gaia.cs.umass.edu to the client computer in reply to the SYN? What is it in the segment that identifies the segment as a SYNACK segment? What is the value of theAcknowledgementfield in the SYNACK segment? How did gaia.cs.umass.edu determine that value?

   - Pada packet SYNACK, dapat dilihat seperti ini :
     ![soal4](/img/4.png)
   - Didapatkan untuk sequence number of the SYNACK segment adalah `seq = 0` atau `seq (raw) = 1068969752`
   - Didapatkan untuk acknowledgement number of the SYNACK segment adalah `ack = 1` atau `ack (raw) = 4236649188`. Acknowledgement number didapatkan dari sequence number dari SYN segment ditambah 1 `(ACK=Seq no+1)`.

5. What is the sequence number of the TCP segment containing the header of the HTTP POST command? How many bytes of data are contained in the payload (data) field of this TCP segment? Did all of the data in the transferred file alice.txt fit into this single segment?

   - Pada packet HTTP POST, dapat dilihat seperti ini :
     ![soal5](/img/5.png)
   - Didapatkan untuk sequence number of the HTTP POST segment adalah `seq = 152041` atau `seq (raw) = 4236801228`
   - Didapatkan untuk payload (data) field of this TCP segment adalah `payload = 1385 bytes` atau
   - Detail packet memiliki keterangan bahwa packet dikirimkan menggunakan multipart or `MIME` sehingga data yang dikirimkan tidak hanya satu segment saja, melainkan beberapa segment. Payload yang dikirimkan sebesar `1385 bytes` sedangkan alice.txt sebesar `149KB`

6. Consider the TCP segment containing the HTTP “POST”as the first segment in the data transfer part of the TCP connection.
   ![soal6](/img/6.png)

   - At what time was the firstsegment(the onecontaining the HTTP POST) in the data-transfer part of the TCP connection sent?

     - Dari screenshot di atas, didapatkan bahwa packet pertama dikirimkan pada `frame: 4` dimana frame tersebut dikirimkan pada `0.24047 seconds`
       ![soal6-1](/img/6-1.png)

   - At what timewas the ACK for this firstdata-containing segment received?
     - Didapatkan bahwa ACK dari packet pertama diterima pada `frame: 7` dimana frame tersebut diterima pada `0.052671 seconds`
       ![soal6-2](/img/6-2.png)
   - What is the RTT for this first data-containing segment?
     - Dari screenshoot poin 6.2 didapatkan juga untuk RTT dari segment pertama adalah `0.028624 seconds`
   - What is the RTT value the seconddata-carrying TCP segment and its ACK?
     - Segment kedua dikirimkan pada `frame: 5` yang dimana ACK dari segment kedua diterima pada `frame: 8` sehingga didapatkan RTT dari segment kedua adalah `0.028628 seconds`
       ![soal6-3](/img/6-3.png)
   - What is the EstimatedRTTvalue (see Section 3.5.3, in the text) after the ACK for the second data-carryingsegmentis received?

7. What is the length (headerplus payload) ofeach ofthe first fourdata-carrying TCP segments?
   ![soal7](/img/6.png)

   - Dari screenshot di atas, didapatkan bahwa length dari 4 segment pertama adalah :
     - frame: 4 : length = 32 + 1448 = 1480 bytes
     - frame: 5 : length = 32 + 1448 = 1480 bytes
     - frame: 6 : length = 32 + 1448 = 1480 bytes
     - frame: 7 : length = 32 + 1448 = 1480 bytes
     
      Sehingga total length dari 4 segment pertama adalah `1480 * 4 = 5920 bytes`

8. What is the minimum amount of available buffer space advertised to the client by gaia.cs.umass.eduamong these first fourdata-carrying TCP segments7? Does the lack of receiver buffer space ever throttle the senderfor these first four data-carrying segments?
    ![soal8](/img/8.png)
    - Dari screenshoot di atas, didapatkan bahwa minimum amount of available buffer space adalah `131712` yang didapatkan dari `window size value`
    - Dari screenshoot di atas juga, didapatkan bahwa receiver buffer space tidak pernah throttle sender karena `window size value` selalu lebih besar dari `length` dari segment yang dikirimkan

9. Are there any retransmitted segments in the trace file? What did you check for (in the trace) in order to answer this question?
    - Retransimtted segments dapat dideteksi melalui sequence no. Ketika melakukan pengiriman ulang maka terdapat paket yang sequence no paket selanjutnya tidak lebih besar dari sequence no paket sebelumnya. Dari trace file yang ada, tidak terdapat retransmitted segments.

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
