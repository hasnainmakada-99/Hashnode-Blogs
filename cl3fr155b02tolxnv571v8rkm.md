## What is Computer Networking & Client - Server architecture

### What is Computer Networking ?
A computer network is a system that connects to numerous other computers to share data and resources, but before moving on to computer networking let us understand what is Internet ?

#### What is Internet ?
Internet is collection of computer networks, That's it. lots and lots of computer are connected to one another and they share data via the web and that is how internet was formed and they depend on various protocols defined by the internet society

### How Computer Networking is useful in general ?
So let us be in a situation where your internet is not working and your ISP (Internet Service Provider) is not picking up your calls, what will you do ?, The problem with the WIFI not working is related with the modem (device which is used to distribute internet to various devices) and the simple solution is to reset to router, but you don't know how to do it ? So that's where Computer Networking comes into the picture, if you know networking you can fix the router otherwise you'll just have to depend on your ISP every time.

#### How the internet works ?
Here's a simple demonstration image taken from the web,

![internet.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1653127367152/Mefa7yGX-.png align="left")

Client send a request to the server and server sends a response back to the client, That's it that's how the internet works.

The request and response objects are HTTP Request & HTTP Response.

#### Now lets discuss about what are some of the questions which are asked in interview regarding computer networks ?

Here are the top 10 most frequent questions asked in interviews,


- Q1. What do you mean by Network ?
- Q2. What do you mean by Node?
- Q3. What do you mean by Network Topology ?
- Q4. What is a Router ?
- Q5. What is the OSI model ?
- Q6. Explain the Different layers of the OSI model.
- Q7. Explain the different Layers of TCP/IP Model.
- Q8. What do you mean by TCP and UDP ?
- Q9. What do you mean by DNS ?
- Q10. What do you mean by Classes of Network?

### What is client - server architecture ?
Here's an image which explains what is client - server architecture,

![client.jpeg](https://cdn.hashnode.com/res/hashnode/image/upload/v1653127953170/mGQc0hfYw.jpeg align="left")

client - server architecture is a part of computer networking in which a client interacts with a server and the server in return responds back to the client.

For example: suppose user opens his favorite web browser in his system and types www.google.com in the search bar of the browser and then hits enter, what will happen ?

The browser will interact with the server of the google and it will tell the server that this user has requested google.com and the server will the give response to the web browser and the web browser will immediately send the respond to the user 

So the hierarchy will be like this,

User → Web Browser → Server → Web Browser → User

Now we have seen the practical aspect of the architecture now let's understand the technical aspect too,

Whatever we discussed in the practical aspect will happen behind the background, it will not be visible to users. There are mainly 2 objects HTTP Request & HTTP Response with which this process is possible and we can make requests on the web. The HTTP class was initiated by sir Tim - Berners lee in CERN 1989 and is known as Hypertext Transfer Protocol

The HTTP Request class will interact with the server and the server will send the response via the HTTP Response class and if by chance the server is not able to send response in the specific time then it will throw error to the user and the error are status codes in networking which I will discuss in my upcoming blogs

So I hope you'll understand the basics of computer networking by now and If you have any doubts then leave a comment I'll surely interact with you :)









