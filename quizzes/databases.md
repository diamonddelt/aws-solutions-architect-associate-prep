# Databases Quiz

1. If you want your application to check RDS for an error, have it look for an ______ code in the response from the Amazon RDS API.
    - Error
2. If you are using Amazon RDS Provisioned IOPS storage with a MySQL or Oracle database engine, what is the maximum size RDS volume you can have by default?
    - 16TB
3. Can I "force" a failover for any RDS instance that has Multi-AZ configured?
    - Yes
4. When creating an RDS instance, you can select the Availability Zone into which you deploy it.
    - Yes, you can.
5. When you add a rule to an RDS DB security group, you must specify a port number or protocol.
    - A port number (3306) is automatically applied to any DB security groups that you create.
6. What data transfer charge is incurred when replicating data from your primary RDS instance to your secondary RDS instance?
    - There is no charge, because replication from primary to secondary RDS instances is provided free as part of the high availability model
7. Amazon's ElastiCache uses which two engines?
    - Redis and Memcached
8. MySQL installations default to port number ________.
    - 3306
9. Which of the following AWS services is a non-relational database?
    - DynamoDB
10. You are hosting a MySQL database on the root volume of an EC2 instance. The database is using a large number of IOPS, and you need to increase the number of IOPS available to it. What should you do?
    - Add 4 additional EBS SSD volumes and create a RAID 10 using these volumes.
11. If I wanted to run a database on an EC2 instance, which of the following storage options would Amazon recommend?
    - EBS (because elastic block store is storage on an instance, which you can configure to use SSDs for better IOPS)
12. Which AWS DB platform is most suitable for OLTP?
    - RDS (Remember RDS = OLTP and Redshift = OLAP)
13. Which of the following is most suitable for OLAP?
    - Redshift
14. What happens to the I/O operations of a single-AZ RDS instance during a database snapshot or backup?
    - I/O may be briefly suspended while the backup process initializes (typically under a few seconds), and you may experience a brief period of elevated latency.
15. Which of the following DynamoDB features are chargeable, when using a single region? (Choose 2)
    - `Storage of Data and Read/Write Capacity` (these are measured in Read Units and Write Units). There is no charge for the transfer of data into DynamoDB, providing you stay within a single region (if you cross regions, you will be charged at both ends of the transfer.) There is no charge for the actual number of tables you can create in DynamoDB, providing the RCU and WCU are set to 0, however in practice you cannot set this to anything less than 1 so there always be a nominal fee associated with each table.
16. In RDS, changes to the backup window take effect ________.
    - Immediately
17. When you have deployed an RDS database into multiple availability zones, can you use the secondary database as an independent read node?
    - No, because that architecture is called `Read Replicas`, and deploying into multiple availability zones is called `Multi-AZ` (used for disaster recovery)
18. Under what circumstances would I choose provisioned IOPS over standard storage when creating an RDS instance?
    - If you use online transaction processing in your production environment. (provisioned IOPS costs more so its more suitable for prod)
19. You can RDP or SSH in to an RDS instance to see what is going on with the operating system.
    - No, because these are controlled by AWS. You can verify the instance is online through other means (such as testing connectivity to it's endpoint DNS address)
20. How many copies of my data does RDS - Aurora store by default?
    - 6
21. Which of the following is not a feature of DynamoDB?
    - The ability to store relational based data
22. Which AWS service is ideal for Business Intelligence Tools/Data Warehousing?
    - Redshift (Because these are considered OLAP)
23. In RDS, what is the maximum value I can set for my backup retention period?
    - 35 days
24. RDS Reserved instances are available for multi-AZ deployments.
    - True
25. With new RDS Db instances, automated backups are enabled by default?
    - True
26. Which set of RDS database engines is currently available?
    - Oracle, SQL Server, MySQL, PostgreSQL
27. Which of the following data formats does Amazon Athena support? (Choose 3)
    - JSON, Apache ORC, and Apache Parquet (wtf?)
28. AWS's NoSQL product offering is known as ________.
    - DynamoDB