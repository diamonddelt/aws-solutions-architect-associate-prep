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