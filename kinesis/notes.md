# AWS Kinesis

Kinesis is a fully managed service for real-time processing of `streaming data`.

Common application use-cases for Kinesis are website clickstreams, application logs, social media feeds, and other `real-time` data consumption models

Examples:

1. Collecting real-time `sentiments` posted on social media over whether people like or dislike the president, and calculating percentages of favor or disfavor for the president based on the real-time data. This could also be called `sentiment analysis`

## Exam Tips

1. Questions asking about ways to `consume big data` are usually asking about Kinesis
2. To `process` the data you consume from Kinesis, the logical AWS services to choose are:
    1. `Redshift` for business intelligence
    2. `Elastic Map Reduce` for Big Data Processing