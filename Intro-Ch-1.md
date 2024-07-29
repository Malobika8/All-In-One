# What is a Computer Network?

Computers connected together. The Internet is basically a collection of these networks.

# How it all started?

We all remember the Cold War between the United States & Soviet Union. They were battling with one another in every field. The US gov created a program ARPA (Advanced Research Project 
Agency). They were supposed to do all the scientific discoveries. ARPA wanted some sort of a way to communicate with each other. They had facilities/buildings in various parts of 
United States. Hence, to communicate, they developed something called the "*ARPANET*". 

There were there at 4 places
- MIT
- Stanford
- UCLA (probably)
- University of Utah

They used TCP for this. 

Let's try to understand in a simple way.

Suppose we send an email to someone. It might require some steps. Or maybe we want to send a file and all data should be sent and not lost.
These are different types of things(email, video, secret files, etc) that we try to send over the Internet. So, different types of rules are required.
These rules that are set by people are known as "**Protocols**".

As years passed, more and more locations were added to ARPANET and started following "TCP/IP". However, it was only able to talk to one another via some protocols.

One problem happened. As this was a research project, many people wanted to share research papers. But it was not working in this particular domain. It was like we wanted to be able to
share some documents that reference some other documents. This automated sharing was missing previously. It needed some sort of a way so that if we click on a link, it takes
us to that resource. 

# World Wide Web

Tim Berners-Lee is a British computer scientist, mathematician, and engineer best known as the inventor of the World Wide Web. In 1989, while working at CERN, he wrote the first web 
browser, HTTP (Hypertext Transfer Protocol), and created the fundamental technologies behind the web, including HTML (Hypertext Markup Language) and URL (Uniform Resource Locator). 

WWW is a project that basically stores these documents & can be accessed via the *World Wide Web*. It allows us to access all these documents. It's a collection of all these pages.

Check out the world's first website.

<img width="909" alt="Screenshot 2024-07-29 at 10 11 30 PM" src="https://github.com/user-attachments/assets/9ec4d679-81ae-4fa5-a93b-e32db27f83e8">
<img width="791" alt="Screenshot 2024-07-29 at 10 14 41 PM" src="https://github.com/user-attachments/assets/c77ff4cd-9b4d-4378-a5a3-1952118056cc">

But there was a problem here. There was no search engine. This option was not available.

# Protocols

#### Why did we even want protocols?

Imagine we develop an application & someone in another country develops another. We might have some different rules about how our application can communicate with someone else's
application. They might have their own rules.

#### In such a case, can we communicate with each other? 

Not really!

Hence, it is important to have rules and regulations. 

#### Who writes/controls these? 

The "Internet Society". We can make submissions via RFC(Request for comments). We can have a document of our idea and submit it. It is usually submitted by high
professionals but anybody can submit till they have an idea.

<img width="1073" alt="Screenshot 2024-07-29 at 10 20 09 PM" src="https://github.com/user-attachments/assets/bd8bd838-604c-4886-91bd-6fa85ae63d8b">

To know more, check out - https://www.internetsociety.org/

### What is a Server?

Suppose we have a computer and we write "*google.com*" and click enter. It sends a request to the Google server and Google sends back a response to the computer.

<img width="887" alt="Screenshot 2024-07-29 at 10 24 06 PM" src="https://github.com/user-attachments/assets/8878d988-b392-46ae-b164-67710b270a23">

#### Fun fact: Various countries and continents across the world are connected via wires that are laid underground, under the ocean.

Our computer sends a request to the server (Google server in this case) and the server responds with a response. It sends back a Web page & a bunch of other things.
This doesn't mean our own computer cannot be a server. Our computer can act as a server as well as a client. 

#### When we write google.com, the web page loads. But how?

If we go to inspect, we will see so many things happening. 

<img width="1147" alt="Screenshot 2024-07-29 at 10 29 02 PM" src="https://github.com/user-attachments/assets/15c8c6c9-1c9c-47a4-aad6-14bb807d8364">

Coming back to the protocols, these are just rules defined by the "Internet Society". 

Basic protocols:
- TCP (Transfer control protocol): It ensures that the data reaches its destination & is not corrupted on the way.
- UDP (User Datagram Protocol): When we do not care if 100% of our data is reaching or not whomever we are sending. Example: Video conferencing.
- HTTP (Hyper Text Transfer Protocol): This is being used by the **Web browser (www)**. It basically defines the format of the data that is being transferred between web clients & servers.
  Client requests come to Servers and servers send back responses. These are all defined by "*HTTP*". How the server will respond is also defined by "*HTTP*".

#### How data is being transferred?
In computers, everything is 0 and 1. So it doesn't make sense to send the entire data at once.  When we load a Web page or watch a movie online, the data we get are in packets.
These are all individual calls and we get different packets of data.

<img width="1143" alt="Screenshot 2024-07-29 at 10 41 01 PM" src="https://github.com/user-attachments/assets/c1fe963c-fd45-438f-83e4-0ee6a7a50b94">


















