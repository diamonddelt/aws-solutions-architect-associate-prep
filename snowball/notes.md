# Snowball

## Before Snowball

There was a service called `Import/Export Disk`, which moved large amounts of data directly into and out of AWS cloud storage. It did this with a high-speed internal network and bypassed the WAN (Internet). You would send in what amounted to a hard disk, and AWS would use their own network to push it into the cloud storage faster than you could transmit it over the Internet.

## Types of Snowball

`Snowball` - a huge physical storage device that can store up to `80TB` of data. Uses multiple layers of security, including tamper-resistant enclosurs, 256 encryption, and Trusted Platform Module (TPM) to ensure chain-of-custody of your data. AWS then erases the data themselves. You load data into the appliance, send it to AWS, and they transfer it into cloud storage.
`Snowball Edge` - `looks like a regular Snowball`, but can store `100TB` of data, with `extra compute capabilities` built into it. That means it could act as a small data center, because it can run Lambda functions (it has compute capacity and can do common AWS compute functions instead of just housing data). The purpose, however, is the same as regular Snowball - send it to AWS for them to move the data into the cloud for you.
`Snowmobile` - this is literally a `huge shipping container on the back of an 18-wheeler truck`. The container is the data storage device... can house `Petabytes or Exabytes of data`. 45-foot long ruggedized shipping container. Moving Exabytes of data could be done in months, as opposed to years with low bandwidth pipes.

## What does it do?

This is a petabyte-scale data transfer solution. Used with secure appliances to transfer large amounts of data into and out of the AWS cloud. Think of moving an impossible large amount of data from one data center to another. Doing this over an internet connection would saturate your bandwidth and take forever, introducing potential data loss issues. `Instead, it's like their version of moving a really powerful USB stick from one place to another.`

## Exam Tips

1. Know what `Snowball is`, and what `Import/Export was`
2. Snowball can `import to S3`, or `export from S3 onto a Snowball`