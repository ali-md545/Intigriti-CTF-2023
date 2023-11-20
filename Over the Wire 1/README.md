# Intigriti-CTF-2023
Challenge: Over the Wire (Part 1)
I'm not sure how secure this protocol is but as long as we update the password, I'm sure everything will be fine 😊

We were given a pcap file. I started analyzing it using Wireshark. Firstly, I tried to filter out the TCP stream and started analyzing it one by one. At tcp.stream eq 8 I found an FTP connection and data was being transferred.  
 
2 things to notice here:
•	A password for user ‘cat’ which is looking like an FTP password.
•	A flag.zip file which is being transferred.

So, after seeing the flag.zip file I immediately looked if I can extract the file from PCAP but that didn’t pay off. So I dug further in TCP stream.  

It seems like a result of an "ls -l" command. At this point, I was only concerned about extracting the flag.zip file from this PCAP. I used CHATGPT to look for some linux tools for this purpose and I came across this tool called ‘Foremost’. 
Foremost is typically used for file carving and data recovery from disk images rather than pcap files. However, you can still try to use Foremost to extract files from a pcap file, but the success might vary depending on the nature of the traffic. 
Using the following command I was able to extract the zip file from PCAP:
foremost -i your_file.pcap -o output_directory
•	-i your_file.pcap: Specifies the input pcap file.
• -o output_directory: Specifies the output directory where Foremost should save the recovered files. 
 
 
 
It was password protected, so I used the one I found earlier in Wireshark ‘5up3r_53cur3_p455w0rd_2022’ but it was wrong. So I went to Wireshark again and further analyzed the TCP stream.

 I got this packet with an interesting bit of information. As it says, ‘update it accordingly’ and also in challenge information it said ’update the password’, so I changed the password fro 2022 to 2023 and voila, I got the flag.
 
