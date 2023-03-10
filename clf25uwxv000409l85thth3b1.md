---
title: "HTTP-Server using GO"
seoTitle: "HTTP-Server using GO"
seoDescription: "In this blog, I am going to teach you how to create an HTTP server using GoLang."
datePublished: Fri Mar 10 2023 06:32:33 GMT+0000 (Coordinated Universal Time)
cuid: clf25uwxv000409l85thth3b1
slug: http-server-using-go
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1678117545392/c0f309a6-c65e-46b2-abe4-98c394b6faa0.png
tags: go, http, apis

---

# Introduction

Hey everyone, I am Hasnain Makada and I am currently building out "[***Open source with Hasnain***](https://hasnainmakada-99.github.io/Open-Source-With-Hasnain/#/)" where I encourage every beginner to get started contributing to open source and network with amazing folks out there.

In this blog, I am going to teach you how to create an HTTP server with the help of Go and inside that server, we'll do some GET and POST operations on a fake API.

So let's get started

# Getting started

**Step 1:** Create a `go-http` folder by running `mkdir go-http` command.

**Step 2:** Navigate to the folder and open it inside your favourite code editor.

**Step 3:** Open the terminal inside the folder and run `go mod init example/web-service-gin`

The above command in step 3 will initialize the current directory as a Go module directory.

**Step 4:** Run the `go get` [`github.com/gin-gonic/gin@latest`](http://github.com/gin-gonic/gin@latest), This will install the Gin framework in go which is a web framework written in [GO](https://go.dev/). It features a martini-like API with performance that is up to 40 times faster thanks to the [**httprouter**](https://github.com/julienschmidt/httprouter).

Now that we've installed all the necessary dependencies and framework, Let's get started writing the actual Go code.

# Creating the data

Create a `main.go` file inside your current directory and import all the necessary dependencies and modules.

```go
package main
import (
	"net/http"
	"github.com/gin-gonic/gin"
)
```

The `net/http` module will help us check the server status and return all the items from the status and the `gin` framework will help us build the API more conveniently.

Then create the `structure` beneath the import declaration,

```go
type album struct {
	ID     string  `json:"id"`
	Title  string  `json:"title"`
	Artist string  `json:"artist"`
	Price  float64 `json:"price"`
}
```

The above structure will create an album of type struct inside which the ID, Title, Artist and Price of the API will be there. The `string` is the data type and the `json:"id"` will serialize each field into JSON type, After serializing the data might look like this

```json
{
    "id": "1234",
    "title": "XYZ",
    "artist": "Heisenberg",
    "price": 3.90
}
```

Beneath the struct declaration, create a map of albums which will contain the data with the datatype struct,

```go
var albums = []album{
    {ID: "1", Title: "Blue Train", Artist: "John Coltrane", Price: 56.99},
    {ID: "2", Title: "Jeru", Artist: "Gerry Mulligan", Price: 17.99},
    {ID: "3", Title: "Sarah Vaughan and Clifford Brown", Artist: "Sarah Vaughan", Price: 39.99},
}
```

Now we have our data ready to create the API, So now let's create the GET and POST requests on the above data which we created.

# Performing the GET and POST requests

Now create a function which will get all the albums in the form of JSON on the web beneath the `albums` map,

```go
func getAlbums(c *gin.context){
    c.IndentedJSON(http.StatusOK, albums)
}
```

The `c *gin.context` is a pointer which will help us directly get the address and get the data

The above function will first check the server status, If it is ok (status == 200) then it will serialize the albums map into JSON format on the web,

Now declare the main function and create a Gin router,

```go
func main() {
    router := gin.Default()
    router.GET("/albums", getAlbums)
    router.Run("localhost:8080")
}
```

The `gin.Default()` function returns a new instance of a Gin router with some default middleware already added, such as logging and recovery middleware. This is a convenient way to quickly create a working Gin router with some useful features already built-in.

We've called the GET method from the router and we've provided the route `/albums` inside the GET method and called the `getAlbums` functions inside that.

![Albums API](https://cdn.hashnode.com/res/hashnode/image/upload/v1678351400721/c2dc9653-33ba-4766-a5ce-7185df165729.png align="center")

As you can see from the above image, our data albums are now serialized into JSON format.

Now we're going to perform the post request. Create a new function named `postAlbums` beneath the `getAlbums` function

```go
func postAlbums(c *gin.Context) {
	var newAlbum album
	if err := c.BindJSON(&newAlbum); err != nil {
		return
	}

	albums = append(albums, newAlbum)
	c.IndentedJSON(http.StatusCreated, newAlbum)
}
```

The above function takes gin pointer for helping use serialize into JSON format, inside this function, we've first declared a variable named `newAlbum` which is of the type `album` .

Then we've conditional operation which will declare the `err` variable and with the `BindJSON` method, it will convert the input into JSON format and it will also check that the `err` is `nil` then only it will return otherwise it will not return.

Lastly, we have appended the `newAlbum` into our map of `albums` and indented the `newAlbum` into JSON format on the web.

Now perform the POST request by running the below command,

```bash
 Invoke-WebRequest -Uri http://localhost:4000/albums `
>>     -Method POST `
>>     -ContentType "application/json" `
>>     -Body '{"id": "4","title": "The Modern Sound of Betty Carter","artist": "Betty Carter","price": 49.99}' `
>>     -Headers @{"Accept" = "application/json"; "User-Agent" = "Mozilla/5.0"}
```

And it will get inserted into the API,

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678352409849/ff8c7220-c29e-461c-b1d4-ab6c3adf23ba.png align="center")

We're now performing the next operation in which we will get the data from the API by requesting a single ID,

Create a new function named `getAlbumsbyID` beneath the `postAlbums` function,

```go
func getAlbumsbyID(c *gin.Context) {
	id := c.Param("id")

	for _, value := range albums {
		if value.ID == id {
			c.IndentedJSON(http.StatusOK, value)
			return
		}
	}

	c.IndentedJSON(http.StatusNotFound, gin.H{"message": "Album Not Found"})
}
```

In this function, we've first got the param id and stored it inside a new variable name `id`, Then we looped the map `albums` and checked that the `value.ID == id` then we will print only that part of the API inside the browser, otherwise, we will set the status to not found and print an error message

The `gin.H{}` method will help us insert the headers inside the browser.

With matching params 👇

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678352748149/c79d617a-c1c0-4021-92cf-17633c69d533.png align="center")

