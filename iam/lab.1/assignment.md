1. Create an IAM user, and assign this user granular access to what they need to use.
    - created `rrrasti`
2. Create a few IAM groups which logically separate your business functions.
    - Noticed AWS now provides very logical permissions groups such as 'Power User' or 'Support User'
    - created `Developers` and `Support Users` groups
3. Create an IAM role, which grants an EC2 instance full permissions to S3, if that role is attached to it.
    - created `rr_ec2_s3_fullaccess`
