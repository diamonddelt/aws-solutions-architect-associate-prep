# S3

## What is it

`Object-based storage` i.e. you upload files to it. Files can be from `0 Bytes up to 5 Terabytes in size.`

`Unlimited` storage, but you pay by the Gigabyte.

S3 bucket URLs look like this:

`https://s3-eu-west-1.amazonaws.com/bucketname`

Where each part of the URI corresponds with data around that bucket, including the `region`, and the `name of the bucket (which must be globally unique)`

`When you upload a file to S3, you will receive an HTTP 200 success response if the upload was successful.`

## What does it do?

Extremely `reliable and durable storage for flat files`

S3 is built for 99.99% availability of the S3 platform, and AWS `guarantees 99.9% availability in the form of an SLA` for S3.
AWS guarantees `11 x 9s of availability for S3 information (objects)`

Stores files in a `bucket`, which is a `universal namespace with a globally unique DNS name`

There are different `tiers` of storage available, `versioning`, `encryption`, `security (ACLs) and bucket policies`, as well as `lifecycle management` rules you can apply.

## Data Consistency Model

1. `New Object PUTS` - when you PUT or add data to S3, the model is *Read after Write* consistency, meaning you can't read any newly added data until the write and replication operations are completed
2. `Overwrite Object PUTS or DELETES` - when you change/modify an object, or delete it, the model is *Eventual Consistency*, meaning that the operation completes almost instantly, but it can take time to fully propagate. So there may be instances where `data retrieval from a modified or deleted S3 endpoint can have unexpected results`, `if that read operation happened right after the time when it was modified or deleted`

Why is there a difference? `S3 is spread across multiple availability zones`, and while replication occurs constantly, `it takes some amount of time`, and the 200 success code for a newly PUT object is only returned once all data has been replicated. This is to avoid distributing an S3 object endpoint which would result in a 404, because replication had not fully completed.

## S3 Objects

An object contains the following

- `Key` = the name of the object
- `Value` = the data; i.e. the sequence of bytes of the object
- `Version ID` = the ID associated with the object; used for versioning of S3 objects
- `Metadata` = data about the data you are storing, like data when it was uploaded, or tags added to the object (department)
- Subresources:
    - `Access Control Lists` = like a NACL for an S3 object; who can actually access this object within the larger group of permissions
    - `Torrent` = can you torrent this object using bitTorrent protocol

## S3 Storage Tiers/Classes

*S3 Standard* = `99.99% availability, 11x9s durability`, stored redundantly across multiple devices and multiple facilities. Can `sustain a loss of 2 facilities concurrently`
*S3 IA (Infrequently Accessed)* = data that is accessed less frequently, but still requires rapid access. `Costs less to store than S3 standard`, but you have to pay a `data retrieval fee`. The thinking is, the data retrieval fee cost is offset by the fact that you access it less frequently, so the lower cost to store the data becomes more relevant to you.
*S3 'One Zone' IA* = `even lower cost than S3 IA` to store data, because you are `losing multiple Availability Zone resilience`. This is not a good choice for data storage that has durability requirements.
*Glacier* = the `cheapest` option, but used `only for data archival` purposes. _Glacier Standard_ takes a `minimum of 3-5 hours to access data`, and you have to `pay a premium to expedite the time to retrieve the data`. You should only use this service when you do not plan to actually need to access stored data here quickly. Mostly for historical record keeping or audit purposes. The three time models to retrieve data from Glacier are `Standard`, `Expedited`, or `Bulk`.

## Types of Encryption

* `Client Side Encryption` (you encrypt the data before it's uploaded on your end)
* Server Side Encryption
    * Server side encryption using `AWS S3 Managed Keys` (SSE-S3)
    * Server side encryption using `KMS` (Key Management Service) (SSE-KMS)
    * Server side encryption with `Customer Provided Keys` (SSE-C)


## Versioning

* Once you enable versioning, `you cannot disable it; you can only suspend it`. Think carefully about enabling it when individual objects in your bucket are `huge` in size and prone to change - this will quickly increase storage costs
* You can enable `MFA Delete`, which requires a multi-factor authentication token to be input from a mobile device in order to even delete an S3 object. `MFA delete requires your security credentials and a serial number + space + 6 digit auth code`


## Charges for Usages

- `Storage` = how much raw data are you storing? This costs per amount of data (GB)
- `Requests` = how many requests to download this S3 object occur per unit of time?
- `Storage Management Pricing` = did you use tags on your S3 object? Did you enable versioning, encryption, etc? These additional services cost more
- `Data Transfer Pricing (Cross-Region Replication)` = it costs money to transfer S3 data from one region to another, because S3 is region specific. I.E `you have to pay to move S3 objects from us-east-1 to us-west-2`
- `Transfer Acceleration` = uses the AWS CDN (CloudFront) to accelerate data transfer from S3 to a specific endpoint, by using the CloudFront endpoints to store the S3 objects there instead.

## Exam tips

1. S3 supports cross-region replication of buckets. When you do this, you have to enable `versioning`
2. If you specify a bucket policy of `DENY` on a bucket, you need to explicity include all IAM resources which need access to the bucket (i.e the resources which `ARE NOT DENIED`). If you are trying to replicate a bucket in region A to region B, and you have setup a DENY bucket policy on bucket A, you need to ensure the role which does the replication is in the exclusion list.
3. If you are given an exam question about choosing the lowest possible cost storage solution, and you don't care about retrieval times, use Glacier.
4. `By default, buckets are private and all objects inside are private`