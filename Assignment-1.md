## Assignment Objective

Create a custom VPC with one public and one private subnet, set up the correct routing for internet access, and deploy EC2 instances across them.

## Tasks

### 1. Create the VPC

<img width="1183" height="258" alt="image" src="https://github.com/user-attachments/assets/894e6947-7830-4036-a59c-01ca3cd610ed" />



Custom VPC (e.g. 10.0.0.0/16)

Public subnet and Private subnet
<img width="995" height="107" alt="image" src="https://github.com/user-attachments/assets/596cda2f-440e-41cd-b4fe-419e72e27c5a" />



### 2. Internet Access

Created and attached an Internet Gateway
<img width="1021" height="73" alt="image" src="https://github.com/user-attachments/assets/b1c6c2cc-3a07-4288-8ff9-1b649971cbd5" />



Created an Elastic IP
<img width="1044" height="166" alt="image" src="https://github.com/user-attachments/assets/005d44bf-ef77-45cd-a160-5259fc5bc077" />

Created a NAT Gateway in the public subnet
<img width="979" height="166" alt="image" src="https://github.com/user-attachments/assets/df190e18-9004-440e-b805-ce5f90eaecce" />




### 3. Route Tables
Public route table → default route via IGW
<img width="1308" height="304" alt="image" src="https://github.com/user-attachments/assets/74e60886-4007-4b0b-9678-7e3bd5cce214" />


Private route table → default route via NAT Gateway
<img width="1167" height="297" alt="image" src="https://github.com/user-attachments/assets/2c4e821b-250c-4caa-8449-4c07623bf0f6" />



### 4. EC2 Instances
Public EC2: launch in public subnet with public IP
<img width="1016" height="512" alt="image" src="https://github.com/user-attachments/assets/1639b99f-8a9b-4613-9cfc-3b3b2677731e" />

Private EC2: launch in private subnet without public IP
<img width="1007" height="524" alt="image" src="https://github.com/user-attachments/assets/2647def4-186e-4be1-8005-70ae49b81867" />



### 5. Security

Public EC2 SG: allow SSH/HTTP only from your IP
<img width="1030" height="212" alt="image" src="https://github.com/user-attachments/assets/ceeb7975-0719-48aa-a986-f3680120d72c" />




Private EC2 SG: allow only internal access (e.g. from public EC2 or Bastion host)
<img width="944" height="188" alt="image" src="https://github.com/user-attachments/assets/4d5993db-85f9-4aa9-9bd0-264f5654d0d2" />


