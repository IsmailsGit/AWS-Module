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

### Introduction to Security Groups(SGs)
Security groups control what traffic is allowed into and out of your ec2 instances.
They are the backbone of network security for ec2 instances.

Security groups only deal with allow rules, unlike normal firewalls where you can have both allow and deny rules, security groups only focus on what's allowed anything else is blocked by default.

You can set rules that specify what traffic is allowed based on ip addresses or even other security groups.

Security groups are stateful - Means if you allow inbound traffic, the corresponding outbound traffic is automatically allowed and vice versa.

#### Security Groups Deeper Dive
Security groups act as a "firewall" on ec2 instances
They regulate:
<br> Access to Ports(which ports are open on your instance)
<br> Authorised IP ranges - IPv4 and IPv6
<br> Control of inbound network(from other to the instance)
<br> Control of outbound network(from instance to other)

It's good practise to keep your security groups as tight as possible, you should only open the port you absolutely need and limit access to trusted ips, this minimises your instance exposure to any potential attacks.

#### Security Groups Good to know
1.Security groups can be attached to multiple instances, can be reused.
<br> 2. Locked down to a region/VPC combination, can't use a security group from one region or vpc in another.
<br> 3. Security groups live "outside" the ec2 instance - if traffic is blocked the ec2 instance won't see it.
<br> 4. Good practise to maintain one separate security group for SSH access - this way you can tightly control what ips can access your instances via SSH without affecting other rules.
<br> 5.If your application is not accessible(time out) then it's a security group issue blocking traffic.
<br> 6. If your application gives a "connection refused" error then it's an application error or instance issue or config issue.
<br> 7. All inbound traffic is blocked by default - needs to be manually configured.
<br> 8. All outbound traffic is authorised by default - needs to be manually configured.

#### Referencing other security groups
Normally security groups define rules using ip addresses but if you want to control access between instances and those instances might change ips you would reference other security groups.

By referencing other security groups in your security group you are allowing traffic from any instances in those security groups.

Why is this useful? - It makes managing security easier. Instead of constantly updating IP addresses, having to manually adjust firewalls, you can just authorize entire SGs to communicate with each other

Examples - 
For example, in a microservice architecture, you might want to allow all instances in one SG.
Another example, a database tier, to talk to all instances in another SG like an app tier
Now this method simplifies configuration by using SGs as references rather than certain IPs.

This kind of referencing is especially helpful in dynamic environments like auto-scaling groups or clusters where instances might come and go, but you still maintain secure communication between them

#### Classic Ports to know

22 = SSH(Secure Shell) - SSH is used to securely log in to a linux instance, you often use this to manage your instances, you should always restrict access to port 22 to only trusted IPs.

21 = FTP(File Transfer Protocol) - Used to upload files into a file share, It's not very secure so its being replaced for more secure options like SFTP.

22 = SFTP(Secure File Transfer Protocol) - Uploads files using SSH, also uses port 22 because SFTP is the secure version of FTP it uses SSH thats why it has the same port.

80 = HTTP - Used to access unsecured websites, web traffic doesn't use encryption.

443 = HTTPS - Used to access secured websites over TLS, it encrypts web traffic which is essential for websites handling sensitive data.

53 = DNS - DNS is responible for translating domain names into ip addresses, essential for any application that requires domain name resolution.

3389 = RDP(Remote Desktop Protocol) - RDP allows you to log into a windows instance it's commonly used for management of windows based instances.

25 = SMTP

3306 = MySQL protocol

5432 = Postgres

