# Lab 2 - Route53

1. Register a domain name directly from Route53 (I didn't do this because I don't want to pay for another one)
2. Once you own a domain name in Route53, you can see it in `Hosted Zones`, where you can do typical DNS management, such as updating NS records, SOA records, or add CNAMEs or A/AAAA records
    1. https://support.dnsimple.com/articles/a-record/
    2. A Record - points a domain name to an IPv4 address
    3. AAAA Record - points a domain name to an IPv6 address
3. Create an application load balancer for an existing running EC2 instance, which listens on port 80, and health check's /index.html
4. Create a record for the `Naked domain name`, or sometimes referred to as the `Zone Apex` address of the domain you have purchased
    1. If you have purchased a domain called `fancy-sandals.com`, the _Naked domain name_ or _Zone Apex_ is literally `http://fancy-sandals.com`
    2. In AWS, the term `Alias Record` is similar to CNAMEs, but you can create an Alias Record for the Zone Apex/Naked Domain name.
    3. https://support.dnsimple.com/articles/alias-record/
    4. Alias Records are only supported for IPv4 and IPv6 records (A/AAAA Records)
    5. Point the Alias Record at the ALB created in step 3. The `Alias Target` will appear once the ALB is created and verified to be serving the content from the EC2 instance(s)