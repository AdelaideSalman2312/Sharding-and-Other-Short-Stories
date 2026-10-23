# System Architecture 

**Scaling Memcache

Social networking sites are known for presenting significant challenges in design . Imagine hundreds of millions and now probably billions use this networks everyday - this imposes computational , network and I/O demands that can be notoriously difficult to satisfy .
 A social network’s infrastructure needs to :

 --
(1) allow near real time communication - refreshing likes , comments , shares , reposts and saves .

(2) aggregate content on-the-fly from multiple sources - you should see a reel, a note , a comment you shared go live.

(3) be able to access and update very popular shared content - so Imagine Kim Kardashian with her 400 million followers posts something that goes viral how will the system handle that .

(4) scale to process millions of user requests per second.- somebody in Kenya is liking , another in Zambia is commenting on somebody's comment .


Meta used Memcached the open source version and improved it to be the building block to construct the distributed key and value store for one of the largest social network in the world .
They  focused on memcached—an open-source implementation
of an in-memory hash table—as it provides low latency
access to a shared storage pool at low cost. These quali
ties enable them  to build data-intensive features that we use for interactions today - a decade plus later.
What Memcache does that would otherwise be impractical ?
Making web pages routinely fetch thousands of key
value pairs from memcached servers.

**Overview of Bottlenecks**
1. Users consume a magnitude more of content than they create .
This behavior suggests that the design should bear in mind for a workload dominated by fetching data and suggests that caching
should be at the forefront of the design.

2. Operations fetch data from a variety of sources : MySQL databases ,HDFS installations, and backend
services. This heterogeneity requires a flexible caching
strategy able to store data from disparate sources. 

