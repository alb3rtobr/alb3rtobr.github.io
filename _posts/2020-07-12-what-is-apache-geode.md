---
title: "What is Apache Geode?"
date: 2020-07-12
categories: [Dev]
tags: [geode, opensource]
toc: true
---

One year and a half ago I started working as open source developer, with the goal of contributing to [Apache Geode](https://geode.apache.org/). When I tell people I work with Geode, most of them don't know the product, but when I tell them what is Geode they are able to name 1 or 2 similar products (actually that happened to me first time I heard about Geode :) ).

This week I gave a presentation at work that included a short introduction about what is Apache Geode, its main components and features... I thought that it could be a good idea to write down what I presented (although it was just a basic introduction) and publish it as a contribution to spread the word about Geode. And this post is the result. So let's start!

What is Apache Geode?
------
Documentation says that "*Apache Geode is a data management platform that provides real-time, consistent access to data-intensive applications throughout widely distributed cloud architectures.*" But long-story short: Geode is an in-memory data grid. So next question is.. what is an in-memory data grid?

There are a lot of definitions out there, but I like this one I saw on other Geode presentation:

>In-memory date grids provide a lightweight, distributed, scale-out in-memory object store — the data grid.
>
>Multiple applications can concurrently perform transactional and/or analytical operations in the low-latency data grid, thus minimizing access to high-latency disk-based data storage.
>
> Source: https://www.gartner.com/reviews/market/in-memory-data-grids


That sounds like a cache to me. A lot of use cases of an in-memory data grid implies caching, I guess this is why you can see the term "*in-memory data grid*" used as an equivalent for "*cache system*". But I think they are not exactly the same. For example, if you use an in-memory data grid as your data base, your are not on a cache system's use case (although the clients of your IMDGs could be caching values from it).

Main components
------
A Geode cluster is mainly composed by **cache servers**, **regions**, **locators** and **clients**.

![Geode main components]({{ "/assets/img/geode-main-components.png" | relative_url }})

Locators have dynamic information about the cluster and provide peer discovery for the servers and server discovery for the clients. They also provide load balancing of connections to the servers.

Clients are used by applications, and provide a local cache to them.  

Servers' are in charge of hosting regions, which provide key-value storage. These keys and values can be complex Java objects. Regions are ConcurrentHashMaps, so as any hash map values are stored in buckets and a hash of the key allows to distribute the data in the different buckets.

Depending on how you handle these buckets, there are different kind of regions:

* **Local regions**: these regions only exist in the server where they are created. They contain the whole set of buckets.

* **Replicated regions**: like local regions, but replicated in two or more server. Each server contains the whole set of buckets. This regions are recommended for small data sets with high read rate.

* **Partitioned regions**: in this case, the buckets are divided across different servers. Each server contains a subset of the whole data set, and also could contain redundant copies of buckets stored in other servers.

Some interesting features
------
* **PDX Serialization**: Geode supports three serialization formats, but the most interesting is PDX. It allows to read object fields without deserializing the whole object and it has support for object versioning. It works for Java and native clients.

* **Server functions**: Geode has an API to implement and distribute your own functions into the servers, so your clients can call them, and they will be executed in the same server that hosts the data you need.

* **WAN replication**: Geode allows to use a multi-site configuration, where several clusters are connected via WAN. In this case, Geode provides asynchronous replication between geographical separated clusters using what are called Gateway Senders and Gateway Receivers.

* **Continuous queries**: Allows clients to subscribe to server-side events that modify the result of a given query. For example, imagine you have a region storing orders from an online store. You can define a query to select all the orders which value is bigger than 100€. From that point on, you will receive any event that provokes a change in the result of that query.

* **gfsh**: Geode's CLI. You can start, manage and monitor Geode processes with it.

* **Pulse**: a web dashboard to monitor Geode clusters and all its members.

Origin of Geode
------
After putting together some public information available in the internet, I think I have compiled something like "the unofficial story of Geode" :) :

It all started in 1982 when GemStone Systems was founded in Beaverton, Oregon. This company had two products called GemStone/S and GemStone/J ( 'S' stands for Smalltalk, and 'J' for Java). In 2002, they released the first version of GemFire, which it seems was based on GemStone/J. In 2010 VMware acquired GemStone Systems, and three years later they sold the GemStone smalltalk business, which is the origin of a new company called [GemTalk Systems](https://gemtalksystems.com/).

Also in 2013, Pivotal is created as a VMware spin-off, so GemFire became Pivotal GemFire. Two years later in 2015 most of Pivotal GemFire code base is donated to the Apache Foundation, entering in the Apache incubator as Apache Geode.

Finally, in 2016 Geode became a graduated project. Also that year was the first edition of the Apache Geode Summit.
Since then Pivotal GemFire (which now is [VMWare Tanzu GemFire](https://tanzu.vmware.com/gemfire), due to VMware acquired Pivotal at the end of 2019) is known as the commercial version of Apache Geode.

The Geode repositories
------
Geode code is hosted on [Github](https://github.com). The main repository *[apache/geode](https://github.com/apache/geode)* has more than one million lines of code, and its mostly Java. There are also other repositories, like:
* *[apache/geode-native](https://github.com/apache/geode-native)* : contains the C++ and C# clients.
* *[apache/geode-examples](https://github.com/apache/geode-examples)* : good set of examples that makes easier to jump into Geode.
* *[apache/geode-benchmarks](https://github.com/apache/geode-benchmarks)* : benchmark tests based on GridGain's Yardstick framework.


How to know more
------
If you want to learn more about Geode, the starting point is the [official documentation](https://geode.apache.org/docs/), but if you want to learn by coding, you can use the geode-examples repository I mentioned before and the "[Apache Geode By Example](https://www.youtube.com/playlist?list=PL62pIycqXx-SrrC-iIYJmIEojOo3V27ho)" Youtube list.
