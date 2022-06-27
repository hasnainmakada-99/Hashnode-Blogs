## Unit testing in flutter & Separate authentication layer in flutter to provide security

### Introduction

Hey everyone in this blog I'm going to explain you what is unit testing in flutter and how to separate the authentication logic in flutter to provide extra security to your flutter code

Starting off with the first topic:

### What is unit testing in flutter and how it is useful ?

We all have seen some cases that when we deploy any version of our application, we usually perform some manual tests in our application to see that each and every functionality should be working perfectly, otherwise if we have not tested and directly deployed it, it will perform crashes in the end user's device.

Unit testing is way to ensure that your app can continue to work even if you add more changes and features to the existing functionality inside your application. Unit tests are very handy for verifying the behavior of a single function, method or a class etc.

For writing unit tests in flutter, it provides the test package which is the core framework for writing unit tests in flutter.

### Why is it necessary to separate auth layer from the main Ui in flutter ?

When we are integrating firebase with our flutter application we have to initialize firebase to its current platform so that whenever we run our application we can do authentication and connect to our database.

But do we have to do it inside our main files which are going to be displayed to the end user ? absolutely not, If we are integrating the functionalities directly onto to the main Ui some phishers can directly access the credentials which we are taking from the user, whether it can be email, password etc. So its all dirty code.

So it is necessary to separate the authentication layer so it can not be directly integrated inside our main application

## How to separate the authentication layer in flutter ?

As of now we've discussed about the need to separate the authentication layer from the main Ui in flutter, Let's implement it practically

The files which we are going to need to separate the code will be as follows

- An `auth_exceptions.dart` file which will include all the necessary exception which we will throw when an error will generate.

- An `auth_user.dart` file which will include all the necessary credentials of a user, but for as of now we will only initialize a Boolean inside the `auth_user` which will be `isEmailVerified`

- The next file will be `auth_provider.dart`. It will be an abstract class and it will contain all the necessary methods, getters and setters. The `auth_provider` will contain future methods which will contain the `auth_user` as a generic. In the end we are performing authentication with the users so `auth_user` will be used as a generic.

- The next file will be the main root file for our authentication, which is the `firebase_auth_provider.dart` this file will implement all the methods, gettter & setters defined inside the `auth_provider.dart` file

- And in the end we will have a `auth_services.dart` file which will implement all methods and getters defined inside the `auth_provider.dart` file and it will also initialize an instance of `auth_provider` class.

So all the file which we've made will be interconnected like this,

![Overview.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1655974060402/GbLq-vuFe.png align="left")

Now that we've discussed about how each and every file will function as per our need, Lets implement those files in code.

(i) `auth_exceptions.dart`

```
// login exceptions

class UserNotFoundException implements Exception {}

class WrongPasswordException implements Exception {}

// Register exceptions

class WeakPasswordException implements Exception {}

class EmailAlreadyInUse implements Exception {}

class InvalidEmailException implements Exception {}

// Generic exception 

class GenericException implements Exception {}

class UserNotLoggedIn implements Exception {}

``` 
In the exceptions file we've separated each and every exceptions as per their use cases and each and every file implements the class exception.

(ii) `auth_user.dart`

```
import 'package:firebase_auth/firebase_auth.dart';

class AuthUser {

  // ignore: prefer_typing_uninitialized_variables
  final isEmailVerified;

  const AuthUser({required this.isEmailVerified});

  
 factory AuthUser.fromFirebase(User user){
  return AuthUser(isEmailVerified: user.emailVerified);
 }

}

```
In the AuthUser we've used the concept of [factory construtor](https://betterprogramming.pub/exploring-the-3-types-of-constructors-in-dart-e2e2d4d6f710) So that we don't have to instantiate a new instance of our class

Currently our class is only instantiating `isEmailVerified` variable inside its construtor and it is using the User class from the `firebase_auth` class of firebase. It will assign true or false to the `isEmailVerified` variable

(iii) `auth_provider.dart`

