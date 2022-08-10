## API(s) in flutter and how to use them ?

### Introduction

Hey everyone I am Hasnain and in this blog I am going to explain you about how to use API(s) in flutter and get data dynamically using an API in flutter. We will see what are the packages required to parse an API and what are some of the tools which can come in handy when parsing API(s) to dart classes.

So let's get started

### What is an API

API stands for Application Programming Interface and it is way in which two or more computer programs can communicate with each other. API are mainly made up of JSON with which we can parse it easily and put them in our App or website. If you want to know more about API(s) check out this amazing website by [amazon](https://aws.amazon.com/what-is/api/#:~:text=API%20stands%20for%20Application%20Programming,other%20using%20requests%20and%20responses.).

### How to deal with API(s) in Flutter ?

In flutter we can use external packages to deal with API(s) such [chopper](https://pub.dev/packages/chopper), [dio](https://pub.dev/packages/dio), [http](https://pub.dev/packages/http) etc. For this blog we're gonna use the http package because it is easy to use and has a lot of benefits also.

So create a new flutter project from terminal with this command `flutter create <project-name>`

Then navigate to your project and open it with Vs Code `cd <folder-name>; code .`

Install the http package dependency using `flutter pub add http`

Now that we've installed the dependencies We need to convert our API to dart syntax so that we can easily parse it. You can parse it with this [Json to dart tool](https://javiercbk.github.io/json_to_dart/). For this blog I'm gonna use my Pokémon API which basically consist all the data for Pokémon's

Here's the link for the [API](https://raw.githubusercontent.com/Biuni/PokemonGO-Pokedex/master/pokedex.json)

Now copy all the JSON code and convert the API to dart class using the tool I mentioned above. Name the dart class as PokeHub and paste all the dart code in a new file inside the lib folder names PokeHub.dart

When you'll paste the code it will throw some error to you that the prevEvolution property is not found, The best way to deal with this error is to remove all the occurences of the previous evolution, because we're not gonna need it

Now that all the work is completed, Our pokehub class should not throw any error, Its time for us to start the main thing with our API

Then create a function in the `main.dart` file which whill fetch our API, Convert it to JSON & then map each property of JSON with the help of the PokeHub class
```
fetchAPIData() async {
    var url =
        "https://raw.githubusercontent.com/Biuni/PokemonGO-Pokedex/master/pokedex.json";
    var res = await http.get(Uri.parse(url));
    var decodedJson = jsonDecode(res.body);
    pokeHub = PokeHub.fromJson(decodedJson);
    setState(() {});
  }

```

Call this function written above inside the initState method of statefull widget

Now create a Gridview inside the statefull widget and map each and every property of pokemon API and get their image and print it in a container

```
GridView.count(
              crossAxisCount: 1,
              children: pokeHub.pokemon!
                  .map(
                    (poke) => Container(
                      width: 500,
                      height: 500,
                      decoration: BoxDecoration(
                        image: DecorationImage(
                          image: NetworkImage(poke.img.toString()),
                        ),
                      ),
                    ),
                  )
                  .toList(),
),
```

Don't forget to convert the pokeHub mapping to List, Otherwise it will throw error and will not execute

And the output will be like this
![Api Blog](https://media.giphy.com/media/UHxGwExO7sDg0CUQvb/giphy.gif)

You can get more things from the API such as name, AvgSpawns etc. and you can use it your way, This was just a demo of how API works in Flutter

### Conclusion

I hope by now you got a basic understanding of how API works in flutter and how to use them, If you like my blog, Make sure to follow me on [hashnode](https://hasnainm.hashnode.dev/), [showwcase](http://showwcase.com/hasnainmakada-99) & [twitter](http://twitter.com/Hasnain_Makada)

Keep fluttering 😀

