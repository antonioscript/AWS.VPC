# AWS.VPC  
Theoretical repository on how VPC works in AWS

# Introduction to AWS VPC
</br>

![image](https://github.com/user-attachments/assets/47a33abc-28cc-408a-9236-713d81d1d8e0)

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

https://cidr.xyz/
---

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

### Simple Analogies

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

</br>

> An example of a Public and Private Subnet is a website. Where a site it needs to be public, for people to access it, but the database that links the site information does not need to be public, has to be private.

</br>

![image](https://github.com/user-attachments/assets/7607b379-8f81-4766-90a8-18ac178431dc)

![image](https://github.com/user-attachments/assets/62f749ae-bba7-46c6-a000-0079847dd9d0)

## References

https://www.youtube.com/watch?v=7_NNlnH7sAg



