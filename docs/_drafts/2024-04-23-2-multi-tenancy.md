---
layout: post
title:  "Let's talk about multi-tenancy"
date:   2024-07-23 00:40:00 +0800
categories: [Multi Tenancy]
---

Multi Tenancy is hard. It is one of the most common requirements today, especially for B2B type products. In this post, we will explore concepts around how multi-tenancies are typically implemented, and where the challenges come in

There are many reasons why multi tenant systems are built in a myraid of different ways. On the tech side, it could be related to the tech stack limitations, team experience and the fine balance between trying to keep sanity on keeping things simple, yet flexible while not compromising on bugs causing data leaks acrosss tenants, as well as deployment hells, and also performance reasons in the more latency sensitive applications. On the business side, it is largely driven by regulatory, compliance and sometimes political, where certain customers may require data to be geographically located in specific regions, or even located on-premise

Due to these limitations/requirements, we will have to consider - where data is processed at, as well as where data is stored

We will speak broadly about the Application and Database layers, as well as the configuration options available

###### Application Layer
###### Database Layer
es least amount of complexity

Logical Storage Type | Scalability | Compute Isolation | Data Domiciling | Development Complexity | Operational Complexity
| - | - | - | - | - | - |
Single Database | Highly dependent on database choice | Highly dependent on database choice | Highly dependent on database choice | Because data is shared, there is higher risks of cross tenant data exposure if there is not enough platform/tooling support to assist | Single databases are generally the easiest to manage, administrate and maintain overall
Single Database Per Tenant | DB Agnostic | DB Agnostic | DB Agnostic | Rare to have tooling support around this, so custom tooling is required to support this model. Can be difficult if self-service tenant creation is required | Each database needs to be administered separately, hence this can also be quite complex
Database Sharding | DB Agnostic	| DB Agnostic | DB Agnostic	| Similar to database per tenant, with more complexity around partitioning strategy | Complexity is highly dependent on partitioning strategy used. Generally speaking this option is the most complex

<!-- In the simplest possible design, we would opt for a system that runs off a single region and single database server cluster. This offers an extreme ease of starting out. You could then decide on your tenant strategy
1. shared
2. table per tenant
3. schema per tenant
4. database per tenant

Each option offers you a different route in terms of ease of future extensibility, albeit highly dependent also on the database technology you have chosen

On the data processing side, it would simply be a shared cluster serving the same set of customers

Should be easy to develop against, while introducing minimal bugs

Deployment can be complex

As we are offering a free tier to customers, we should generally ensure that the system is built to be cost effective

I want my data to be processed and stored at specific regions due to reason ____
I need blazing fast response times <50ms as my app is latency sensitive
I want my data to have dedicated/isolated data storage as that is required for ____
Given we have different customer tiers, we need to ensure that we meet our SLAs to our paid customers, while maintaining reasonable overall costs of running our systems -->
