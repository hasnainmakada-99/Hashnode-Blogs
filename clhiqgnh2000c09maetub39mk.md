---
title: "Creating a Discord Bot with JavaScript"
seoTitle: "Creating a Discord Bot with JavaScript"
seoDescription: "In this blog, we are going to create a discord bot which will post motivational and encouraging messages inside your discord server."
datePublished: Thu May 11 2023 06:13:03 GMT+0000 (Coordinated Universal Time)
cuid: clhiqgnh2000c09maetub39mk
slug: creating-a-discord-bot-with-javascript
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1683527507675/3c8aa13f-7b97-4551-8241-6dae84677c18.png
tags: bot, javascript, discord, discordjs

---

# Introduction

Hey everyone, I am Hasnain Makada and I am currently a **Founding Creator** and a **Chief Creative Officer** at [Showwcase](https://showwcase.com) where I create meaningful content for the community and build a global developer community network for folks around the world to get started with it. I am also currently building out ['*Open Source with Hasnain'*](https://oswh.tech/) where each and every beginner regardless of their field can get started contributing to open source and network with amazing folks.

In this blog, we are going to build a discord bot which can post motivational quotes and encouraging messages inside your discord server. If the user prompts '**$inspire'** then it will reply with a motivational quote to the user and If the user replies with any sad words, it will encourage the user.

**Sounds interesting!** then let's get started building the bot.

# Choosing the development environment

For creating this bot, we are going to choose [**Replit**](https://replit.com) which is an online integrated development environment. You can choose to develop this bot manually inside VS Code, but for your ease of access, I prefer Replit as it automatically installs all the dependencies manually when you use them in your code.

The list of dependencies which we are going to use.

* [@replit/database](https://www.npmjs.com/package/@replit/database) - Replit database client is a simple way to use Repl.it Database in your Node.js repls. It uses `await/async`.
    
* [discord.js](https://www.npmjs.com/package/discord.js) - discord.js is a powerful [**Node.js**](https://nodejs.org/) module that allows you to easily interact with the [**Discord API**](https://discord.com/developers/docs/intro).
    
* [express](https://www.npmjs.com/package/express) - Fast, unopinionated, minimalist web framework for [**Node.js**](http://nodejs.org/).
    

The above 3 dependencies are the most important for our discord bot because our bot will be completely dependent on that itself.

You can create a node js app inside your local machine and start the project after installing all the dependencies.

# Creating the Bot

In Replit, create a new Repl and select the **NodeJS** Template, it will automatically specify that the application is server-based and will provide your the boilerplate code of node js with **index.js** and **package.json** files preinstalled.

Similarly, on your local machine create a new directory and open it inside your terminal and run `npm install <dependency-name>` put the name of the above 3 dependencies and they will get installed.

Now it's time to create our bot inside the [**Discord Developer portal**](https://discord.com/developers/applications)**.**

Click on `New Application` , fill in the name of your application and create it.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683535532371/7e5736d1-a400-43f9-beb4-48c433559147.png align="center")

You'll be then redirected towards your newly created application, go to **OAuth2** from the side panel and select the **Bot** Scope and then select all the text permissions as I have done it.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683529996957/0cb907ed-28cc-4c27-863b-977cc5f9530f.png align="center")

After selecting all the permissions, create a new server inside your discord account for testing and invite this bot with the generated URL from your developer portal 👇

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683530065634/b2f80188-50ae-418d-941e-1bb073e67e7f.png align="center")

It will ask for a captcha and it will be inside your server.

Now the discord side work is done by ourselves, now let's code the bot.

Don't forget to enable all the privileged gateway intents as well.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683530578433/9f0ee358-6120-4a28-b4ec-5f5bb8a63bbc.png align="center")

Copy the **BOT Token** from the developer portal

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683530225801/031a7db2-104f-4a8b-af81-2de2e9a15140.png align="center")

and create a **.env** file inside your node js app put this token in the below format 👇

```apache
TOKEN=<your-token-here>
```

Now open the `index.js` file and initially get all the dependencies and create the objects.

```javascript
const { Client, GatewayIntentBits } = require("discord.js");
const mySecret = process.env['TOKEN']
const keepAlive = require("./server");
const Database = require("@replit/database");
```

For posting motivational quotes, we're going to use the [Zenquotes](https://zenquotes.io/) API. It is a free-to-use API and it will generate a random quote every time a new request is generated

[https://zenquotes.io/api/random](https://zenquotes.io/api/random)

The above API will throw the below **JSON** in response

```json
[
    {
        "q": "Don't give up the fight, Stand up for your rights.",
        "a": "Bob Marley",
        "h": "<blockquote>&ldquo;Don't give up the fight, Stand up for your             rights.&rdquo; &mdash; <footer>Bob Marley</footer></blockquote>"
    }
]
```

The `q` stands for a quote, `a` stands for author and `h` is a blockquote which we are not going to use, we just need the first 2 elements for our bot.

Now after requiring all the dependencies, paste the code below.

```javascript
const db = new Database();

const client = new Client({
  intents: [
    GatewayIntentBits.Guilds,
    GatewayIntentBits.GuildMessages,
    GatewayIntentBits.MessageContent,
  ],
});

const sadWords = ["sad", "depressed", "unhappy", "angry"];

const starterEncouragements = [
  "Cheer up!",
  "Hang in there.",
];
```

The above code initializes a few variables and creates instances of two different classes: `Database` and `Client`.  
The `Database` instance is created with the `new` keyword, which creates a new object of the `Database` class. The `Database` class is the replit's database class and it is used to interact with the replit database.

The `Client` instance is also created with the `new` keyword, and is initialized with an object that contains some configuration options. Specifically, the `intents` property is set to an array that contains three different `GatewayIntentBits` values. These values likely represent different types of actions that the client will be able to take when it is connected to a Discord gateway. For example, `GatewayIntentBits.Guilds` may allow the client to receive information about guilds (i.e. servers) that the bot is a member of, while `GatewayIntentBits.GuildMessages` may allow the client to receive messages sent to those guilds.

The `sadWords` variable is an array of strings that contain words which are associated with negative emotions.

The `starterEncouragements` variable is an array of strings that contain messages of encouragement that are sent to users in response to negative messages. For example, if a user sends a message containing one of the words in `sadWords`, the bot will respond with one of the messages in `starterEncouragements`.

After defining all the arrays, paste the code below 👇

```javascript
db.get("encouragements").then((encouragements) => {
  if (!encouragements || encouragements.length < 1) {
    db.set("encouragements", starterEncouragements);
  }
});

db.get("responding").then((value) => {
  if (value == null) {
    db.set("responding", true);
  }
});
```

The above code will first set the encouragements array inside the replit database, it will first check whether the encouragements exist inside the database or not and based on that will set the `starterEncouragement` inside the replit database.

Then the code will set the responding nature of the bot inside the replit database, it will initially set the value to true which means that the bot is responding.

After setting up the encouragement and responding nature of the bot, let's fetch the API,

Paste it below after the above code 👇

```javascript
const myUrl = "https://zenquotes.io/api/random"
async function getQuote() {
  const res = await fetch(myUrl);
  const data = await res.json();
  return data[0]["q"] + " -" + data[0]["a"];
}
```

The above function is an async-await function which will use the fetch API of JS and after fetching the data from the API, it will return the necessary elements as we discussed above.

After fetching the API, paste the below code 👇

```javascript
function updateEncouragements(encouragingMessage) {
  db.get("encouragements").then((encouragements) => {
    encouragements.push([encouragingMessage])
    db.set("encouragements", encouragements)
  });
}

function deleteEncouragements(index) {
  db.get("encouragements").then((encouragements) => {
    if (encouragements.length > index) {
      encouragements.splice(index, 1);
      db.set("encouragements", encouragements);
    }
  });
}
```

The above code defines two functions, `updateEncouragements` and `deleteEncouragements`, that interact with a database using the `db` object.

`updateEncouragements` takes in an `encouragingMessage` parameter, which is a string representing a new encouraging message to be added to the list of encouragements stored in the database. The function first calls `db.get("encouragements")` to retrieve the current list of encouragements from the database. The `get` method returns a Promise, which means that the code inside the `then` method is executed once the database has returned the current list of encouragements. Once the current list of encouragements is retrieved, the function pushes the new `encouragingMessage` string onto the end of the list and then uses `db.set("encouragements", encouragements)` to update the list of encouragements in the database with the new, updated list.

`deleteEncouragements` takes in an `index` parameter, which is an integer representing the index of the encouraging message to be deleted from the list of encouragements stored in the database. The function first calls `db.get("encouragements")` to retrieve the current list of encouragements from the database. The `get` method returns a Promise, which means that the code inside the `then` method is executed once the database has returned the current list of encouragements. Once the current list of encouragements is retrieved, the function checks if the `encouragements` list has a length greater than the `index` parameter. If it does, then the function uses the `splice` method to remove the encouragement message at the specified `index` and update the list of encouragements in the database with the new, updated list using `db.set("encouragements", encouragements)`. If the `encouragements` list has a length less than or equal to the `index` parameter, then no action is taken and the list of encouragements in the database remains unchanged.

After defining the update and delete functions of encouragements, Let's integrate our code with the discord bot.

```javascript
client.on("ready", () => {
  console.log(`Logged in as ${client.user.tag}`);
});

client.on("messageCreate", (message) => {
  if (message.author.bot) return;

  if (message.content === "$inspire") {
    getQuote().then((quote) => message.channel.send(quote));
  }

  db.get("responding").then((responding) => {
    console.log("responding:", responding);
    if(!responding){
      db.set("responding", true)
    }
    if (responding && sadWords.some((word) => message.content.includes(word))) {
      console.log("message contains sad word:", message.content);
      db.get("encouragements").then((encouragements) => {
        console.log("encouragements:", encouragements);
        const encouragement =
          encouragements[Math.floor(Math.random() * encouragements.length)];
        console.log("encouragement:", encouragement);
        message.reply({
          content: `${encouragement}`,
        });
      });
    }
  });

  if (message.content.startsWith("$new")) {
    encouragingMessage = message.content.split("$new ")[1]
    updateEncouragements(encouragingMessage)
    message.channel.send("New encouraging message added.")
  }

  if (message.content.startsWith("$del")) {
    index = parseInt(message.content.split("$del ")[1])
    deleteEncouragements(index)
    message.channel.send("Encouraging message deleted.")
  }

  if (message.content.startsWith("$list")) {
    db.get("encouragements").then((encouragements) => {
      if (encouragements && encouragements.length > 0) {
        const messageText = encouragements.join("\n");
        message.channel.send(`List of encouragements:\n${messageText}`);
      } else {
        message.channel.send("No encouragements found.");
      }
    });
  }


  if (message.content.startsWith("$responding")) {
    value = message.content.split("$responding ")[1]
    if (value && value.toLowerCase() === "true") {
      db.set("responding", true)
      message.channel.send("Responding is On")
    } else {
      db.set("responding", false)
      message.channel.send("Responding is Off")
    }
  }

});
```

Let's break down the above code step by step,

1. The code defines an event listener for the `"messageCreate"` event using the Discord.js library. This listener is triggered whenever a message is sent in the server.
    
2. The first conditional statement checks if the message was sent by a bot. If it was, the code returns without taking any further action.
    
3. The second conditional statement checks if the content of the message is equal to `"$inspire"`. If it is, the code calls the `getQuote()` function, which is not shown in this code snippet, to retrieve an inspirational quote and sends it as a message to the same channel where the `"$inspire"` message was sent.
    
4. The next block of code retrieves the value of the `"responding"` key from a database using the `"db"` variable. If "responding" is false, the code sets `"responding"` to true in the database.
    
5. The next conditional statement checks if `"responding"` is true and if the message contains any of the words in the `"sadWords"` array. If both conditions are met, the code retrieves a list of encouraging messages from the database using the `"encouragements"` key. The code then selects a random encouraging message from the list and sends it as a reply to the message containing the sad word.
    
6. The next conditional statement checks if the message starts with `"$new"`. If it does, the code extracts the encouraging message from the message content and calls the `"updateEncouragements"` function, passing the encouraging message as an argument. This function is not shown in this code snippet but is assumed to add the new encouraging message to the `"encouragements"` list in the database. The code then sends a message to the same channel indicating that a new encouraging message has been added.
    
7. The next conditional statement checks if the message starts with `"$del"`. If it does, the code extracts the index of the encouraging message to be deleted from the message content and calls the `"deleteEncouragements"` function, passing the index as an argument. This function is not shown in this code snippet but is assumed to remove the encouraging message at the specified index from the `"encouragements"` list in the database. The code then sends a message to the same channel indicating that the encouraging message has been deleted.
    
8. The next conditional statement checks if the message starts with `"$list"`. If it does, the code retrieves the "encouragements" list from the database using the `"encouragements"` key. If the list is not empty, the code joins the list elements with new lines and sends the resulting message to the same channel. If the list is empty, the code sends a message indicating that no encouraging messages were found.
    
9. The last conditional statement checks if the message starts with `"$responding"`. If it does, the code extracts the value of the responding status from the message content and sets the `"responding"` key in the database accordingly. If the value is `"true"`, the code sends a message indicating that responding is turned on. If the value is anything else, the code sends a message indicating that responding is turned off.
    

That's a high-level summary of what this code does. It listens to messages, retrieves and updates data in a database, and responds with appropriate messages based on the content of the messages it receives.

Here is the GitHub Repository which contains the complete code of the above bot which we just built.

[Encouraging Bot](https://github.com/hasnainmakada-99/Encouraging-Bot-Discord)

# Let's see the Output

Here's the output 👇

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683723025461/3e03defb-b19a-4b0a-969f-0aad0a838498.gif align="center")

# FAQ's

1. **What does the Discord.js dependency do?**
    

The Discord.js dependency enables developers to build out bots and other types of applications on Discord, the dependency almost provides every feature which the programmer can quickly integrate inside the Discord app/bot.

1. **Can Discord bots only be created using JS?**
    

No, you can create a Discord bot using various programming languages such as Python, Go Lang etc... It depends upon your fluency in any one of these languages and how quickly you can build one.

1. **What does the Discord developer portal do for us?**
    

The Discord developer portal helps us to build every type of application or bot which we want to, also we can provide various rights and privileges to the application we are building and without the developer portal, we can not even code our bot. So it is an essential part of the building process.

# Conclusion

In this blog, we built an entire Discord bot from scratch using JavaScript. If you have any further doubts related to the bot feel free to reach me on [Twitter](https://twitter.com/Hasnain_Makada) and [Showwcase](https://showwcase.com/hasnainmakada-99).

Till then, Happy Coding 😀