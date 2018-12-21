# Route53 Quiz

1. In Route53, which of the following are true?
    - A CNAME record `assigns an Alias name to a Canonical Name`. (`CNAME stands for Canonical Name`)
    - `Alias` Records provide a `Route 53–specific extension to DNS functionality`
2. You have an enterprise solution that operates Active-Active with facilities in Regions US-West and India. Due to growth in the Asian market you have been directed by the CTO to ensure that only traffic in Asia (between Turkey and Japan) is directed to the India Region. Which of these will deliver that result? (Choose 2)
    - R53 - `Geolocation` routing policy (routes traffic based on national boundaries)
    - R53 - `Geoproximity` routing policy (routes traffic based on latitude/longitude)
3. Route53 is named so because ________.
    - The DNS Port is on `Port 53` and Route53 is a DNS Service.
4. True or False: There is a limit to the number of domain names that you can manage using Route 53.
    - True and False. With Route 53, there is a `default limit of 50 domain names`. However, this `limit can be increased by contacting AWS support`.
5. Route53 does not support `zone apex records (naked domain names)`.
    - False (it `definitely does`)
6. You have created a new subdomain for your popular website, and you need this subdomain to point to an Elastic Load Balancer using Route53. Which DNS record set should you create?
    - `CNAME` (because you `can't point a CNAME directly at an IP address`, and `Elastic Load Balancers only expose domain names`)
7. Which of the following Route 53 policies allow you to a) route data to a second resource if the first is unhealthy, and b) route data to resources that have better performance?
    - Failover Routing and Latency-based Routing