# Aurora (component of RDS)

Aurora is a mySQL compatible database engine that combines speed and availability of high-end commercial databases, but for less cost. It has `5 times` better performance than vanilla mySQL.

It's a competitor to Oracle, in that you get the high availability and performance, but it's much cheaper than Oracle.

## Scaling

Aurora scales in 10GB increments, up to 64TB, and it scales automatically. It also scales vCPUs automatically. There are `two copies` of data contained in each availability zone, with a minimum of 3 availability zones. 6 copies of your data in total. It can basically handle the loss of up to _two copies of data without affecting database write availability_, and _three copies of data without affecting read availability_.

It is `self-healing` - meaning Aurora continuously scans it's own storage infrastructure for bad blocks and removes or repairs them.

## Replication

There are two types of replica features available

1. Aurora Replicas (currently 15)
2. MySQL Read Replicas (currently 5)

The primary difference between the two types of replicas is that the `Aurora Replicas support high availability automatic failover`, whereas the MySQL Read Replicas require manual intervention to fail over.

The replication and failover is specified in `tiers`, with *tier 0 being the highest priority*, and will be used first if there are multiple replicas

## Region Availability

Currently only available in certain regions (US EAST 1 and Ireland)