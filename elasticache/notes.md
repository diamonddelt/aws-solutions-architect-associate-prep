# Elasticache

An in-memory caching layer which is typically installed to house the `top X number of queries against a database`, which are commonly run and generate a large performance penalty. Adding the data from those queries in a caching layer allows the app to quickly retrieve the results from there, instead of having to ask the database for it each time.

Elasticache's main goal is `to improve web application performance by providing in-memory caches as an alternative to disk-based databases`

It improves `latency and throughput` for read-havy application workloads or compute-intensive workloads like a recommendation engine

There are two types of caching engines in Elasticache

1. *Memcached* - widely adopted; Elasticache is `protocol compliant` with Memcached, so tools that work with memcached integrate seamlessly with Elasticache
2. *Redis* - a popular open-source in-memory key-value store; supports `sorted sets and lists`. `Elasticache supports Master/Slave replication and Multi-AZ with Redis` which makes this easy to achieve AZ redundancy

## Exam Tips

1. Elasticache is a good solution to a scenario type questions where a particular database is under stress or load, if the database is `read-heavy and not prone to frequent change`. Redshift is a good answer to this question if the stress is being caused by management of OLAP transactions (because OLAP is synonymous with Redshift/Data Warehousing, whereas Elasticache is synonymous with improving performance of commonly cached read-workloads)