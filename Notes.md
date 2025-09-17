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






