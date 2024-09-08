# OLA 1
## By cph-Pack (Patrick, Albert, Caroline og Kevin)

### 1 Technology Stack
Type of Tool | Chosen Tool
---------- | -------------|
Version Control Platform | Git with GitHub
Text Editing | Notepad++, Visual Studio Code, StackEdit
Diagram Tool | Mermaid, Eraser
Online Research and Documentation | Zotero
IDE | Visual Studio for C#, IntelliJ for Java
Programming Language | C# .NET version 8, Java version 21 or newer

### 2. Link to video presentation


### 3. Report

# Enterprise Integration Patterns
In modern software development, integration and communication between various systems are crucial to building and maintaining efficient and scalable applications. But integrating between systems, applications, or data, and handling communication within distributed systems can be challenging. 
Enterprise Integration Patterns provide a set of design patterns that offer a standardized approach  to handling the complexities of system integration by defining best practices. 

This report aims to explain some key components of enterprise integration by focusing on understanding message-based systems, which is a fundamental aspect of how modern applications communicate. In addition, this report will explore the diagramming standards commonly used to model integrations, and finally explain the monolith and microservices architectures as these are common architectural styles used for distributed systems.


## Message-based systems

 

### Channels

Messaging applications transmit data through a message channel. One application writes data to the message channel and another reads data from the channel. The application adding info doesn't necessarily know what particular application will be receiving the info, but it can be assured that whatever application retrieves that info will be interested in the info. This is because the messaging system has different message channels for different types of data it wants to communicate.

  

  

### Messages

A message is a packet of data broken up into a Header and a Body. The header describes the data being transmitted while the body is the data

  

  

### Multi-step delivery

Also known as pipes and filters. Sometimes data must first be processed before it can be used, for example it may need to be decrypted first or to remove duplicate messages. The pipes and filters architectural style is used to divide a larger processing task into smaller steps (filters) connected by channels (pipes)

  

  

### Routing

In larger enterprises, messages may have to go through multiple channels before it reaches its final destination. In this case, the message may need to be sent to a message router. 

A router is a special filter that connects to multiple channels and sends the message to a specific channel depending on certain conditions. A key property of the router is that it doesn't modify the message itself. 
A benefit of the router is that the decision making criteria for the destination of a message is kept in a single location. If new message types are defined, new processing components are added, or the routing rules change, only the message router logic needs to be changed and all other components will remain unaffected. Also, since all messages pass through a single message router, incoming messages are guaranteed to be processed one-by-one in the correct order.

  

  

### Transformation

Various applications may expect to receive data formatted in different ways. To fix this, the message may need to go through a message translator that converts it from one format to another

  

  

### Endpoints

Message endpoints take the command or data and turn it into a message. The endpoint doesn’t know anything about formats or messaging channels, just that it should send or receive a message, unpack the content and provide it to the application in a meaningful way.

## Diagram standards

UML is one of the most widely used diagram types for modeling software, even in enterprise integration. It is useful, because it provides a diagram that can be modeled both for structural and behavioral aspects of a system.

  

An example of a UML type we could use is the common Class Diagram to show the data structure within our system and how different classes relate and interact with each other.

  

Another example would be a Sequence Diagram, which would illustrate the messaging needed within the system as well as the data flow.

### Code for integration pattern

For a Message Router Pattern, an example could be that we have payment methods in our system and based on the customers payment method, the message will then be directed based on the selected payment. This can be done with a switch statement, which in this case will register 3 different cases (Credit Card, PayPal & Unsupported payment method)

```
switch (order.PaymentMethod)

{

case "CREDIT_CARD":

ProcessCreditCardPayment(order);

break;

case "PAYPAL":

ProcessPaypalPayment(order);

break;

default:

Console.WriteLine($"Unsupported payment method: {order.PaymentMethod}"); break; }
```

This is a fairly simple, yet easy to understand example. For future development, it would also be easy to add more cases to the code, for example by adding an option to do a bank transfer.

## Monolith

  

*Almost all the successful microservice stories have started with a monolith that got too big and was broken up.*

*Almost all the cases where I've heard of a system that was built as a microservice system from scratch, it has ended up in serious trouble.*

