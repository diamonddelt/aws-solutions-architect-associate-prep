# The AWS Well-Architected Framework

## Business Benefits of Cloud

- Almost zero upfront infrastructure investment; `just-in-time` infrastructure (when you need it, upgrade it)
- Resource and usage-based cost models
- Reduced time to deploy to international markets (overseas especially)

## Technical Benefits of Cloud

- Automation - "Scriptable infrastructure"
- Autoscaling which responds to real-time changes in load
- More efficient development and testing cycles
- Disaster recovery options and BCP options to extend or failover into the cloud

## Design Infrastructure for Failure

- Be pessimistic when desigining infrastructure i.e. `assume all parts will fail, and implement strategies to recover from those failures automatically`. Especially focus on hardware failure, such as natural disasters, DoS attacks, or internal subversion. How will you handle your application if an entire data center blows up in a fire? What about if you get 1 billion requests per second another day?
- `Decouple` all components when possible (i.e. remove hard or tight dependencies)

## Implement Elasticity

- You can scale your application proactively in a `cyclical` nature (i.e. in anticipation of future demand on a fixed interval)
- You can scale your application proactively based on `events` (such as before a new product launch or before a major holiday)
- You can autoscale `based on demand (reactively)`, using real-time monitors of metrics like traffic, load, and utilization of webservers

## Security Models for Applications

- Leverage the AWS EC2 Security Groups as a firewall when possible, locking down `web servers to port 80 and 443`, only allowing` SSH port 22 to app servers` within a corporate intranet or VPN, and `deny all access to DB servers` from any source other than the application itself

## Five Pillars

- Security
- Reliability
- Performance Efficiency
- Cost Optimization
- Operational Excellence

## General Principles

- Stop guessing your capacity needs, but rather build in the ability to scale up or out based on real-world demand
- Always test systems at _production scale_ i.e. test systems as if they were deployed to production
- Automate architectural processes and systems so you can experiment and build up/tear down easier
- Allow for evolutionary architectures (i.e. systems that can be expanded upon when new opportunities/business materializes, without having to do more upfront investing)
- Data-driven architectures are preferred (i.e. systems which are designed around metrics and real-world data to support the architecture choices, as opposed to personal preferences)
- Improve through `game days`

## Security Pillar

- Apply security at every level of the architecture (EC2 instances, security groups, network layer, etc)
- Enable logging, monitoring, and traceability (find out where attacks come from)
- If a security event is triggered, automate as much as possible responses to those events (including lock-down procedures, fail-overs, and fail-safes)
- Automate security best practices (examples being created a `hardened` base AMI, and spin up instances from that AMI)

## Security Pillar - Shared Responsibility Model

- The customer is typically responsible for `data` on AWS, as well as IAM configuration, OS, network, and firewall configuration, as well as choosing an encryption and network traffic protection method
  - `Security IN the cloud`
- AWS is typically responsible for `hardware and service offerings`, such as compute, storage, database, networking primitives, as well as the globally available regions, AZs, and edge locations
  - `Security OF the cloud`

## Security Pillar - Definitions

- `Data protection`
  - Classify your data into security `categories`, like public, sensitive, private, and implement a principle of least privileged access to secure data
  - Most importantly, `encrypt everything` when possible
  - Questions to ask
    - How are you encrypting and protecting your data `at rest`, and `in transit (SSL)`?
- `Privilege Management`
  - Ensures only authorized and authenticated users can access resources
  - Uses ACLs, Role-based access controls, and policies
  - Questions to ask
    - How are you protecting access and using root account credentials?
    - How are you controlling human access to the AWS CLI or console
    - How are you limiting access from services, apps, and third-parties to AWS resources?
    - How are you managing keys and credentials?
- `Infrastructure protection`
  - How do you protect your data center _outside of the cloud_ ? Things like RFID controls, CCTV cameras, door locks, etc
  - Questions to ask
    - How are you enforcing network and host-level boundary protection?
    - How are you enforcing AWS service-level protection (password protection policies, etc)
    - How are you protecting EC2 instance operating systems (antivirus/antimalware)
- `Detective controls`
  - Use tooling from AWS to detect or identify security breaches/threats, such as AWS CloudTrail, CloudWatch, Config, S3, and Glacier
  - Questions to ask
    - How are you capturing and analyzing AWS logs?

