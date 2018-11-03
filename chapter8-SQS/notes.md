# Simple Queue Service

## What is SQS?

- A web service that gives you access to a message queue to store messages in a holding area, to allow other systems/processes to read them incrementally
- `Messages can contain up to 256KB of test in any format` <- EXAM QUESTION ->
- The SQS queue can automatically resolve conflicts between consumer or producer working faster than the other in the queue workflow, or bad connectivity
- SQS supports multiple readers and writers interacting with the same queue
- SQS is a distributed queue, and supports two types of queues
    - `Standard Queue` - unlimited number of transactions per second (TPS) per API action
        - `At Least Once` delivery - meaning each message in the queue is delivered at least once, but possibly more than once. This is usually not a problem for distributed systems, who only care about getting a certain type of message, not necessarily when or how many times.
        - Less expensive option
    - `FIFO Queue` - "First in, First Out" supporting up to 300 messages per second. You would use this is message order is important to you
        - Supports `Exactly Once Processing` - meaning a message will be delivered only once
        - More expensive option
- SQS supports `Long Polling` as a way to save money. Long polling allows a polling time (maximum 20 seconds) to wait for a message to arrive in the queue, before returning a response. Each poll costs you money, so allowing a longer polling time can translate to less requests you are charged for if the data being sent into the queue takes awhile to get there.
- `Fanning Out` menas using an SNS topic to subscribe to multiple SQS queues. So when the SNS topic receives a message, it is sent to all of the SQS queues subscribed to. This allows you to send the same message to multiple SQS queues at the same time (in other words, a work-around to send a single message to multiple SQS queues - I guess this isn't supported officially)

## Exam Tips

1. Asynchronously `pull` task messages from the queue (SQS always `pulls` - never pushes. A push operation might be more like SNS) <- EXAM QUESTION ->
2. Do some work or processing on the message in the queue. The queue will maintain the message based on a visibility timeout period
3. The visibility timeout period `only starts when a service retrieves/pulls a message from the queue` <- EXAM QUESTION ->
4. You are billed for using SQS in 64KB `chunks`. Each 64KB chunk is considered `1 request`. So a 256KB payload = 4 requests
5. First 1 million SQS requests per month are free in free tier. $0.50 per 1 million SQS requests per month afterwards
6. A single request can have from 1 to 10 messages, up to a maximum payload of 256KB
7. When you the word `decouple your application`, think SQS
8. `Default visibility timeout is 30 seconds`
9. `Maximum visibility timeout is 12 hours`
10. You can use the `ChangeMessageVisibility` API action to set a new timeout value
11. The maximum retention period for an SQS message is `14 days`.