# Local First Software

So what is this local-first paradigm and what does it doo and what are its origins

soo the main source for this local-first paradigm is made here by

- Martin Kleppmann
- Adam Wiggins
- Peter van Hardenberg
- Mark McGranaghan

These are the group of researchers that coined this term "Local first software" soo lets dive deep in what is this local-first paradigm and what does it help with

[Kleppmann](https://martin.kleppmann.com/papers/local-first.pdf)

# **What is local-first software** :

These set of principles are made by those researchers due to a trend that was rapidly increasing using cloud providers for compute , storage etc etc . But here comes the tricky part when we store data on a cloud with a provider suppose some X provider it creates a subtle lock in freedom that only few notice which is suppose if a service shuts down or the company shuts down the software stops working as intended and data created with that software is lost  ( not whole data , the data created during time when service is down )

there are 7 Ideals that local-first software must satisfy :

- Fast : the software must be fast due to the fact that data is accessed locally
- Multi-Device Sync : All data must be synced across multiple devices
- Offline : as software uses local data it should work offline
- Collaboration : should be able and capable enough to enable seamless collaboration among multiple users
- Longevity : a users data should continue to be accessible even after that company produced software is gone
- Privacy :  software must be secure and must use end to end encryption
- User control : Company must not be able to restrict what user can do

Here if u observe carefully your precious data is in hands of the cloud provider and they are like having authority to enable access to you so this local-first paradigm emerged to solve this

local first software save data locally and then sync that data with server here highest priority is for local data rather than the cloud for browser based apps many people used [indexedDb](https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API)  which is  clunky to write and  when u are developing software this is not a issue u wanna face soo then came wrappers for this indexedDB wrappers which include [Rxdb](https://rxdb.info/) , [dexie-js](https://dexie.org/product) where the data storage of client side is taken care of but one might reasonably ask if data is stored locally and servers are just used for data sync then wont there be any problems in syncing the data

You are damnn right there are many problems that rise here because this is a problem of  **distributed systems** and if u know a thing are two about distributed systems u know how hard of a thing this is

There are multiple approaches to solve those syncing problems that raise

## Naive approach - Last writer wins:

this approach states that we just update the data to whoever updates the data in last this might be seen as a viable but when the number of users increase and no of options increase this breaks very quickly

there are some more better approaches such as OT which was made for text editing but then came CRDT which exists for many types and can handle much more than text

## Operational Transformation :

This is a technique that is behind early collaborative editors like google docs, where data is sent to server and server adjusts and gives a sense and this was mainly designed for text

## CRDT :

Conflict free replicated data types is a data structure designed so that copies can be edited independently and merged to get same result in any order but without any central referee  there are libraries such as Automaker and Yjs but there are some issues here

- they work on character level and store data as ( "CHAR" , ID ) which can use more memory than normal and a automatic merge might not make sense
- They cant enforce rules

## Sync Engines :

Sync engine is a software that keep all devices in sync while taking care of conflicts that   may arise and also manage much more things such as internet connection , retrying etc etc , some of famous sync engines in web world are [Zero](https://zero.rocicorp.dev/) , [PowerSync](https://powersync.com/) they are super fast and take care of many things under the hood

## Working Flow :

```other
flowchart LR
    1["1. User Input"] --> 2["2. UI"]
    2 -->|"Write"| 3[("3. Local DB")]
    3 -->|"Live Data"| 2

    3 -->|"Sync"| 4["4. Sync Engine"]
    4 --> 5[("5. Server DB")]

    5 -->|"Changes"| 4
    4 -->|"Sync"| 3

    5 -->|"Changes"| 6["6. Other Device"]
    6 --> 7[("7. Other Local DB")]
    7 --> 6
```

many apps or websites that u might know already use this this approach can give good UX by instantly updating data and UI  but it has its own tradeoffs

References : [https://powersync.com/blog/local-first-software-origins-and-evolution](https://powersync.com/blog/local-first-software-origins-and-evolution)

research paper : [https://martin.kleppmann.com/papers/local-first.pdf](https://martin.kleppmann.com/papers/local-first.pdf)

I started writing blogs recently if there are any problems and issues with blog u can contact me inavoluvathsav@gmail.com

Thank You for reading

