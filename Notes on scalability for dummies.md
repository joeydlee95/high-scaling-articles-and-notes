# Notes on scalability for dummies
## [Scalability for Dummies](http://www.lecloud.net/tagged/scalability)

## Cloning
Servers hidden behind load balancer.
* evenly distributes load (requests) on clusters of app servers.
* every server contains exactly the same codebase
* servers store no user-related data
  1. session stored on centralized data store
  2. external persistent cache [Redis](https://redis.io/) > external db
* [Capistrano](http://capistranorb.com/) allows code change is sent to all servers. 
* Or you can use [docker-compose](https://docs.docker.com/compose/)
* Horizontally scaled

## Database
* MySQL = master-slave replication, read from slaves and write to master
 - scale db with more RAM
 - sharding, denormalization, SQL tuning

* NoSQL = denormalized, no more joins
  - MongoDB or CouchDB
  - Joins done in app code
  - soon db requests will be slow again, introduce a cache

* Results:
  - endless storage (in Terabytes)
  - users suffer slower page requests when lots of data is fetched from db

## Cache
* Memcached or Redis
  - Not file-based caching, cloning and auto-scaling is harder
  - key-value store in RAM
  - Redis can do several ~100,000 reads per second being hosted in standard server.

* Caching DB queries
  - query to db, store result dataset to cache
  - problems arise in the expiration, it is hard to delete a cached result

* Cached Objects
  - MOST RECOMMENDED
  - data as objects
  - makes asynchronous process possible
  - objects to cache: user sessions, fully rendered blog articles, activity streams, user relationships with friends.

## Asynchronism
* Do time-consuming work in advanced and serve the finished work with low request time. PRECOMPUTE!
* Turns dynamic content into static content
* These computing tasks are called regularly, maybe by a cronjob
* [RabbitMQ](http://www.rabbitmq.com/) helps implement async processing
* TIME-CONSUMING = PRECOMPUTE ASYNC!



