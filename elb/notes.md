# Notes

## What does ELB provide

- Provides three types of load balancers to use across your application, to balance the load on various protocols to hopefully increase the chances that your app stays online during heavy load.


## What are the three types of load balancers on AWS?

- Application load balancer (ALB)
- Network load balancer (NLB)
- Classic load balancer (ELB Classic)

### Application Load Balancer

- Operates on the OSI layer 7 (application layer)
- Smart enough to read where the packets are destined, such as `/sales`, and route them to that endpoint
- Best suited for balancing HTTP/HTTPS traffic, and using advanced routing rules
- For example, send all traffic to a specific set of webservers with a specific application running on them
- Customizability - think of the differences between the makes, models, colors, and package options of the same Subaru

### Network Load Balancer

- Operates on OSI layer 4 (network layer)
- Most expensive load balancer, but the fastest - you would want to use these in production
- These balance TCP traffic, and can handle millions of request per second, with ultra low latencies
- Extreme performance - think of a high end super-car

### Classic Load Balancer

- Amazon no longer recommends using this anymore, but it's maintained for legacy purposes
- They can load balance HTTP/HTTPS and handle sticky sessions or X-Forwarded headers.
- They can also handle layer 4 (network) load balancing for strict TCP applications, although they don't excel at this either.
- Think of a really old convertable car from the 1940s - it can get the job done, but it's old an unreliable

### Common Load Balancer Errors

- If your application stops responding which is hosted on an ELB (Classic load balancer), you are greeted with a 504
    - The important thing to remember is that this isn't being caused by the load balancer, its either the application or the database
    - The load balancer doesn't get a response from the application, so it throws a *Gateway Timeout*

### What is the X-Forwarded-For Header?

- X-Forwarded-For header is sent in a request to a load balancer to enable the application to understand where the _original public IP_ of the request came from
- For example, a user at IP address 124.12.3.231 sends a request to an ELB at private IP address 10.0.0.23
    - Then, that ELB disseminates the request to an EC2 instance, but the EC2 instance would normally only see the request coming from the ELB's private IP address (10.0.0.23).
    - By including the X-Forwarded-For header, the EC2 instance will also know where the _original_ request came from.
    - In other words, think of *who the original request is being forwarded for*
    - Instances would want the original IP address of a request if they wanted to know location information or respond based on specific IP addresses

## Key Exam Terms

- `Application Load Balancer`
- `Network Load Balancer`
- `Classic Load Balancer`
- `504 Gateway Timeout` - this happens when application stops responding within the idle timeout period. Troubleshoot the application or the database. It is not a problem with the load balancer itself.
- `X-Forwarded-For` - use this request header if the application behind the ELB needs the original IPv4 address of any request it receives directly from the load balancer.

## Questions
