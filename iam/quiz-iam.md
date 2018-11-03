# Quiz - IAM

1. Which of the following is NOT a feature of IAM?
    1. Centralized control of your AWS account
    2. Integrates with existing AD account allowing single sign-on
    3. Fine-grained access control to AWS resources
    4. Allows you to setup biometric authentication, so no passwords are required (`Correct Answer`)

2. AWS recommends that EC2 instances have credentials stored on them so that the instances can access other resources (such as S3 buckets).
    1. True
    2. False (`Correct Answer` - AWS recommends using IAM roles whenever possible, and discourages storing credentials on instances)

3. Which IAM entity can you use to delegate access to your AWS resources to users, groups or services?
    1. IAM User
    2. IAM Web Identity Federation
    3. IAM Role (`Correct Answer` - IAM Roles are used to delegate access to various services)
    4. IAM Group

4. In AWS, what is IAM used for?
    1. Secure VPN access to AWS
    2. Creating and managing users and groups, managing access to AWS services and assigning permissions to allow or deny AWS resources (`Correct answer`)
    3. To move large amounts of data (TBs) into AWS
    4. IAM is a serverless platform

5. What is an IAM policy?
    1. A csv file which contains a users Access Key and Secret Access Key
    2. A JSON document which defines one or more permissions (`Correct Answer`)
    3. A file containing a user's private ssh key
    4. The policy which determines how your AWS bill will be paid

6. What is the best way to enable your EC2 instance to read files in an S3 bucket?
    1. Create a new IAM user and grant read access to S3. Store the user's credentials locally on the EC2 instance and configure your application to supply the credentials with each API request.
    2. Configure a bucket policy which grants read access based on the EC2 instance name.
    3. Create an IAM role with read access to S3 and assign the role to the EC2 instance. (This is `Most Correct` - IAM Roles should be used, AND credentials `should not` be stored on EC2 instances)
    4. Create a new IAM role and grant read access to S3. Store the role's credentials locally on the EC2 instance and configure your application to supply the credentials with each API request.

7. Which statement best describes IAM?
    1. IAM allows you to manage users, groups, and roles and their corresponding level of access to the AWS Platform. (`Correct Answer`)
    2. IAM allows you to manage users' passwords only. AWS staff must create new users for your organization. This is done by raising a ticket.
    3. IAM allows you to manage permissions for AWS resources only.
    4. IAM stands for Improvised Application Management, and it allows you to deploy and manage applications in the AWS Cloud.