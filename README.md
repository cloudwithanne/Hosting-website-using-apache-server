# Hosting a Website on Apache Server

This document explains how to provision an AWS EC2 instance running Ubuntu, installing Apache2, deploy a simple HTML page.

## Table of Contents

- [Provisioning the EC2 Instance](#provisioning-the-ec2-instance)
- [SSH into the EC2 Instance](#ssh-into-the-ec2-instance)
- [Installing Apache2 Web Server](#installing-apache2-web-server)
- [Deploying a Simple HTML Page](#deploying-a-simple-html-page)

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

1. **Update System Packages**
```
sudo apt update -y
```
