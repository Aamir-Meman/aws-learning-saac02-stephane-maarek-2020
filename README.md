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
---
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
---
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
---
## 3.5 EC2 Introduction

**Q=1 What is EC2 (Elastic Compute Cloud)**
- EC2 is one of the most popular of AWS offering.
- It mainly consist in the capability of:
  - Renting Virtual Machines (EC2)
  - Storing data on virtual drives (EBS)
  - Distributing load across machines(ELB)
  - Scaling the services using an auto-scaling group (ASG)
---
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
---
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
---
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
---
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
---
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
----
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
---