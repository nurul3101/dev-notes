## AWS (Amazon Web Services)

IAM
Identity and Access Management
- Do not use the root account
- Users
- Groups
- Roles
- Users ( A physical person )
- Users can be grouped together e.g by teams
- Roles are for machine
- IAM has a global view
- Permissions are governed by policies
- Least privileged principles
- IAM FEDERATION (for huge enterprises)
- Only 1 IAM Role per application strongly recommended

Public ip will change when we stop our instance and restart it.
Private ip remains the same.

Security groups are like a firewall which controls the inbound and outbound traffic which can access our EC2 instance.
Elastic Cloud Compute

Elastic IPs are ip which persists even after our instance is stopped.
Usually we should not use Elastic Ip as it represents poor architectural decisions.

- If there is any timeout issue while accessing the instance it is generally due to security group.

---

- Ec2 instance launch types
- On demand instance
- Reserved instance
- Convertible reserved instance
- Scheduled reserved instance
- Spot instances
- Dedicated instances
- Dedicated hosts

---

## EC2 Instance Types:

- R: applications that needs a lot of RAM –in-memory caches
- C: applications that needs good CPU –compute / databases
- M: applications that are balanced (think “medium”) –general / web app
- I: applications that need good local I/O (instance storage) –databases
- G: applications that need a GPU –video rendering / machine learning
- T2 / T3: burstable instances (up to a capacity)
- T2 / T3 -unlimited: unlimited burst
---
## Amazon Machine Image

- AMI are built for a specific AWS region
- AMI occupies storage in S3
- Can use Public AMIs
- when a new instance is created it gets created from the snapshot of our AMIs
- Cross Account EMI Copy
- You can't copy an encrypted AMI that was shared with you from another account. Instead, if the underlying snapshot and encryption key were shared with you, you can copy the snapshot while re-encrypting it with a key of your own. You own the copied snapshot, and can register it as a new AMI.
- You can't copy an AMI with an associatedbillingProductcode that was shared with you from another account. This includes Windows AMIs and AMIs from the AWS Marketplace. To copy a shared AMI with abillingProductcode, launch an EC2 instance in your account using the shared AMI and then create an AMI from the instance.
- --
## EC2 placement group
- 
- Spread
- Partition

DocumentDB vs DynamoDB
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEyMTY1NzMyMF19
-->
