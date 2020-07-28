---
template: post
title: An overview of 4 pillars of OOPs
slug: /posts/pillars-of-oops
draft: false
priority: 1
date: 2020-06-07T18:28:09.109Z
description: Understanding 4 pillars of OOPs in plain English.
category: Programming
tags:
  - Programming
  - OOPs
  - Object-Oriented-Concept
  - Abstracton
  - Encapsulation
  - Inheritance
  - Polymorphism
---
Object oriented programming is an approach of writing code for better maintainability and re usability. Stick to the rules and make complex code easier to develop, reuse and maintain. There are mainly four concept which help us to achieve this and we generally call them as 4 pillars of OOPs.

In this post, I will explain these 4 concept in simple terms with real time example. I will be using the same example that I used to explain class and objects in my previous post. You can read [that](https://saileshdhakal.com.np/posts/oops-concept) before proceeding to this.

![pillar](/media/pillar.jpg 'pillar')

*Photo Courtesy: Google*

Lets start with the definition of each and then try to understand them using the examples.

## **Abstraction**

> Abstraction is the process of showing only the essential/necessary features of an entity/object to the outside world and hide the other irrelevant information.

Lets looks at the example now and try to relate it with the definition

The guy from our previous post who made the smartphone later made one for his best friend. His friend had seen it first time and didn't know what to do with it. The guy simply explained him that he can use this device for multiple purpose. If you want to call me, simply dial my number from here and click this button. If you want to take pictures, open camera and click this button. Record the beautiful moments with the video button. The guy explain the procedure to play games, watch movies, listen radio and many more. He was happy to get it and right there started to take pictures. He does not have any idea how that thing is working internally and he might not even need to know about it.

He needs to be aware with the interface i.e screen and how to access different feature through it. From here, we can say that the **implementation of phone has been abstracted from the interface** to make it easier and effective to use.

Coming back to the definition, abstraction is the process of showing only the essential/necessary features of an entity/object to the outside world (Screen with the icons to access features) and hide the other irrelevant information (All hardware and software components to make those features available).

Relating it with the programming, we achieve abstraction by using **interfaces and abstract classes**. I will cover details of interface and abstract classes in my upcoming post.

> *In short, abstraction reduces code complexity by separating interface from implementation. It lets us focus on what the object does instead of how it does.*

## *Encapsulation*

> Encapsulation means wrapping up data(attributes) and member function (methods) together into a single unit to keep values or state of data safe from the outside interference and misuse.

Lets continue with the example. The smartphone that was developed has a camera in it. The camera is actually mounted in a motherboard using some cables and is programmed to perform different actions such as zoom in, zoom out, focus, blur and so on. The guy wanted to capture object which is far from him. To do this he drags his two fingers in his screen and magnifies the object. But internally how the mobile phone is able to interpret those human gesture to operate the camera hardware and change the focal length is unknown.

The guy don't have to know how the camera works but he sure knows that object magnifies when he drag two fingers away from each in the screen.

Coming back to definition, Encapsulation means wrapping up data(attributes) and member function (Method) together into a single unit(hardware components, software and interface as an single component) to keep values or state of data(internal operations) safe from the outside interference and misuse(By providing the interface as per our choice). We can always have the control over the operation that user can perform.

Relating with the programming, encapsulation is **achieved using class.** We usually define access permissions on attributes(using access modifiers) and make them illegal to access from the methods outside of that class. The value on that attribute can only be accessed outside of the class through the public methods of that class.

> *The meaning of encapsulation and abstraction might sound similar however, the encapsulation is the way to implement abstraction. In other word, encapsulation is a subset of abstraction.Encapsulation is basically denying the access to the internal implementation or knowledge about internals to the external world , while abstraction is giving a generalized view of any implementation that helps the external world to interact with it.*

![Abstraction Vs Encapsulation](/media/abstract.png 'Abstraction Vs Encapsulation')

*Photo Courtesy: Google*

## *Inheritance*

> Inheritance is the ability of creating a new class from an existing class. Inheritance allows a class (subclass) to acquire the properties and behavior of another class (super-class) and *it can have additional properties* *or behavior.*

Lets try to understand it with our example. We saw the guy created a smartphone with which he was able to make calls, take pictures, play games, store photos and videos and so on. On the long run, he got bored and wanted to add more features. He thought of adding a mobile router to connect to internet via wifi, provide security to his phone using fingerprint sensor and audio jack to connect to earphones or headphones. To create this, he don't need to start from the begining since he has already created a phone which provides other features. He can utilize those features already build in the current phone and enhance it by adding the new features. He can simply add those extra hardwares and sensors to his phone and override the behavior to add some new functionality. Finally he created a new one with less effort and named it as The Smartest.

Coming back to definition, Inheritance is the ability of creating a new class(The Smartest ) from an existing class(Smartphone). Inheritance allows a class (subclass) to acquire the properties (camera, screen, storage, battery and so on )and behavior(watch movie, play games and so on) of another class (super-class) and *it can have additional properties(mobile-router, fingerprint-sensor, audio-jack)* *or behavior(connect to internet, lock device, connect earphone)**.***

In programming, there are different ways in which inheritance can be done. Details on each will be out of the scope for this post.

* **Single Inheritance**
* **Multi-level Inheritance**
* **Multiple Inheritance**
* **Hierarchical Inheritance**

## *Polymorphism*

> *Polymorphism* is the ability of an object to take on many forms.

*For example, lets take an example of power button in the smartphone. When our phone is locked, pressing the power button wakes our phone. However, pressing the same button will lock the screen if the phone is already awake. So the behavior of same button was different based on the state of phone.*

*Also the guy wanted to save the phone number of his best friend in his phone. He can save the number under the contact name of his friend or can even save multiple numbers under the same contact name.*

*Suppose, his friend has single number than the operation to save contact might look like:*

*`SaveContact(name, phone)`*

*If he has multiple contact numbers than the operation will look like:*

*`SaveContact(name, phone1, phone2)`*

*Coming back to definition, polymorphism is the ability of an object to take multiple form(same button to power on or off, same method to store one or multiple contact)*

*In programming, there are two types of polymorphism namely:*

* ***Dynamic Polymorphism / Runtime polymorphism***
* ***Static Polymorphism / Compile time polymorphism***

*Dynamic polymorphism is achieved using **method overriding.** The behavior of method will be decided at runtime. We can consider our first example of power button as Dynamic polymorphism*

*Static Polymorphism can be achieved using **method overloading**. The behavior of method will be decided at the compile time. We can consider our second example as Static Polymorphism.*

*Hope I was able to help you understand these concept. I will be coming with more posts related to OOPs concept. Keep reading :)*