```
import 'package:todoapp/services/auth/auth_user.dart';

abstract class AuthProvider{
    Future<void> initialize();

    AuthUser? get currentUser;

    Future<AuthUser> login({
      required String email,
      required String password,
    });

    Future<AuthUser> createUser({
      required String email,
      required String password,
    });

    Future<void> logout();
    Future<void> sendEmailVerification();
}

```

In this file we've provided the `AuthUser` as a generic to all the future methods except the initialize method as it will be used to initialize the connection to firebase and it has nothing to do with our user, And we've provided `AuthUser` as a generic to the `createUser` and `login` methods as they are going to interact directly with our user. The rest is the `sendEmailverification` method which is used to send verification email to the user to verify them, and the last is the logout and a getter which is used to get the `currentUser` and logout is used to log the user out of the application back to the login screen.

(iv) `firebase_auth_provider.dart`

```
import 'package:todoapp/firebase_options.dart';
import 'package:todoapp/services/auth/auth_provider.dart';
import 'package:todoapp/services/auth/auth_exceptions.dart';
import 'package:firebase_core/firebase_core.dart';
import 'package:todoapp/services/auth/auth_user.dart';
import 'package:firebase_auth/firebase_auth.dart';

class FirebaseAuthenticationProvider implements AuthProvider{
  
  

  @override
  Future<void> initialize() async {
    await Firebase.initializeApp(
      options: DefaultFirebaseOptions.currentPlatform
    );
  }


  @override
  Future<AuthUser> createUser({required String email, required String password}) async {
      try{
          await FirebaseAuth.instance.createUserWithEmailAndPassword(email: email, password: password);
          final user = currentUser;
          if(user!=null){
            return user;
          }
          else{
            throw UserNotLoggedIn();
          }
      }
      on FirebaseAuthException catch(e){
        if (e.code == 'weak-password') {
            throw WeakPasswordException();
          } else if (e.code == 'email-already-in-use') {
            throw EmailAlreadyInUse();
          } else if (e.code == 'invalid-email') {
            throw InvalidEmailException();
          } else {
            throw GenericException();
          }
      }
      catch(e){
        throw GenericException();
      }
  }


@override
  AuthUser? get currentUser{
    final user = FirebaseAuth.instance.currentUser;
    if(user != null){
      return AuthUser.fromFirebase(user);
    }
    else{
      return null;
    }
  }

  @override
  Future<AuthUser> login({required String email, required String password}) async {

      try {
          await FirebaseAuth.instance.signInWithEmailAndPassword(email: email, password: password);

          final user = currentUser;

          if(user!=null){
            return user;
          }
          else{
            throw UserNotLoggedIn();
          }
          

      } on FirebaseAuthException catch(e){
         if (e.code == 'user-not-found') {
        throw UserNotFoundException();
      } else if (e.code == 'wrong-password') {
        throw WrongPasswordException();
      } else {
        throw GenericException();
      }
      }
      catch(e){
        throw GenericException();
      }
  }

  @override
  Future<void> logout() async{
    final user = FirebaseAuth.instance.currentUser;
    if(user != null){
      await FirebaseAuth.instance.signOut();
    }
    else{
      throw UserNotLoggedIn();
    }
  }

  @override
  Future<void> sendEmailVerification() async {
    final user = FirebaseAuth.instance.currentUser;
    if(user!=null){
      await user.sendEmailVerification();
    }
    else{
      throw UserNotLoggedIn();
    }
  }
  

}

``` 

In this file we've imported each and every file we've created till now and implemented the Auth provider with this class and overridden all of its method inside this class.

This file contains the core logic of how the register screen will perform, how the login screen will perform and so on.. We've also thrown exception at each and every error that can occur while working with firebase.

(v). `auth_service.dart`

