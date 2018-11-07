# Dynamo DB

The most common and popular NoSQL solution on AWS. Stores documents as JSON objects with key/value pairs. Used for `unstructured` data - i.e. non-relational.

DynamoDB supports `document` and `key/value` models. 

Creating a new instance of DynamoDB is called a `table`. You can also reserve capacity, like in EC2, for a cheaper price. These are also 1 or 3 year contracts.

DynamoDB is stored on SSD storage in `3 geographically distinct data centers`.

There are two types of reads (since the data is spread across multiple data centers)

1. *Eventual Consistent Reads* - consistency across all copies of the data is usually achieved within a second. This has the `best read performance`, but you may need to repeat a read if the data was in the process of updating when you accessed it
2. *Strongly Consistent Reads* - only returns a read result after all writes were received. You would choose this model if your application cannot handle instances where a read operation does not have the most up to date data (`best reliability`)

DynamoDB charges you `separately for write and read operations`. These are measured in _read capacity units_ and _write capacity units_


## Exam Tips

1. When you think of Dynamo DB, think `single digit latency` - you would always choose a NoSQL solution for a `scalable and fully managed database` that can be in `multiple regions` at once. It is very fast.
2. When you are presented with possible choices for a NoSQL database, choose DynamoDB for `push button scaling` with no downtime