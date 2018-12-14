# Notes

## What does Route53 provide?

- Route53 is the AWS DNS (Domain Name Service)
- Allows mapping your domain names to
    - EC2 Instances
    - Load balancers (all types)
    - S3 buckets

### Registering Domain Names

Route53 is a `global` service

- Route53 allows you to buy a domain name from any of the TLDs available directly from the interface

When you buy a TLD such as `.com`, Route53 will create multiple Nameserver (NS) records at multiple other TLDs, such `.co.uk`, `.net`, and `.org`. This is to prevent an outage of your particular domain name if one of the top-level domains goes down.

There are 5 types of `routing policies` for a given `record set` in Route53:

- `Simple` = default routing policy when making a new record set; most commonly used for `single-resource` domains, such as a single web server serving content at http://hello.com. There is no need to make decisions based on where to send traffic, because there is only one resource. If there are more than one resource in a simple routing policy, such as 3 webservers behind a load balancer, the behavior is `round-robin`
- `Weighted` = you can specify `arbitrary percentages of traffic` which are sent to various instances behind a DNS endpoint. `For example, you can say that 20% of all traffic ingressing should go to instances in us-east-1, and 80% of traffic ingressing should go to us-west-2`
- `Latency` = allows you to specify r`ecord sets in different regions that are chosen based on lowest latency`. In other words, when Route53 receives a query for your site, it `chooses the record set in the region with the lowest latency to serve that request`.
- `Failover` = this routing policy will redirect traffic to instances depending on the health of the `primary` region. If the `primary` region goes down, it will route traffic to a `standby` or `secondary` region/instance. This involves creating two record sets: the primary and the secondary
- Geolocation
- Multivalue Answer


### Creating DNS Records

- Route53 allows you to create Alias records which can point at existing AWS resources, such as ALBs, NLBs, EC2 instances, etc.
- You could also add the other supported types of records, including MX, A/AAAA, NS, SOA, and others

## Transferring DNS Records

- Route53 also supports transferring ownership from one DNS Registrar to AWS. So if you owned a domain name from NameCheap, you could transfer ownership to AWS, and manage it from there instead.

## Exam Tips

1. When you register a new domain in Route53, you always have two record sets created by default: an `NS record` (with multiple TLDs registered), and an `SOA record`
2. A `naked domain name` is otherwise known as a domain name with `no prefix in front` of it i.e. `http://domain-name.com`
3. A `zone apex` is the same as a `naked domain name`
4. You can make an `Alias record` for a naked domain name / zone apex. You'd typically assign the `Alias target` to a load balancer
5. In general, you have to choose a `single routing policy/strategy for your Route53 A-records`. You `can't mix and match weighted records with latency based routing` records, for example.