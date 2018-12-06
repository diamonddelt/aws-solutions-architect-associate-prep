# EC2 Quiz

1. I can use the AWS Console to add a role to an EC2 instance after that instance has been created and powered-up.
    - True
2. You can add multiple volumes to an EC2 instance and then create your own RAID 5/RAID 10/RAID 0 configurations using those volumes.
    - True
3. The use of a placement group is ideal _______
    - Your fleet of EC2 instances requires high network throughput and low latency within a `single availability zone`. Placement groups are intended to optimize single AZs because they keep instances in the same high speed rack, so `this only makes sense for applications that have extremely low latency requirements.`
4. In order to enable encryption at rest using EC2 and Elastic Block Store, you must ________.
    - Configure encryption when creating the EBS volume
5. Amazon's EBS volumes are ________.
    - Block based storage
6. To retrieve instance metadata or userdata you will need to use the following IP Address:
    - http://169.254.169.254
7. Individual instances are provisioned ________.
    - In Availability Zones
8. EBS Snapshots are backed up to S3 in what manner?
    - `Incrementally` i.e. it backs up `differentials`
9. I can change the permissions to a role, even if that role is already assigned to an existing EC2 instance, and these changes will take effect immediately.
    - True
10. Is it possible to perform actions on an existing Amazon EBS Snapshot?
    - Yes, through the AWS APIs, CLI, and AWS Console.
11. What is the underlying Hypervisor for EC2 ? (Choose 2)
    - `Xen` and `Nitro`
12. Can a placement group be deployed across multiple Availability Zones?
    - Yes, but they are called `Spread placement groups`, and they can span multiple hardware and AZs
13. Can you attach an EBS volume to more than one EC2 instance at the same time?
    - No
14. You need to know both the private IP address and public IP address of your EC2 instance. You should ________.
    - Retrieve the instance Metadata from http://169.254.169.254/latest/meta-data/.
15. When creating a new security group, all inbound traffic is allowed by default.
    - False
16. Will an Amazon EBS root volume persist independently from the life of the terminated EC2 instance to which it was previously attached? In other words, if I terminated an EC2 instance, would that EBS root volume persist?
    - Only if I specify (using either the AWS Console or the CLI) that it should do so.
17. To help you manage your Amazon EC2 instances, you can assign your own metadata in the form of ________.
    - Tags
18. Which AWS CLI command should I use to create a snapshot of an EBS volume?
    - aws ec2 create-snapshot
19. Can I move a reserved instance from one region to another?
    - No
20. If an Amazon EBS volume is an additional partition (not the root volume), can I detach it without stopping the instance?
    - Yes, although it may take some time
21. Which of the following statements are true about containers on AWS? (Choose 5)
    - To be able to use ECS, you must use the ECS Agent.
    - ECR can be used to store Docker images.
    - You can install and manage Kubernetes on AWS, yourself.
    - ECS allows you to control the scheduling and placement of your containers and tasks.
    - You can have AWS manage Kubernetes for you.
22. Can I delete a snapshot of an EBS Volume that is used as the root device of a registered AMI?
    - Yes