# Hosting a Website on Apache Server

This document explains how to provision an AWS EC2 instance running Ubuntu, installing Apache2, and deploying a simple HTML page.

## Table of Contents

- [Provisioning the EC2 Instance](#provisioning-the-ec2-instance)
- [SSH into the EC2 Instance](#ssh-into-the-ec2-instance)
- [Installing Apache2 Web Server](#installing-apache2-web-server)
- [Deploying the Simple HTML Page](#deploying-the-simple-html-page)

## Provisioning the EC2 Instance

1. **Login to AWS Console**:  
   Visit [AWS](https://aws.amazon.com/) and log in

2. **Launch EC2 Instance**:
   - Search for **EC2** on the AWS dashboard → click on **Instances** → click on **Launch Instance**
   - Input the name for the server (eg. Altschool-Exams-Server)
   - Select **Ubuntu Server** as the AMI (e.g., Ubuntu 20.04 LTS)
   - Choose **t2.micro** for the instance type (This is for the Free Tier)

3. **Key Pair**:
   - Create a new **key pair** and download the `.pem` file to your local device.

4. **Security Group Configuration**:
   - Set up a security group to allow HTTP (port 80) and SSH (port 22):
     - Type: **HTTP**, Port: **80**, Source: **Anywhere (0.0.0.0/0)**.
     - Type: **SSH**, Port: **22**, Source: **Anywhere (0.0.0.0/0)**.
       
5. **Launch Instance**:  
   Click **Launch Instance**.


## SSH into the EC2 Server

1. **Click connect**
   - Click on **connect** at the top right corner
   - Connect into server using **EC2 Instance Connect**
  

## Installing Apache2 Web Server

1. **Update System Packages** : This is to ensure the server has up to date system packages
```
sudo apt update
```

2. **Install apache2** : This is the webserver the server will run on
```
sudo apt install apache2 -y
```

3. **Ensure Apache2 is running**
```
sudo systemctl start apache2
```

4. **Enable Apache2 is running on boot**
```
sudo systemctl enable apache2
```


## Deploying the simple HTML page

1. **Navigate to Apache's default web directory**
```
cd /var/www/html
```

2. **Create an index.html file**
```
sudo nano index.html
```

3. **Add the script into the index.html file**
   
[View the script](./index.html)

4. **Confirm your website is live by copying the and pasting your EC2 public IP on your browser**
   
[Here is a screenshot of what your website will look like](./Website-running-with-IP.png)


# Bonus
This further goes to showcase how a free domain was purchased and configured with an SSL certificate

## Obtaining a Free Domain

### 1. Create an Account on Afraid.org
1. Visit [FreeDNS Sign-Up Page](https://freedns.afraid.org/signup/).
2. Fill in the required details (username, password, email) and fill in the CAPTCHA
3. Submit the form to create your account.
4. Activate your account from your email

### 2. Search for a Free Subdomain
1. From the dashboard, click on **Subdomains**
2. Click the **Add Subdomain** link 
3. **Type**: Select the record type (`A`)
4. **Subdomain**: Enter the desired subdomain name (e.g., `anneusang.mooo.com`)
5. **Destination**: Enter your server's public IP address (e.g., AWS EC2)
6. Click **Save** to complete the process

### 3. Test the Subdomain
1. Open a web browser and navigate to your subdomain (e.g., `http://anneusang.mooo.com`)
[Here is a screenshot of what my website looks like](./Website-running-on-http-domain-name.png)


## Configuring SSL with Let’s Encrypt

To do this, go back into your EC2 server and run the following scripts

1. Install the Let's Encrypt client:
```
sudo apt install certbot
```

2. Run the certification process:
```
sudo certbot --apache
```

3. Create a new Apache configuration file for HTTPS:
```
sudo nano /etc/apache2/sites-available/default-ssl.conf
```

4. Edit the file and add the following configuration:
```
<VirtualHost *:443>
  ServerName your_domain_name
  DocumentRoot /var/www/html

  SSLEngine on
  SSLCertificateFile /etc/letsencrypt/live/your_domain_name/cert.pem
  SSLCertificateKeyFile /etc/letsencrypt/live/your_domain_name/privkey.pem
</VirtualHost>
```
- Replace "your_domain_name" with your actual domain name.
- Save and close the file (ctrl + o, enter, ctrl + x)

5. Restart Apache to apply the changes
```
sudo service apache2 restart
```
6. Test your configuration using the domain name, now with https (eg., https://anneusang.mooo.com)
[Here is a screenshot of my website running on HTTPS](./Website-running-on-HTTPS.png)




