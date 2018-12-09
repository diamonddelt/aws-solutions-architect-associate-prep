# What is Lambda

A `compute service` where you can upload code directly to AWS, and AWS Lambda takes care of provisioning servers to run that code, and `scales automatically and continuously`

Highest level of abstraction which frees the developer from worrying about

- No Servers! No containers! No managing infrastructure at all!
- data centers
- hardware
- assembly code/protocols
- lower level operating systems running your code
- networking/routing/switching

## How can you use Lambda

- Event-driven compute service where AWS Lambda runs code in response to an event. Examples include changing data in an S3 bucket or a DynamoDB table
- A compute service to run code in response to HTTP requests using API gateway or API calls made using AWS SDKs.
- Lambda functions can trigger other lambda functions. Chaining them together is a way to build complex web architectures to rival other stack types
- A user can send an HTTP request -> API Gateway. API Gateway forwards that to a Lambda function, which does some work, returns it back to API Gateway, who then returns it back to the user in the HTTP response. This HTTP request/response workflow can and should be done in parallel

## What languages are supported by Lambda

- Node.js
- Java
- Python
- C#
- Go

(Remembering these is most likely an exam question)

## How is Lambda priced

- Number of requests - the first 1 million requests are free per MONTH
    - $0.20 per 1 million requests after you exceed the free tier
- Duration - calculated from the time your code begins executing until it returns or otherwise terminates, rounded up to the nearest 100ms
    - the price depends on the amount of memory you allocate to the function
    - $0.00001667 for every GB-second used


## Other interest facts

- Amazon Echo uses Lambda each time you talk to it. It takes your voice commands, runs them through a natural language processor/understanding, and sends the text commands using Lambda to various services which compute or do what your command requires

## Exam Tips

- You need to know the `list of possible triggers` for Lambda: refer here (https://docs.aws.amazon.com/lambda/latest/dg/invoking-lambda-function.html)
    - From a high-level, any service which is serverless, or generates output data that can be consumed, could trigger lambda. For example, you can trigger from an SNS notification, because this is a `push` event, or output data, or CloudFront, because it spits out log data based on things that are happening in the CDN.
- Lambda scales out (not up) automatically (millions of functions can run in parallel, but if any function runs out of memory, you have to scale that up yourself)
- Lambda functions are independant, 1 event = 1 function
- Lambda is serverless
- And know what AWS services are actually serverless! Lambda, API Gateway, S3, and DynamoDB are serverless, whereas EC2 and RDS (think traditional servers/databases) are not serverless
- Lambda functions can circumvent the 1 event to 1 function rule by triggering other lambda functions. So actually, 1 event can equal X functions if you chain them
- Architectures can be complicated, so AWS X-Ray was designed to debug Lambda functions as they run
- Lambda works globally, so you can back up S3 buckets to other regions and get around the S3 region limitation that way
- Know what can trigger Lambda (a popular exam question). For example, can this event or behavior trigger a lambda function?