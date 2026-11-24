# Hosting a personal Domain on AWS EC2 with Nginx and Cloudflare 

## Project Summary 

Successfully deployed and hosted my personal website on an AWS EC2 instance using Nginx, connecting it to a custom domain managed through Cloudflare. The project involved setting up and configuring a cloud-based Ubuntu server, establishing remote access through SSH, configuring AWS security groups, and directing the custom domain to the EC2 instance using Cloudflare DNS.

The project provided hands-on experience in deploying and managing a website within a cloud environment, developing my understanding of AWS infrastructure, Linux server administration, web server configuration and DNS management.


## Technologies used 

- **Amazon Web Services (AWS):** EC2 instance
- **Ubuntu:** Operating system running on the EC2 instance
- **Nginx:** Web server used to host the site
- **Cloudflaire:** Domain management and DNS configuration
- **HTML/CSS:** Website customization


## Architecture

<img width="920" height="331" alt="image" src="https://github.com/user-attachments/assets/b25785f4-5789-4d40-aaa5-821de9b92893" />


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

<img width="292" height="246" alt="image" src="https://github.com/user-attachments/assets/7391dc13-ed55-4a1e-b1de-0f1bf0235656" />

- I then opened a terminal and navigated to the directy with my **.pem** file 
- Next I secured the key with the chmod command:

    `chmod 400 <name_of_pem_file>.pem`

- I then connected via SSH:

    `ssh -i <name_of_pem_file>.pem ubuntu@<MY_EC2_PUBLIC_IP>`

## Step 4: Linking my domain (Cloudflare => EC2)
- On the Cloudflare site I navigated to DNS/Records

<img width="261" height="915" alt="image" src="https://github.com/user-attachments/assets/2e8084f9-3d7a-4c40-84aa-cba7fca6d0b5" />

- I then clicked "Add record" and created an A record.
- I used "@" for root domain & optionally a second record with "www"
- IPv4 address: <EC2_PUBLIC_IP>
- Proxy Status: Proxied (Orange cloud)
- I saved the record and waited for the DNS to progogate.

<img width="770" height="439" alt="image" src="https://github.com/user-attachments/assets/36be188d-936c-4fee-a87f-f7749fb26a00" />

## Step 5: Installing and Configuring Nginx 
- After connecting to the server, I updated the Ubuntu package list and installed Nginx
  
  `sudo apt update`

  `sudo apt install nginx -y` (The "-y" flag simply automatically answers yes to the confirmation prompt)
  
- Enabling and starting Nginx
  
  `sudo systemctl enable nginx`

  `sudo systemctl start nginx`

At this stage, when I visited my domain, the default Nginx page appeared: 

<img width="1922" height="966" alt="image" src="https://github.com/user-attachments/assets/494c9382-6a0f-4606-9adc-aeafd106c182" />

## Step 6: Testing the domain connectivity
- After configuring the DNS, I tested whether my domain resolved to the EC2 instance.

- I used the nslookup command:
  `nslookup amr-mohamad.co.uk`

- I also tested the HTTP response with the curl command:
  `curl -I http://amr-mohamad.co.uk`

The domain successfully returned an HTTP 200 OK response, confirming that Nginx was serving requests through my custom domain.

<img width="1136" height="305" alt="image" src="https://github.com/user-attachments/assets/ca6ee56e-d20b-402b-8aa1-ff114252b0e9" />

  
## Step 7: Customizating my Nginx webpage
Once the domain was working, I customized the default Nginx page. 

I edited the website's HTML file: 
  `sudo vim /var/www/html/index.html`

I replaced the default Nginx welcome page with my own customized version. 

After saving my changes, I tested the Nginx configuration:
  `sudo nginx -t`

I then reloaded the page: 
  `sudo systemctl reload nginx`

After making these changed I reloaded my domain on the web and saw my customized landing page.  

<img width="1920" height="968" alt="image" src="https://github.com/user-attachments/assets/a7b993f5-2515-4833-93f2-774297cf5c3a" />

## Key Takeaways

Through completing this project, I gained practical experience and developed the following skills:

- AWS EC2: Provisioning, launching and managing a cloud-based Linux server.
- Linux Administration: Connecting to and managing a remote Ubuntu server using SSH.
- Network Security: Configuring AWS EC2 security groups to manage network access.
- Web Server Management: Installing, configuring and managing Nginx to host a website.
- DNS Management: Creating and configuring DNS records through Cloudflare.
- Domain Configuration: Connecting a custom domain to an AWS EC2 public IP address.
- Web Development: Customising and publishing a personal website using HTML and CSS.
- Cloud Deployment: Understanding the process of deploying and hosting a publicly accessible website using cloud infrastructure.
  
<br>

**Live website link:** http://amr-mohamad.co.uk *(The EC2 instance will only be kept running when required and may be shut down during periods of inactivity to minimize cloud expenditure)* 













