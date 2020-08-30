# Basics and Key Concepts of Elasticsearch


### Getting Started with Elasticsearch Basics

This week finally I started learning Elasticsearch, I decided to keep some notes and share my concepts and understanding on this blog. So that if anyone wants to learn Elasticsearch he/she can learn with me.

In this part, I will write about the some Elasticsearch theory and basic concepts anyone needs to understand. Most of them I learned form [Elasticsearch](https://www.elastic.co/) official site and some videos on youtube.


##### _What is Elasticsearch?_


_Elasticsearch_ is a distributed, real-time, RESTful search and analytics engine. Its also a NoSQL database, which written in Java and built on top of [Apache Lucene](https://lucene.apache.org/core/) technology like [Solr.](http://lucene.apache.org/solr/)  It has Inverted indices and it is very easy to scale. You can speak to it using RESTful API with JSON over HTTP, using a web client from your favorite programming language, or even from the command line. It's also open-source, it is available under the [Apache 2 license.](http://www.apache.org/licenses/LICENSE-2.0.html)

Elastic Search comes with lots of buzzwords and some key concepts, let me explain some of them a little...

**Near Real Time:** A near real-time search platform means there is a slight latency. When you index a document normally within one second it becomes searchable.

**Distributed:** Elasticsearch is distributed by nature, I can start a node on my machine, and if you were to start nodes on your laptop's they'd start talking to each other and form a cluster and they'd be able to spread the load up between the cluster. Which makes it really scalable. You can give it more hardware and it knows how to spread all the loads across all of this hardware automatically.

**Schema-less:** A schema is a description of one or more fields that describe the document type and how to handle the different fields of a document.

Elasticsearch is schema-less which not completely true, it has the ability to be schema-less, which means that documents can be indexed without explicitly providing a schema. If you do not specify a mapping, Elasticsearch will by default generate one dynamically for you when detecting new fields in documents during indexing.

**Cluster:** A cluster is a collection of one or more nodes (servers) that together holds your entire data and provide federated indexing and search capabilities across all the nodes. Every cluster has a unique name, by default it is `elasticsearch`. A node can be configured to join a specific cluster by the cluster name.

**Nodes:** A node is a single server that is part of your cluster, stores your data, and participates in the cluster’s indexing and search capabilities. A node also identified by a name which is by default is a random _Universally Unique IDentifier (UUID)_ that is assigned to the node at startup.

By default, each node is set up to join a cluster named `elasticsearch` which means that if you start up a number of nodes on your network and—assuming they can discover each other—they will all automatically form and join a single cluster named `elasticsearch`.

**Index:** An index is a collection of documents that have somewhat similar characteristics. An index is identified by a name (that must be all lowercase) and this name is used to refer to the index when performing indexing, search, update, and delete operations against the documents in it. In a single cluster, you can define as many indexes as you want.

**Type:** Within an index, you can define one or more types. A type is defined for documents that have a set of common fields. For example, let’s assume you run a blogging platform and store all your data in a single index. In this index, you may define a type of user data, another type of blog data, and yet another type of comments data.

**Documents:** A document is a basic unit of information that can be indexed. For example, you can have a document for a single customer, another document for a single product, and yet another for a single order. This document is expressed in [JSON](http://json.org/) (JavaScript Object Notation) which is a ubiquitous internet data interchange format. Within an index/type, you can store as many documents as you want.
[table id=1 /]

**Shards & Replicas:** Let's say you have a 1 TB machine and your data is on it. If your data is growing really fast - at one point, you'll run out of that 1 TB and disk space may not fit on the disk of a single node or may be too slow to serve search requests from a single node alone. To solve this problem, Elasticsearch provides the ability to subdivide your index into multiple pieces called shards. When you create an index, you can simply define the number of shards that you want. Each shard is in itself a fully-functional and independent "index" that can be hosted on any node in the cluster.


A shard is an unbreakable entity in Elasticsearch, in the sense that a shard can only stay on one machine (Node). An index which is a group of shards can spread across multiple machines (ES nodes) but shards can not.


Now In a network/cloud environment where failures can be expected anytime, it is very useful and highly recommended to have a failover mechanism in case a shard/node somehow goes offline or disappears for whatever reason. To this end, Elasticsearch allows you to make one or more copies of your index’s shards into what are called replica shards, or replicas for short.


To summarize, each index can be split into multiple shards. An index can also be replicated zero (meaning no replicas) or more times. Once replicated, each index will have primary shards (the original shards that were replicated from) and replica shards (the copies of the primary shards). The number of shards and replicas can be defined per index at the time the index is created. After the index is created, you may change the number of replicas dynamically anytime but you cannot change the number of shards after-the-fact.

For today I will stop here, [next part](https://rimonmostafiz.com/post/installing-and-running-elasticsearch/) is about Elasticsearch Installation.

