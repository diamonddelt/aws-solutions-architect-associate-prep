# What is API Gateway

An `API` in an Application Programming Interface.

The example of understanding what an API from a high level is

- Imagine a couple at a restaurant, who want to order some food
- The couple do not want to go directly into the kitchen to ask the chefs to make their food
- The chefs do not want to go directly to the couple to ask them what to make
- The waiter serves as an `API` which allows the couple to `order`, by sending the request and the response back and forth

`API Gateway` is a fully-managed service that allows users to create, maintain, monitor, and secure APIs at any scale. You can link the APIs to any applications running on AWS, such as EC2 instances hosting web apps, code running from a Lambda function, or outside web apps

## Types of APIs

- REST APIs (`RE`presentational `S`tate `T`ransfer)
    - Uses JSON to encapsulate data transfer
    - 70% of overall API usage; intended to replace SOAP
- SOAP APIs (`S`imple `O`bject `A`ccess `P`rotocol)
    - Uses XML to encapsulate data transfer
    - Been around since the 90s

## Typical example

A user using any sort of device (smartphone, pc, IoT, etc) makes a web request to the API Gateway endpoint. The API Gateway determines what should happen based on that request, and forwards the request to other various AWS services, such as Lambda, EC2, or DynamoDB.

## What can API Gateway do

- Expose HTTPS endpoints to define a restful API
    - `api.openweathermap.org/data/2.5/weather?q=London` - an example API endpoint which would return weather data
- Serverless-ly connect to services like Lambda and DynamoDB
- Send each API endpoint to a different target
- Run efficiently with low cost and scales easily
- Track and control usage by API key
- Throttle requests to prevent attacks (DoS, DDos)
- Connect to CloudWatch to log all requests for monitoring
- Maintain multiple versions of the API

## How do you configure API Gateway

1. Define an API (container)
2. Define `Resources` and nested Resources (`URL paths`)
    1. For each resource, select a support `HTTP method (verbs)`, such as GET, POST, PUT, DELETE
    2. Set security on the resource
    3. Choose a target (EC2, Lambda, DynamoDB, etc) for the resource
    4. Set request and response transformations
3. Deploy API to a `Stage` (Dev / Test/ Prod)
    1. Uses API Gateway domain by default, but you can customize the domain
    2. Supports AWS Certificate Manager (free SSL/TLS certs if your domain is hosted in Route53)

## What is API Caching

You can cache common calls to an API which return predictable responses. This allows you to reduce the number of calls to the endpoint and improves the latency of those calls (this reduces the cost). The caching for a stage is specified in `time-to-live` (TTL) periods, in seconds. When API Gateway receives a request for a cached call, it responds from the cache instead of making a request to the given endpoint

## Same Origin Policy

`Same-origin policy` is an important concept in web application security models. A web browser permits scripts contained in a first webpage to access data in a second webpage, but only if both webpages have the same origin.

This is done to prevent Cross-Site scripting (XSS) attacks.

Its enforced by web browsers, but can be ignored by REST testing utilities like PostMan or cURL

## Cross-Origin Resource Sharing (CORS)

`Cross-Origin Resource Sharing` is one way the server at the other end (not the client code in the browser) can relax or circumvent the same-origin policy.

CORS is a mechanism that allows restricted resources (like fonts or form elements) on a web page to be requested from another domain outside of the original domain where the first resource was served.

(CORS is a popular exam topic with respect to API Gateway and S3)

## How does CORS workflow look

1. The browser makes an HTTP `OPTIONS` call for a URL
    1. https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/OPTIONS
2. The server returns a response saying `These other domains are approved to GET this URL`
3. Error - `Origin policy cannot be read at the remote resource?`
    1. This can be thrown when you have not enabled CORS on API Gateway