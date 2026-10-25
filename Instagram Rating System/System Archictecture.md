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

**Memcache as a demand-filled look-aside cache**

The left half illustrates the read path for a web
server on a cache miss. The right half illustrates the
write path
'Memcached' to refer to the source code or a running binary
'Memcache' to describe the distributed system

**Query Cache**

Meta relies on memcache to lighten the read load on their databases.
In particular Facebook , they use memcache as a demand - filled look-aside cache as shown in Figure 1.(Draw.io)
When a web server needs data , it first requests the value from memcache by providing a string key.
 If the item addressed by that key is not cached, the web
server retrieves the data from the database or other back
end service and populates the cache with the key-value
pair. For write requests, the web server issues SQL state
ments to the database and then sends a delete request to
memcache that invalidates any stale data. 

**Why they Chose to delete cached Data instead of updating it**

because deletes
are idempotent. Memcache is not the authoritative source
of the data and is therefore allowed to evict cached data.


**The Several ways to adress excessive read traffic on MySQL databases**


*Why did they choose MemCache*

The goal was to separate the caching layer form the persistence layer allowing them some sort of flexiblity nad independence  - to adjust each layer independently as their workload changes.

**Generic Cache**

They also leverage memcache as a more general key value store . Example : engineers use
memcache to store pre-computed results from sophisti
cated machine learning algorithms which can then be
used by a variety of other applications.

*Words that need non technical research and interpretation*

 It takes little effort for new services to leverage the existing marcher
infrastructure without the burden of tuning, optimizing,
provisioning, and maintaining a large server fleet.
Memcached provides no server to server coordination ; it is an in memeory hash table running on a single server . Their  system provides a suite of configuration , aggregation , and routing services to organize memcached instances into a distributed system.

**Themes that emerge at Meta's Three Deployment Scales**

The primary design concern :  
1. **read heavy workload and wide fan-out** .

 As the neccessity to scale multiple frontend clusters - they address data replication between the clusters 

# Tech Glossary / Assignment 

1. server -server architecture 
2. serverless architecture 
3. marcher infrasructure.
4. In the remainder of this paper we de
scribe how we built a distributed key-value store based
on memcached capable of operating under Facebook’s
workload





 

