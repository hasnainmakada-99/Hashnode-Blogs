# My Riverpod Learnings

# Introduction

Hey everyone I am Hasnain Makada, currently building out **Open Source with Hasnain** where every beginner regardless of their field can find tons of resources related to Web Dev, Android, AI & ML etc... This project is also intended for beginners to contribute to it and get their journey started with Open Source. You can check out the project on [**GitHub**](https://github.com/hasnainmakada-99/Open-Source-With-Hasnain)**.**

In this blog, I'm posting my learnings related to riverpod (A state management solution). This blog contains all the necessary providers and I've also provided the steps to install riverpod and get started with it in Flutter

I've learnt about `flutter_riverpod` but there are also many other riverpod packages which you can get started with it. You can explore them from the [**official docs**](https://riverpod.dev/docs/getting_started#what-package-to-install)

# Installing Riverpod

We are going to install `flutter_riverpod` in this blog so create a new flutter project by running `flutter create riverpod_demo` and after the project is created successfully, run `flutter pub add flutter_riverpod` and the riverpod package will be added successfully to the project.

# What is Riverpod

Let me give you an overview of what riverpod is and what does it in your flutter apps,

Riverpod is a state management library for Flutter, a mobile app development framework. It allows developers to manage the state, or data, of their app in a consistent and organized way, making it easier to build and maintain the app. It uses the concept of "providers" to manage states, which are objects that hold and provide access to the app's data. This makes it easy to update and access the state in different parts of the app and ensures that the data is always in a consistent state.

One of the main features of Riverpod is that it uses "providers" to manage the state. These objects hold a piece of data and provide access to it. You can think of them as similar to global variables, but with the added benefit of being able to update the data in a consistent way.

Overall, Riverpod aims to make state management in Flutter apps more predictable, organized and easier to maintain, by providing a consistent and powerful way to manage the state throughout the application.

Now that we've discussed Riverpod, let's start with the providers which are in it.

# Providers

### 1\. Provider

Provider is the most basic type of provider in riverpod. It basically creates value and that's all about it.

Before using any provider in riverpod, wrap the `MyApp` widget with the `ProviderScope` widget so that we can read all our providers in our app.

```dart
runApp(
    // For widgets to be able to read providers, we need to wrap the entire
    // application in a "ProviderScope" widget.
    // This is where the state of our providers will be stored.
    ProviderScope(
      child: MyApp(),
    ),
```

The use of provider is as follows,

```dart
class MyApp extends ConsumerWidget {
  @override
  Widget build(BuildContext context, WidgetRef ref) {
    final String value = ref.watch(helloWorldProvider);

    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(title: const Text('Example')),
        body: Center(
          child: Text(value),
        ),
      ),
    );
  }
}
```

Riverpod provides us with `ConsumerWidget` with which you can update the data in your app without rebuilding the whole widget and it also improves the performance in your app.

### 2\. StateProvider

`StateProvider` is a provider that exposes a way to modify its state. It is a simplification of [StateNotifierProvider](https://riverpod.dev/docs/providers/state_notifier_provider), designed to avoid having to write a [StateNotifier](https://pub.dev/documentation/state_notifier/latest/state_notifier/StateNotifier-class.html) class for very simple use cases.

The use of `StateProvider` is as follows,

```dart
final nameProvider = StateProvider<String?>(
  (ref) {
    return null;
  },
);
// It initially returns null over here

final name = ref.watch(nameProvider); // we can refrence it with the Ref inside the build mathod but make sure that the whole widget should be a consumer widget or call this only inside the consumer wrap around.

ref.watch(nameProvider.notifier).update((state) => value); // to update the values, call the provider with the .notifier parameter and it will provide you with a set of methods to update, dispose etc..
```

### 3\. StateNotifier and StateNotifierProvider

`StateNotifierProvider` is a provider that allows you to create and expose a `StateNotifier` to your widgets. This provider can be used to observe the state of the `StateNotifier` and rebuild the widgets that depend on it when the state changes.

The use of `StateNotifierProvider` is as follows,

```dart
class UserNotifier extends StateNotifier<User> {
  UserNotifier()
      : super(
          User(name: '', age: 0),
        );

  void updateName(String n) {
    state = state.copyWith(name: n);
  }

  void updateAge(int age) {
    state = state.copyWith(age: age);
  }
}

// State Notfier Provider
final userProvider = StateNotifierProvider<UserNotifier, User>( // exposes the usernotifer to the outside world
  ((ref) => UserNotifier()),
);
```

### 4\. FutureProvider

`FutureProvider` is a provider in the Riverpod library that allows you to easily manage the state of a future in your Flutter app. It is used to provide an `Future` object to a descendant widget and automatically handles the loading, error, and data states. When the future completes, the widget tree is rebuilt with the data from the future. It's a way to manage the state of an asynchronous task in your app.

The `FutureProvider` implemented as follows,

```dart
class UserRepository {
  Future<User> fetchUserData() {
    const url1 = "https://jsonplaceholder.typicode.com/users/1";
    return http.get(Uri.parse(url1)).then((value) => User.fromJson(value.body));
  }
}

// Always create a separate class when working with futureproviders/ Stream Providers

final fetchUserProvider = FutureProvider(
  (ref) {
    return UserRepository().fetchUserData();
  },
);

// Main.dart File
 final user = ref.watch(fetchUserProvider);
     return user.when(
       data: (data) {
         return Scaffold(
           appBar: AppBar(title: const Text('Sample')),
           body: Center(
             child: Text(
              style: const TextStyle(fontSize: 30),
              data.name.toString(),
             ),
           ),
         );
       },
       error: (error, stackTrace) {
        return Text('Error');
       },
       loading: () {
         return Text('Loading');
       },
     );
```

### 5\. StreamProviders

`StreamProvider` is used to provide a value that is generated by a `Stream` and it is automatically updated when the Stream emits a new value.

`StreamProvider` is implemented as follows,

```dart
final streamProvider = StreamProvider(
  (ref) async* {
    yield [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12];
  },
);

// Main.dart file
return ref.watch(streamProvider).when(
      data: (data) {
        return Scaffold(
          body: Center(
            child: Text(
              data.toString(),
            ),
          ),
        );
      },
      error: (error, stackTrace) {
        return Text("Error Found");
      },
      loading: () {
        return Text('Loading');
      },
    );
```

**Now that we have discussed the basic providers which are used in riverpod and also seen the implementation of all of them in code also. Now let's look into some of the modifiers which riverpod provides to us.**

# Modifiers

Riverpod mainly provides us with 2 modifiers,

* `.family`
    
* `.autoDispose`
    

The `.family` modifier has only one purpose in a provider: Getting a unique provider based on external parameters.

Some common use-cases for `family` would be:

* Combining [FutureProvider](https://riverpod.dev/docs/providers/future_provider) with `.family` to fetch a `Message` from its ID
    

The `.autoDispose` modifier destroys the state of the provider when it is no longer used.

There are multiple reasons for doing so, such as:

* When using Firebase, close the connection and avoid unnecessary costs.
    
* To reset the state when the user leaves a screen and re-enters it.
    

# Provider Observers

Provider observer listens to the changes in a provider container. It is basically used to provide loggers for all the providers we use in our app.

To know more about provider observers, check out the [**official documentation**](https://riverpod.dev/docs/concepts/provider_observer).

# Wrapping up!!!

So that was all my learnings curated inside one blog, These are just the basics of riverpod and it took me almost a week to learn and understand it. I hope that this blog will help you in some way while you are learning and you can use my blog as a reference while you are learning it. If you have any doubts related to flutter and DevOps, feel free to reach out on [**Twitter**](https://twitter.com/Hasnain_Makada) and [**Showwcase**](https://showwcase.com/hasnainmakada-99)