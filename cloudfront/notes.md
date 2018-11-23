# Cloudfront

This is the AWS `Content Delivery Network (CDN)`

## Key Terms

*Edge Location* - location `where content is actually cached`. This is `separate from an AWS region/AZ`. There are over `50 edge locations across the globe`
*Origin* - the single location of all files that the CDN distributes. It can be an `S3 bucket, and EC2 instance, an ELB, or Route53` (using DNS to determine the endpoints to cache)
*Distribution* - the name given to the CDN which consists of a collection of Edge Locations. This is the term for what you actually `create` in CloudFront i.e. you create a `CloudFront distribution`

*Web Distribution* - typically used for websites
*RTMP* - used for media streaming

## How does the CDN work from the user's perspective?

1. User requests contents from an edge location
2. The first time this request is made, the edge location does not have the data
3. The edge location requests the content from the origin, and caches it for subsequent requests
4. The edge location keeps that content cached for the length of the TTL (which is configured on the distribution)
5. All subsequent requests to that edge location for the same content and much quicker because the request did not have to traverse to the origin like the first attempt
6. Because the first-time attempt is not faster, a common technique which is used is `priming/warming up` the CDN, by making a lot of requests for all possible content types before an application goes live, so users do not have to wait the extra time for first-resource requests.

Requests made from users/clients are `automatically routed to the nearest edge location` to increase performance.

## What types of content can be delivered?

- Dynamic content
- Static content (html/css/js files)
- Streaming data
- Interactive content

## Exam tips

1. You can create a cloudfront distribution (CDN) using a load balancer, an S3 bucket, or a MediaPackage channel endpoint as an `origin`. However, you cannot directly use `Lambda` as an origin.
2. You can `read AND write to edge locations`
3. The TTL (time to live) controls how long the objects are cached
4. You can clear cached objects, but this costs money every time you do it