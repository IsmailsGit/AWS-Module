# Assignment 2 - Application Load Balancer
A common DevOps pattern: multiple EC2 instances behind an ALB. This teaches load balancing, health checks, and proper security group isolation.

## My Objective 
Deploy two EC2 instances behind an ALB. The ALB must handle all incoming traffic. EC2 instances should not be accessible directly from the internet.

## Tasks

### 1. Two EC2 Instances

Launch two EC2 instances in the same VPC

Instance 1

<img width="223" height="268" alt="image" src="https://github.com/user-attachments/assets/6436a040-e3d8-4125-8fd7-3f62d1a6e17c" />


<br> Instance 2

<img width="229" height="326" alt="image" src="https://github.com/user-attachments/assets/1c952daf-4c8a-4d3c-a308-d1b6c809258b" />

Both instances are in two different availability zones





Install a simple web server using user-data
<br> Each instance should return different content for testing

Instance 1 Web Server

<img width="717" height="148" alt="image" src="https://github.com/user-attachments/assets/8effc79d-c008-4228-8dd6-ef51e3d87f12" />

Instance 2 Web Server

<img width="724" height="145" alt="image" src="https://github.com/user-attachments/assets/face030d-f3e6-4501-b977-f03cc751c3c8" />

### 2. Set up an ALB

Create an ALB in two public subnets

<img width="427" height="202" alt="image" src="https://github.com/user-attachments/assets/22cf3181-0abe-49a2-8379-1bdb465abd93" />


Add HTTP (port 80) listener

<img width="296" height="234" alt="image" src="https://github.com/user-attachments/assets/65ce4fd4-71ca-44fb-ad15-ba63e3785860" />


Created a Target Group and registered both EC2 instances

<img width="457" height="595" alt="image" src="https://github.com/user-attachments/assets/64036402-e51e-4f37-afe1-3d8b063c4b26" />



Configure a health check on the root path /

<img width="338" height="260" alt="image" src="https://github.com/user-attachments/assets/edc7f4cf-549f-4e38-9f33-c157e9ca858b" />

### 3. Security Groups

ALB SG: allow HTTP from anywhere

<img width="711" height="523" alt="image" src="https://github.com/user-attachments/assets/60f027d6-e306-4208-abb0-3d86124d7583" />

EC2 SG: allow HTTP only from the ALB SG

Both instances
<img width="680" height="525" alt="image" src="https://github.com/user-attachments/assets/cdf9baf2-5c84-436d-a2d5-a455d0e9b5e6" />

<img width="695" height="609" alt="image" src="https://github.com/user-attachments/assets/fcea0781-83e7-4ddf-8c42-e252e9a6d4b3" />



### 4. Testing

