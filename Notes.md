# Intro to AWS
AWS (Amazon Web Services) is a cloud computing platform that provides on-demand services like computing power, storage, and databases to help businesses and developers build, deploy, and scale applications efficiently.

AWS allows you to build sophisticated and scalable applications and regardless if you're a small or big company aws will be able to support you in terms flexibility and performance. 
It's used by a diverse set of industries.
<br> AWS is used by companies for backup and storage, big data analytics, website hosting, mobile and social apps and gaming.

AWS regions - A region is a cluster of data centres, AWS has regions all around the world.

How to choose an AWS Region?
<br> Compliance with data governance and legal requirements 
<br> Availability for services, certain services aren't available in every region
<br> Proximity to customers faster response times and reduced latency
<br> Pricing, the pricing varies region to region

### AWS Availability Zones(AZs) 
<br> Each region is made up of multiple az's (usually 3-6 zones) which are data centres. They're separated from each other so they're isolated from disasters and the others can keep running.
<br> Even though the az's are physically separated they're connected with high bandwidth and low latency networking so they communicate fast with each other.
<br> AZ's give you that extra layer of protection and reliability while keeping everything connected and smooth.

Points of Presence(Edge Locations) 
Content is delivered to end users with lower latency, amazon has 400+ edge locations in 90+ cites across 40+ countries. The closer an edge location is to your end user the faster aws can deliver your content.

## IAM(Identity and Access Management)

### Users and Groups
These are what allow you to control access in AWS
<br> When you create an aws account the root account is auto created, it has complete access to everything but you don't want to give that to people so you create user accounts and you can limit/control what they have access to.
<br> Users are people within your organization and Groups only contain users not other groups

To make managing users easier you can put them into a group and assign permissions to the whole group instead on manually assigning each user permissions.  
Users don't have to be in a group and users can be in multiple groups.
Users in multiple groups inherit all permissions, and inline policies can be given to a user only and not the group for specific permissions.

### Permissions
Users or groups can be assigned JSON documents called policies
<br> These policies define the permissions of the users.
<br> In aws you apply the least privilege principle - don't give a user more permissions than necessary.

