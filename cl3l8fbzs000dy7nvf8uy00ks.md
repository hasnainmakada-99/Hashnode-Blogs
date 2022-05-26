## Introduction to Topologies & networking models in computer networking

### Introduction

Hey everyone [in the previous blog](https://hasnainm.hashnode.dev/protocols-in-networking) we discussed about what are protocols in networking and what is LAN, MAN & WAN in networking. Today we are going to discuss about the most crucial things in networking which are topologies and the OSI & TCP/IP model.

So this blog is also divided into 2 topics, In the first topic we will discuss about topologies and in the second topic we will discuss about the models in networking.

lets begin with our first topic:

### What is topologies & what are the types of topologies in networking ?

Topologies are a arrangement of elements of a communication network. what this means ? let me explain it to you, networking topologies is a structure which will define that how each and every devices will be connected to each other. It is basically the structure of the network and how all the components are interconnected to each other.

There are basically 5 main topologies are there in networking:
- Bus Topology
- Ring Topology
- Star Topology
- Tree Topology
- Mesh Topology

Lets break down each and every topology and see how are they useful compare to others:

#### Bus Topology

Here's a simple demonstration image referring bus topology:

![bus.jpg](https://cdn.hashnode.com/res/hashnode/image/upload/v1653376667089/4LzFj3wZ7.jpg align="left")

As you can see from the above image in the bus topology each and every device is connected to a single backbone cable, If the cable breaks down entire system will go fail.

In the bus topology at a time only one device can send information. They are used for small, cheap and often temporary network which does rely on high data - transfer speed.

Pros:
- Works very efficiently when there is a small network.

#### Ring Topology

Here's a simple demonstration image referring ring topology:

![ring.jpg](https://cdn.hashnode.com/res/hashnode/image/upload/v1653376956185/KYF49_vVl.jpg align="left")

As you can see from the above image in the ring topology there is a ring like structure between devices and each and every device is connected to one another. It has also the same issue like bus topology, If one link get broken the entire system will fail.

In the ring topology lots of unnecessary calls are made between systems and whenever a system sends a data it will travel the whole ring and then it will delivered to the destination system.

Pros:
- Equal access to all resources
- Token passing makes the ring topology better as it can handle heavy traffic compare to bus topology

#### Star Topology

Here's a simple demonstration image referring star topology:

![star.jpg](https://cdn.hashnode.com/res/hashnode/image/upload/v1653377500776/oRTncBc2i.jpg align="left")

As you can see from the above image in the star topology each and every device is connected to a central server or hub. If the central server will go down entire system will go down. Each and every device will be connected via ethernet cable, so the cost of caballing will be high over here

The star topology is one of the most common computer network topologies, and it is also far more reliable than others because if one cable or device fails it will not affect the other devices, they will continue to operate and they can even handle heavy traffic. 

Pros:
- Easy to add new devices just.
- Does not affect if a single device fails.

#### Tree Topology

Here's a simple demonstration image referring tree topology:

![tree.jpg](https://cdn.hashnode.com/res/hashnode/image/upload/v1653378077429/LQTnBuUlU.jpg align="left")

As we can see from the above image in the tree topology each and every device will be connected to the central hub and the central hub will be connected to a backbone cable from. So we can say that tree topology is a combination of bus & star topology, and it is also known as star bus topology.

In the tree topology if one device goes down it will not affect other devices as they are connected to the central hub, but if the backbone cable goes down it will fail the central hub as well as the devices with which it is connected too. The structure of the tree topology is more complex compare to other topologies.

Pros:
- Highly secure compare to others.
- Easy maintenance and fault identification.

#### Mesh Topology

Here's a simple demonstration image referring mesh topology:

![mesh.jpg](https://cdn.hashnode.com/res/hashnode/image/upload/v1653381567416/uqOUb1tD_.jpg align="left")

As we can see in the above image in mesh topology each and every computer will be connected to each other and no central hub or backbone cable is present in the mesh topology. Even though each device is connected to one another failing of a single device wont affect other devices and that's the main advantage of mesh topology.

We can easily add new devices in this topology and they wont even disrupt the whole network. Dedicated point to point link is there in each device so there will be no traffic issue over here and it provides high privacy and security. It is also expensive compare to others.

Pros:
- Fault identification is straightforward.
- Failing of a single device will not interrupt the whole network.

So that was all about the overview of topologies in the first topic how do they work what are their advantages etc.

Now moving on to our second topic of the blog in which I am going to explain you the OSI & TCP/IP models of computer networking.

So starting off with the OSI model first:

### What is OSI Model in computer networking ?

OSI stands for Open Systems Interconnection Model and it is a conceptual model which is used to describe the functions of a networking system. The OSI model contains 7 layers in it starting from the application layer and ending at physical layer.

Here's the OSI Model:

![osi.jpeg](https://cdn.hashnode.com/res/hashnode/image/upload/v1653454334017/pFAFNOpEN.jpeg align="left")

As we can see in the above image the data is transmitted from the application layer and the end user receives it with the help of the physical layer. But how the data is transmitted and received ? lets break down each and every layer,


#### Physical Layer (Layer - 1)

Physical layer is the first layer in the OSI model. It is the first layer from which the data is delivered to the user after it has been transmitted by the application layer. The physical layer consist of devices such as routers, cable, wires etc.

#### Data Link Layer (Layer - 2)

The data link layer is the protocol layer in the OSI model which handles the moving of data into and out of physical link in a network.

The data link layer is used to do physical addressing over here, now physical addresses means the MAC (Media Access Control) addresses of the user and these addresses of sender & receiver are assigned to a data packet which are called frames. Frames are a unit of data, transmitting over the data link layer, In simple terms it is a container which consist of the mac addresses of sender & receiver inside it.

#### Network Layer (Layer - 3)

The Network layer transmits the data segments which you received from the transport layer from one computer to another. Each data segments are located on different networks. In the Network layer logical addressing, Load balancing and routing performed.

Logical Addressing: A logical address helps you access a network device by using an address that you provide and they mainly generated by CPU.

Load Balancing: It is the process of distributing network traffic across multiple servers.

Routing: It is used to deliver the network packets by choosing the most optimal path from one network to another, It is mainly performed in the network layer

#### Transport Layer (Layer -4)

The Session layer send data to the transport layer, The transport layer divides the data into small units called segments. Every segment has a source & destination's port number as well as a sequence number. The Session layer also handles flow control & error control.

Flow Control: It is the management of the flow of data between computer and network devices and sometimes in the node of the network, so the data can be handled at an efficient pace.
 
Error Control: It is a technique of detecting and correcting blocks of data during communication. So that no error should be there while the communication is happening.

#### Session Layer (Layer - 5)

The session layer helps in setting up the connections and enables the sending and receiving of data followed by a termination of connected sessions. All the authentication and authorization takes place inside the session layer.

After the session layer has authorized it will transmit the data which it has collected to the transport layer.

#### Presentation Layer (Layer - 6)

The presentation layer converts the data, messages received from the application layer into a machine representable binary format. All the encoding, encryption happens inside the presentation layer and it also provides data abstraction, compression and translation.

Data Abstraction: Abstraction layer exposes the interface and hides the logical implementation of the data it has.

Data Compression: It is the reduction in the number of bits needed to represent the data.

Data Translation: It uses NAT (Network Address Translation) techniques to convert IP addresses of different computers in a local network to a single IP address.

#### Application Layer (Layer - 7)

The application layer is implemented in software. It consist the normal applications such as browsers, chatting apps etc. This layer lies in our devices.

----

So that was all about the OSI model and we've dived deep into it. I hope you have understand it by now.

So let's move on to TCP/IP model now:

### What is TCP/IP model in computer networking ?

TCP stands for Transmission Control Protocol model and it is basically known as the internet protocol suite. The TCP/IP model is a concise version of the OSI model as we have seen in the OSI model it consist of 7 layers where as in TCP/IP model it only consist of 5 layers

The TCP/IP model is the most used model in the networking architecture and it is more reliable than the OSI model. The OSI model gives us a logical understanding that how each and every layer operates.

![tcp.jpg](https://cdn.hashnode.com/res/hashnode/image/upload/v1653460343770/V9IC1RgwH.jpg align="left")

As we can see from the above image in the TCP/IP model the presentation layer and the session layer are not present which means the application layer directly sends the data to the transport layer and then after the normal process begins as we've seen in the OSI model.

Lets break down each and every layer:

#### Physical Layer (Layer -1)

The physical layer is the first layer in the TCP/IP model and it basically consist of all the networking devices such as routers, cables, wires etc.

The physical layer is used to transmit data in human - readable format back to the application layers or software.

#### Data Link Layer (Layer - 2)

The Data link layer performs the same as we've seen in the OSI Model and there is nothing new in over here to explain.


#### Network Layer or Internet Layer (Layer - 3)

The Network layer performs the same procedure as in OSI model, performs logical addressing, routing, load balancing etc. and transmits the received data segments from one computer to another.

#### Transport Layer (Layer - 4)

The transport layer also performs the same operations as in OSI model divides the data received into small data units known as segments and so on..

#### Application Layer (Layer - 5)

The Application layer plays the main role in the TCP/IP model, it does the work of both the presentation layer and the session layer as well both in the user's device. And after performing both the processes only it will move to other layers.

The Application layer consist of the software, applications as well.

### Conclusion

So I hope now you have the basic understanding of the topologies and of the OSI & TCP/IP model as well, If you have any doubts regarding any of the topics I've released till now you can reach me out on [showwcase](https://www.showwcase.com/hasnainmakada-99) and [twitter](https://twitter.com/Hasnain_Makada) :)




