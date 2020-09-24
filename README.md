# aws-learning-saac02-stephane-maarek-2020
This is the notes created from Stephane Maarek course - AWS SAACO2 2020

# Section 1: Introduction - AWS Certified Solutions Architect Associate
## 1.0 What is AWS
- Amazon Web Services is a Cloud Provider.
- They provide you with servers and services that you can use on demand and scale easily.
- AWS has revolutionized IT over time.
- AWS powers some of the biggest websites in the world
  - Amazon.com
  - Netflix

# Section 3 AWS Fundamentals: IAM and EC2

## 3.1 AWS Regions and AZs 
**Q=1 What are AWS Regions?**
- AWS has Regions all around the world.
- Names can be: us-east-1 , eu-west-3
- A region is a cluster of data centers
- Most AWS services are region-scoped.

**Q=2 What are AWS Availaibilty Zones?**
- Each region has many availability zones :- (usually 3, min is 2, max is 6)
   For example:- 1) ap-southeast-2a 2)ap-southeast-2b and 3)ap-southeast-2c
- Each Availaibilty Zone(AZ) is one or more discrete data centers with redundant power, networking and connectivity.
- They are seperate from each other, so that they are isolated from disasters.
- They are connected with high bandwidth, ultra-low latency networking.

## 3.2 IAM Introduction

**Q=1 What is an IAM**
- IAM (Identity and Access Management)
- Your whole AWS security is there:
  - Users :- Usually a physical person
  - Groups :- Functions(admins, devops) , Teams(engineering,design..) Contains users!
  - Roles :- **Internal usage within AWS resources**
- Root account should never be used (and shared)
- Users must be created with proper permissions
- IAM is at the center of AWS
- Policies are written in JSON(JavaScript Object Notation)
- **Policies (JSON Documents) Defines what each of the above can and cannot do.**
- IAM has a **global** view.
- Permissions are governed by Policies(JSON).
- MFA (Multi Factor Authentication) can be setup
- IAM has predefined "managed policies"
- **It is best to give users the minimal amount of permissions they need to perform their job** (least privilege principles)

**Q=2 What are IAM Federation**
- Big enterprises usually integrate their **own repository** of users with IAM.
- This way, one can login into AWS using their company credentials.
- Identity Federation uses the SAML standard (Active Directory).

**Q=3 IAM 101 Brain Dump**
- One IAM **User** per PHYSICAL PERSON
- One IAM **Role** per Application
- IAM credentials should NEVER BE SHARED
- Never,ever, ever,ever, write IAM credntials in code. EVER.
- And even less, NEVER EVER EVER COMMIT YOUR IAM credentials.
- Never use the ROOT account except for initial setup.
- Never use ROOT IAM Credentials.

## 3.5 EC2 Introduction

**Q=1 What is EC2 (Elastic Compute Cloud)**
- EC2 is one of the most popular of AWS offering.
- It mainly consist in the capability of:
  - Renting Virtual Machines (EC2)
  - Storing data on virtual drives (EBS)
  - Distributing load across machines(ELB)
  - Scaling the services using an auto-scaling group (ASG)

## 3.12 Introduction to Security Groups

**Q=1 What is SG's?**
- Security Groups are the fundamental of network security in AWS.
- They control **how traffic is allowed into or out of our EC2 Machines**.
- It is the most **fundamental skill to learn to troubleshoot networking issues**.

**Q=2 What are SG's i.e. Deeper Dives?**'
- Security Groups are acting as a "firewall" on EC2 instances.
- They regulate
   - Access to Ports
   - Authorised IP ranges - IPv4 and IPv6
   - Control of inbound network (from other to the instance)
   - Control of outbound network (from the instance to other)

**Q=3 Security Groups Good to know ?**
- It can be attached to multiple instances.
- Locked down to a region/VPC combination.
- Does **live "outside" the EC2** - if traffic is blocked the EC2 instance won't see it
- **It's good to maintain one seperate security group for SSH access**
- If your application is not accessible (time out), then it's a security group issue.
- If your application gives a "connection refused" error, then it's an application error or it is not launched.
- All **inbound** traffic is blocked by default.
- All **outbound** traffic is authorised by default.