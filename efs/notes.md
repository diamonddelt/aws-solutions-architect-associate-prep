# Elastic File System (EFS)

## What it is

Amazon EFS (Elastic File System) provides simple, scalable file storage for use with Amazon EC2 instances. This works like a `cloud-based NAS that you can attach multiple EC2 instances at once`. This is `in contrast to EBS`, which acts like a local mounted hard disk drive, and `can only be attached to one EC2 instance at a time.`

EFS allow dynamic sizing of storage, without having to provision with a certain size ahead of time, like EBS forces you to do.

- Support `NFSv4`.
- `Pay for what you use` (in terms of net storage, unlike having to over-provisiong in EBS and pay for that flat size of volume)
- Can `scale up to petabytes`
- Supports `thousands of concurrent NFS` connections
- Data is stored across `multiple AZs within a region`
- `Read After Write consistency` (like S3), but EFS is `Block-based storage`, unlike S3 (which is object-based)

## Attaching EFS to EC2 Instances

- The EFS `must be in the same security group` as the EC2 instances
- You have to `mount` the EFS on the EC2 instances using the EC2 metadata lookup (the 169.154 IP address /latest/meta-data) + the DNS name of the EFS itself.
    - The following command mounts the EFS to the `efs` local directory on an EC2 instance
    - `sudo mount -t nfs4 $(curl -s http://169.254.169.154/latest/meta-data/placement/availability-zone).fs-7834d83kd.efs.us-west-2.amazonaws.com:/ efs`

## Exam Tips

- The primary use case as of December, 2018 is using EFS as a `filesystem across multiple EC2 instances`, `without worrying about pre-provisioning` storage
- You can also use it as a `more highly available file-server` for a web application that is deployed on EC2 instances, because it can be `read from by multiple instances at once via NFS`, instead of only a single EC2 instance reading from an EBS volume.