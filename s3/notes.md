# S3

## What is it

`Object-based storage` i.e. you upload files to it. Files can be from `0 Bytes up to 5 Terabytes in size.`

`Unlimited` storage, but you pay by the Gigabyte.

S3 bucket URLs look like this:

`https://s3-eu-west-1.amazonaws.com/bucketname`

Where each part of the URI corresponds with data around that bucket, including the `region`, and the `name of the bucket (which must be globally unique)`

`When you upload a file to S3, you will receive an HTTP 200 success response if the upload was successful.`

## Data Consistency Model

1. `New Object PUTS` - when you PUT or add data to S3, the model is *Read after Write* consistency, meaning you can't read any newly added data until the write and replication operations are completed
2. `Overwrite Object PUTS or DELETES` - when you change/modify an object, or delete it, the model is *Eventual Consistency*, meaning that the operation completes almost instantly, but it can take time to fully propagate. So there may be instances where `data retrieval from a modified or deleted S3 endpoint can have unexpected results`, `if that read operation happened right after the time when it was modified or deleted`

Why is there a difference? `S3 is spread across multiple availability zones`, and while replication occurs constantly, `it takes some amount of time`, and the 200 success code for a newly PUT object is only returned once all data has been replicated. This is to avoid distributing an S3 object endpoint which would result in a 404, because replication had not fully completed.

## What does it do?

Extremely `reliable and durable storage for flat files (11 9s of availability)`

Stores files in a `bucket`, which is a `universal namespace with a globally unique DNS name`

## Exam tips

1. S3 supports cross-region replication of buckets. When you do this, you have to enable `versioning`
2. If you specify a bucket policy of `DENY` on a bucket, you need to explicity include all IAM resources which need access to the bucket (i.e the resources which `ARE NOT DENIED`). If you are trying to replicate a bucket in region A to region B, and you have setup a DENY bucket policy on bucket A, you need to ensure the role which does the replication is in the exclusion list.