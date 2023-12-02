# Devops Tooling Website Solution

Embark on a journey to build a comprehensive DevOps tooling website solution in this project. Explore the integration of various tools and technologies to create a unified platform that enhances collaboration, automation, and efficiency for software development and operations teams

## Prerequisites

- Cloud Service Providers; AWS,Azure,GCP,etc.
- Launch a Linux instance on RedHat.
- Priot knowledge on how to SSH into virtual host.

### Implementing a business website using NFS for the backend file storage

1. Spin up a new EC2 instance with RHEL Linux 8 Operating System.
  
3. Configure LVM on the Server.

4. Install NFS server, configure it to start on reboot and make sure it is u and running

```
sudo yum -y update
sudo yum install nfs-utils -y
sudo systemctl start nfs-server.service
sudo systemctl enable nfs-server.service
sudo systemctl status nfs-server.service
```


   <img width="1063" alt="Screenshot 2023-12-02 at 3 39 01 PM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/214f8a47-e5da-48d3-8568-1a5e919f23f3">


5.  Export the mounts for webservers' to connect as clients. For simplicity, you will install your all three Web Servers inside the same subnet, but in production set up you would probably want to separate each tier inside its own subnet for higher level of security.
To check your

<img width="1208" alt="Screenshot 2023-12-02 at 3 41 01 PM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/05593828-0bf0-4877-8591-09658bf65066">

 
```
sudo chown -R nobody: /mnt/apps
sudo chown -R nobody: /mnt/logs
sudo chown -R nobody: /mnt/opt

sudo chmod -R 777 /mnt/apps
sudo chmod -R 777 /mnt/logs
sudo chmod -R 777 /mnt/opt

sudo systemctl restart nfs-server.service
```














