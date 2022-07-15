# Explain Object-Oriented Programming

> Please note that, in Sciences such as Computer Science, things are never set in stone, and what this page describes as a fact can be implemented in a number of different ways that wouldn't match this description 100%. The idea of this exercise is to give a birds-eye view of the OOP paradigm, not to be an academic paper on Object-Oriented Programming.

It is a programming paradigm, often represented by Java, which models programming constructs as "objects".

An object is an instance of a class. Class is a general descriptor of the features for a specific construct. For example, you can have a `vehicle` class, of which a Ford Focus with license plate `ABC123XYZ` is an instance of. This `vehicle` can have attributes and methods.

## Attributes

Class attributes are simply variables that instances (objects) can make use of. Sometimes these attributes cannot be changed, because they are controlled by the class definition, such as the number of wheels, but other attributes, like speed, or colour, can vary by instance.

## Methods

Methods are computing devices attached to classes (and objects) that allow you to perform actions on the object itself. Going back to the `vehicle` analogy, if we have a `fordFocusABC123XYZ` variable assigned to this object, we can call `fordFocusABC123XYZ.startEngine()` to start the engine on this one vehicle. This way of writing a dot and a function after the name of the variable is the way methods are typically invoked. For example, Java uses this convention. When invoking the `startEngine()` method on this particular instance, notice that we are only starting the engine of this car, and this method call will not affect the rest of the system or other instanfces.

## Inheritance

Inheritance allows to create subclasses out of classes. In the class `vehicle`, we can have other classes like `truck`, `car` or `airplane`. These three are still classes, an they have similar objectives (moving people or goods around), but they can have totally different attributes. For example, the truck will have six wheels, while the car only has four. And the airplane will have wings and jet engines that neither of the other vehicles do.

## Polymorphism

A consequence of class inheritance is polymorphism. Certain methods can be common to `vehicle`, `truck`, `car` and `airplane`, and you don't necessarily need to know the class of the instance on runtime, as long as the four of them have this method defined. In this case, these four vehicles have an engine that you can start and stop. The minutia of start and stopping engines is hidden away behind the `startEngine()` and `stopEngine()` but all of them will implement it.
