# Java Sprint Concepts

# Table of Contents
* [Dependency Injection](#dependency-injection)
* [Inversion of Control](#inversion-of-control)

## Dependency Injection

```Dependency Injection is where a needed dependency is injected by another object or by a framework such as spring```.

Dependency Injection aka **DI** it means the class being injected has no responsability in instantiating the object being injected.

### Types of Dependency Injection
* **By Class Properties**
* **By Setters**
* **By Constructor**

## Inversion of Control

```Inversion of Control aka IoC is a technique to allow dependencies to be injected at runtime```

In IoC the framework is going to control most of the activity bringing up the structure.

## Dependency Injection VS Inversion of Control

| Dependency Injection (DI)| Inversion of Control (IoC) |
| ----------- | ----------- |
| Refers much to the composition of your classes | IoC is the runtime environment of your code |
| You compose your classes with DI in mind       | Spring is is control of the of the injection of dependencies |

## Spring Context

You can think of the **Spring Context** as all the stuff that's going to be around your application.

* We can ask the Spring Context for the objects
* 