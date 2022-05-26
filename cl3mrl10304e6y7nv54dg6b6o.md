## Introduction to HTTP methods & difference between IPV4 and IPV6

### Introduction

Hey everyone [in the previous blog](https://hasnainm.hashnode.dev/topologies-models) we talked about what are topologies in networking and discussed some of the networking models which are used in computer networks.

Today we are going to discuss about the last and final topic of the [computer networking series](https://hasnainm.hashnode.dev/series/computer-networking) in which I'm going to explain you about what is HTTP, what are HTTP methods & difference between IPV4 vs IPV6.

Lets begin with our first topic:

### What is HTTP & what are some of its methods ?

HTTP stands for Hyper Text Transfer Protocol is an application layer protocol in the internet protocol suite. The HTTP is used for transmitting hypermedia documents such as HTML and it was designed to make communication between browser and web servers. HTTP is a stateless protocol means the server will not keep any data between 2 requests.

The HTTP contains mainly 4 methods in it:
- GET
- POST
- PUT
- DELETE

![http.jpg](https://cdn.hashnode.com/res/hashnode/image/upload/v1653551717179/-MbKgSGms.jpg align="left")

Let's breakdown each method

####  HTTP GET method

The GET method is used to request the server for some data, It can only be used to retrieve response from the server and should not send any data to the server. The GET method is the least secure method, because if the user tries to send data via the GET method, the data will be clearly visible in the browsers URL and we can send maximum 2000 characters data via the GET method.

The GET method can be used to bookmark a webpage because the data is clearly visible in the URL.

#### HTTP POST method

The HTTP POST method is the most secure method to send data to the server from an HTTP client. The HTTP method does not display the data in the URL unlike GET method and it is mainly used in login forms or while submitting some data to the server from the client side. The POST method does not have any limit on sending data, the user can send as much data as they want. The POST cannot be used to bookmark a web page as the data is not visible in the URL.

#### HTTP PUT method

The HTTP PUT method is used to update data which is in the server it can also be used to send data to the server similarly like post method but it can not send duplicate data again to the server, it will update the same data again. That is the main reason why PUT method is mainly used to update data onto the server and should not be used to send data.

#### HTTP DELETE method

The HTTP DELETE method is used to delete data from the server, for deleting data it should contain a key to map towards the data to the server and after it matches the key it will delete the data.

That was all about the HTTP and its method which are used on the internet to interact with the server.

Let's move on to the second topic:

### Difference between IPV4 & IPV6

Here's a table which explains the difference:

![table.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1653554118402/x6Y5_lpj1.png align="left")

### Conclusion

I hope now you have understand the basics of HTTP and its method and also about IPV4 and IPV6, if you have any doubts feel free to reach me out on [Showwcase](https://www.showwcase.com/hasnainmakada-99) & [Twitter](https://twitter.com/Hasnain_Makada) 
