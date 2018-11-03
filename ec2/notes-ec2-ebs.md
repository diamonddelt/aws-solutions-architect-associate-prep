# Notes

## What does EC2 provide

- "Elastic Compute Cloud" - resizable compute in the cloud
- Allows developers to build fault tolerant apps and isolate from common failure points. Allows the use of VPCs, load balancers, and security ACLs

## What are the pricing options?

- `On Demand` - you pay a fixed rate by the hour or by the second, with no commitment
- `Reserved` - provides capacity reserved for a 1 or 3 year period, but at a significant discount over the `On Demand` rate for the same instance tier
- `Spot` - allows you to bid whatever you want for instance capacity, allowing the greatest savings, with the caveat that your apps must have flexible start and end times, because you could be outbid and suddenly experience an instance outage
- `Dedicated Hosts` - physical EC2 server dedicated for your own use. This is the most expensive option outright, but it can save you money if you have server-bound software licenses that would cost you more if you had a lot of smaller instances (think Oracle or SQL Server and their per-server licensing fee)

## Instance use cases by type

### On Demand

- good for low cost and flexibility to not pay a long-term commitment on server infrastructure, with guaranteed uptime
- good for first-time application tests or proof of concepts
- good for applications with short term or unpredictable workloads

### Reserved

- applications for steady or predictable usage
- applications that require reserved capacity
- standard RIs can be up to 75% of the on-demand price
- convertable RIs can be up to 54% of on-demand price, but these only work if the change in the RIs attributes result in equal or greater value. These are like a reserved instance that you can still scale up, if you are midway through your contract period and suddenly want to double-down on the reserved capacity.
- scheduled RIs can be launched in a specific time window you specify. These are good if you app only needs reserved capacity for a fraction of a day, week, or month, and at predictable times.

### Spot

- applications with flexible start and end times
- only feasible at very low compute prices (examples are big pharmaceutical companies or genomics, who need to do spikes of massive computing, but absolutely don't care when that takes place, as long as they get the best price. So their spot instance fleet might start up at 2AM on a Sunday morning to process a massive chunk of work, and spin down for another 3 days until the spot price is met again. It's necessary because the high compute instances required are very expensive on-demand)

### Dedicated Hosts

- regulatory requirements that don't support multi-tenant virtualization (such as health fields or places with a lot of strict regulation like HIPAA)
- great for licensing models which don't support cloud deployments or multi-tenancy (think SQL server or Oracle)
- can be purchased on-demand (hourly)
- can be purchased on reservation (up to 70% off on-demand)

## Instance Types (Not necessary to memorize this for Associate-level exams)

- `F1` - Field Programmable Gate Array (think genomics, real-time video processing, big data, etc)
- `I3` - High Speed Storage (think NoSQL DBs, Data Warehousing, or other big data lakes which need fast access)
- `G3` - Graphics Intensive (video encoding/3D application streaming services)
- `H1` - High Disk Throughput (MapReduce based workloads, HDFS, and distributed file systems)
- `T2` - Lowest Cost; General Purpose (web servers or small databases)
- `D2` - Dense Storage (fileservers/data warehousing/hadoop or other things that need a shit load of storage)
- `R4` - Memory Optimized (memory-intensive apps/DBs)
- `M5` - General Purpose; Better than the T2 series (application servers that need more power than T2)
- `C5` - Compute Optimized (CPU intensive apps/DBs)
- `P3` - Graphics/General Purpose GPU (applications which require GPU computing as opposed to CPU, like bitcoin mining, machine learning, etc)
- `X1` - Memory Optimized; Better than the R4 series (SAP HANA, Apache Spark, etc)

## How to remember the EC2 Instance Types (acronym)

`FIGHTDRMCPX` - "Fight Dr. McPix"
F - FPGA
I - IOPS
G - Graphics
H - High Disk Throughput
T - cheap general purpose (t2 micro)
D - density
R - RAM
M - main choice for most things
C - compute
P - graphics (think pics)
X - Xtreme memory

## What is EBS?

- `Elastic Block Storage` - the main storage volume system that pairs with EC2 instances
- these are attached to instances, and can have file systems mounted on them
- EBS volumes are replicated across availability zones, so if an actual hard disk fails, the EBS volume itself stays alive
- think of it as a 'disk in the cloud'

## What are the EBS Volume Types?

- `General Purpose SSD GP2` - balance between cost and performance; 3 IOPS per GB up to 10,000 IOPS; allows bursting up to 3000 IOPS for volumes over 3TBs
- `Provisioned IOPS` - designed for I/O intensive apps such as large relational databases and NoSQL databases; use if you need more than 10,000 IOPS; you can provision up to 20,000 IOPS per volume
- `Throughput Optimized HDD ST1` - useful for big data, data warehouses, log processing; _cannot be a boot volume_
- `Cold HDD SC1` - lowest cost storage for infrequently accessed workloads; typical usecase is a file server; _cannot be a boot volume_
- `Magnetic Standard` - lowest cost per gigabyte of all EBS volume types that is _bootable_. Ideal for lowest cost applications where storage is not a concern and infrequent access.

## Key Exam Terms

- `On Demand` - you pay a fixed rate by the hour or by the second, with no commitment
- `Reserved` - provides capacity reserved for a 1 or 3 year period, but at a significant discount over the `On Demand` rate for the same instance tier
- `Spot` - allows you to bid whatever you want for instance capacity, allowing the greatest savings, with the caveat that your apps must have flexible start and end times, because you could be outbid and suddenly experience an instance outage
- `Dedicated Hosts` - physical EC2 server dedicated for your own use. This is the most expensive option outright, but it can save you money if you have server-bound software licenses that would cost you more if you had a lot of smaller instances (think Oracle or SQL Server and their per-server licensing fee)
- If a spot instance is terminated by Amazon EC2, you are not charged for a partial hour of usage. However, if you terminate the instance yourself, you will be charged for the complete hour the instance ran.
- FIGHT DR MCPX acronym for remembering instance types
- `General Purpose SSD GP2` - balance between cost and performance; 3 IOPS per GB up to 10,000 IOPS; allows bursting up to 3000 IOPS for volumes over 3TBs
- `Provisioned IOPS` - designed for I/O intensive apps such as large relational databases and NoSQL databases; use if you need more than 10,000 IOPS; you can provision up to 20,000 IOPS per volume
- `Throughput Optimized HDD ST1` - useful for big data, data warehouses, log processing; _cannot be a boot volume_
- `Cold HDD SC1` - lowest cost storage for infrequently accessed workloads; typical usecase is a file server; _cannot be a boot volume_
- `Magnetic Standard` - lowest cost per gigabyte of all EBS volume types that is _bootable_. Ideal for lowest cost applications where storage is not a concern and infrequent access.

## Questions
