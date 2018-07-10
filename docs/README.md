# Serverless Platform - Overview

Serverless infrastructure is a new type of cloud infrastructure that auto-scales and charges you only when it's used.  If you embrace it to build your applications, you will reduce overhead, innovate more and move incredibly fast.

However, many teams and organizations don't know how to do serverless development, let alone cloud development.  We built the [Serverless Platform](https://www.serverless.com) to help them.  It includes everything teams and organizations need to practice serverless development safely, and deliver results faster than ever.

## Product Areas

The Serverless Platform contains three product areas.  Each solve core problems of building and operating serverless applications:

### Serverless Framework

The serverless application framework.  Use it to build, deploy and update serverless applications across vendors.

### Serverless Dashboard

The serverless operations console.  Monitor, collaborate and secure your serverless applications.

### Event Gateway

The serverless integration infrastructure.  Connect your serverless applications and functions to your existing workloads and services.

## Concepts

After a few years of doing serverless development, we've designed the best possible abstractions for reasoning about serverless applications.  Here's what they are and how they fit together:

```
- Tenant / Event Gateway
  - Applications
    - Services
      - Functions
      - Events
      - Subscriptions
      - Resources
```

### Tenant

A Tenant is a secure workspace which can contain one or many Applications.  Every Serverless Platform user gets a Tenant when they register.  They can invite others to their Tenant to collaborate on the Applications within that Tenant.

Tenants are most often created for a team, or an individual's personal use.

### Event Gateway

The [Event Gateway](https://www.github.com/serverless/event-gateway) is open-source pub/sub infrastructure for routing Events from any source to Functions running on any type of serverless compute (e.g. AWS Lambda, Azure Functions, containers).

Every Tenant comes with a hosted version of the Event Gateway (operated by us, Serverless Inc.).  This Event Gateway is shared across all Applications in a Tenant, enabling you to share Events across Applications easily and react to them with serverless Functions.

You can also self-host the Event Gateway and plug it into the Serverless Platform, instead of using our hosted version.  If you're interested in this, message us [here](https://serverless.com/enterprise/).

### Application

A serverless Application is built on serverless infrastructure, typically using Functions-as-a-Service (e.g. AWS Lambda) along with other serverless infrastructure (e.g. DynamoDB, Aurora, Kinesis).  

The Serverless Platform uses the Application concept as a unit of organization for grouping related logic and infrastructure (like any other software application).

Examples of Applications:

- An entire web, mobile or IoT application
- A single Function

Each Application gets its own subdomain on the Event Gateway that is shared across the parent Tenant.

```
myapp.slsgateway.com
```

### Service

A serverless Service is designed to be a smaller unit of organization than an Application.  Services group together resources that have a lot of interdependencies.  For example, a group of Functions and Resources (e.g. a database) pertaining to your Application's *Users* or *Products*.

An Application can have many Services.  They seek to help you break up large Applications so you can have smaller stacks of infrastructure which you or your team can work on autonomously, without affecting the Application as a whole.  Services can also be used within different Applications.

They are declared by a `serverless.yml` file and provisioned with the Serverless Framework.

Examples of Services:

- A data model's database and logic (e.g. users, products, blog posts).
- A workflow of Functions and Events.
- An entire Application can be put into one Service.

### Function

A serverless Function is a small amount of business logic, usually designed to perform one task.  This logic is typically run on a Functions-as-a-Service/serverless compute service, like AWS Lambda, Azure Functions or Google Cloud Functions.  It can also be in a container.

Examples of Functions:

- Typical microservice use-cases, like saving a user to a database or processing events asynchronously.
- Transforming a piece of data and sending it to another destination.
- Running GraphQL.
- Building an Alexa Skill.

### Event

An Event is data that reports something has happened.  Events trigger serverless Functions.  The Serverless Platform describes all data in-flight as an Event, including asynchronous bits of data, as well as synchronous requests or commands, like an HTTP request.  

Events on the Serverless Platform can be used with or without the Event Gateway.  Though, the Event Gateway gives you powerful abilities to dispatch, route, share and trace Events.

Examples of Events:

- A piece of state that has changed (e.g. user updated)
- A notification that something has happened (e.g. an IoT light turned on)
- A synchronous command or request (e.g. an HTTP request)

### Subscription

A Subscription is an instruction to call a Function when an Event is received.  Subscriptions can be made between external sources and Functions directly (e.g. AWS + AWS S3) or via the Event Gateway as middleware (e.g. AWS S3 + Event Gateway + AWS S3).

### Resource

A serverless Resource is any serverless infrastructure included in your Application/Service, like databases, CDNs, caches, etc.

Examples of Resources:

- AWS S3
- AWS DynamoDB
- AWS Kinesis
- AWS AppSync
- Auth0
- Stripe
- Twilio