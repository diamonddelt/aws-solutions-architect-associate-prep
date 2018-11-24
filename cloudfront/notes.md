# Cloudfront

This is the AWS `Content Delivery Network (CDN)`

## Key Terms

*Edge Location* - location `where content is actually cached`. This is `separate from an AWS region/AZ`. There are over `50 edge locations across the globe`
*Origin* - the single location of all files that the CDN distributes. It can be an `S3 bucket, and EC2 instance, an ELB, or Route53` (using DNS to determine the endpoints to cache)
*Distribution* - the name given to the CDN which consists of a collection of Edge Locations. This is the term for what you actually `create` in CloudFront i.e. you create a `CloudFront distribution`

*Web Distribution* - typically used for websites
    - intended for speeding up `static and dynamic content, like html, css, php, and image` files
    - delivered over `HTTP or HTTPS`
    - allows `adding, updating, or deleting objects` and data from web forms
*RTMP* - used for media streaming
    - speeds up distribution of `larger media files, such as videos and music`
    - allows the user to `begin playing the media file before it has completely downloaded` from the edge location

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

## Creating a Distribution Notes

- You can create an `Origin Access Identity`, which is basically a _CloudFront-specific user that has permissions to read and write to your origin_.
- When desigining the distribution, `if you anticipate your cached CDN objects to be changing frequently, you should specify a short TTL`
- You can `restrict viewer access` to CDN files/content by using `signed URLs or signed cookies` (think how ACG uses this to restrict view access to video files to only those who have paid for the course). This is used to `secure CloudFront/S3 objects` for only paying customers
- You can enable `geo-restriction` to restrict access to certain geographic areas of the world. These are sorted by `countries`, and it works like a regular `whitelist/blacklist` filter.
- You can create an `invalidation`, which is a way to remove objects from edge location caches by force. This has a cost every time you use it, and is typically used after you create a distribution and realize some objects you are `caching contain sensitive or incorrect data`.

## Exam tips

1. You can create a cloudfront distribution (CDN) using a load balancer, an S3 bucket, or a MediaPackage channel endpoint as an `origin`. However, you cannot directly use `Lambda` as an origin.
2. You can `read AND write to edge locations`
3. The TTL (time to live) controls how long the objects are cached
4. You can clear cached objects, but this costs money every time you do it