# Hosting my personal Domain on AWS EC2 using Nginx and Cloudflare 

## Project Overview

In this project, the goal was to buy a domain, deploy Nginx on an EC2 instance, and make the page load over my domain.

**Live website link:** http://amr-mohamad.co.uk *(The EC2 instance will only be kept running when required and may be shut down during periods of inactivity to minimize cloud expenditure)* 

<br>

<img width="1920" height="967" alt="image" src="https://github.com/user-attachments/assets/cbe46559-3231-471b-a351-37400cc29c6b" />

## Technologies used 

- **Amazon Web Services (AWS):** EC2 instance
- **Ubuntu:** Operating system running on the EC2 instance
- **Nginx:** Web server used to host the site
- **Cloudflaire:** Domain management and DNS configuration
- **HTML/CSS:** Website customization


## Architecture

<img width="920" height="331" alt="image" src="https://github.com/user-attachments/assets/b25785f4-5789-4d40-aaa5-821de9b92893" />

## Steps Taken

Below are the steps I followed to complete this project.

## Step 1: Purchasing a Domain on Cloudflare 
- I navigated to the Cloudflare site to purchase a domain name
- I searched for the domain name: amr-mohamad.co.uk and purchased it

<img width="1920" height="702" alt="image" src="https://github.com/user-attachments/assets/b4ca1381-6865-4a08-8e7d-bcc317cde796" />

## Step 2: Launch an EC2 instance 
- On the AWS site I went to EC2 and clciked Launch Instance
- I gave my instance a name
- I choose Ubuntu as the OS image

<img width="1074" height="680" alt="image" src="https://github.com/user-attachments/assets/90eb140c-57b3-4a55-8f50-5bf87cde3bf1" />

- I selected t3.micro instance type

<img width="1073" height="203" alt="image" src="https://github.com/user-attachments/assets/31c90dd0-e7c0-4b90-b0e4-f844e842eb0c" />

- Then I created a new key pair (.pem, RSA)  

<img width="599" height="540" alt="image" src="https://github.com/user-attachments/assets/2e0feb26-8225-4df5-9407-da5a64dfc8b1" />

- After creating a new key pair I configured the security group:
  - Allow SSH => My IP
  - Allow HTTP
 
<img width="1073" height="590" alt="image" src="https://github.com/user-attachments/assets/6c2c2315-dca9-496a-a956-e4039231c221" />

Then I launched the instance. 

## Step 3: SSH into EC2 instance
- I selected my instance and clicked **Connect**
- I then opened a terminal and navigated to the directy with my **.pem** file 
- Next I secured the key with the chmod command:

    `chmod 400 <name_of_pem_file>.pem`

- I then connected via SSH:

    `ssh -i <name_of_pem_file>.pem ubuntu@ec2<ec2_public_dns>`
  