Quote by [Martin Fowler](https://martinfowler.com/bliki/MonolithFirst.html)

  

But is he right? If a monolith is such a good solution why would we even consider microservices? What do they provide that we cannot fix in a monolithic approach?

  

### What is a monolith?

  

*In software engineering, a monolithic application is a single unified software application which is self-contained and independent from other applications, but typically lacks flexibility* - Wikipedia

  

![App Platorm](https://wac-cdn.atlassian.com/dam/jcr:95b9a276-c524-42b1-8d06-ded56d589858/Monolithic%20architecture@2x.png?cdnVersion=2216)

  

  

  

The pros should always outweigh the cons when choosing your solution. It is true that most programming problems can be solved by smashing it enough with the hammer, but sometimes a screwdriver is just the better tool. Let's inspect the pros and cons of a monolith.

  

### Pros

  

- Excellent for simple applications.

- You only have 1 project instead of 2,3,4,5...

- Prototyping an idea is faster due to less integration.

- Gives an oversight enabling us to split into microservices at a later point.

- Easier to debug.

- Easier to deploy.

  

  

### Cons

  

- Over time becomes difficult to navigate which can slow down development speed.

- 1 change can inadvertently cause issues in other parts of the project.

- Poor scalability.

- Lack of flexibility.

- Any changes require the entire project to be redeployed.

  

### So why monolith?

  

As we can see the biggest benefit of a monolith is the lack of complexity and a lot of "this is easier". With microservices comes a different approach to development and strategies needed to become successful. More on that in the microservices part.

  

When we host everything under one project, we reduce the amount of API's needed to connect our functionality behind the scene. API´s are more focused towards exposing the data our project produces rather than passing it on to a long chain of microservices mutating that data. We need less management of servers and infrastructure which can save a lot of money and time.

  

The monolith approach was the only way for a long time as microservices is a relatively new way of thinking. This means that a vast majority of companies still run with the monolith. Making the switch to microservices has a huge impact on the company and the way they are structured. For the big companies this is an investment that yields no new functionality making it a low priority to switch, unless they have severe performance issues at hand.

## Microservices
Microservices are an architectural style in software development where the system's functionality is divided into small, independent services that communicate with each other via networks. 

![Example of Microservice Architecture. Credit: Atlassian](https://wac-cdn.atlassian.com/dam/jcr:5308ccab-dc94-46f5-978c-8a77b8d5be57/Microservice%20architecture@2x.png?cdnVersion=2216)

Each microservice is modelled around a specific business domain and its scope is therefore defined by the bounded context of that domain. This ensures the autonomy of each microservice, since it can focus on its own task and encapsulate its own logic.

In *'Building Microservices: Designing Fine-Grained Systems'*, Sam Newman explains that individual microservices are treated as black boxes from the outside. This means that the internal implementation details are hidden from the consumer, whether it be another microservice or another type of program. This information-hiding concept of the black box further allows for clear separation between the microservices and reinforces the loose coupling in the architecture. 

As a result, the microservices can be independently developed, deployed, and scaled. Furthermore, microservices are technology agnostic as they can be written in different programming languages or frameworks for example. 

In a video discussing microservice architecture, Dave Farley emphasizes that the most important attribute of microservices is that they are independently deployable. He further argues that all other attributes of microservices are important because they help make the microservices independently deployable. 

### Advantages of microservices
The independence of each microservice greatly contributes to the benefits of the architecture. Smaller, more focused teams can work autonomously on different microservices, and according to Farley, those teams will build *"better software faster"*. The small teams are also happier according to the Atlassian article *'Microservices vs. monolithic architecture'* by Chandler Harris. 

Microservices can be developed in an agile manner with continuous deployment allowing for more frequent software updates, which promotes improved reliability, uptime, and performance. It also allows for vertical scaling.

Another advantage is the improved robustness as the failure in one microservice can be isolated and the rest of the system should be able to continue working. Newman does however warn that this robustness is not a given and in order to achieve it, the developers must have an understanding of the new sources of failure that distributed systems such as microservices have to deal with.
    
### Disadvantages of microservices
Although, individual microservices can be relatively simple, the microservice architecture as a whole can be quite complex. 

An aspect that can add to the complexity of building microservices is the added organizational overhead. Since development can be done in smaller, autonomous teams, a need for another level of communication and collaboration between teams arises. Additionally, there's the aspect of added costs as each microservice can have its own costs associated. 

Testing microservices can also be challenging as the scope of end-to-end testing may become very large, covering multiple services and interactions. Similarly, debugging can become more complicated as issues may span across several services and machines.

The individuality of microservices can also impact the data consistency and there might be a lack of standardization. 

Newman explains that some challenges of microservices are due to their distributed nature, and could therefore also be evident in a distributed monolith for example.  However, the complexity in microservices is can be more pronounced due to the amount of independent services and the interactions between them, making careful design and coordination even more critical.

