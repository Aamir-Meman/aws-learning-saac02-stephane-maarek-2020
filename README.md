# aws-learning-saac02-stephane-maarek-2020
This is the notes created from Stephane Maarek course - AWS SAACO2 2020
- [Section 1: Introduction - AWS Certified Solutions Architect Associate](https://github.com/Aamir-Meman/aws-learning-saac02-stephane-maarek-2020#section-1-introduction---aws-certified-solutions-architect-associate)
- [Section 3 AWS Fundamentals: IAM and EC2](https://github.com/Aamir-Meman/aws-learning-saac02-stephane-maarek-2020#section-3-aws-fundamentals-iam-and-ec2)
   - [3.1 AWS Regions and AZs](https://github.com/Aamir-Meman/aws-learning-saac02-stephane-maarek-2020#31-aws-regions-and-azs)
   - [3.2 IAM Introduction](https://github.com/Aamir-Meman/aws-learning-saac02-stephane-maarek-2020#32-iam-introduction)
   - [3.5 EC2 Introduction](https://github.com/Aamir-Meman/aws-learning-saac02-stephane-maarek-2020#35-ec2-introduction)
   - [3.12 Introduction to Security Groups](https://github.com/Aamir-Meman/aws-learning-saac02-stephane-maarek-2020#312-introduction-to-security-groups)
   - [3.14 Private vs Public vs Elastic IP](https://github.com/Aamir-Meman/aws-learning-saac02-stephane-maarek-2020#314-private-vs-public-vs-elastic-ip)
   - [3.16 EC2 User Data](https://github.com/Aamir-Meman/aws-learning-saac02-stephane-maarek-2020#316-ec2-user-data)
   - [3.17 EC2 Instance Launch Types](https://github.com/Aamir-Meman/aws-learning-saac02-stephane-maarek-2020#317-ec2-instance-launch-types)
   - [3.18 Spot Instances & Spot Fleet](https://github.com/Aamir-Meman/aws-learning-saac02-stephane-maarek-2020#318-spot-instances--spot-fleet)
   - [3.19 EC2 Instance Types Deep Dive](https://github.com/Aamir-Meman/aws-learning-saac02-stephane-maarek-2020#319-ec2-instance-types-deep-dive)
   - [3.20 EC2 AMIs](https://github.com/Aamir-Meman/aws-learning-saac02-stephane-maarek-2020#320-ec2-amis)
   - [3.21 Cross Account AMI Copy (FAQ + Exam Tip)](https://github.com/Aamir-Meman/aws-learning-saac02-stephane-maarek-2020#321-cross-account-ami-copy-faq--exam-tip)
   - [3.22 EC2 Placement Groups](https://github.com/Aamir-Meman/aws-learning-saac02-stephane-maarek-2020#322-ec2-placement-groups)
   - [3.23 Elastic Network Interfaces (ENI) with hands On](https://github.com/Aamir-Meman/aws-learning-saac02-stephane-maarek-2020#323-elastic-network-interfaces-eni-with-hands-on)
   - [3.24  EC2 Hibernate](https://github.com/Aamir-Meman/aws-learning-saac02-stephane-maarek-2020#324-ec2-hibernate)
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
---
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
---
**Q=2 What are IAM Federation**
- Big enterprises usually integrate their **own repository** of users with IAM.
- This way, one can login into AWS using their company credentials.
- Identity Federation uses the SAML standard (Active Directory).
---
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
---
**Q=2 What are SG's i.e. Deeper Dives?**'
- Security Groups are acting as a "firewall" on EC2 instances.
- They regulate
   - Access to Ports
   - Authorised IP ranges - IPv4 and IPv6
   - Control of inbound network (from other to the instance)
   - Control of outbound network (from the instance to other)
---
**Q=3 Security Groups Good to know ?**
- It can be attached to multiple instances.
- Locked down to a region/VPC combination.
- Does **live "outside" the EC2** - if traffic is blocked the EC2 instance won't see it
- **It's good to maintain one seperate security group for SSH access**
- If your application is not accessible (time out), then it's a security group issue.
- If your application gives a "connection refused" error, then it's an application error or it is not launched.
- All **inbound** traffic is blocked by default.
- All **outbound** traffic is authorised by default.

## 3.14 Private vs Public vs Elastic IP

**Q=1 Fundamental Difference between Private and Public IP (IPv4)**
- Public IP
  - Public IP **means the machine can be identified on the internet (www)**
  - Must be **unique across the whole web (not two machines can have the same public IP).**
  - Can be **geo-located easily**
- Private IP
  - Private IP **means the machine can only be identified on a private network only.**
  - The IP must be unique across the private network.
  - But **two different private networks (two companies) can have the same IPs.**
  - Machines **connect to WWW using an internet gateway (a proxy)**
  - Only a **specified range of IPs can be used as private IP.**
---
**Q=2 What is an Elastic IP's?**
- When you **stop and then start an EC2 instance, it can change its public IP.**
- If you need to have a **fixed public IP** for your instance, you need an Elastic IP.
- An Elastic IP is a public IPv4 IP you own as long as you don't delete it.
- You can attach it to one instance at a time.
- With an Elastic IP address,you can mask the failure of an instance or software by rapidly remapping the address to another instance in your account.
- You can only have **5 Elastic IP** in your account (you can ask AWS to increase that).
- Overall, try to avoid using Elastic IP:
  - They often **reflect poor architetural decisions**.
  - Instead, use a random public IP and register a DNS name to it
  - Or, as well see later, use a Load Balancer and don't use a public IP.
---
**Q=3 Private vs Public IP (IPv4)**
- By default, your EC2 machine comes with:
  - A private IP for th internal AWS Network
  - A public IP for the WWW.
- When we are doing SSH into our EC2 machines:
  - We can't use a private IP, because we are not in the same network
  - We can only use the public IP
- If your machine is stopped and then started, the public IP can change.

## 3.16 EC2 User Data

**Q=1 What is EC2 User Data?**
- It is possible to bootstrap our instances using an EC2 User data script.
- bootstrapping means launching commands when a machine starts
- The **script is only run once at the instance first start**
- EC2 user data is used to automate boot tasks such as:
  - Installing updates
  - Installing software
  - Downloading common files from the internet
  - Anything you can think of
- The **EC2 User Data Script runs with the root user**

## 3.17 EC2 Instance Launch Types

**Q=1 What are EC2 Instance Launch Types?**
- **On Demand Instances**:- short workload, predictable pricing
- Reserved: **(MINIMUM 1 year)**
  - Reserved Instances: long workloads
  - Convertible Reserved Instances:  Long workloads with flexible instances
  - Scheduled Reserved Instances: example every Thursday between 3 and 6 pm
- Spot Instances: short workload, **for cheap**, can lose instances (less reliable)
- Dedicated Instances: no other customer will share your hardware
- Dedicated Hosts: **book an entire physical server**, control instance placement.
---
**Q=2 What is EC2 On Demand?**
- Pay for what you use (billing per second, after the first minute)
- Has the highest cost but no upfront payment.
- No long term commitment
- **Recommended for short-term and un-interrupted workloads, where you can't predict how the application will behave.**
---
**Q=3 What are EC2 reserved Instances?**
- Up to **75% discount** compared to On-demand.
- Pay upfront for what you use with long term commitment.
- Reservation period can be 1 or 3 years.
- Reserve a specific instance type.
- **Recommended for steady state usage applications(think database)**
---
**Q=4 What are Convertible Reserved Instance?**
- It can change the EC2 instance type.
- Up to 54% discount.
---
**Q=5 What are Scheduled Reserved Instances?**
- Launch within time window you reserve.
- When you require a fraction of day/ week/ month.
---
**Q=6 What are EC2 Spot Instances?**
- It can get a discount of up to 90% compared to On-demand.
- Instances that you can "lose" at any point of time if your max price is less than the current spot price.
- The **MOST** efficient instances in AWS
- Useful for workloads that are resilient to failure
   - Batch jobs
   - Data analysis
   - Image processing
   - ...
- Not great for critical jobs or databases
- Great Combo:- Reserved Instances for baseline + On-Demand & Spots for peaks.
---
**Q=7 What are EC2 Dedicated Hosts?**
- Physical dedicated EC2 server for your use.
- Full control of EC2 Instance placement.
- Visibility into the underlying sockets/ physical cores of the hardware.
- Allocated for your account for a 3 year period reservation.
- More Expensive

- Useful for software that have complicated licensing model(BYOL - Bring Your Own License)
- Or for companies that have strong regulatory or compliance needs.
---
**Q=8 What are EC2 Dedicated Instances?**
- Instances running on hardware that's dedicated to you.
- May **share hardware with other instances in same account**.
- No control over instance placement ( can move hardware after Stop/Start)

## 3.18 Spot Instances & Spot Fleet

**Q=1 What is EC2 Spot Instance Requests?**
- It can get a discount of up to 90% compared to On-demand
- Define max spot price and get the instance while current spot price < max
  - The hourly spot price varies based on offer and capacity
  - If the current spot price > you max price you can choose to stop or terminate your instance with a 2 minutes grace period.
- Other Strategy: **Spot Block**
   - "block" spot instance during a specified time frame (1 to 6 hours) without interruptions
   - In rare situations, the instance may be reclaimed
- **Used for batch jobs, data analysis or workloads that are resilent to failures**.
- Not great for critical jobs or databases.
---
**Q=2 How to terminate Spot Instances?**
- You can only cancel Spot Instance requests that are open, active or disabled.
- **Cancelling a Spot Request does not terminate instances**.
- You must first cancel a Spot Request, and then terminate the associated Spot Instances.
---
**Q=3 What are Spot fleets?**
- **Spot Fleets = set of Spot Instances + (optional) On-Demand Instances.**
- The Spot Fleet will try to meet the target capacity with price constraints
   - Define possible launch pools: instance type(m5.large), OS, AZ.
   - Can have multiple launch pools, so that the fleet can choose
   - Spot Fleet stops launching instances when reaching capacity or max cost.
- Strategies to allocate Spot Instances:
   - lowestPrice: from the pool with the lowest price (cost optimization, short workload)
   - diversified: distributed across all pools (great for availaibility, long workloads)
   - capacityOptimized: pool with optimal capacity for the number of instances
- Spot Fleets allow us to automatically request Spot Instances with the lowest price.

## 3.19 EC2 Instance Types Deep Dive

**Q=1 The EC2 Instance Types = Mains ones**
- R: applications **that needs a lot of RAM** - in-memory caches.
- C: applications **that needs good CPU** - compute/databases.
- M: applications **that are balanced (think "medium")** - general/ web app
-  I: applications **that need good local I/O (instance storage)** - databases
- G: applications **that need a GPU** - video rendering / machine learning.
- T2/T3: burstable instances (up to a capacity)
- T2/T3 - unlimited: unlimited burst 
---
**Q=2 What are Burstable Instances (T2/T3)?**
- AWS has concept of burstable instances (T2/T3) machines.
- Burst means that overall, the instance has OK CPU performance.
- When **the machine needs to process something unexpected ( a spike in load for example), it can burst, and CPU can be VERY good**.
- if the machine bursts, it utilizes "burst credits"
- If all the credits are gone, **the CPU becomes BAD**
- If the machine stops bursting, credits are accumulated over time.
- Burstable instances can be amazing to handle unexpected traffic and getting the insurance that it will be handled correctly.
- If your **instance consistently runs low on credit, you need to move to a different kind of non-burstable instance.**
---
**Q=3 What is T2/T3 Unlimited?**
- On Nov 2017: **It is possible to have an "unlimited burst credit balance"**
- You pay extra money if you go over your credit balance, but you don't lose in performance
- Overall, **it is a new offering, so be careful, costs could go high if you are not monitoring the health of your instances.**

## 3.20 EC2 AMIs

**Q=1 What's an AMI**
- As we saw, AWS comes with base images such as:
  - Ubuntu
  - Fedora
  - RedHat
  - Debian
  - Windows
  - Etc...
- These images can be customized at runtime using EC2 User data
- But what if we could create our own image, ready to go?
- **That's an AMI - an image use to create our instances**
---
**Q=2 Why would you use a custom AMI?**
- Using a custom built AMI can provide the following advantages:
  - Pre-installed packages needed
  - Faster boot time (no need for ec2 user data at boot time)
  - Machine comes configured with monitoring/enterprise software
  - Security concerns - control over the machines in the network
  - Control of maintenance and updates of AMIs over time
  - Active Directory Integration out of the box
  - Installing your app ahead of time (for faster deploys when auto-scaling)
  - Using someone else's AMI that is optimised for running an app,DB etc..
- **AMI are built for a specific AWS region (!)**
---
**Q=3 Using Public AMIs**
- You can leverage AMIs from other people
- You can also pay for other people's AMI by the hour
  - These people have optimised the software
  - The machine is easy to run and configure
  - You basically rent "expertise" from the AMI creator
- **AMI can be found and published on the Amazon Marketplace**
- **Warning**
  - Do not use an AMI you don't trust.
  - Some AMIs might come with malware or may not be secure for enterprise.
---
**Q=4 AMI Storage**
- Your AMI take place and they live in Amazon S3.
- Amazon S3 is a durable, cheap and resilient storage where most of your backups will live(but you won't see them in the S3 console).
- **By default, your AMIs are private, and locked for your account/region**
- You can also make your AMIs public and share them with other AWS accounts or sell them on the AMI Marketplace
----------
**Q=5 AMI Pricing**
- AMIs live in Amazon S3, **so you get charged for the actual space in takes in Amazon S3**.
- Overall it is **quite inexpensive** to store private AMIs
- Make sure to remove the AMIs you don't use.
-------
## 3.21 Cross Account AMI Copy (FAQ + Exam Tip)
**Q=1 What are the permissions for cross account AMIs copy?**
- You can share an AMI with another AWS account.
- Sharing an AMI does not affect the ownership of the AMI.
- If you **copy** an AMI that has been shared with your account, you are the **owner** of the target AMI in your account.
- To copy an AMI that was shared with you from another account, **the owner of the source AMI must grant you read permissions for the storage that backs the AMI, either the associated EBS snapshot(for an Amazon EBS-backed AMI) or an associated S3 bucket(for an instance store-backed AMI)**.
- **Limits**:
  - You can't copy an encrypted AMI that was shared with you from another account. Instead, if the underlying snapshot and encryption key were shared with you, you can copy the snapshot while re-encrypting it with a key of your own. You own the copied snapshot, and can register it as a new AMI.
  - You can't copy an AMI with an associated **billingProduct** code that was shared with you from another account.This includes Windows AMIs and AMIs from the AWS Marketplace. To copy a shared AMI with a **billingProduct** code, launch an EC2 instance in your account using the shared AMI and then create an AMI from the instance.
 
## 3.22 EC2 Placement Groups
**Q=1 What are EC2 Placement Groups?**
- Sometime you want control over the EC2 Instance placement strategy.
- That strategy can be defined usig placement groups.
- When you create a placement group, you specify one of the following strategies for the group:
  - **Cluster** - clusters instances into a low-latency group in a single Availability Zone.
  - **Spread** - spread instances across underlying hardware (max 7 instances per group per AZ)**critical applications**.
  - **Partition** -spread instances across many **different partitions** (which rely on different sets of racks)within an AZ. Scales to 100 of EC2 instances per group (Hadoop, Cassandra, Kafka)
---
**Q=2 What is EC2 Cluster Placement Groups?**
 - Pros:- Great network (10 - Gbps badnwidth between instances)
 - Cons:- If the rack fails, all instances fails at the same time
 - Use case:
   - **Big Data job that needs to complete fast**
   - **Application that needs extremely low latency and high network throughput**
---
**Q=3 What is EC2 Spread Placement Groups**
- Pros:
  - Can span across Availability Zones (AZ)
  - Reduced risk is simultaneous failure
  - EC2 Instances are on different physical hardware
- Cons:
  - Limited to 7 instances per AZ per placement group
- Use Case:
  - **Application that needs to maximize high availability**
  - **Critical Applications where each instance must be isolated from failure**
---
**Q=4 What is EC2 Partition Placement Groups**
 - Up to **7** partitions per AZ.
 - Up to **100s** of EC2 instances
 - The instances in a partition do not share racks with the instances in the other partitions.
 - A partition failure can affect many EC2 but won't affect other partitions.
 - EC2 instances get access to the partition information as metadata
 - Use cases:
   - **HDFS, HBase, Cassandra, Kafka**

## 3.23 Elastic Network Interfaces (ENI) with hands On
**Q=1 What is Elastic Network Interfaces(ENI)?**
 - Logical component in a VPC that represents a **virtual network card**
 - The ENI can have the following attributes:
   - **Primary private IPv4, one or more secondary private IPv4**
   - One Elastic IP (IPv4) per private IPv4
   - One Public IP (IPv4)
   - One or more security groups
   - A MAC address
 - **You can create ENI independently and attach them on the fly(move them) on EC2 instances for failover**
 - Bound to a specific availability zone (AZ)

## 3.24 EC2 Hibernate
**Q=1 What are EC2 Hibernate**
 - We know we can stop, terminate instances
   - Stop: The data on disk(EBS) is kept intact in the next start.
   - Terminate: any EBS volumes(root) also set-up to be destroyed is lost.
 - On start, the following happens:
   - First start: the OS boots and the EC2 User Data script is run
   - Following starts: the OS boots up.
   - **Then your application starts, caches get warmed up, and that can take time!**
 - Introducing **EC2 Hibernate**:
   - The in-memory(RAM) state is preserved.
   - The instance boot is much faster!(the OS is not stopped/restarted)
   - **Under the hood: the RAM state is written to a file in the root EBS volume**
   - **The root EBS volume must be encrypted**
 - Use cases:
   - **long-running processing**
   - **saving the RAM state**
   - **services that take time to initialize**

**Q=2 EC2 Hibernate - Good to know**
 - Supported instance families - C3,C4,C5,M3,M4,M5,R3,R4 and R5
 - Instance RAM Size - must be less than 150 GB.
 - Instance size - not supported for bare metal instances.
 - AMI - Amazon Linux 2, Linux AMI, Ubuntu and Windows
 - Root Volume - must be **EBS**,encrypted,not instance store and **large**
 - Avaialaible for On-Demand and Reserved Instances
 - An instance cannot be hibernated more than 60 days.

# Section 4 High Availability and Scalability: ELB and ASG

## 4.1 High Availability and Scalability
**Q=1 What does it mean by Scalability and High Availability**
 - Scalability means that an application can handle greater loads by adapting
 - There are 2 kinds of scalability:
   - Vertical Scalability
   - Horizontal Scalability(= elasticity)
 - **Scalability is linked but different to High Availability**

 **Q=2 What is Vertical Scalability?**
  - Vertically Scalability means increasing the size of the instance
  - For example, your application runs on a t2.micro
  - Scaling that application vertically means running it on a t2.large
  - Vertical Scalability is very common for non distributed systems such as Database.
  - **RDS,ElasticCache are service that can scale vertically.**
  - There's usually a limit to how much you can vertically scale(hardware limit)

**Q=3 What is Horizontal Scalability?**
 - Horizontal Scalability means **increasing the number of instances / systems for your application**
 - Horizontal scaling implies distributed systems
 - This is very common for web applications/ modern applications.
 - It is easy to horizontally scale thanks the cloud offerings such as **Amazon EC2** 

**Q=4 What is High Availability?**
 - High Availability usually goes hand in hand with **horizontal scaling**.
 - High Availability means running your application / system in at least 2 data centers (== Availability Zones)
 - The goal of high availability is to survive a data center loss.
 - **The high availability can be passive (for RDS Multi AZ for example)**.
 - **The high availability can be active (for horizontal scaling)**

**Q=5 High Availability and Scalability for EC2**
 - Vertical Scaling: Increase instance size **(= scale up / down)**
 - Horizontal Scaling: Increase number of instances **(= scale out / in)**
   - ASG(Auto Scaling Group)
   - Load Balancer
 - **High Availability: Run instances for the same application across Multi AZ**
   - Auto Scaling Group multi AZ
   - Load Balancer multi AZ

## 4.2 Elastic Load Balancing (ELB) Overview
**Q=1 What is Load Balancing?**
 - Load balancers are servers that forward internet traffic to multiple servers (EC2 Instances) downstream.

**Q=2 Why use a Load Balancer**
 - Spread load across multiple downstream instances.
 - Expose a single point of access (DNS) to your application.
 - Seamlessly handle failures of downstream instances.
 - Do regular health checks to your instances.
 - Provide SSL termination (HTTPS) for your websites.
 - Enforce stickiness with cookies.
 - High availability across zones.
 - Seperate public traffic from private traffic.

 **Q=3 Why use an EC2 Load Balancer?**
  - An ELB(EC2 Load Balancer) is a **managed load balancer**
    - AWS guarantees that it will be working
    - AWS takes care of upgrades, maintenance, high availability
    - AWS provides only a few configuration knobs
  - It costs less to setup your own load balancer but it will be a lot more effort on your end.
  - It is integrated with many AWS offerings/ services.
  