```
import 'package:todoapp/services/auth/auth_provider.dart';
import '../auth/auth_user.dart';
import './firebase_authentication_provider.dart';

class AuthService implements AuthProvider{
final AuthProvider provider;

const AuthService(this.provider);

  factory AuthService.firebase() => AuthService(FirebaseAuthenticationProvider());


  @override
  Future<AuthUser> createUser({required String email, required String password}) =>
    provider.createUser(email: email, password: password);
  
  @override
  AuthUser? get currentUser => provider.currentUser;

  @override
  Future<void> initialize() => provider.initialize();

  @override
  Future<AuthUser> login({required String email, required String password}) => provider.login(email: email, password: password);

  @override
  Future<void> logout() => provider.logout();

  @override
  Future<void> sendEmailVerification() => provider.sendEmailVerification();

}

``` 
In this class we've delegated each and every method of `auth_provider` directly to the `firebase_auth_provider`. Firstly we've implemented the Auth provider class and then instantiated and instance of it, after then we've override all the methods and delegated each one of them toward the `firebase_auth_provider` methods 

We've also used a factory constructor over here to call the firebase authentication provider class every time we call the `AuthService.firebas()` method.

Now that we know how to provide abstraction to the firebase authentication methods, Let's now implement them in our main files

Here I am sharing a login file which I've created for my project implementing all the Authservice methods

```
import 'dart:developer';
import 'package:flutter/material.dart';
import 'package:todoapp/constants/routes.dart';
import 'package:todoapp/services/auth/auth_exceptions.dart';
import 'package:todoapp/services/auth/auth_services.dart';
import 'package:todoapp/services/auth/auth_user.dart';
import 'package:todoapp/views/notes_view.dart';
import '../firebase_options.dart';
import 'package:todoapp/services/auth/firebase_authentication_provider.dart';
class loginView extends StatefulWidget {
  const loginView({Key? key}) : super(key: key);

  @override
  State<loginView> createState() => _loginViewState();
}

class _loginViewState extends State<loginView> {

late  final TextEditingController _email;
  late  final TextEditingController _password;

  @override
  void initState() {
    _email = TextEditingController();
    _password = TextEditingController();
    super.initState();
  }

  @override
  void dispose() {
    _email.dispose();
    _password.dispose();
    super.dispose();
  }

   @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
      title: const Text('Welcome to Todoist'),
      ),
      // ignore: avoid_unnecessary_containers
      body:Container(
        margin: EdgeInsets.only(top: 20, left: 10, right: 10),
        alignment: Alignment.center,
        width: 500,
        height: 320,
      decoration: BoxDecoration(color: Color.fromARGB(255, 130, 126, 127), borderRadius: BorderRadius.circular(10) ),
      padding: EdgeInsets.all(15),
        child: Column(
          children: [
              Container(
                margin: EdgeInsets.only(bottom: 20),
                child: const Text('Log into todoist',
                  style: TextStyle(
                    fontSize: 30,
                    color: Colors.white,
                    ),
                ),
              ),

              Container(
                width: 510,
                alignment: Alignment.center,
                height: 50,
                decoration: BoxDecoration(
                  color: Colors.white,
                  border: Border.all(color: Colors.transparent),
                  borderRadius: BorderRadius.circular(10)
                
                ),
      
                child:TextField(
                controller: _email,
                autocorrect: false,
                keyboardType: TextInputType.emailAddress,
                decoration: InputDecoration(hintText: '   Enter Your Email Here', border: InputBorder.none),
            ),
              ),
             Container(
               margin: EdgeInsets.only(top: 10),
               width: 500,
               height: 50,
               decoration: BoxDecoration(
                 border: Border.all(color: Colors.transparent),
                 borderRadius: BorderRadius.circular(10),
                 color: Color.fromARGB(255, 255, 255, 255)
               ),
               padding: EdgeInsets.only(bottom: 10),
               child: TextField(
                controller: _password,
                autocorrect: false,
                obscureText: true,
                keyboardType: TextInputType.visiblePassword,
                decoration: InputDecoration(hintText: '  Enter Your Password Here', border: InputBorder.none),
            ),
             ),
            SizedBox(
              width: 200,
              child: Container(
                margin: EdgeInsets.only(top: 20),
                child: Column(
                  children: [
                    TextButton(
                      onPressed: () async {
                        await AuthService.firebase().initialize();
                        final email = _email.text;
                        final password = _password.text;
      
                          try 
                          {

                          await AuthService.firebase().login(email: email, password: password);
                          final user = await AuthService.firebase().currentUser;
                          if(user?.isEmailVerified){

                          Navigator.of(context).pushNamedAndRemoveUntil(notesRoute, (route) => false);

                          }
                          else{
                            await AuthService.firebase().sendEmailVerification();
                             final snack = SnackBar(
                            content: const Text("We've sent you a verification email"),
                            action: SnackBarAction(label: 'close', onPressed: (){}),
                            );

                        ScaffoldMessenger.of(context).showSnackBar(snack);
                          }
                        
                         }
                            
                          on UserNotFoundException {
                             await showErrorDialog(context, 'User not found');
                          }
                          on WrongPasswordException {
                             await showErrorDialog(context, 'Password Incorrect');
                          }

                          on InvalidEmailException {
                            await showErrorDialog(context, 'Invalid Email');
                          }

                          on GenericException {
                             await showErrorDialog(context, 'Authentication Error');
                          }
                      },
                       
                      child: const Text('Login', style: TextStyle(fontSize: 20)),
                      style: TextButton.styleFrom(backgroundColor: Color.fromARGB(255, 236, 234, 234)),

                      
                      ),
                      
                      TextButton(onPressed: () {
                        Navigator.of(context).pushNamedAndRemoveUntil(registerRoute, (route) => false);
                      }, 
                      child: const Text('Not registered ?, Click here'),
                      style: TextButton.styleFrom(backgroundColor: const Color.fromARGB(255, 236, 234, 234)),
                      ),

                  ],
                ),
                 
              ),
            ),
          ],
        ),
      ),

       
    );
  }
}

```