#### Private vs Public IPs Example(IPv4)
Example - Relates to how routers function at layer, directing traffic between different networks. In this example traffic is moving between private and public networks
![Screenshot](https://github.com/user-attachments/assets/7e2d42b8-5ba5-4a18-966d-c57c9e59047e)
Both companies have their own private networks using private ip addresses
<br> These private ips are not routable on the public internet meaning they can't communicate directly with an external website or service.

So to reach the internet they would use an internet gateway, an internet gateway is similar to your home router. 
<br> Your router assigns private IPs to the devices. When you visit a website, your router acts as the middleman, translating those private IP addresses into a public IP so your traffic can travel over the internet to the other servers. 

In this diagram, each company's internet gateway is taking traffic from their private networks and translating it into a public IP. This allows them to communicate with web servers which have their own public IPs.

The router at home or the internet gateway at a company both perform NAT(network address translation). They're converting private IPs to public IPs and vice versa, enabling devices in a private network to communicate with the public internet.

Why is the internet gateway so important?  - Without the internet gateway, just like without your home router, the private network would be isolated, meaning company A and company B wouldn't be able to access websites or services on the public internet. The internet gateway is essential for moving data between these networks.

An interesting point is that private IPs can be reused across different networks like company A and company B. However, public IPs are globally unique, which is why each company gets a different public IP when connected to the internet.

#### Private vs Public IP (IPv4) Differences
Public IP                            
<br> Public IP means a machine can be identified on the internet(WWW) 

Must be unique across the internet no two devices can have the same public ip,like how no two houses can have the same postcode.

Can be geo-located easily, someone can generally tell the country and city you're machine is in.

Private IP
<br> A private ip is only used inside a private network like your home or a companies internal network. Devices within that private network can identify each other, but they can't be seen directly on them from the internet.

While a public must be unique globally, the private ip only needs be unique within its own private network. Means multiple networks can use the same private ip ranges without a problem.

Machines connect to the public internet using a NAT+ internet gateway(a proxy).
<br> Only a specified range of ips can be used as private ips.

Type of IP	         
Private IP	
Where it lives	
Stored directly on the ENI	
Description
Used for internal VPC communication

Type of IP
Public/Elastic IP
Where it lives	
Mapped to the ENI by AWS (via NAT or routing tables)	
Description
Used for communication with the internet




#### Elastic IPs
Usually if you stop and restart an instance, it would get assigned a new public ip address because aws allocates public ips dynamically.

If you need a fixed public ip for your instance you need an elastic IP

An elastic ip is a public ipv4 ip you own as long as you don't delete it.

You can attach it to one instance at a time, but you can remap it if you need to.

#### Elastic Network Interface
The ENI in aws is like a virtual network interface card, it holds a private ip that is used to communicate within a vpc. It also holds information about the Mac address and security groups. Once a public/elastic ip is mapped to it, it is able to use it to connect to the internet and receive traffic.


#### When to use Elastic IP
With an Elastic IP address, you can mask the failure of an instance or software by rapidly remapping the address to another instance in your account. - Can be useful in scenarios when we need to switch traffic from one instance to another without downtime.

However you can only have 5 elastic ip's in your account(you can ask aws to increase that).

Best practise is to avoid using elasic ips unless absolutely necessary, reasons why:
They often reflect poor architectural decisions because there are better ways to manage traffic and ips in the cloud environment.
Instead use a random public IP and register a dns name to it so you can still have a consistent way to connect to your instance, right, without needing to rely on a static IP address or use a load balancer.

### Storage
#### What's an EBS(Elastic Block Store) Volume
An EBS volume is like an network drive you can attach to your ec2 instance while they run, it's not a physical drive but it works in a similar way.

It allows your instances to persist data, even if you stop or terminate your instance the data on the ebs volume remains intact unless you choose to delete it. It can be reconnected to the same instance or another instance within the same az.

They are bound to a specific availability zone, you can't move it across zones but you can snapshot the volume and create new ones in different zones needed.

AMI
An Amazon Machine Image (AMI) is a preconfigured template that contains the operating system, application server, and software needed to launch and create new EC2 instances.

#### EFS(Elastic File System)
EFS is a managed NFS(network file system) which allows you to create a shared file system that can be mounted on multiple instances at the same time. It's like a network drive all instances can access.

EFS is designed to be used in different AZ's, its reliable as your data is automatically replicated.

EFS is scalable, it automatically grows as you add more data, no need to worry about resizing the storage volume.

However EFS is expensive, so it's best to use it when your application truly needs shared storage across multiple instances.


### Load Balancing and Scalability
#### Scalability and High Availability
Scalability means that an application or system can handle increasing loads by adapting to demand.

There are two types of scalability - Vertical Scalability and Horizontal Scalability.

#### Vertical Scalability
Vertical Scalability means increasing the size of the instance/resource you're using,you're adding more power to the server instead of adding more servers.

For example your applications runs on a t2.micro, scaling it vertically menas running it on a t2.large.

Vertical scalability is common for non distributed systems such as databases.
There's usually a hardware limit to how much you can vertically scale.

#### Horizontal scalability/Elastic Scaliung
Horizontal scalability means increasing the number of instances/systems for your application/system to handle more load

Horizontal scaling implies distributed systems, instead of relying on one powerful machine, you spread the workload across muliple smaller ones.

For example if a website gets a huge spike in traffic, with horizonral scaling you can spin up more instances to handle extra traffic and scale them down once the traffic reduces.

That flexibility is why Horizontal Scaling is often called Elastic Scaling
It's easy to implement thanks to EC2 and the process can even be automated thanks to auto scaling groups.

Horizontal scaling is key for systems that need to handle unpredictable or fluctuating workloads.

#### High Availability(HA)
High availability refers to running your application or system in multiple locations to ensure that if one part of the infrastructure goes down another part can take over.

HA usually goes hand in hand with horizontal scaling because to be highly available you need multiple instances/systems across different locations.

The goal of high availability is to survive a data centre loss, if a data centre or az goes down your application should be able to keep running in another zone without downtime.

High availability can be passive like RDS Multi AZ.
And it can be active like horizontal scaling

#### Load Balancing
Load balancing are servers that distribute traffic across multiple servers or ec2 instances, so that one server doesn't get overwhemled.

The elastic load balancer sits in between your user and your ec2 instances, when traffic comes in, it forwards the request to the ec2 instances downstream. It is constantly checking which instances are healthy and directs traffic to the ones that can handle it. It does this automatically.

Elastic Load Balancer(ELB) is AWS's version of load balancers. AWS handles the updates, maintenance and high availability.

Why use a Load Balancer? Not including the obvious reasons like distribute traffic
<br> Provides SSL termination(HTTPS) - you can configure the load balancer to handle ssl certificates and https traffic for websites. The LB handles the encrypting and decrypting of traffic.
<br> Enforce stickiness with cookies - Known as session persistence an ALB can ensure that when needed users are sent back to same instance for their requests using cookies. Can cause an imbalance due to the load over from the backend ec2 instances. 
<br> Health checks - Check to see if your instances are healthy by sending a request to a port/route if it responds with 200 its healthy, if unhealthy it sends traffic to another instance. 
<br> Separate public traffic(user facing) from private traffic(internal) - Ensures security and proper flow.

Reverse Proxy
A reverse proxy is similar to a load balancer but with extra functions.
It also sits between your users and your servers.
Reverse proxy features can route traffic based on the content of the request, routing traffic and different services.

Types of load balancers
<br> Classic Load Balancer(CLB) - It's the old generation of load balancers that was introduced to AWS in 2009, not commonly used today. Supports basic HTTP, HTTPS, TCP, and SSL traffic but it lacks the advanced features of the newer load balancers.

Application Load Balancer(ALB) - Released in 2016, designed for HTTP, HTTPS, and WebSocket traffic, making it ideal for modern web apps. It can make routing decisions based on the content of the request, like URLs, headers, query parameters, even cookies. Operates at layer 7, the application layer.
<br> ALB
<br> Routing based on path in url(coderco.io/users and coderco.io/posts)
<br> Routing based on hostnames in url (blog.coderco.io and news.coderco.io)
<br> Routing based on query string or headers which is a request coming from a mobile phone or desktop.
Has a port mapping feature to redirect to a dynamic port in ECS, this allows it to redirect traffic to containers running on different ports. ensures that even as services are deployed and scaled across various ports, the ALB knows where to send traffic.

<br> ALB gives each load balancer a fixed hostname in the format of xxxwhatever.region.aob.amazon.com. This is the URL your clients will use to access your services through the load balancer.

<br> Your application servers won't see the client's IP directly. When a client connects to the AOB, their connection is terminated at the load balancer. This means the request appears to come through the AOB's private IP and not the client's IP. ---> AWS has a way to pass along the client's actual IP address using a special HTTP header. This is called the X-Forwarded-For, which you might have seen before. Now, this header contains the true client IP and it's up to your application to read it if you need the real client's address.

Network Load Balancers(NLB) - These are layer 4 load balancers at the transport layer, they're built for TCP, UDP traffic. Designed for high-performance scenarios where you need very low latency. NLB is ideal for handling millions of requests per second, making it a good choice for high throughput, low latency applications, such as real-time gaming, or even high-frequency trading systems.

Gateway Load Balancer(GWLB) - It operates at layer 3, the network layer, and it works with the IP protocol. Designed to help you deploy, scale, and manage third-party network applications like firewalls, intrusion detection systems, and even traffic analyzers in your VPCs.

Target groups are groups of resources that your ALB routes traffic to.
<br> Types of target groups
<br> EC2 Instances - Can be managed by an auto scaling group to auto add or remove instances based on load, the alb routes http traffic to these instances, it makes sure requests are balanced between them.
<br> ECS tasks - Alb can route traffic to ecs tasks which are essentially containers running your applications, ideal for microservices and container apps.
<br> Lambda functions - Routes http requests to lamda functions, the load balancer translates the request into a json event, which the lambda function can process. Great for serverless application where you don't rely on infrastructure.
<br> IP addresses - Must be private because the ALB routes traffic inside the VPC network.
<br> Can route to multiple target groups(several services) with a single ALB.
<br> Health checks - Health checks are at the target group level

#### SSL(Secure Sockets Layer)/TLS(Transport Layer Security) 
An SSL certificate allows traffic between your clients and your load balancer to be encrypted in transit(in-flight encryption) as it travels over the internet.

SSL is used to encrypt connections but TLS is a newer version
<br> TLS certificates are mainly used but it's refered to as SSL.

Public SSL certificates are issued by Certificate Authorities(CA), they're trusted third parties that verify the identity of a website.
<br> Common CA's are Comodo, Symantec, GoDaddy, Digicert, Letsencrypt etc.

SSL certificates have an expiration date that you set and must be renewed.


Load Balancer - SSL Certificates
<br> The load balancer uses an X.509 certificate(SSL/TLS server certificate)
<br> You can manage certificates using ACM(AWS Certificate Manager)
<br> You can create and upload your own certificates alternatively
<br> HTTPS listener(process on ALB that listens for HTTP requests on a port e.g., 80):
<br> You would need to specify a default certificate
<br> You can add an optional list of certs to support multiple domains.
Clients can use SNI(Server Name Indication) to specify the hostname they want to connect to (SNI allows you to host multiple websites on the same web server with different SSL certificates).
<br> Ability to specify a security policy to support older versions of SSL/TLS(legacy clients).

Workflow
<br> Your user connects via HTTPS, which is encrypted over the internet. The load balancer handles that connection. Once you're inside your VPC, the load balancer forwards the request using plain old HTTP. Now this is private traffic, remember? So encryption isn't necessary. The request then reaches the EC2 instance. That's it, straightforward.

Deregisteration Delay/Connection Draining
Deregistration delay is when you're deregistering an instance from a load balancer because its unhealthy or you're scaling down and you want to don't want to cut off any ongoing connections immediately as that would be very bad for user experience.

In-flight requests to the user instances are allowed to complete. The load balancer stops sending new requests to that instance, but it waits for the active request to finish up. And you can control how long this process takes, between 1 to even 3,600 seconds.

#### Auto Scaling Group
Auto scaling groups add or remove instances according to the load on your websites/applications.

The goal of an ASG is to:
Scale out(add EC2 instances) to match an increased load.
Scale in(remove EC2 instances) to match a decreased load.
Ensure we have a minimum(during low traffic periods) and a maximum number(during high traffic periods) of ec2 instances running.
Automatically register new instances to a load balancer.
Recreate an ec2 instance in case a previous one is terminated(e.g. if unhealthy)

ASG's are free, you only pay for the ec2 instances they manage.

Scaling Policies
<br> Dynamic Scaling:
<br> Target Tracking Scaling - When you want the average ASG cpu to stay around 40%,if it increases it adds more instances.
<br> Simple/Step Scaling - When a CloudWatch alarm is triggered e.g. cpu > 70% then add 2 units.
<br> Scheduled Scaling - Anticipate a scaling based on known usage pattern.

### AWS Containers ECS, EKS, Fargate and ECR
Amazon Elastic Container Service(Amazon ECS) is amazons own container orchestration platform. It's a fully managed service that allows you to run Docker containers without having to install and manage orchestration software. You can define how many containers to run, what images to use, how they should interact, all through a simple interface.

Amazon Elastic Kubernetes Service(Amazons EKS) is amazons managed kubernetes service(open source) Kubernetes is an open source container orchestration platform. Amazon offers a way to use it without managing the control plane yourself. With EKS, you can take advantage of all the Kubernetes features like load balancing, scaling, while AWS handles the management of the Kubernetes control plane.

AWS Fargate is amazons own Serverless container platform which works with ECS and EKS. The difference is that Fargate removes the need for you to manage servers or EC2 instances. You just define the task and Fargate provisions the infrastructure automatically.

Amazon ECR is a container image repository where you can store, manage, and also retrieve your Docker images. Think of it like Docker Hub but fully integrated with AWS services.


### Serverless
With Serverless, developers don't have to manage servers, they just deploy code/functions. For example, in AWS, you use Lambda functions, which get triggered by events.
<br> It includes anything that's managed for you without needing to think about servers such as databases, messaging, storage etc.
<br> Serverless does not mean there are no servers, just that AWS manages the servers for you behind the scenes.

##### AWS Serverless Servers
AWS Lambda: The core of AWS service offerings. You just write your code in a function, upload it, and AWS Lambda runs it for you. No need to manage any servers.

Dynamo DB: DynamoDB is a fully-managed, serverless, NoSQL database that scales automatically. No need to worry about provisioning or managing database servers

AWS Cognito: This service helps manage user authentication, making it easy to handle logins and signups in your application. It's great for scaling your application without manual infrastructure.

AWS API Gateway: This kind of acts as a bridge between your users and Lambda functions. It allows you to create and monitor APIs which interact with your backend services.

AWS S3: S3 is a serverless offering. If you think about it, it's used for storing files and static content. Now, it's completely serverless and scales automatically based on the amount of data stored.

AWS SNS(Simple Notification Service) and SQS(Simple Queue Service): These services help with communication between different parts of your system. SNS handles notifications and SQS is for queuing messages between services.

AWS Kinesis Data Firehose: Can be used to load streaming data into AWS for analysis and storage. And this is great for real-time analytics without managing any servers.

AWS Aurora Serverless: This is a fully-managed, serverless database that autoscales based on demand.

AWS Step Functions: If you have workflows that, for example, involve many or multiple Lambda functions or services, Step Functions helps you manage and monitor these workflows seamlessly.

AWS Fargate: Fargate is the serverless compute option for containers, right? You don't need to manage any of these EC2 instances. AWS handles that while you just focus on your containers.

Benefits of Lambda
<br> Short executions - Lambda is meant for a quick task, it has a runtime limit of 50 minutes.
<br> Runs on demand - You only pay per request and compute time, you don't pay for any idle time.
<br> Integrated with AWS's services, makes everything smoother. And with many programming languages.
<br> Easy monitoring through AWS's CloudWatch

# AWS Networking
## Amazon VPC(Virtual Private Cloud)

A VPC is like your own private network in the cloud where you can isolate and control your resources and control who has access to it, also where and how traffic flows.

#### Understanding CIDR - IPv4
Classless Inter-Domain Routing - A method for allocating IP addresses 
<br> Used in security groups and AWS networking in general

They help define an IP address range
<br> For example if we see 122.149.196.85/32 - it means just one ip
<br> 0.0.0.0/0 - Means all IPs.
<br> CIDR's have more flexibility - 192.168.0.0/26 => 192.168.0.0 - 192.168.0.63(64 IP addresses)

A CIDR consists of two components
<br> Base IP: Represents an ip contained in the range and usually the start of the range (XX.XX.XX.XX) e.g.  10.0.0.0, 192.168.0.0
<br> Subnet Mask: Defines how many bits can change in the IP range
e.g. /0(means all bits can change),/24,/32(allows only one specific ip), the number following the slash determines how flexible that range is.

Subnet mask
<br> The subnet mask alows parts of the underlying ip to get additional next values from the base ip.
For example
192.168.0.0/32 - allows for 1 IP (2⁰) -> 192.168.0.0
192.168.0.0/31 - allows for 2 IP's (2¹) = 192.168.0.0 -> 192.168.0.1
192.168.0.0/30 - allows for 4 IP's (2²) = 192.168.0.0 -> 192.168.03
etc goes to /24 which allows for 256 IP's(2⁸) 192.168.0.0 -> 192.168.0.255

and 192.168.0.0/16 = allows for 65,536 IP's (2¹⁶) = 192.168.0.0 -> 192.168.255.255

Octets
/0 - All octets can change
/8 - Last 3 octets can change
/16 - Last 2 octets can change
/24 - Last octet can change
/32 -  No octet can change

Public vs Private IP(IPv4)
The Internet Assigned Numbers Authority(IANA) established certain blocks of IPv4 addresses for the use of private(LAN) and public (Internet) addresses.

Private IP can only allow certain values:
10.0.0.0 - 10.255.255.255(10.0.0.0/8) - Used for big networks
172.16.0.0 - 172.31.255.255(172.16.0.0/12) - AWS default VPC in that range.
192.168.0.0 - 192.168.255.255(192.168.0.0/16) -e.g. commonly used for home networks.

All the rest of the IP addresses that are not in these  three ranges are Public IPs with the exception of 127.0.0.1















## DNS(Route53)

## CDN(CloudFront)

     






