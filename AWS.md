## AWS

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
- 1 IAM Role per application

Public ip will change when we stop our instance and restart it.
Private ip remains the same.

Security groups are like a firewall which controls the inbound and outbound traffic which can access our EC2 instance.
Elastic Cloud Compute

Elastic IPs are ip which persists even after our instance is stopped.
Usually we should not use Elastic Ip as it represents poor architectural decisions.

- 
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTYxNzgwMjAzOCwtMjAzMzc5MTc5MywxMT
E4MjU2Njg1LC0yMDc4OTcwNDIxLC0xNzYwMjUzOTI0LDEwMzM4
NzcwOTldfQ==
-->