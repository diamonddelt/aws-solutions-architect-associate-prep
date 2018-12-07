# Notes

## What does EC2 provide

- "`Elastic Compute Cloud`" - resizable compute in the cloud; virtual machines in the cloud
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

## What is a Security Group?

You can think of this as a `virtual firewall` that stands right in front of any EC2 instance. 

Security groups are `stateful`. This means that any rule you allow in, is automatically allowed back out. You do not get the ability to specify allow or deny rules that pinhole specific IP addresses. As an example, if you have an `Inbound` rule that says to allow all HTTPS traffic to 0.0.0.0/0, but you have no `Outbound` rules, all HTTPS traffic can still flow in an out, because the `Inbound` rule works both ways.

Remember: 
```text
Security Groups = STATEFUL
Security Groups CANNOT DENY traffic

Network ACLS = STATELESS
Network ACLs CAN DENY traffic
```

`Any changes applied to a security group are immediately visible to any instances behind them.`

## Selecting AMI types based on EBS vs Instance Volumes

All AMIs are categorized as either `Instance backed` or `EBS backed`.

`Instance Store` = *Ephemeral* Storage; You can only attach up to 2 of these before spinning up an instance - you can't add them while it's running.
`EBS-backed Instance` = root volume is stored on EBS. This means you can move it around to other instances, and generally can persist the data when the instance itself stops running.

You cannot start/stop an instance store volume - you can only do that with an EBS-backed volume.

AMIs are `not encrypted at rest`.

## Encrypt Root Device Volumes

You generally need to `make a snapshot of an EBS volume that is unencrypted`, then when you choose to `make a new copy` of the volume from the snapshot, you have the `option to encrypt` it at that time.

If the volume was already encrypted before you took the snapshot, the `snapshot is also encrypted.`

The snapshot -> restore process is also how you would move an EBS volume from one region to another.

You cannot share encrypted snapshots, because the encryption key is contained within your AWS account.

## EC2 Placement Groups

`Clustered Placement Group` - a grouping of EC2 instances within a `single Availability Zone (on purpose)`. These are typically put on the same high-powered network hardware infrastructure, and are only `recommended for instances which require low network latency`, `high network throughput, or both` (and thus benefit most from all instances being the shortest distance away i.e. in the same AZ). These `CANNOT span multiple availability zones`.

`Spread Placement Group` - a grouping of EC2 instances which are intentionally `placed on different pieces of underlying hardware/infrastructure (on purpose)`. They `can span multiple availability zones`. The primary usecase is for applications which have a small number of critical instances that `should, for whatever reason, not be deployed on the same underlying hardware`.

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

## Exam Tips

1. Know the difference between `EBS Backed EC2 instances` vs `Instance Store` - the primary difference being that EBS backed instances have persistent data, because the EBS volume is a separate AWS object with it's own lifecycle, independent of the instance itself. Instance store is ephemeral - if you kill the instance, you lose the data too
    1. You cannot `stop` instance backed volumes - they are wiped if you do. You `can` stop EBS volumes without losing data
2. You need to know how to get the public IP address from an EC2 instance using the command line
    1. `curl/wget http://169.254.169.254/latest/meta-data/`
    2. You need to remember that the IP address is considered an `instance's METADATA, NOT USERDATA`
3. You cannot launch an EBS-optimized EC2 instance with the root volume `encrypted`. You would need to make a snapshot of the root volume after the instance is already created, and use the `option to encrypt the snapshot`. Then, create a new instance with that encrypted, snapshotted volume.
4. `Termination protection is disabled by default` - you must turn that on
5. The `default action for a roob EBS volume` is to be `deleted when the instance is terminated`
6. EBS `root` volumes for `DEFAULT AMIs` cannot be encrypted, but custom AMIs can encrypt the root volume. A default AMI is one of the pre-provided AWS flavors, such as AWS Linux or AWS Ubuntu HVM. If you add an additional volume to a `DEFAULT AMI`, you can encrypt that.
7. When you create an EC2 instance with EBS volumes attached, both the instances and volumes will be created in the `same availability zone`. `You cannot attach EBS volumes in AZ A to an EC2 instance in AZ B`.
8. You can `upgrade the root device volume to a better volume type and increase the size on demand, with no downtime`. You `cannot downgrade seamlessly`, though.
9. You can create a snapshot copy of an EBS volume in a different availability zone - this is the only way to copy an EBS volume over to other AZs.
10. You can copy an AMI to another region by taking a snapshot of it, and making a new image from that snapshot in the different region.
11. Snapshots are `point in time, incremental` copies of Volumes, and they only contain diffs of changes in Volumes. `Snapshots exist in S3.`
12. `Snapshots of encrypted volumes are encrypted automatically`, and volumes `restored from encrypted snapshots are encrypted automatically`
13. It is `now possible to change a role on a running EC2 instance` directly from the EC2 instances dashboard
14. Finding the public IPV4 address of a running EC2 instance uses the meta-data endpoint: `curl http://169.254.169.254/latest/meta-data/public-ipv4`
15. To see the bootstrap script provided to a running EC2 instance use the `user-data` endpoint: `curl http://169.254.169.254/latest/user-data/`
16. Placement groups must be `uniquely named within the AWS account`
17. Only certain types of instances can be launched in a placement group: `Compute Optimized, GPU, Memory Optimized, Storage Optimized (basically anything specifically for high performance and not general purpose)`
18. AWS recommends `homogenous EC2 instances within a placement group `i.e. they should all be the same instance type, size, etc
19. You `cannot merge` placement groups.
20. You `cannot move an existing instances into a placement group` - you can `only launch new instances` within placement groups. The workaround is to create an AMI from existing instances and re-launch into the placement group.