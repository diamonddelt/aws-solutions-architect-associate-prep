# Storage Gateway

## What is Storage Gateway

A service which connects on-premises software apps with cloud-based storage. This allows native, in-house applications to treat AWS' storage infrastructure as if it were native or on-prem.

You can securely store data in the cloud this way directly from your data center or on-prem organization, while scaling it and being cost-effective.

## How is is installed

Acts as a `virtual appliance` that you install on your infrastructure. You can download this as a Virtual Machine image (VM) in your datacenter.
Storage gateway works/supports VMware ESXi or Microsoft Hyper-V.

## Four types of Storage Gateways

`File Gateway (NFS)`- stores flat files in S3, like PDFs, spreadsheets, images, etc. Simulates file systems compatible with Windows systems. These are accessed via an NFS mount point. Ownership, permissions, and timestamps are stored in S3 in user-metadata. You can apply S3 bucket policies and versioning, lifecycle management, and cross-region replication directly to the objects stored in the File Gateway S3 bucket.

`Volume Gateway (iSCSI)` - uses `block-based` storage and is not suitable for flat files. These are considered `disk-volumes`, like VMX or OVA files (virtual machine disk images), and can be `asynchronously backed up as point-in-time snapshots and stored in EBS`. Snapshops are incremental backups and are `compressed` to minimize storage charges. You can think of this `like Altaro VMBackup`, which incrementally backs up VM disk differentials to the cloud.

- `Stored Volumes`: stores the entire volume locally first, then asynchronously backs it up to the cloud; This is the best option if you need low-latency access to the stored volume on-prem. The backups are of EBS snapshops. Snapshots can be between 1 - 16TB in size.
- `Cached Volumes`: `stores only recent and frequently accessed data on prem in the storage gateway cache and upload buffer storage for faster access`; similar to a caching layer like Elasticache; infrequently accessed data in still stored in the cloud. These backups can go up to 32TB, and the storage volumes can be attached

`Tape Gateway (VTL)` - create virtual `tapes` and send them to AWS Glacier; this is mostly used for archival purposes. Allows you to leverage existing tape-based backup infrastructure to create `virtual tapes`, which act a lot like virtual hard disks. These virtual tapes are created on Tape Gateway and is `configured with a media changer and tape drives`. Supported by `NetBackup, Backup Exec, Veeam`, etc

## Exam Tips

1. You need to basically know which type of storage is used for which scenario (tapes vs. on-prem iSCSI disk volumes vs. flat files)