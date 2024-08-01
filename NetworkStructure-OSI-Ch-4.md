# Structure of Network

Let's imagine a real-world scenario. Order something online(amazon) and then Amazon will ship your order to a local delivery agent/company from where the order will be sent out/transported. Then we receive our order.

<img width="822" alt="Screenshot 2024-07-30 at 10 23 49 PM" src="https://github.com/user-attachments/assets/4e2be595-f71f-4514-a733-1372e110493c">

Similarly we request something, maybe a movie on YouTube or any video then YouTube will take care of it. It will prepare data and then give it to us in terms of transportation from its server. It will reach the server in our country and we will receive it.

This layer where we get the order is the "Application Layer" from which we are interacting. Ex: Whatsapp messenger

## OSI Model

It was developed to have a standard way for computers to communicate with each other. there are a few layers in this model.

* Application Layer: It's implemented in software (as the name suggests). AL protocols: TCP/IP
* Presentation Layer: The data is sent over from the application layer to the presentation layer. Data in the application layer will be in 
  the form of words, characters, letters & numbers, etc. The presentation layer will convert these characters to machine-representable         binary format. From ASCII to EBCDIC. This is known as "*Translation*". Before the data is transmitted further, it goes under encoding and    encryption. It also provides abstraction. Data is also compressed. Here SSL protocol is used.
* Session Layer: data is then sent to the Session layer. Session layer protocols basically help in setting up & managing the connections &     enable the sending & receiving of data followed by the termination of the connected sessions. Before a session is established, it will do    authentication (the server many times asks for a user & password). Then authorization takes place. This also assumes below layer will do     its work and take it forward.
* Transport Layer: Data is transferred from the session to the transport layer. It has its own protocol for how data is transferred like UDP   & TCP. It does it in three ways.
  - Segmentation: Data that is received from the session layer, will be divided into small data units called segments. Every segment will        contain the source and destination port number & the sequence number(it helps to reassemble the segments into the correct order). data       is transferred in chunks which is why we have sequence numbers.
  - Flow control: The transport layer controls the amount of data that is being transferred. Suppose the server is sending at 40mbps but the     client is receiving at 20 Mbps, data transfer will be slowed down.
  - Error control: some data packets got lost or corrupted. It adds something known as the checksum to every data segment. That way it can       figure out whether the data received by your friend was good or not.
  
    - Connection-oriented transmission: TCP (acknowledgment received)
    - Connectionless oriented transmission: UDP (faster) (acknowledgment not received/ packets lost)
      
* Network layer: It works for the transmission of the received data segments from one computer to another that is located in a different       network. The router lives over here. (now it communicates with other computers outside). Function: Logical addressing (IP addressing done    in the network layer is known as logical addressing). The network layer assigns the sender's and receiver's IP Address to every              segment & it forms an IP Packet. Routing protocols & transportation of packets happen at the network layer. Load balancing also happens
  here.
* DataLink Layer: It lets us communicate directly with the computers and hosts. It receives the data Packet from the Network layer & 
  this data Packet contains the IP Addresses of the sender & receiver. Physical addressing is done at the Datalink layer. Mac addresses of
  sender & receiver are added to the Data Packets to form a frame. A frame is a data unit of the datalink layer. Mac address is the 12-digit
  an alphanumeric number of the network interface of our computer. It's not like our computer has only one Mac address. Our computer's 
  Bluetooth may have another Mac address. Our computer's wifi may have another Mac address. The datalink layer adds a Mac address layer in a 
  frame and then transports that frame.

  <img width="564" alt="Screenshot 2024-07-31 at 3 18 02 PM" src="https://github.com/user-attachments/assets/abf381c6-4c31-4037-8919-f8fe0c5c5cb9">

* Physical Layer: It contains the hardware. Here we actually have mechanical wires. It transmits the bits from electrical signals. It works
  with cables and all those things.

  


























