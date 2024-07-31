---
layout: post
title:  The rise of Distributed Frameworks
date:   2024-07-31 22:22:00 +0800
categories: [Software Engineering, Distributed Systems]
comments: true
---

I have always had an obsession around frameworks. Primarily driven by my experiences in both an engineer and an engineering leader with many challenges faced and mistakes made. Hopefully this does not come as a surprise to many, since all we have been working on top of, especially in product and/or application engineering, are simply frameworks. If you are a Java developer, for example, you are working on top of the Java SDK, which in fact is a framework that is comprised of thousands of different functions and tools to help you in different areas. Hopefully no one doing application engineering has to write in assembly anymore

So why do people use frameworks? Simply put, they offer quite a lot of benefits over writing it yourself. Scale, Costs, Security & Reliability

When I say "scale", i do not mean being able to add more server instances. I mean the ability to add more engineers, or to replace them. Having frameworks mean that you can expect high level of structure and predictability within your codebase. Additionally, you get both documentation and a larger community to support your development. In many ways, you have successfully increased the resources in your team, without actually adding any headcount/hence cost. Many argue that heavier/large frameworks have a larger learning curve. I would argue that a given bespoke codebase that has spent enough time in the wild, it will have an impossible learning curve without the right foundations, documentation and knowledge transfers. Such codebases are only possible in organizations large enough to have several platform engineering teams to build internal tooling and it is not something that smaller organizations can afford

Guess what? I write perfect code. The codes that I have written, it never fails, never breaks and never has any bugs and hence it is 100% reliable. Anyone who tells you that must either be a god, or bullshitting you. Either way you should probably not hire that person. Unfortunately writing code is complex. Even the simplest things can be complex. And hence we have different stages and types of testing today. Unfortunately, it can still sometimes take some time to perfect the codes and these things just generally takes time, and sometimes even a lot of frustrations from stakeholders. Many frameworks in the community have been battle tested across hundreds, if not thousands of scenarios and edge cases that you would not even think about. They have several folks and years to perfect their framework. As an application engineering team, you probably have 2-4 weeks to deliver outcomes. Do you really want to try to compete with that? Unless you are in the business of selling an application framework, I suggest not to write one yourself

I was a computer science security major. The number one takeaway in the entire bachelors for me really is that nobody really understands security and it is a majorly under-invested area in many companies that creates bespoke software. Leave it to the experts. Don't try to write your own authentication framework. There are plenty out there in each language. Pay for it. It is worth it. Many compromises around credential leaks, are related to poor/incorrect implementation of credential storage. And even many of the experts have came a long way in terms of their learnings. Even Windows XP had an issue around weak hashing security for their passwords under default credential configuration

Now that we have that out of the way on why you should not write your own codes for anything not related to your business core, let's get into the main topic - Distributed Systems

My journey as a software engineer started off as a .NET C# Windows Forms developer. Great platform, only 1 issue - multi-threading was a pain to deal with. Mind you this was a long time back before async awaits were even a thing. Things were hard then. You had to deal with raw threads and often that meant poor utilization/optimization of threads as there just was not enough knowledge on expensive context switches, synchronizing data and dealing with dead locks that came along with it, spawning too many threads can affect your performance in a negative way, synchronizing back to the UI thread was a big pain

Today, it is quite different from where we were. Most languages now offer a higher level abstraction that enables you create asynchronous work that allows you to yield time back to your CPU for IO based operations, which is far beyond how things were in the past. Depending on platform, thread synchronization is still an issue/challenge

Then there were frameworks like Akka, which offered to solve thread synchronization issues by employing the actor model. One caveat of it being an alternative programming model that is message driven. No matter what you tell me about message driven architectures and how scalable they are, the primary and major pitfall is that nobody understands message driven programming models. You cannot hire someone with the knowledge, and it is extremely hard to teach someone message driven programming models because it is "unnatural"

Then there was event sourcing, which was a supposed silver bullet to solve complex business needs due to it's nature in saving every possible past states which can be replayed

Along came the rise of cloud computing, which meant provisioning machines were now significantly more accessible than before, and horizontal scaling suddenly became a big thing. Anyone who has been thru this era must've heard of SOA and must have used some sort of messaging buses before. Even today, if you wanted to build a distributed system that uses multiple machines for processing, messaging queues are still defacto

However I would argue that messaging queues are not frameworks, but instead it is no different from writing bespoke/custom codes that require massive documentation, and also significant costs in deployment overtime due to the need of managing and provisioning several queues. Even to build a simple system that you would want to reliably send out an email after an action has been taken becomes overly complicated to build using queues

Enter the era of distributed frameworks, which in my opinion solves many of the intricacies of building and deploying a distributed application. The best things about it is that they are usually extremely easy to deploy as they are "stateless"/(semi)homogeneous clusters, and comes with pre-built observability and many times plug into OpenTelemetry

The good ones, in my opinion try to keep the same programming paradigm, without forcing you into writing some sort of message driven programming model. And by simply writing against the framework in simple functions, you have now successfully written your own scalable and reliable distributed system, for "free"

Of course nothing comes "free". These platforms typically have their own learning curve, as with any other frameworks and sometimes it can be difficult to comprehend at the start, but trust me it is well worth it at the end. Also for many of them it is paid to use their cloud offerings, which if you are a smaller company, my advice is just do it. It will save you more pain down the line

Here are some distributed frameworks I have used and encountered

###### Azure Service Fabric (.NET)
I have only played around with this in the early stages and it has built in support for "Reliable Actors". I don't know if any new development has been done here, but personally if you are on .NET and you are interested in Microsoft's virtual actor system, just use Microsoft Orleans. Service Fabric is an infrastructure, platform and framework, which will likely not fit many of the use cases out there. Orleans offers a much more flexible deployment path/option

###### Microsoft Orleans (.NET)
Have used this quite extensively in the past. It does what it says it does. Personally this is a much more superior model than Akka, especially for backend systems. It is primarily based off a virtual actor model system, which they call them grains. And these grains are activation free and is always assumed to exist. All your codes are built off these grains. This is a true P2P distributed framework with no single point of failure

###### proto.actor (.NET)
Not used this outside of POCs. This has a combination of both the traditional akka actor model, as well as orleans' virtual actor model, grains

##### Dapr.io
I have read about this quite a bit. This is likely the most comprehensive, hence most complicated out of the bunch here. It has every pattern for every possible scenario you have in terms of building a distributed system

##### temporal.io
Originally a fork of uber cadence. This is my personal favorite at the moment. It only has 2 basic building blocks - workflows and activities. Everything performed within the workflows and activities are scalable and fault tolerant, without worrying about the plumbing around it. Also it is cross platform compatible, which allows you potentially build workflows in nodejs and maybe certain activities in python, for example. It has helped solve 95% of the use cases I have had in building reliable and scalable distributed systems. This is likely good enough for small to medium-ish sized workloads. Architecturally, it does use a coordinator type model and hence it does carry a single point of failure if your infrastructure is not setup well. Hence, get the cloud service instead

##### restate.dev
Very new kid in the block. I have not used it personally in any shape or form. While it is marketed as simple and easy to deploy, It feels like the architecture is extremely similar to the likes of temporal.io
