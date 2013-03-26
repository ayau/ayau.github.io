---
layout: post
title: "Technical Interviews for the Typical College Student"
date: 2013-03-26 14:04
comments: true
categories: 
---

In the past two years, I have interviewed with countless places for the "Software Engineering Internship" position. I have done my research on common tech interview questions and most of the advices are along the lines of "study your data structures" or something vague like that. How much do I actually need to know?

There are usually two types of questions. Knowledge and programming ability questions. While I cannot help you with the latter, here is a cheat sheet for the common knowledge questions I get asked, based on my experiences from all the interviews I've been through so far. Feel free to open it up during a phone interview. They all ask the same ones.

<!-- more -->

Data Structures
=

Hashmaps
-
Implemented using Hash tables  
hashMap.put(key, value);

### Big-O
O(1) expected, O(n) worst case

O(1) if good hashing function  
O(n) if all hashed to the same bucket
- assuming linked list implementation of collided items

O(n/b) average - items/number of buckets

### Collision
(when the bucket is already filled)

1. Append to linked list in bucket  
2. Probe for the next bucket - Linear probing, Quadratic probing, Double hashing

### Functions to be implemented for the object to be hashed
getId() - returns identifier to be passed into the hash function. Can simply be the address of the object

equals() - comparison between objects (differentiate objects with the same hash code)

---  

Binary Search Trees
-

### Big-O
O(nlogn)

### Functions to be implemented
compare(obj1, obj2) - true if obj1 > obj2, false otherwise

* Can be used on ordered lists

``` java Find the number of times x appears in an ordered list of integers
//    Binary search for x - 0.5, return top bound  
//    Binary search fo x + 0.5, return top bound  
//    Find difference  
//    O(1)
```

Algorithms
=

_Coming soon_

Know at least one sort really well


Java
=

4 Major principles of Object Oriented Programming
-

__Encapsulation__
    Hiding of data implementation by restricting access to accessors and
    mutators

    Accessors - getters
    Mutators - setters

Advantages - Don't have to worry we are going to break other code that is using and calling the class for information

__Abstraction__
    Public and private methods to hide implementation
    Only expose simple interface

__Inheritance__
    Subclass, superclass, interface
    Extends, implements

__Polymorphism__
    Overriding - run-time polymorphism
    Same method signature - overrides method in superclass
    
    Overloading - compile-time polymorphism
    Different method signatures, same method name

---

### Synchornize
    Enforcing exclusive access to an object's state

When a thread invokes a synchronized method, it automatically acquires the intrinsic lock for that method's object and releases it when the method return. The lock release occurs even if the return was caused by an uncaught exception.


``` java synchronize -> locks object  
    
    class Foo {
        public synchronized void f(){
            // stuff
        }
    }

    Foo x = new Foo();
    Foo y = new Foo();

    x.f(); // only locks for instance x. y can still call y.f();
```

``` java static synchronize -> locks Class

    class Bar {
        public static synchronized void f(){
            // stuff
        }
    }

    Bar x = new Bar();
    Bar y = new Bar();

    x.f(); // locks on the class. y.f() cannot run

```
``` java synchronize blocks

    // Can synchronize blocks too
    public void addName(String name) {
        
        synchronized(this) {
            // make changes
        }

        // lock released
    }

```

Android
=

Five components - Service, Intents, Resources, Notifications, Content providers

__Service__ -> activity with no interface

__Thread__ -> concurrent unit of execution

__Handler__ -> message or runnable communication between threads, UI

__Content provider__ -> share data across applications

__Intents__  
explicit - specify activity  
implicit - let platform finds activity  
sticky - stays around after it is used  

Activity Lifecycle
-

![android activity life cycle](http://2.bp.blogspot.com/-xeMDielmiUo/UOU6lxU5LXI/AAAAAAAAArA/xw4LV_gzjDk/s1600/activity_lifecycle.png)

View Lifecycle
-
![android view life cycle](https://lh5.googleusercontent.com/-TTZ-LN41ygA/UIQt75DBSEI/AAAAAAAAFAY/v8jAR9WWg5w/s648/android.png)

Important View functions

- onMeasure() - compute the size of itself and its children
- onLayout() - compute the bounds of its children for rendering
- onDraw()

New in 4.1 4.2
-

__4.2__

Multi user, nested fragments, lock screen widgets and daydream, RTL support

__4.1__ 

notifications (expandable), resizable app widgets, android beam

project butter - vsync timing (consistent frame rate) - synchronize with touch of finger


C
=
_Coming soon_

Linked list, Combination, Permutation


Javascript
=

Highly recommended - [Javascript Cheat Sheet](http://superherojs.com/)

types - Number, String, Boolean, Function, Object, Null, Undefined
parseInt to convert base

var - containing scope  
no var -> global scope -> pollution - no scope (difficult to maintain and test)

``` javascript Use namespace to overcome pollution
MyApp = {}
MyApp.object = new Object();

```

``` javascript Scope
(function(){
    // Containing scope
}).call(this);
```

__loosely typed (weakly typed)__  
no type declaration needed when variables are created

__undefined__ - has not been initialized  
__null__ - empty

== coercion   
=== check type as well. Null and undefined

== null -> null or undefined

__this__ 
    object that owns the method, depends on how the function is called
    points to the currently in scope object that owns where you are in the code

__event bubbling__ - behavior of events in child and parent nodes in DOM (Document Object model)
    all child events are passed to parent
    benefit - speed - only need to traverse dom tree once
    useful if you want to place more than one event listener on a DOM element

framework - jQuery

errors  - try/catch/finally blocks - throw

setTimeout, setInterval, clearTimeout


Tips
=

[Programming Interviews Exposed](http://www.amazon.com/Programming-Interviews-Exposed-Secrets-Landing/dp/1118261364) - Book on programming interviews, mostly in C

Don't drink the night before D:
