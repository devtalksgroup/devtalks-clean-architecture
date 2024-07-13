# The clean architecture

The Clean Architecture is the system architecture guideline proposed by Robert C. Martin (Uncle Bob) derived from many architectural guidelines like Hexagonal Architecture, Onion Architecture, etc... over the years.
This is one of the guidelines adhered to by software engineers to build scalable, testable, and maintainable software.

## Why do we need to architect?

> "The goal of software architecture is to minimize the human resources required to build and maintain the required system.” ― Robert C. Martin, Clean Architecture

## Advantages of Proper Architecture
* Testable
* Maintainable
* Changeable
* Easy to Develop
* Easy to Deploy
* Independent

## The Clean Architecture
Here’s the clean architecture illustration created by Robert Martin:
We can see there are four layers in the diagram. Blue layer, Green layer, Red layer, and Yellow layer.
Each circle represents different areas of the software. The outermost layer is the lowest level of the software and as we move in deeper, the level will be higher. In general, as we move in deeper, the layer is less prone to change.

## The Dependency Rule
The Dependency Rule states that the source code dependencies can only point inwards.
This means nothing in an inner circle can know anything at all about something in an outer circle. i.e. the inner circle shouldn’t depend on anything in the outer circle. The Black arrows represented in the diagram show the dependency rule.
This is the important rule that makes this architecture work. Also, this is hard to understand. So I’m gonna break this rule at first to let you understand what problems it brings and then explain and let’s see how to keep up with this rule. So please bear with me.
First of all, this circular representation might be confusing for many. So let's try to represent it vertically.
The colors represented here are the same as the colors represented in the clean architecture diagram.
Remember, the arrow should be read as “depend on”. i.e. Frameworks and Drivers should depend on Interface Adapters, which depend on Application Business Rules which depend on Enterprise Business Rules.
Nothing in the bottom layer should depend on the top layer.

## Frameworks and Drivers
Software areas that reside inside this layer are
* User Interface
* Database
* External Interfaces (eg: Native platform API)
* Web (eg: Network Request)
* Devices (eg: Printers and Scanners)

## Interface Adapters
This layer holds
* Presenters (UI Logic, States)
* Controllers (UI Logic, States)(Interface that holds methods needed by the application which is implemented by Web, Devices or External Interfaces)
* Gateways (Interface that holds every CRUD operation performed by the application, implemented by DB)

## Application Business Rules
Rules which are not Core-business-rules but essential for this particular application come under this. This layer holds Use Cases. As the name suggests, it should provide every use case of the application. i.e. it holds each and every functionality provided by the application.
Also, this is the layer that determines which Controller / Gateway to be called for the particular use case. Sometimes we need controllers from different modules.
This is where different modules are coordinated. For instance, we want to apply a discount for the user who purchased for x amount within a month.
Here we need to get the amount the user has spent on this month from the purchase module and then with the result we need to apply the discount for the user in the checkout module. Here applyDiscountUseCase calls the purchase module’s controller for the data and then applies the discount in the checkout module.

## Enterprise Business Rules
This is the layer that holds core-business rules or domain-specific business rules. Also, this layer is the least prone to change.
Change in any outer layer doesn’t affect this layer. Since Business Rules won’t change often, the change in this layer is very rare. This layer holds Entities.
An entity can either be a core data structure necessary for the business rules or an object with methods that hold business logic in it.
For example: calculating Interest module in the banking application is the core business logic that should be inside this layer.
Let’s look at a simple example to understand this well.
