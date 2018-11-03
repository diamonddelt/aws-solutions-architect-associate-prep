# Lambda exam tips

- Lambda scales out (not up) automatically (millions of functions can run in parallel, but if any function runs out of memory, you have to scale that up yourself)
- Lambda functions are independant, 1 event = 1 function
- Lambda is serverless
- And know what AWS services are actually serverless! Lambda, API Gateway, S3, and DynamoDB are serverless, whereas EC2 and RDS (think traditional servers/databases) are not serverless
- Lambda functions can circumvent the 1 event to 1 function rule by triggering other lambda functions. So actually, 1 event can equal X functions if you chain them
- Architectures can be complicated, so AWS X-Ray was designed to debug Lambda functions as they run
- Lambda works globally, so you can back up S3 buckets to other regions and get around the S3 region limitation that way
- Know what can trigger Lambda (a popular exam question). For example, can this event or behavior trigger a lambda function?