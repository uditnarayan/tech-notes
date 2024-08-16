## Approach 1 - Three step process
According to [[Microservices Patterns]], its a three step process:
### Step 1 - Identify System Operations
Starting point are the requirements like user stories. Instead of describing the requirements in terms of communication technologies like REST or messages, use more abstract notions like operations. A system operation is an abstraction of a request, that application must handle. It is either a command or a query. Use operations to understand business scenerios that illustrate how different components in a monolith collaborate. 
#### How?
* Create a high level domain model from requirements consisting of key components that provide a vocabulary to describe system operation.
* Identify system operations in terms of commands and queries and describe each one's behaviour in terms of domain model.  Its also a good point to think about preconditions and post conditions of the operations.

### Step 2 - Identify Services
Decompose the monolith into functionally independent services. A service can represent a business capability or can represent a subdomain in the terms of domain driven design. The end result should be set of services which are organised around business concepts rather than technical concepts.
#### How?
Decompose by subdomain and Decompose by business capability are the two main patterns for defining an application’s microservice architecture.

* Decompose by business capability - each business capability or collection of related business capabilities can thought as a business oriented service rather than technical. It defines clear contracts and SLAs. 
* Decompose by sub domain - Capture knowledge about a domain and use that to solve problems within that domain. Domain defines the vocabulary used by the team.Domain driven design solves the problem by defining separate domain for each sub domain in application problem space. Sub domain are identified in a similar way as business capabilities.  The scope of the sub domain is called as a bounded context which is represented by a service. 

### Step 3 - Identify APIs
Assign each service operations identified in the first step to a particular service. A service can fulfil the operation itself or can collaborate with other services to accomplish the same. In that case, also determine how services collaborate and determine additional supporting operation needed for the same. A service publishes events primarily to enable it to collaborate with other services.
#### How?
* Map service operations to corresponding services
* Determine the apis required to support collaboration.

Note: So far we have identified service and operations in an abstract manner. Operations can be sync or async in nature. Refer to [[Interprocess Communication]] to more detials on communciation standards.

## Decomposition Guidelines
There are, some useful guidelines for decomposition that have their roots in object-oriented design. Let’s take a look at them.

### Single Responsibility Principle 

`_A class should have only one reason to change._`

We can apply SRP when defining microservice architecture and create small, cohesive services with single responsibility. This will reduce the size of the service and increase stability. 

### Common Closure Principle

`_The classes in a package should be closed together against the same kinds of changes. A change that affects a package affects all the classes in that package._`

We can apply CCP when creating microservice architecture and package components that change for same reason in same service. 

## Challenges of decomposition

There could be challenges in defining microservices:
1. Network latency - too many round trips between services.
2. Sync Communication - can reduce the availability of overall user story.
3. Consistency - need to use patterns like [[Saga]] to maintain consistency of operations.
4. God Code - common code used throughout the application.