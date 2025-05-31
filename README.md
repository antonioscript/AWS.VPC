# AWS.VPC  
This repository provides a clear and structured overview of how Virtual Private Cloud (VPC) works within AWS. It covers core concepts such as CIDR blocks, subnets, route tables, Internet Gateways, NAT, and security layers (Security Groups vs NACLs). Ideal for learners, developers, and cloud engineers seeking to understand or document VPC architecture and networking in a practical, theory-backed way.


# Introduction to AWS VPC
</br>



![image](https://github.com/user-attachments/assets/f3084062-188e-4fe9-80db-b14bf67a7b5e)

---
</br>

## What is a VPC?

**VPC (Virtual Private Cloud)** is an isolated private network within AWS where you can launch cloud resources such as EC2, RDS, Lambda, etc. You have full control over:

- IP ranges  
- Subnets  
- Routing  
- Firewalls (Security Groups and NACLs)  
- Internet and on-premise connectivity  

---

## Core Components of a VPC

### 1. CIDR Block  
Defines the IP range of your VPC. Example:  

_10.0.0.0/16_  

Allows up to 65,536 IP addresses.

This means:

- `10.0.0.0` is the starting IP address  
- `/16` indicates the number of bits used for the network prefix  
- The remaining bits are used for host addresses

In this example, `/16` allows up to **65,536 IP addresses** (from `10.0.0.0` to `10.0.255.255`).

> The smaller the prefix (e.g., `/16`), the more IP addresses are available.  
> The larger the prefix (e.g., `/28`), the fewer IPs are available.

This IP range defines the total address space available to create subnets within your VPC.

</br>

![image](https://github.com/user-attachments/assets/58f20c42-f6a3-438a-8a9b-a63132cb113d)

---

https://cidr.xyz/


### 2. Subnets
> Subnets are usually referring to availability zones. 
In northern virginia has 6 availability zones, so it has 6 subnets by default

</br>

Sub-networks within the VPC. They can be:

- **Public Subnet** – with internet access  
- **Private Subnet** – without direct internet access  

Example:  
</br>  
_Public: 10.0.1.0/24_  
_Private: 10.0.2.0/24_

</br>

> Every subnet is part of an availability zone

## Simple Analogies

- `/8` → You control an entire **city** (`10.x.x.x`)
- `/16` → You control **neighborhoods** (`10.0.x.x`)
- `/24` → You control **streets** (`10.0.1.x`, `10.0.2.x`, etc.)

With `/24`, each street (the third octet) has **256 houses** (IP addresses).



---

### 3. Internet Gateway (IGW)  
Allows instances in public subnets to communicate with the internet.

---

### 4. Route Tables  
Define routing rules. Associated with subnets to determine how traffic should be directed.

---

### 5. NAT Gateway  
Allows instances in private subnets **to access the internet** (e.g., for updates), without being accessible from outside.

---

### 6. Security Groups vs NACLs  

- **Security Groups**: Firewall at the instance level (e.g., EC2). *Stateful*.  
- **NACLs (Network ACLs)**: Firewall at the subnet level. *Stateless*.

</br>

![image](https://github.com/user-attachments/assets/0f57f7d5-b097-4393-a2a6-9ced121623e8)

---

## Example Architecture

1. Create a VPC with `10.0.0.0/16`  
2. Create two subnets:  
   - Public: `10.0.1.0/24` (web servers)  
   - Private: `10.0.2.0/24` (database)  
3. Attach an Internet Gateway to the VPC  
4. Create a route table for the public subnet pointing to the IGW  
5. Create a NAT Gateway in the public subnet  
6. Set the private subnet's route to go through the NAT Gateway  
7. Use Security Groups and NACLs to protect the resources  

---
## Console

![image](https://github.com/user-attachments/assets/f1eaea94-56a6-408d-8502-2c85efa703ea)

---
</br>

> An example of a Public and Private Subnet is a website. Where a site it needs to be public, for people to access it, but the database that links the site information does not need to be public, has to be private.

</br>

![image](https://github.com/user-attachments/assets/7607b379-8f81-4766-90a8-18ac178431dc)

---

![image](https://github.com/user-attachments/assets/62f749ae-bba7-46c6-a000-0079847dd9d0)

---

## Create VPC

![image](https://github.com/user-attachments/assets/5be98706-eb70-4c7a-9f49-3bb4e5de92c0)

---
### Create Subnets

![image](https://github.com/user-attachments/assets/fab77381-4760-41ea-a8d6-5f4acb104108)

---
</br>

![image](https://github.com/user-attachments/assets/a9e18aec-630b-49fa-a609-976fda67f133)

---
### Internet Gateway

![image](https://github.com/user-attachments/assets/1b096fd6-01ca-43e4-a0b5-7b600419c95a)

> The Internet Gateway is used to enable internet for subnets. However, just creating it does not guarantee this access, you need to create a routing table

---
#### Atach to VPC

![image](https://github.com/user-attachments/assets/bbe023b0-9f95-4968-9871-06a17caaff5a)

---
### DNS Hostnames 

![image](https://github.com/user-attachments/assets/c0b2f2c0-b0db-4e48-8d0b-8944ec0dce7b)

---

![image](https://github.com/user-attachments/assets/b5cc0081-367f-4df6-98ab-df9336bdc648)

---

### Route Tables
![image](https://github.com/user-attachments/assets/7c39635d-1509-4df4-9ea7-a2cfe0f8fe0d)

---

![image](https://github.com/user-attachments/assets/4aa221fd-2b89-4ac8-8cf6-228af04851cc)

---

![image](https://github.com/user-attachments/assets/b8ca0692-e522-47b0-9dee-0408b6e6fba9)


----

![image](https://github.com/user-attachments/assets/3b0165d9-d818-422a-85ab-e89fc3718211)

</br>

> From now on the VPC has internet access

> From now on the VPC has access to the internet and consequently the subnets of that VPC also


---

### Security Groups
</br>

> Security Groups are associated with the resources of that subnet/vpc

</br>

![image](https://github.com/user-attachments/assets/88bc62ea-f26d-47eb-8380-515fba0d9a4e)


---

![image](https://github.com/user-attachments/assets/bbab2680-797c-42b2-9ea7-97ce0fe0176b)

----

</br>

- All Security Grup belongs to a single VPC
- Security Grup cannot be used in another VPC (not even in the same region).
- A VPC can have multiple Security Groups

</br>

> Each resource can use more than one Security Group.For example, an EC2 instance may have up to 5 SGs associated at the same time. The rules of all SGs apply together (are combined).


</br>
</br>


![image](https://github.com/user-attachments/assets/8ef988ca-ab45-4f75-a2b5-f071f326cbe4)

----

- Inbound Rules: Tells which rules are going to be for those who are trying to access a certain resource in a security group
- Outbound Rules: Tells the rules that this feature has to have when trying to access something out
  
</br>

![image](https://github.com/user-attachments/assets/e128501e-9378-4182-adae-5743a95324a0)


----


> In this image, in Inbound Rules, when the type is MySQL, only my IP can access the services that are within that security group

</br>

![image](https://github.com/user-attachments/assets/065c0be7-95df-4d4f-9a15-75342cb4c2d2)

---

> In another caso, only my IP can access the services


</br>

#### Case access for Security Group
</br>

> Let’s say I want multiple virtual machines to have access to MySQL instance. How do I do since all machines have a different IP?
</br>


Nesse caso eu crio uma nova regra de entrada onde ao invés de eu colocar a origem com um IP específico, eu coloco todo o grupo de segurança da API

</br>


![image](https://github.com/user-attachments/assets/910b4037-b98a-4eaa-bab5-64a1396cf749)




## References

https://www.youtube.com/watch?v=7_NNlnH7sAg

https://www.youtube.com/watch?v=WMsADIgy4ms

