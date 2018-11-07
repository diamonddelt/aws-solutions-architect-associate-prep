# Redshift

Amazon's OLAP / Data Warehousing solution, which allows scaling from a small solution to a large enterprise, `petabyte-scale` data warehouse `cheaply`.

Recall that Redshift is used for OLAP (Online Analytics Processing) transactions i.e. complex queries on huge sets of data and creating huge tables via joins.

Redshift uses `Columnar Data Storage`, which is storing data by `column instead of by row`. This is great for OLAP analytics because it *requires fewer I/O operations for large data sets, which improves query performance*.

Redshift also uses `Advanced Compression`, which allows data stores to be _compressed tighter because its columnar and is stored sequentially on disk_. This allows the storage footprint to remain small. Redshift automatically samples your data and selects the appropriate compression scheme.

Redshift uses `Massively Parallel Processing (MPP)`, which automatically *distributes data and query load across all compute nodes.* You can easily add compute nodes and this allows your query performance to remain fast as the data warehouse gets larger.

## Configurations

Redshift has two possible configurations

- *Single Node* - 160Gb maximum
- *Multi Node* - consists of a `Leader Node` (which manages client connections and receives queries), and one or more `Compute Nodes` (which store data and perform queries/computations). There is a limit of 128 maximum Computer Nodes

## Pricing

Redshift charges you for `compute node hours`, or the total number of hours you run across all compute nodes. Leader nodes do not incur charges.

Redshift also charges for `backups`, and `data transfers within a VPC` (you can't transfer outside of the VPC from Redshift)

## Security

Redshift is encrypted `in transit` using SSL and AES-256. It also automatically handles key management concerns, but `you can use your own security keys with HSM or AWS KMS`

## Availability

Redshift is only available in one AZ at a time (not designed for high availability), but you can restore snapshots to other AZs in an outage scenario.