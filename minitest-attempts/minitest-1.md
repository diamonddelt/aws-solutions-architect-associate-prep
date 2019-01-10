# Minitest 1

## Reviewed

1. Your company provides an online image recognition service and uses SQS to decouple system components. Your EC2 instances poll the image queue as often as possible to keep end-to-end throughput as high as possible, but you realize that all this polling is resulting in both a large number of CPU cycles and skyrocketing costs. How can you reduce cost without compromising service?
    - Enable long polling by setting the ReceiveMessageWaitTimeSeconds to a number > 0
    - https://aws.amazon.com/sqs/faqs/

2. Choose the features of Consolidated Billing. (Choose 3)
    - Account charges can be tracked individually
    - A single bill is issued containing the charges for all AWS Accounts
    - Multiple standalone accounts are combined and may reduce your overall bill
    - https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/consolidated-billing.html

3. Which of the following are not valid CloudFormation template sections?
    - Options (Remember that `Parameters` IS a valid template section)
    - https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/template-anatomy.html

4. You successfully configure VPC Peering between VPC-A and VPC-B. You then establish an IGW and a Direct-Connect connection in VPC-B. Can instances in VPC-A connect to your corporate office via the Direct-Connect service, and connect to the Internet via the IGW?
    - VPC peering does not support edge to edge routing (i.e. if one of the VPCs in the peering relationship do not have access to a VPN/Corporate Network/Internet directly, you can't get access to those via the peering relationship)
    - https://docs.aws.amazon.com/vpc/latest/peering/invalid-peering-configurations.html

5. A client is concerned that someone other than approved administrators is trying to gain access to the linux web app instances in their VPC. She asks what sort of network access logging can be added. Which of the following might you recommend? (Choose 2)
    - Make use of an OS level logging tools such as iptables and log events to CloudWatch or S3.
    - Set up a Flow Log for the group of instances and forward them to CloudWatch. Flow logs can be setup at the VPC, subnet, or network interface level.
    - http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/flow-logs.html
    - http://www.howtogeek.com/177621/the-beginners-guide-to-iptables-the-linux-firewall/

6. By default, all EC2 instances are monitored by CloudWatch. Using the default settings, how many minutes elapse between when metrics are sent to CloudWatch? Using the detailed option, how many minutes would elapse between metrics being sent to CloudWatch?
    - 5 minutes by default; 1 minute if you configure detailed monitoring (extra charge)
    - https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-cloudwatch.html

7. You have been engaged by a company to design and lead the migration to an AWS environment. An argument has broken out about how to meet future Backup & Archive requirements and how to transition. The Security Manager and CTO are concerned about backup continuity and the ability to continue to access old archives. The Senior engineer is adamant that there is no way to retain the old backup solution in the AWS environment, and that they will lose access to all the current archives. What information can you share that will satisfy both parties in a cost effective manner? (Choose 2)
    - Suggest that during transition a 2nd AWS Storage Gateway VTL solution could be commissioned in the customer's new VPC and integrated with existing VTS. At the same time, the existing Enterprise Backup Solution could be used to perform tape-to-tape copies to migrate the Archives from tape to VTL/VTS virtual tape
    - Meet with both parties and brief them on the AWS Storage Gateway VTL solution. Explain that it can initially be installed in the on-premises environment utilizing the existing enterprise backup product to start the transition without losing access to the existing backups and archives. Over the duration of the migration, most (if not all) the backup cycles will be replaced by the new VTL & VTS tapes.
    - https://aws.amazon.com/importexport/disk/
    - http://docs.aws.amazon.com/storagegateway/latest/userguide/storage-gateway-vtl-concepts.html
    - http://docs.aws.amazon.com/storagegateway/latest/userguide/GettingStartedTrySetupStep2-vtl.html
    - http://www.ironmountain.com/Services/Data-Management/Archive/Data-Restoration-and-Migration/Data-Restoration.aspx
    - http://www.veritas.com/community/forums/how-duplicate-netbackup-media-tape-backup-another-media-tape