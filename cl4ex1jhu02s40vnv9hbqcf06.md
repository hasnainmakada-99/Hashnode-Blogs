## Introduction to sound null safety in dart & ways to provide it

### Introduction

Hey everyone in this blog I'm gonna discuss about sound null safety which is a way to assign null values to variables. Dart's null safety enables compiler optimization which determines that is something isn't null then its value can never be null.

In dart when you opt null safety then by default the types in your dart are non nullable, which means that your variables can't contain null values unless you assign it to them. 

### Ways to assign null safety to variables

Here's an example in which the following variables cannot contain null values by default,

```
int a = 10; // Here the variable a cannot contain null value, If provided null then it will throw error

String name = "Hasnain"; // The same applies for string also

``` 

So how do we assign null safety to the variables so that if we assign null to them they shouldn't throw error. 

In dart whenever you want to provide null safety to variables then we always have to postfix our data type with question mark (?) such as `String?` so that it will tell the compiler that the variable which are assigned to the string data type can be a null and not null also.

Here's an example in which we have used null safety,

```
int? a = null; // Here it tells the compiler that the variable a can be nullable or non-nullable

String? name = null; // The same rule applies for the string too

print(name) // Here it will print null on the screen

``` 
The main benefit of null safety is that it converts your runtime dereferences errors into edit time analysis errors.

Similarly in dart as we've provided null safety to variables we can also provide null safety to complex data structures such as lists, map, sets etc.

```
// Null safety in List
List<String?> values = ['Foo', 'Bar', 'Baz', null];

// Null safety in Map
Map<String?, String?> values = {
    'name': 'Hasnain',
    'age' : '18',
    'profession' : 'student',
     'Employement_history' : null,
  };
  
 values.values.forEach((values){
    print(values);
 });

``` 
In dart sometimes we need to know at runtime which variables contain a value and which does not. There is a way we can check the values of the variables in dart with the help of the null aware operator (??)

The null aware operator only takes the values of the variables and prints it to the users. So if we have 3 variables in our program and 2 of them contains null and the 3rd contains the actual value then the null aware operator will take the actual value from the 3rd variable and print it to the user

Lets see an example,

```
String? firstName = null;
String? middleName = null;
String? lastName = 'Makada';

String actualValue = firstName ?? middleName ?? lastName; // Here it will store the variable which contains the actual value which is "Makada"

print(actualValue); // Here it will print the value

``` 

### Conclusion

I hope you now understood what is sound null safety in dart and how to use it, if you have any doubts feel free to reach me out on [showwcase](https://showwcase.com/hasnainmakada-99) and [twitter](https://twitter.com/Hasnain_Makada)