You can clearly see that we've completely abstracted the authentication layer from our main UI.

Let's move towards unit testing 

### Performing unit tests

For performing unit tests in flutter we will need a package named `test` and it will provide necessary methods to write the test

Install the test package from CLI,

`flutter pub add test --dev`

After installing the test make a new file inside the test folder named `auth_test.dart`

We are generally going to perform only 2 tests for now, but you provide as many tests as you want

Create a main function inside the `auth_test.dart` file

```
void main()
{
    // tests
}

```

After then create a MockAuthUser class outside the main function and create a method inside it,

```
import 'package:flutter_test/flutter_test.dart';
import 'package:todoapp/services/auth/auth_exceptions.dart';
import 'package:todoapp/services/auth/auth_provider.dart';
import 'package:todoapp/services/auth/auth_user.dart';

class MockAuthProvider
{
  AuthUser? _user;
  bool _isInitialized = false;
  bool get isInitialized => _isInitialized;

  Future<void> initialize() async {
    await Future.delayed(const Duration(seconds: 2));
    _isInitialized = true;
  }

```

Then create a group inside the main method and create and instance of `MockAuthProvider` and start performing the tests

```
group('Mock Authentication', () {
    final provider = MockAuthProvider();
    test('Should not be initialized to begin with', () {
      expect(provider._isInitialized, false);
    });

    test('Should be able to initialize', () async {
        await provider.initialize();
      expect(provider.isInitialized, true);
    });

});

```

Here I've not provided any logic while performing the tests, The above code is just for explanation that how we can perform tests

After providing the tests save the file and run it using the 
`flutter test test/auth_test.dart` command

The command will take some time and it will show a summary to you you that how many tests were passed and how many were failed with the errors happened during the testing phase

### Conclusion

I hope you've now understood what is unit testing and how to provide tests and separate the auth layer from flutter and make it abstract, If you have any doubts feel free to reach me out on [Twitter](https://twitter.com/Hasnain_Makada) & [Showwcase](https://showwcase.com/hasnainmakada-99) 😀