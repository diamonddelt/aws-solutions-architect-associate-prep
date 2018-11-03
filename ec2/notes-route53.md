# Notes

## What does Route53 provide?

- Route53 is the AWS DNS (Domain Name Service)
- Allows mapping your domain names to
    - EC2 Instances
    - Load balancers (all types)
    - S3 buckets

### Registering Domain Names

- Route53 allows you to buy a domain name from any of the TLDs available directly from the interface.

### Creating DNS Records

- Route53 allows you to create Alias records which can point at existing AWS resources, such as ALBs, NLBs, EC2 instances, etc.
- You could also add the other supported types of records, including MX, A/AAAA, NS, SOA, and others


### Transferring DNS Records

- Route53 also supports transferring ownership from one DNS Registrar to AWS. So if you owned a domain name from NameCheap, you could transfer ownership to AWS, and manage it from there instead.