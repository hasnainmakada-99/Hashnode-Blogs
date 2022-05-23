## Protocols in networking & what is LAN, MAN & WAN ?

Hey everyone so today we're gonna discuss about some of the protocols which are mostly used in networking, who defines theses protocols & what is LAN, MAN & WAN in networking.
So coming to our first topic of this blog..

### What are protocols in networking ?

So before moving on in depth of this topic let us understand what are protocols by giving me to you a practical example,

Suppose you are playing a football match with your friends so in the game of football there are going to be some rules with which you have to play the game right ? you cannot break the rules by any means otherwise you will get terminated from the game. Similarly there are also a set of predefined rules in computer networking by which we can only interact with the web and send data across the web, If we break the rules we cannot surf the internet.

In simple words protocols is an established set of rules which will determine that how the data will be sent across to different devices the same network

There are lots of protocols are defined on the web but here are some of few,
- TCP / IP Protocol (Transmission Control Protocol / Internet Protocol)
- UDP Protocol (User Datagram Protocol)
- FTP (File Transfer Protocol)
- Email Protocols (POP3, IMAP, SMTP)
- HTTP & HTTPs

So in this blog we are going to discuss about TCP / IP Protocol & UDP Protocol because they are most used protocols on the web for sending data.

Moving on to our 1st protocol,

#### What is TCP / IP Protocol ?

![tcpip.webp](https://cdn.hashnode.com/res/hashnode/image/upload/v1653218006974/3rws38eDC.webp align="left")

TCP/IP Protocol mainly know as transmission control protocol is a set of communications protocols used on the internet to send data across different devices on the same network, The TCP/IP protocol is connection-oriented protocol. The TCP/IP protocol ensures 100% delivery of data without the loss of any information. It will either send 100% data to the receiver's device or it will send no data.

For example: 
- Sending an email to someone
- Sending a text message to someone

There are mainly 5 layers in the TCP / IP model which are
- Application layer
- Transport layer
- Network layer
- Data link layer
- Physical layer

> Will discuss in my upcoming blogs

So this was the overview of the TCP/IP protocol used in networking.

Moving on to our 2nd protocol,

#### What is UDP Protocol ?

![udp.jpg](https://cdn.hashnode.com/res/hashnode/image/upload/v1653219354503/2wPnaXuni.jpg align="left")

UDP protocol or User Datagram Protocol is a part of the internet protocol suite so it can often be referred as UDP/IP protocol and one of main demerits of this protocol is that it is an unreliable & connection-less protocol, So it will not worry about the data of the user and it is usually fast compare to TCP/IP protocol. The UDP protocol does not guaranty that if the whole data will be sent to the user or not but it will sent the data quickly to user, So loss of data is its main factor over here.

For example:
- Video calling someone on WhatsApp or Facebook 
- Attending video conferences on zoom

So this was the overview of the UDP protocols used in networking.

Now let move on to our second topic of this blog which describes us what is LAN, MAN & WAN in networking.

### What is LAN, MAN & WAN ?

Let's break this topic into three parts, in first part we will discuss about LAN, in second part we will discuss about MAN, in third part we will discuss about WAN.

Coming to out first part of the topic,

#### What is LAN (Local Area Network) ?

Here's a simple demonstration image on LAN,

![lan(2).jpg](https://cdn.hashnode.com/res/hashnode/image/upload/v1653282186158/ORz7qWimu.jpg align="left")

LAN is a computer network which interconnects the computer and other devices within a limited area of network range. Generally the LAN is connected via TCP/IP ethernet or the WIFI to different devices. The LAN is normally limited to an organization such as a school or college and it ranges from 100 - 1000 meters only.

For Example: 
- WIFI router which we use in our home

Coming to our second part of the topic,

#### What is MAN (Metropolitan Area Network) ?

Here's a simple image demonstrating MAN,
![MAN.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1653282875421/-baksGzbC.png align="left")

A MAN is computer network which connects computer to a geographic region of the size of a metropolitan area or a city. As we can see from the above image each and every LAN is interconnected to MAN so in simple terms MAN is a collection of multiple LANs. The normal range of MAN can range from 5 - 50 Kms in diameter and it is more secure compare to LAN.

For example:
- Larger network that connects several buildings in the same city and town.

Coming to our third part of our topic,

#### What is WAN (Wide Area Network) ?

![WAN.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1653283376320/ndhmOxt2y.png align="left")

A WAN is a telecommunications network that extends over a large geographical area and they are often established by leased communication lines. As seen from the above figure we can see that multiple LAN connections share data through the WAN. The WAN ranges from 0 - 100,000 Kms.

Let's take a situation that a company which is based in New York wants to send data to another company which is based in London, How will they send data to such a far place ? so that's why WAN comes into the picture, the company will transfer data on to the web via the LAN, the LAN will establish a connection with the WAN and the WAN will again establish a connection with the receiver's LAN and then the receiver will receive the data

So the hierarchy of sending data will be like this,

Sender → LAN → WAN → LAN → Receiver

So I hope that I am able to clear your doubt regarding protocols and LAN, MAN & WAN in computer networking if you have any doubts feel free to reach me out on Twitter & Showwcase :)


