# Minitest 2

## Unreviewed

How is the Public IP address managed in an instance session via the instance GUI/RDP or Terminal/SSH session?
    - The Public IP address is not managed on the instance: It is, instead, an alias applied as a network address translation of the Private IP address.

You have been ask to deploy a clustered application on a small number of EC2 instances. The application must be placed across multiple Availability Zones, have high speed, low latency communication between each of the nodes, and should also minimise the chance of underlying hardware failure. Which of the following options would provide this solution?
    - deploy the EC2 servers in a Spread Placement Group
    - https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/placement-groups.html

Which of the following components are not part of Amazon ECS?
    - File Storage
    - https://aws.amazon.com/ecs/features/

You are leading a design team to implement an urgently needed collection and analysis project. You will be collecting data for an array of 50,000 anonymous data collectors which will be summarized each day and then rarely used again. The data will be pulled from collectors approximately once an hour. The Dev responsible for the DynamoDB design is concerned about how to design the Partition and Local keys to ensure efficient use of the DynamoDB tables. What advice would you provide. (Choose 2)
    - Create a new table each day, and reconfigure the old table for infrequent use after the summation is complete.
    - Insert a calculated hash in front of the Date/Time value in the partition key to force DynamoDB to hop from partition to to partition.
    - http://docs.aws.amazon.com/amazondynamodb/latest/developerguide/GuidelinesForTables.html#GuidelinesForTables.Partitions
    - http://docs.aws.amazon.com/amazondynamodb/latest/developerguide/HowItWorks.Partitions.html
    - https://aws.amazon.com/blogs/aws/optimizing-provisioned-throughput-in-amazon-dynamodb/

## Reviewed