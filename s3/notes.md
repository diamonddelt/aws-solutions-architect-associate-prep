# S3



## Exam tips

1. S3 supports cross-region replication of buckets. When you do this, you have to enable `versioning`
2. If you specify a bucket policy of `DENY` on a bucket, you need to explicity include all IAM resources which need access to the bucket (i.e the resources which `ARE NOT DENIED`). If you are trying to replicate a bucket in region A to region B, and you have setup a DENY bucket policy on bucket A, you need to ensure the role which does the replication is in the exclusion list.