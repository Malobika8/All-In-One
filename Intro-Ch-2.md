### When we write "google.com", how does it find which server to connect to?

The "*IP Address*" identifies these computers and servers. Every device on the internet that can talk to each other has an "*IP Address*".

#### Format: X.X.X.X (every single X can have numbers from 0-255)

To check the IP(Internet Provider) Address of our computer, use the command

```
curl ifconfig.me -s
```

Suppose we have 4 different computers connected to a Router/modem (wifi). 

#### Will they have the same IP address or a different one?

We have ISPs (Internet service providers) like Airtel, Jio & many more. They provide us with a Router/Modem. It has a global IP address. Now, all devices connected to this modem have the 
same IP Address. 

The modem gives IP addresses to these as well. They are known as local IP Addresses.

#### How does it do it? - DHCP

(Dynamic Host Configuration Protocol) . It assigns IP addresses using the DHCP protocol.

If we request *Google*, it only sees the global IP address for all the devices connected to the modem.

<img width="1038" alt="Screenshot 2024-07-30 at 10 22 28 AM" src="https://github.com/user-attachments/assets/b2178c4a-9034-4b9a-81c8-bed965472aae">

When it gets the response, the Router decides who was the one who had this request. It does it using NAT(Network Access Translator).

IP Address decides which device to send the data to. 

## Ports 
#### But how is it decided which application to send the data to in that device?

It is done using Ports. These applications might have the same IP address but the port is what differentiates them.

If we talk to our friend using our chat application, we'll have an IP address & Port. IP address determines where our computer is located & Port number locates which application
we're using in our computer.

<img width="862" alt="Screenshot 2024-07-30 at 10 28 10 AM" src="https://github.com/user-attachments/assets/b947c0df-c1cf-453e-9713-508e82837d7c">

- The port number is a 16-bit number. Total Port numbers that are possible are 2^16 which is something around 65000.
- Webpages use HTTP. So, there is some sort of port number defined for it. All the HTTP that we do happens on port 80. It is a very defined and well-known port.
- Ports that are from 0-1023 are reserved ports. If we create our application & intend on hosting it on port 80, we cannot do that as it is reserved for HTTP.
- 1024-49152: They are also registered for some applications.
- Every SQL Server that we run on our system has a port of 1433.
- We can use the remaining ones.

<img width="1045" alt="Screenshot 2024-07-30 at 11 12 45 AM" src="https://github.com/user-attachments/assets/027a8ff1-b940-4e65-ace9-d081f179c92e">

## Internet Speed

- What do we mean by 1mbps speed? - We can transfer 1 megabits per second i.e. 1000000 bits/sec.
- 1gbps = 10^9 bits/sec.
- 1kbps = 1000 bits/sec. (very slow)
- Upload: When we send data from our computer to another.
- Download: Someone sends data to us.


















