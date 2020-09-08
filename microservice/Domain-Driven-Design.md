 Domain-Driven Design (DDD)
========================

![enter image description here](https://github.com/VickyFengYu/vicky.github.io/blob/master/microservice/image/microservice-1.jpg?raw=true)

![enter image description here](https://github.com/VickyFengYu/vicky.github.io/blob/master/microservice/image/agile-1.jpg?raw=true)

##  <i class="icon-folder-open"></i>Bounded Contexts

![enter image description here](https://github.com/VickyFengYu/vicky.github.io/blob/master/microservice/image/bounded-context-1.jpg?raw=true)

So we have two distinct contexts here. One of them is the store and the responsibilities of things within the store context is primarily sales. And the other one is the warehouse, and the responsibilities within the warehouse context are shipping. And that's an important way to keep contexts separate from each other, is think in terms of what are the responsibilities of the people working within that context? If somebody went to work in the morning at the warehouse they would not be thinking that my job is to sell books, and the same happens over on the store side and somebody who works in the store is not going to be thinking I need to know how to ship books. So within each of the contexts you have distinct people working, and they are working within their context without thinking too much about other contexts. Now of course in order to do that, they have to communicate with each other. And the communication is for the most part entirely within a given context, which is one of the reasons why domain-driven design makes for a good design principle. 'Cause things that happen inside the context stay inside the context. Things go wrong when you end up having objects that are on both sides talking to each other without any regard to the context boundaries. So that's something that clearly you want to avoid. So, the way that DDD solves that problem is by allocating responsibility for communication between context to one small object. In other words, in this picture on the store side we have one person, if you will, whose job is to talk to one person on the warehouse side in order to communicate between these two contexts. And this is the way it usually works in the real world.

![enter image description here](https://github.com/VickyFengYu/vicky.github.io/blob/master/microservice/image/modeling-1.jpg?raw=true)

![enter image description here](https://github.com/VickyFengYu/vicky.github.io/blob/master/microservice/image/aggregate-1.jpg?raw=true)

![enter image description here](https://github.com/VickyFengYu/vicky.github.io/blob/master/microservice/image/name-1.jpg?raw=true)

##  <i class="icon-file"></i> Entity

Another critical thing to bear in mind as we're talking about entities, is that what we're talking about are the roles that people take on as they're working, not the actor, not the person who is in that role. Within the context of say, a timesheet system, a manager authorizes timesheets, that's the role. An employee fills out timesheets, that's their role. Nowhere do you need to be both a manager and an employee, in other words, the fact that a manager is an employee in the real world is irrelevant with respect to our domain-driven design. What we care about are the roles, the fact that an individual person sometimes logs on to the system in the role of manager in order to authorize timesheets, and that at other times, the same person logs on to the system in the role of employee to fill out a timesheet, is irrelevant from the point of view of the design, as far as we are concerned they are separate people. So one of the things that we're doing with the ubiquitous language is trying to identify the roles that people take on as the stories play out. And the entities then, will be named after those roles, not after the job title of the person that happens to be filling the role in a specific situation, or to put it another way, you never model the guy typing, the guy typing is not an entity. The entities are the roles that that person takes on as they are actually doing work.

![enter image description here](https://github.com/VickyFengYu/vicky.github.io/blob/master/microservice/image/samename-differenctentity-1.jpg?raw=true)

![enter image description here](https://github.com/VickyFengYu/vicky.github.io/blob/master/microservice/image/samename-differenctentity-3.jpg?raw=true)

![enter image description here](https://github.com/VickyFengYu/vicky.github.io/blob/master/microservice/image/samename-differenctentity-2.jpg?raw=true)

###  <i class="icon-file"></i> Orchestrated/declarative systems
 
Now, declarative systems can work okay inside a monolith. They cannot work very well inside of a microservice system and the reason for that is those blue lines, those communication lines, are network connections in the microservice world. In a monolith, of course, they're just function calls. Network connections can have all sorts of things going wrong with them. 
 
 The other problem associated with these kinds of declarative systems is that there's a very tight coupling relationship between the various services here. Put another way, the shopping cart service needs to know quite a bit about the warehouse service in order to use it.

The point being, that if you make a change to the warehouse service, you also have to change the shopping cart service. And the same applies to every one of these downstream services. If you make a change to any downstream service, odds are the upstream service will be impacted,

[enter link description here](https://github.com/VickyFengYu/vicky.github.io/blob/master/microservice/image/declarative-system-1.jpg?raw=true)

###  <i class="icon-file"></i>  Orchestrated/reactive systems

![enter image description here](https://github.com/VickyFengYu/vicky.github.io/blob/master/microservice/image/reactive-system-1.jpg?raw=true)

![enter image description here](https://github.com/VickyFengYu/vicky.github.io/blob/master/microservice/image/reactive-system-2.jpg?raw=true)

![enter image description here](https://github.com/VickyFengYu/vicky.github.io/blob/master/microservice/image/reactive-system-3.jpg?raw=true)

##  <i class="icon-file"></i> Event Storming

First one being an event. So an event is something that happens at the business level that your customers, or end users, or domain experts care about. It's a business level thing. Remember what we're doing with domain level, domain driven design, is implementing the domain.

![enter image description here](https://github.com/VickyFengYu/vicky.github.io/blob/master/microservice/image/event-1.jpg?raw=true)
