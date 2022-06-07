## Introduction to YAML &  working with YAML files

### Introduction

Hey everyone in this blog I'm going to introduce you to YAML which is not a markup language but is a data - serialization language, I'm going to cover all the important topics of YAML in this blog.

Here is the list of topics I'm going to cover in YAML:

- What is YAML ?

- Data serialization & deserialization ?

- Benefits of YAML

- For what purposes YAML files are used ?

- Working with YAML files 

- Datatypes in YAML

- Tools to check YAML syntax

- Advanced data types in YAML

- DevOps tools for YAML

Let's get started with it:

#### What is YAML ?

YAML stands for Yaml Ain't Markup Language earlier it was addressed as Yet Another Markup Language but after pointing out that YAML doesn't use and tags or elements inside it, it was renamed to Yaml Ain't Markup Language.

YAML is a data serialization language which is used to write configuration files for you system, YAML files are generally made for the data of your system and it does emphasizes the documents. YAML is a popular programming language because it is human readable and easy to understand and it can also be used in conjunction with other programming languages.

#### Data serialization and deserialization

Here is a image demonstrating data serialization & deserialization,

![serialization-deserialization-diagram.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1654420571138/m-xLIBvUD.png align="left")

As we can see from the above image a data serializer acts as a mediator in converting the object to stream bytes, it will take the object then it will convert it to stream of bytes and then serializer will store the stream of bytes to various types of files. It can store the stream of bytes into a file, database or memory of the system.

We can serialize our own data if we want to send it to another file, In PHP it provides the serialize and un - serialize function so we can convert the object to stream bytes directly and send it over to other files, on the other side if the user wants to understand that data they can deserialize it and view it as stream bytes are difficult to understand.

That's what YAML does it converts the object to stream bytes and sends it over to other files.

On the other hand deserialization works as a mediator to convert the stream of bytes into an object and makes it easy to read and modify as native structure in a programming language.

#### Benefits of YAML

Let's discuss some the benefits of YAML and see how it's useful,

- It is more human readable, YAML allows you to represent complex data structures in human readable format

- Has a strict syntax the YAML specification has minimum leeway for flexibility, this increases its robustness.

- Fast implementations, YAML is fast to load and easy to process in memory.

- More powerful than JSON when it comes to specify complex data structures

- Provides lists, sequence to specify data in a structured way/

- Has a consistent data model to support generic tools.

#### For what purposes YAML files are used ?

YAML files are mainly used to set up the configuration files on your system means the configuration files are written in YAML only because the data is stored and transmitted via the configuration files.

YAML is also used by some of the most useful tools of DevOps such Docker, Kubernetes, Datree.io, Circle ci etc.

#### Working with YAML files

We've seen the introduction of YAML and discussed about what is serialization, deserialization and so on..

Let's get started working with YAML files: 

 (1) How to create a YAML file

Create a new folder on your desktop and open it with Vs Code, we are generally gonna use Vs Code to deal with YAML files.

Click on the create icon and assign any name to it such as demo and remember yaml files are saved with either a .yaml or .yml extension so do remember it. Your 1st yaml file is created successfully as we can see here,

![yml blog 1.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1654422198274/KcfCGEjOA.png align="left")

In YAML data is usually stored in Key - Value pair so for every data we are specifying in YAML we have to specify a key to it to as I have assigned it here,

![yml blog 2.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1654422599064/_OAJbYOwq.png align="left")

In the above image I've specified my name hasnain to a name key inside the YAML file, So whenever I need to access my data I can usually find it using the key of my value which I provided.

We can also name our key as an integer value and assign it some string data and that's where datatypes comes in the picture.

#### Datatypes in YAML

We all have been familiar with the concept of datatypes as we have used them whenever working with a programming language such as java, python, dart etc. Similarly YAML also supports basic 3 types of datatypes which are Scalar, Lists & Dictionary.

In the section we are going to discuss about the scalar datatypes in YAML and in the later section we are going to see lists & dictionary.

Scalar is a simple datatype inside which it contains 2 types of data types

- Numeric data types (Integer, Floating point, Boolean)
- Strings

(i) Numeric data types

An Integer data type can be a decimal value, octal or hexadecimal value

```
# In YAML comments are represented by a single hashtag and it does not support multiline comments

"Age" : 18  # Here we have given the value of age which is an integer value and its key is a string

"Octal" : 726746425  # Here we given a octal value to the octal key, It seams like an integer but when you convert it from octal to decimal it will be 123456789

"Hexa" : 21C1 # Here is a hexadecimal value which we have given to the hexa key, in hexa decimal it converts numbers to letter after they cross certain limit so when you convert the number it will be 8641

``` 
(ii) Strings

Strings are basically a set of characters which are represented in single quotes & double quotes. In YAML it doesn't matter if you write string in single quotes or double quotes or without quotes if there are character in a joined together it will consider it a string only

```
name : 'Hasnain'   # string in single quotes

country : "INDIA"   # string in double quotes

studying : Computer engineering # string without quotes

``` 
(iii) Booleans

Booleans contains 2 keywords, True or False

```
# Boolean data type

"error" : true

"page reload succeeded" : false

``` 
That's all about about the basic datatypes in YAML and how we can use it.

#### Tools to check YAML syntax

There are a bunch of tools to check your YAML syntax whether you have properly written your YAML file or not, Here are some of the tools which are as follows,

- [YAML Checker](https://yamlchecker.com/)

- [YAML Lint](http://www.yamllint.com/)

- [Code beautify](https://codebeautify.org/yaml-validator)

- [wtools](https://wtools.io/validate-yaml-online)

That was all about the tools to validate your YAML make sure to check out

#### Advance data types in YAML

We have seen the basic data types in YAML and how to use it so now let's see what are some of the

There are basically 2 types of advanced data types in YAML. Lists & Dictionaries

(i) Lists

Lists represent a set of items which are enclose in square brackets []. In list data duplication is allowed

```
# Lists

fruits : [apple, mango, pineapple, orange] # we can store them in a single line also

cities:  # And we can also put them in a block style or multiline format also
 - Mumbai
 - Delhi
 - Kolkata
 - Delhi

```

(ii) Dictionaries

Dictionaries are a way to hold complex data structures in our YAML file, it basically holds key : value pairs which is nested with a lot of options

```
# Dictionaries 

student:  # Here we can see that in dictionaries it is nested with a lot of other options, the options can be a list or a map (key : value pairs) too.
 - name : 'abc'
 - age : 18 
 - subjects:
      - Maths : 90
      - Science : 87
      - English : 50

``` 
That was an overview of the advance data types of YAML, hope you understand it by now if you want to know more about data types make sure to check out [grav documentation](https://learn.getgrav.org/17/advanced/yaml)

#### DevOps tools for YAML

There are a bunch of YAML tools are there which are used in DevOps but here are the most useful YAML tools which will get you sorted while working with YAML

- [Datree](https://datree.io/)
- [K8s lens](https://k8slens.dev/)
- [Kubeshop](https://kubeshop.io/)

### Conclusion

So I hope that you would have got an overview about what are YAML files and in general what is YAML and how to work with YAML files. If you have any doubts feel free to check me out on [showwcase](https://showwcase.com/hasnainmakada-99) and [twitter](https://twitter.com/Hasnain_Makada)
 



