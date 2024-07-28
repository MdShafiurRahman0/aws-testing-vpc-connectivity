### AWS Testing VPC Connectivity


Get ready to:

⬆️ Connect to your Public Server from the AWS Management Console.

🤝 Test connectivity between your EC2 instances.

🛜 Test VPC connectivity with the internet.


High Level Arcitecture Diagram

![image](https://github.com/user-attachments/assets/a97b647d-050f-451b-9218-6a773a2d3b67)


### Step 1:  Set up your VPC basics:

![image](https://github.com/user-attachments/assets/5f67e8c2-0b4e-4774-a247-a92f8d43b145)


1. Head to your VPC console.
2. From the left hand navigation bar, select Your VPCs.
3. Select Create VPC.
4. We previously stuck to creating a VPC only, but this time let's select VPC and more.
5. Under Name tag auto-generation, enter any name


![image](https://github.com/user-attachments/assets/73ab9383-7c36-4f9e-a1c7-757d7f2cfd2b)

# Next, for the NAT gateways ($) option, make sure you've selected None. As the dollar sign suggests, NAT gateways cost money!


![image](https://github.com/user-attachments/assets/05099395-8a66-4bc8-81bc-032251a5f7fd)


![image](https://github.com/user-attachments/assets/3ca49e1f-1f52-4217-ab5d-471773434614)


# Select Create VPC.


![image](https://github.com/user-attachments/assets/c3950403-12de-4ad7-9910-0fe028e59228)


![2024-07-27_12h48_24](https://github.com/user-attachments/assets/15316f1c-25ad-4c42-a3ed-19747eec9ac4)

![2024-07-27_13h47_37](https://github.com/user-attachments/assets/0c46f96d-cb7c-40a2-a58f-195c8af78b30)



### Step 2: Create Network ACLs

1. Select Network ACLs from the left hand navigation panel.
2. Select Create network ACL on the top right.
3. For the name, enter 
3. Select NextWork VPC.
4. Select Create network ACL.
5. Select the checkbox next to 
6. Switch tabs to Subnet associations.
7. Select Edit subnet associations.
8. Select your private subnet.
9. Select Save changes.

To tidy up your network ACLs' naming conventions, let's also rename your VPC's default NACL to 


Observe the Inbound rules and Outbound rules tabs for your private network ACL.


All inbound and outbound traffic is denied for your Private NACL!

![image](https://github.com/user-attachments/assets/d4d32ccb-4a83-471b-9387-f3a0c096367d)




### Step 3:  Security Groups

1. Select Security groups from the left hand navigation panel.
2. Yay default security groups have already been set up for us! Their names are launch-wizard-1 and launch-wizard-2.
3. Select launch-wizard-1 and observe its inbound rules.


![image](https://github.com/user-attachments/assets/12f553f1-1f8b-4fa5-a4f5-65530f85b021)

# Inbound rules allow SSH traffic!


# Hmmm launch-wizard-1 doesn't quite have the same inbound rules as the ones we used to set up ourselves.

1. Let's create new security groups instead of using the default ones.
2. Choose Create security group.
3. Security group name:  
4. Description: 
5. VPC: NextWork VPC
6. Under the Inbound rules panel, choose Add rule.
7.Type: HTTP
8. Source: ANYWHERE IPV4

At the bottom of the screen, choose Create security group



### Launch a new EC2 instance in NextWork Public Subnet


![image](https://github.com/user-attachments/assets/6d11b8da-bdf3-4c0a-80b2-82b6b763a2b6)


1. Select Instances at the left hand navigation bar.
2. Select Launch instances.
3. Since your first EC2 instance will be launched in the public subnet, let's name it 
4. For the Amazon Machine Image, select Amazon Linux 2023 AMI.
5. For the Instance type, select t2.micro.


![image](https://github.com/user-attachments/assets/5b90bc05-3b0f-4f39-9ad1-69eccea6a9ca)



![2024-07-27_14h07_11](https://github.com/user-attachments/assets/0f4383ad-6d34-432e-942d-5614e33ffb0a)


![2024-07-27_14h13_37](https://github.com/user-attachments/assets/10facc82-793a-474b-9172-4fe8e33eb7cc)



![image](https://github.com/user-attachments/assets/db43f465-5526-4b96-bff0-b734430203f3)




###  NextWork Public Server's Networking details.


![image](https://github.com/user-attachments/assets/e4c72c5d-7583-4e13-bb3e-7a200901724c)


### Launch a new EC2 instance in NextWork Private Subnet


![image](https://github.com/user-attachments/assets/fe89f590-f0fa-447a-b95a-3c089f9ce1c1)


1. Select Launch instances again.
2. Name: Private Server 
3. Amazon Machine Image (AMI): Amazon Linux 2023 AMI
4. Instance type: t2.micro
5. Key pair: NextWork key pair
6. At the Network settings panel, select Edit.
7. Network: NextWork VPC
8. Subnet: NextWork Private Subnet

# Select Create security group.
For Security group name, let's use private server




# Edit Inbound Rules 


![image](https://github.com/user-attachments/assets/018c4b5e-1c35-422a-85da-2ff0bfc6a703)


![image](https://github.com/user-attachments/assets/95611d94-4291-46c4-901a-61ebe69014b6)




### Step 4 : Connect to NextWork Public Server



![image](https://github.com/user-attachments/assets/0756015d-1467-472d-b555-b391d4d4fd36)

1. Still in your EC2 console, select Instances from the left hand navigation panel.
2. Select the checkbox next to NextWork Public Server.
3. Select Connect.



![image](https://github.com/user-attachments/assets/f0938946-b3a9-44cb-ba10-f9b248a2c357)


# Here's how EC2 Instance Connect works:


![image](https://github.com/user-attachments/assets/999bf261-1306-4ec8-9464-039f0c620d18)


# Select Connect.


![image](https://github.com/user-attachments/assets/014cdab4-d1cd-40ab-8fd7-2720435e2733)


# let's take a look! Investigate the Route table and Network ACL tabs - what do you see?


![image](https://github.com/user-attachments/assets/6217fdfe-cd9f-4c17-bb59-8f3982768608)


1. In the Inbound rules tab, select Edit inbound rules.
2. Select Add rule.
3. For your new rule, configure the Type as SSH.
4. Then, under Source type, select Anywhere-IPv4.
 
![image](https://github.com/user-attachments/assets/6d6f6e0e-f214-4871-a880-9f139e79a707)



# Phew! Success.

![image](https://github.com/user-attachments/assets/d913ef36-7813-4053-baca-8a46ba52a6a8)

