# Ansible Nginx Static Website Deployment
## Project Overview
- Automates installation and configuration of Nginx using Ansible roles,
  deploys a custom Nginx server block, and hosts a static website on an EC2 instance.
  ## - Tech Stack
  - Ansible
  - Nginx
  - Linux (Ubuntu)
  - AWS EC2
  - YAML, Jinja2

# Deploy a Static Website on AWS EC2
### I) Set up an AWS EC2 instance

  1. Login to your AWS Console
  2. Create an EC2 instance
      - Select an OS image - Ubuntu
      - Instance type - t3.micro
      - Create a new key pair & download `.pem` file
      - Create a Security Group - Allow ssh Access
      - Launch Instance

### II) Set up Passwordless Authentication to AWS EC2 Instance  ----> prerequisite for Ansible
  1. Using SSH
     ```
     ssh-copy-id -f "-o IdentityFile <PATH TO PEM FILE>" ubuntu@<INSTANCE-PUBLIC-IP>
     ```
  2. Now you can connect to your Instance without any Identity File (key)
     ```
     ssh ubuntu@<INSTANCE-PUBLIC-IP>
     ```
### III) Clone this Project
  -  ```
     git clone https://github.com/SHANKAR-REGATI/Ansible-nginx-static-site-deployment-using-Roles.git
     ```

### IV) Update the Inventory.ini file with your EC2 user and public ip
       example - [web server]
                 ubuntu@40.192.35.148

### V) Update the source location of configuration file (nginx.conf.j2) in tasks/main.yml 
### VI) Update the source location of static website (index.html) in tasks/main.yml
### VII) Execute the project
  - ```
    ansible-playbook -i inventory.ini nginx_server.yml
    ```
### Project is deployed on AWS 🎉
> NOTE - We will have to edit the **inbound rules** in the security group of our EC2, in order to allow traffic from our particular port (7000)

### Verify Deployment
  - ```
    http://<EC2_PUBLIC_IP>:Port Numbr
    ```
    example -  http://40.192.35.148:7000
                 
