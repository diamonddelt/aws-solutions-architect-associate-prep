# RDS

RDS is typically an OLTP and can be one of the following Relational database types:

1. SQL
2. MySQL
3. PostgreSQL
4. Oracle
5. Aurora
6. MariaDB

`Data Warehousing` - think Cognos, Jaspersoft, SSRS, Oracle Hyperion, SAP Netweaver, etc. This is used to pull in large and complex data sets and do queries on data. Uses `OLAP` (complex processing) vs. `OLAP` (simple processing). Data warehouses are designed differently than regular databases, because they are intended to have extremely costly queries run against them, while not impacting performance of an application reading from them at the same time. Therefore they commonly use the read-only replica pattern