### IAM Policies Structure
*To put a screenshot into an md file copy this ![Screenshot]() then copy the image and remove anything before the https including the "" and paste into the brackets*
![Screenshot](https://github.com/user-attachments/assets/622ea9c0-646a-4020-811b-94ee6383897c) 

#### IAM Password Policy
In AWS you can setup a password policy, it will include a minimum password length, includes upper and lowercase letters, numbers and non alphanumeric characters. You also require users to change their password after some time (password expiration) and allow users to change their own passwords.
Aws also prevents password re-use, you can't reuse old passwords
Stronger password = higher security for your account.

#### MFA Multi Factor Authentication
Hackers could get into your account and change configs, run a massive bill on your account or delete everything.
MFA protects your root account and IAM user because even if anyone gets access to your account they need a security device like an app to verify that would produce a one time password(OTP).

MFA device options in AWS:
Virtual MFA device - Google authenticator, supports multiple tokens on a single device.
Universal 2nd Factor(U2F) Security Key (Yubikey by Yubico 3rd party) - Just plug in, supports multiple root and iam users using a single security key.
Hardware Key Fob MFA Device - Generates a new code every 30 seconds(Provided by Gemalto, 3rd Party)
Hardware Key Fob MFA Device for AWS GovCloud(US) - This is specifically for AWS GovCloud in the US.

#### 3 Main ways Users access AWS
AWS Mangement Console - This is the web interface you're familiar with, great for spinning up instances, creating s3 buckets and confinguring resources manually on the console(also known as click ops). Its protected by a password and MFA
AWS Command Line Interface(CLI) - You can automate tasks on the CLI, good for scripting and mangaging resources from your terminal, it's protected by access keys.
AWS Software Developer Kit(SDK) - Good for writing code, if you're a software dev this is how you interact with aws. This is protected by access keys 
Language-specific APIs(kind of like a prebuilt set of libraries that makes it easier to work with aws whether its python, javascript) 
SDK enables you to access and manage aws services directly within your application


Access keys are generated through the AWS Console, Users manage their own access keys.
Access keys are secret like a password, it shouldn't be shared.
Access Key ID - Like a username 
Secret Access Key - Like a password
Never share your access keys and it's best practice to rotate your keys which means to generate new ones.

#### IAM Roles for Services
Some aws services will need to perform actions on your behalf e.g. an ec2 instance may need to read from an s3 bucket. 

But you don't want to put hardcode credentials into those services thats where iam roles come in.

IAM roles lets aws services get temporary access to other aws services without using long term credentials like access keys or passwords. It's basically giving your aws service permission to act on your behalf in a secure way .
Common use cases: 
EC2 Instance Roles - When you launch an ec2 instance you can attach a role to it, this role gives the instance permission to access other aws services.

Lambda Function Roles - If your lambda needs to interact with other aws services, you can attach a role to it which gives it the right permissions to do its job.

Roles for CloudFormation - CloudFormation often needs to create and manage resources across multiple aws services, assigning a role allows it to handle those tasks securely without exposing credentials 

#### IAM Security Tools
These security tools help you manage your aws users and their permissions.

IAM Credentials Report(account-level) -  A report that lists all your account’s users and the status of their various credentials e.g. lets you see which users have access keys, who’s using MFA.

IAM Access Advisor(user-level) - Shows you the service permissions granted to a user and when those services were last accessed.

You can use this to remove any old or unnecessary permissions.

#### IAM Guidelines & Best Practices
1. Don’t use the root account except for aws account setup, for security reasons as the root user has access to everything, use an IAM user that has appropriate permissions instead .
2. One physical user per One aws user, no sharing logins, every person should have an account, this keeps things traceable and secure.
3. Assign users to groups and assign permissions to groups, this makes managing permissions easier and more scalable as your team grows.
4. Create a strong password policy e.g. minimum length and mixing it with characters.
5. Use and enforce the use of MFA especially those that have access to important sensitive resources.
6. Create and use roles for giving permissions to aws services instead of hard coding credentials, this is more secure and gives you better control of what services can access.
7. Use access keys for programmatic access(CLI and SDK).
8. Audit the permissions of your account using iam credentials report and iam access advisor to see what users and services are accessing and when they need these permissions.
9. Never share IAM users and access keys.


#### How to access the AWS CLI from the terminal
Do "aws configure" in the terminal then it will ask you for your access keys

Once you do all of that and your logged in do the command "aws sts get-caller-identity" to check if you are really logged in.

You can do aws iam list-users to list iam users

### EC2 and Amazon Compute
Amazon Compute provides the processing power to run applications in the cloud while AWS handles the physical servers, while you get to focus on what you want those servers to actually do.

EC2(Elastic Compute Cloud)
EC2 is one of the most popular AWS services because of its flexibility.

It mainly consists of:
Renting virtual machines(EC2) = Infrastructure as a Service

Storing data on virtual drives(EBS Elastic Block Store), kind of like a hard drive for ec2 instances.

Distributing load across machines(ELB Elastic Load Balances) - When you have multiple ec2 instances running at the same time, you want to make sure that the traffic is shared evenly. ELBs help distribute the incoming requests to your instances, so one machine isn't overloaded while others sit idle.

Scaling the services using an auto-scaling group(ASG) - This allows ec2 to scale automatically, if your application gets more traffic, more instances are added. And if your traffic slows down, extra instances are removed. This is known as scaling in and scale out. You only pay for what you use.

#### EC2 Sizing and configuration options 
Before you launch an ec2 instance aws lets you configure the instance:

What operating system - Linux, Windows, even MacOS and more, the os you go for depends on what your application needs.

How much compute power and cores(CPU), you can tailor this if you need more or less processing power.

How much RAM,memory your instance will have, more memory helps with handling more data in real time.

How much storage space - 
Network attached EBS and EFS(Elastic File System) EBS is kind of like the hard drive attached to your virtual machine and think of EFS like shared storage accessible from multiple instances. 
Hardware(EC2 Instance Store) is basically a hardware-level storage that's physically attached to the host machine. It's fast, but temporary. Means that if the instance is stopped, you lose the data on it.

Network card - you can configure the speed of the network card depending on how much traffic you expect. 
Public ip address - You can get a public ip address if you want your instance accessible from the internet.

Firewall rules - Security groups(Known as SGs) act as firewalls for your instance, you can set up rules to control who can access your instance and which traffic can get through. Now this is super important for securing your EC2 instances.

Bootstrap script or known as EC2 User Data - Details are in the next section

Wrong sizing/config settings can lead to underperformance or overpaying for resources you don't need.

#### User Data/Bootstrap Script
Bootstrap script or known as EC2 User Data - it's a script that runs automatically only when the instance launches for the first time, it can be used to install software, run updates or downloading files from the internet like common packages, config files, any automation task you'd want to run when your machine first boots up, you do it here.
EC2 user data script runs with root, meaning that it has full control of the system, that's powerful, but it means that you should be careful about what you include in this script.

User data is perfect for automating deployments, why? because in larger production environments, manually logging into every instance to run setup commands would be a nightmare. With user data, you set it once, and AWS takes care of the rest.

#### EC2 Instance Types Overview
General Purpose - these are your go-to well-rounded instances. They work for a lot of different use cases, whether you're on your web server, a basic one, a small database, or other general workloads.

Compute Optimized - if you need lots of processing power, these are quite useful. Compute Optimized instances give you extra CPU for tasks like heavy calculations, batch processing, or even high-performance computing. 

Memory Optimized - When your application needs a lot of memory or even RAM, you go for these. Things like in-memory databases, big data processing, or high-performance computing workloads benefit from Memory Optimized instances

Storage Optimized - These are designed for fast and high-throughput storage. What does that mean? If you're dealing with large datasets or running databases that require quick access to storage, these instances are the right choice.

Accelerated Computing Optimized - this is where AWS steps up the game with GPUs and FPGAs* and so on. If you're doing machine learning, video processing/graphics processing these are what you need
FPGAs* (Field-Programmable Gate Arrays) are reprogrammable hardware chips that can be customized to run specific workloads with very high efficiency, unlike general-purpose CPUs or GPUs. In AWS, they’re used through EC2 F1 instances for tasks like genome analysis, financial modeling, video processing, and machine learning inference.

HPC Optimized (High-performance computing) - It's designed for intensive computing tasks, yes, that require a lot of powerful processing and even fast networking such as complex simulations, deep learning, and visual effects rendering.

Instance naming example m5.2xlarge
M = Instance class, this one is a general type, 
5 = is the generation of the instance, AWS improves its instance over time each new generation is more powerful or efficient than the last
2xlarge = Size within the instance class, There are small, large, xlarge, and even up to 32xlarge. The bigger the size, the more resources like CPU and memory that instance has and more expensive.

### Security Groups(SGs)
Security groups control what traffic is allowed into and out of your ec2 instances.
They are the backbone of network security for ec2 instances.