With an invalid param id provided 👇

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678352806098/2fc2aa3d-93bd-4a2f-8014-4c15816c5cff.png align="center")

So we have successfully performed all the GET and POST operations which we were required while building the API.

> **Note:** This is just a demo of the API, but you can add more functionalities and host the API on web and use it for further usage.

Here's the complete code 👇

```go
package main

import (
	"net/http"

	"github.com/gin-gonic/gin"
)

// album represents data about a record album.
type album struct {
	ID     string  `json:"id"`
	Title  string  `json:"title"`
	Artist string  `json:"artist"`
	Price  float64 `json:"price"`
}

// albums slice to see record album data.
var albums = []album{
	{ID: "1", Title: "Blue Train", Artist: "John Coltrane", Price: 56.99},
	{ID: "2", Title: "Jeru", Artist: "Gerry Mulligan", Price: 17.99},
	{ID: "3", Title: "Sarah Vaughan and Clifford Brown", Artist: "Sarah Vaughan", Price: 39.99},
}

func getAlbums(c *gin.Context) {
	c.IndentedJSON(http.StatusOK, albums)
}

func postAlbums(c *gin.Context) {
	var newAlbum album
	if err := c.BindJSON(&newAlbum); err != nil {
		return
	}

	albums = append(albums, newAlbum)
	c.IndentedJSON(http.StatusCreated, newAlbum)
}

func getAlbumsbyID(c *gin.Context) {
	id := c.Param("id")

	for _, value := range albums {
		if value.ID == id {
			c.IndentedJSON(http.StatusOK, value)
			return
		}
	}

	c.IndentedJSON(http.StatusNotFound, gin.H{"message": "Album Not Found"})
}

func main() {
	router := gin.Default()
	router.GET("/albums", getAlbums)
	router.GET("/albums/:id", getAlbumsbyID)
	router.POST("/albums", postAlbums)
	router.Run("localhost:4000")

}
```

# Conclusion

We've created an HTTP server using GO and also created an API with GO inside where we performed all the GET and POST requests. If you have any doubts related to this, feel free to reach out on [Twitter](https://twitter.com/Hasnain_Makada) and [Showwcase](https://showwcase.com/hasnainmakada-99)