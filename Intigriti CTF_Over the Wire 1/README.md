# Intigriti-CTF-2023
Challenge: Over the Wire (Part 1)
I'm not sure how secure this protocol is but as long as we update the password, I'm sure everything will be fine 😊

![image](https://github.com/ali-md545/Intigriti-CTF-2023/assets/149575457/a6897100-cbb8-4da0-b470-2861fbe06a5c)


We were given a pcap file. I started analyzing it using Wireshark. Firstly, I tried to filter out the TCP packets and followed TCP stream. At tcp.stream eq 8 I found an FTP connection and data was being transferred.  

![image](https://github.com/ali-md545/Intigriti-CTF-2023/assets/149575457/89e77469-cd10-4ec0-aba1-1e02ff348e7d)
 
2 things to notice here:
•	A password for user ‘cat’ which is looking like an FTP password (as the protocol also suggests).
•	A flag.zip file which is being transferred.

So, after seeing the flag.zip file I immediately checked if I can extract the file from PCAP (using Exports Objects in Wireshark) but that didn’t pay off. So I dug further in TCP stream.  

![image](https://github.com/ali-md545/Intigriti-CTF-2023/assets/149575457/e195fa94-2cdf-4f4e-83e1-476f8451a4f8)

It seems like a result of an 'ls -l' command. At this point, I was only concerned about extracting the flag.zip file from this PCAP. I used CHATGPT to look for some linux tools for this purpose and I came across this tool called ‘Foremost’. 
Foremost is typically used for file carving and data recovery from disk images rather than pcap files. However, you can still try to use Foremost to extract files from a pcap file, but the success might vary depending on the nature of the traffic. 
Using the following command I was able to extract the zip file from PCAP:
foremost -i your_file.pcap -o output_directory
•	-i your_file.pcap: Specifies the input pcap file.
• -o output_directory: Specifies the output directory where Foremost should save the recovered files. 
 
 ![image](https://github.com/ali-md545/Intigriti-CTF-2023/assets/149575457/132f1092-1f7a-42d5-a141-dc5ac1e7c6c9)
![image](https://github.com/ali-md545/Intigriti-CTF-2023/assets/149575457/208c1ca2-3c2c-48e1-8285-87fdbbcd3617)
![image](https://github.com/ali-md545/Intigriti-CTF-2023/assets/149575457/b931c628-fdbc-451f-9142-7fa1d23e2da6)

The 'flag.txt' file was password protected, so I used the password I found earlier in Wireshark ‘5up3r_53cur3_p455w0rd_2022’ but it was wrong. So I went to Wireshark again and further analyzed the TCP stream.

![image](https://github.com/ali-md545/Intigriti-CTF-2023/assets/149575457/ff43a550-ed4d-42d0-abab-6ce2228a2da5)

I got this packet with an interesting bit of information. As it says, ‘update it accordingly’ and also in challenge information it said 'update the password', so I changed the password from 2022 to 2023 and voila, I opened the file and got the flag.
![image](https://github.com/ali-md545/Intigriti-CTF-2023/assets/149575457/d59c79bf-4fdc-4eee-ac81-6b2620580776)
 
