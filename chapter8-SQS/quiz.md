# Quiz - SQS

1. What is the maximum long poll time out?
    1. 20 seconds
2. An SQS message can be delivered multiple times.
    1. True
3. SQS was the first service on the AWS platform?
    1. True
4. You have a fleet of EC2 instances that are constantly polling empty SQS queues, burning CPU cycles and costing your company money. What should you do?
    1. Enable SQS Long Polling (which increases the time between a poll/request, saving money)
5. You are designing a new application that processes payments and delivers promotional emails to customers. You need to ensure that the payment process takes priority over the creation and delivery of emails. How might you use SQS to achieve this.
    1. Use 2 SQS queues for the platform. Have the EC2 fleet poll the payment SQS queue first. If this queue is empty, then poll the promotional emails queue. (in other words, monitor the payment queue, and only check the processing one if the payment queue is empty)
6. Your EC2 instances download jobs from an SQS queue. However, they are taking too long to process the messages. What API call can you use to extend the length of time to process the jobs?
    1. ChangeMessageVisibility
7. What is the maximum visibility of an SQS message in a queue?
    1. 12 hours
8. You run a video-hosting website with two types of members: premium, fee-paying members; and free members. Each video that is uploaded is processed by a fleet of EC2 instances, which poll an SQS queue as videos are uploaded. However, you need to ensure that the videos uploaded by your premium, fee-paying members have a higher priority than those of your free members. How might you work with SQS to endure priority treatment of the premium members' videos?
    1. Create two SQS queues — one for premium members, and one for free members. Program your EC2 fleet to poll the premium queue first and, if empty, to then poll your free members SQS queue.
9.  Which Amazon service can you use in conjunction with SQS to "fan out" SQS messages to multiple queues.
    1.  SNS
10. What is the maximum retention period for an SQS message?
    1.  14 days
11. How large can an SQS message be?
    1.  256KB
12. What is the default visibility timeout for a message in an SQS queue?
    1.  30 seconds