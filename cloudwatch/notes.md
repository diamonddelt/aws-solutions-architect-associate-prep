# Cloudwatch

## What does it do?

CloudTrail logs who asked for what in the API, while CloudWatch tracks metrics and related performance events. You can install this on EC2 instances for example (if it doesn't already come installed), and configure it to `collect custom performance and resource metrics in real-time. This is the AWS flavor of Resource Monitor/NewRelic, or APM (application performance monitoring)`

## Creating CloudWatch Dashboards, Alarms, and Metrics

You can create 4 types of Widgets for Dashboards: Text with Markdown, Line Graph, 

`Line Graph` - you can chart various metrics like EC2 or EBS per instance metrics along a line graph.
`Stacked area` - like a multi-line line graph which shades underneath the line of each metric
`Number` - shows a plain number metric in a box for the given metric e.g. `0.07 %`

You cannot start receiving alarms until you confirm the email address the new alarm SNS topic creates.

`Events` are sent to an `event stream`, which you can poll for, looking for specific events you are subscribed to. These events are emitted on state changes of AWS infrastructure, like EC2 instance going from a stopped to a start state.

`Logs` allow you to monitor `HTTP` response codes, `kernel` logs, or `application` logs. These require installing an `agent` on a particular EC2 instance. These are more customized data than `Metrics` provided by default from AWS.


## Exam Tips

1. What Metrics are available by default for `EC2` instances in CloudWatch? `CPU related, Disk Read/Write, Network In/Out, and Status Checks Passed/Failed`. There is `NO RAM UTILIZATION`
2. `Standard Monitoring = 5 minutes; Detailed Monitoring = 1 minute`
3. `CloudWatch` is for `logging and log aggregation`; `CloudTrail` is for `auditing of AWS service usage and reporting who does what` in the AWS console or using the API.