## Security Pillar - Exam Tips
- 4 areas: Data protection, Privilege Management, Infrastructure protection, Detective controls

## Reliability Pillar

Basically, the reliability pillar is all about making sure your infrastructure and AWS resources have fail-safes built in to ensure that failure in individual components does not actually bring down overall service.

- `Foundations`
  - You should test recovery procedures and automate failure recovery systems when possible
  - Scale horizontally to increase aggregate system availability
  - If you guess capacity, it can either be over or under-provisioned. Either case hurts you (with under being the worst from an SLO perspective)
  - It's important to acknowledge the `service limits` imposed by AWS on new accounts by default. These can be modified (usually) by requesting changes via ticket.
  - Systems Involved - IAM, VPC
  - Questions
    - How are you managing service limits for your account (is there a person assigned to monitor this?)
    - How did you design your network topology?
    - Do you have an escalation path to deal with technical issues if they arise?
- `Change Management`
  - Automating change management is very possible with AWS, and can be done in lock-step with auditing for compliance
  - CloudWatch and CloudTrail are primary offerings here for monitoring and auditing, respectively
  - Systems Involved - CloudTrail
  - Questions
    - How does your system adapt to changes in demand?
    - How are you monitoring AWS resources?
    - How are you executing change management?
- `Failure Management`
  - Architect your systems and solutions with the assumption that failure `will` occur
  - Have regular post-mortems about failures and learn from them, and improve systems to account for those failures next time
  - Systems Involved - CloudFormation
  - Questions
    - How are you backing up your data?
    - How does your system withstand component failures?
    - How are you planning for recovery?

## Reliability Pillar - Exam Tips
- 3 areas: Foundations, Change Management, Failure Management

## Performance Efficiency Pillar

How to efficiently use cloud resources and keep up with evolving technologies and standards

- Democratize advanced technologies
- Go global in minutes
- Use serverless architectures when possible
- Experiment more often

## Performance Efficiency - Best Practices

- `Compute` - choose the best virtual compute and RAM for your needs (this depends on your application)
  - Questions
    - How do you select the appropriate instance type for your system?
    - How do you ensure that you continue to have the most appropriate instance type as new instance types come out (EC2)
  - Systems involved: Autoscaling
- `Storage` - storage best practices depends on multiple factors { `access method: block, file, or object | patterns of access: random, sequential | throughput required | frequency of access: online, offline, archived | frequency of updates | availability | durability` }
  - Questions
    - How do you select appropriate storage solution for your system?
    - How do you ensure you have the appropriate storage as new storage types come out?
    - How do you measure and manage performance, read/write efficiency, and database types and how they impact performance
  - Systems involved: EBS, S3, Glacier, RDS, DynamoDB, Redshift
- `Space/Time trade-off` - you can utilize other services besides pure storage to improve data retrieval, including direct-connect (to improve VPN latency), Elasticache (to reduce access times of frequently used KV pairs), CloudFront (to improve client-side resource request response time)
  - Questions
    - How to select appropriate solution now, as well as ensure you keep up with latest advancements in caching/proximity
    - How do you monitor proximity/caching solutions to ensure they meet demand and perform as expected?
  - Systems involved: Elasticache, CloudFront, RDS Read-Replicas, Direct Connect

## Cost Optimization

Cost optimization is all about reducing costs to a minimum while meeting business objectives.

## Cost Optimization - Design Principles

- Transparently explain/attribute expenses (i.e. this is what each department spent via cost explorer)
- Use managed services to reduce cost of ownership
- Trade capital expenses for operating expenses (instead of buying an entire server outright, you lease it by the hour you use it)
- Stop spending money on datacenter operations

## Definitions

- Matched supply and demand: you should align supply with demand, and use services to alert you when you need more resources, when you are using too many, and serverless resources that only trigger based on need
- Cost-effective resources: always use the right instance type for cost savings; an instance too large costs more than you need, and too small might cause an outage causing you penalties
- Expenditure awareness: cloud introduces a need to be proactive about usage and cost, because the supply is unlimited; if you aren't monitoring what you are using, the costs could escalate quickly and surprise you. Billing alerts are a must to set up.
    - What controls do you have in place to govern your cost usage? How do you monitor and decommission resources no longer needed?
- Optimizing over time: keep track of changes in AWS over time, and keeping tabs on the newer services to see if a newer offering makes more sense now for your unique business model