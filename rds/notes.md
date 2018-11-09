# RDS

RDS is typically an OLTP and can be one of the following Relational database types:

1. SQL
2. MySQL
3. PostgreSQL
4. Oracle
5. Aurora
6. MariaDB

`Data Warehousing` - think Cognos, Jaspersoft, SSRS, Oracle Hyperion, SAP Netweaver, etc. This is used to pull in large and complex data sets and do queries on data. Uses `OLAP` (complex processing) vs. `OLAP` (simple processing). Data warehouses are designed differently than regular databases, because they are intended to have extremely costly queries run against them, while not impacting performance of an application reading from them at the same time. Therefore they commonly use the read-only replica pattern

## Provisioned IOPS SSD Storage Chart

The following table shows the range of Provisioned IOPS and storage size range for each database engine.

```text
Database Engine	Range of Provisioned IOPS	Range of Storage
MariaDB	1,000–40,000 IOPS	100 GiB–32 TiB
SQL Server, Enterprise and Standard editions	1000–32,000 IOPS	20 GiB–16 TiB
SQL Server, Web and Express editions	1000–32,000 IOPS	100 GiB–16 TiB
MySQL	1,000–40,000 IOPS	100 GiB–32 TiB
Oracle	1,000–40,000 IOPS	100 GiB–32 TiB
PostgreSQL	1,000–40,000 IOPS	100 GiB–32 TiB
```


## Backups, Multi-AZ, Read-Replicas

There are two types of database backups for AWS: `Automated Backups` and `Database Snapshots`.

*Automated Backups* - allows full recovery of a database up to any point in time within a `retention period`. The retention period is between `1-35 days`. These automatic backups will take a `full daily snapshot` and will also `store transaction logs throughout the day`. AWS chooses the first most recent daily backup, and applies the transaction logs to restore to a pristine state, within the retention period.

Automated backups are `enabled by default, and are stored in S3`, making them highly reliable. You get free storage space in S3 equal to the size of your RDS instance.

Backups are taken during a `defined time window` (aka between 8-12PM UTC daily - you can configure this). During the backup window, `you will experience elevated latency`.

*Database Snapshots* - these are done `manually`, and are stored even after you delete the original RDS instance (unlike automated backups, which are gone when the RDS instance is deleted). You can think of these like EC2 snapshots - i.e. `a point in time copy`.

## Restoring Backups

Restoring from either an Automated Backup or a manual Snapshot results in a new RDS instance with a `new DNS endpoint`:

```text
original.eu-west-1.rds.amazonaws.com -----> restored.eu-west-1.rds.amazonaws.com
```

## Encryption

Encryption at rest is supported for MySQL, Oracle, SQLServer, PostgreSQL, MariaDB, and Aurora. It uses the AWS KMS service (Key management service).

If you decide to encrypt your RDS instance, the data stored in the underlying storage, as well as the automated backups, read replicas, and shapshots, are also all encrypted.

You cannot currently encrypt an existing database instance. The work-around is:

1. make a snapshot
2. make a copy of the snapshot
3. encrypt the copy
4. restore your database from the encrypted copy

## Differences between Multi-AZ and Read-Replicas

Multi-AZ creates a disaster recovery, `exact-copy` of your production database in `another Availability Zone`. In the situation that the primary database fails, the `standby database becomes primary`, and `AWS automatically updates DNS to point to the IP address of standby database`, so you don't have to update or modify the domain name when that happens. `Data replication and synchronization is also handled automatically by AWS`.

*Multi-AZ is for Disaster Recovery Only, not for performance.*

For performance, you would choose a `Read-Replica`. A read replica setup involves `sending all database write operations to read replica databases`, and construction your application tier to offload all of the *read operations* from the primary database to the read replicas. It makes sense that if most of the traffic on a web application is going to be performing read operations on a database, that you may want to pidgeonhole only the write operations to the primary, so that `the read operations get better performance`.

The primary trade off here is that there is some degree of latency between when a write is finished on the primary database, and when the read-replicas obtain that write operation.

The read-replica is a `read-only` copy of the database, which uses asynchronous replication from the primary RDS instance. Primary use-cases are for very read-heavy database workloads, like users reading blog content (but not necessarily contributing).

Read-replicas are not available for `SQL Server or for Oracle`.

Read-replicas also `require automatic backups being turned`, and you can have `up to 5 read replica copies` of any one database.

## Exam Tips

- A common exam question is how to get an EC2 instance in one security group to be able to connect to an RDS instance in another security group. You will need to `open up port 3306 for the security group of the EC2 instance in the security group configuration 'inbound' section of EC2.`
- Multi-AZ = think `automatic failover`