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