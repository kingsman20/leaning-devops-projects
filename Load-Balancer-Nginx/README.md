# Implementing LoadBalancers With Nginx

## Introduction to Load Balancing and Nginx

Load balancing spreads incoming network traffic across a group of backend servers to ensure satisfactory speed and optimized functioning. The group of backend servers is commonly called a server farm or server pool. This is done so that no one computer gets overloaded with too much work

Nginx is a versatile software, it can act as a webserver, reverse proxy and a load balancer etc. All that is needed is to configure it properly to server your use case.

## Setting Up a Basic Load Balancer

We are going to be provisioning two two EC2 instances running ubuntu and install apache webserver in them. We will open port 8000 to allow traffic from anywhere, and finally update default page of the webservers to display their public IP addresses.

Next we will provision another EC2 instance running ubuntu 22.04.3 and install Nginx. We will now configure it to act as a load balancer distributing traffic across the webservers.

**Step 1**: Provisioning EC2 instances 

Launching two instances providing a unique name for each of the webservers. 

<img width="1266" alt="Screenshot 2023-11-25 at 7 52 59 AM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/5060798d-c901-41ae-b837-6033b1402184">


**Step 2**: 
We will be running our webservers on port 8000 while load balancer runs on port 80. We need to open port 8000 to allow traffic from anywhere. To do this wee need to add rule to the security groups of each of our webservers.

<img width="1254" alt="Screenshot 2023-11-25 at 7 56 56 AM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/89c1997c-3f11-41d2-9d3f-4175ba652ddf">

<img width="1227" alt="Screenshot 2023-11-25 at 7 57 32 AM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/258d7ab6-3ee8-4096-ab4f-cf4dd684fb7e">


**Step 3**: Install Apache Webserver

After provisioning both servers and have opened the necessary ports, we now install apache software on both servers. We connect both servers through ssh and run commands on the terminal of our webservers.

Open a terminal on your loacl machine, cd into the folder where the keypair of your webserver is located and paste the ssh command. The folder in this case is Downloads 

<img width="1034" alt="Screenshot 2023-11-25 at 7 59 36 AM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/4c7f9180-efaf-4eae-8d82-4300e720b7b5">


- Next install apache with the command below 

`sudo apt update`

`sudo apt install apache2 -y`

<img width="1027" alt="Screenshot 2023-11-25 at 8 00 48 AM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/9f6eb30e-02f3-4986-a859-242830efa5bb">


Verify that apache is running 

`sudo systemctl status apache2`

<img width="1056" alt="Screenshot 2023-11-25 at 8 01 16 AM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/6c7e8098-e74c-4356-8d48-6abf44a0ecf7">


**Step 4**: Configure Apache to server a page showing its public IP address:

We will start by configuring Apache webserver to serve content on port 8000 instead of its default port 80. Then we will create a new **index.html**
file. The file will contain code to display the public IP of the EC2 instance. We will then override apache webserver's default html file with our new file. 

- Configure Apache to serve content on port 8000:

1. Using the text editor nano open file /etc/apache2/ports.conf/

`sudo vi /etc/apache2/ports.conf` 

2. Add a new listen directive for port 8000:

<img width="1023" alt="Screenshot 2023-11-25 at 8 04 17 AM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/8ada0ba3-ada6-4600-a9d4-4edd63a48469">


`cat /etc/apache2/ports.conf`

<img width="940" alt="Screenshot 2023-11-25 at 8 05 32 AM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/4a6728e8-8a37-493c-927e-d42405198c6c">


3. Open the file /etc/apache2/sites-available/000-default.conf and change port 80 on the virtualhost to 8000:

`sudo vi /etc/apache2/sites-availabe/000-default.conf`

`cat /etc/apache2/sites-availabe/000-default.conf`

<img width="937" alt="Screenshot 2023-11-25 at 8 09 32 AM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/56ec6894-ffbd-4893-b0fd-538e2809be87">


4. Restart apache to load the new configuration:

`sudo systemctl restart apache2`


- Creating a new html file:

1. Open index.html file 

`sudo vi index.html`

2. Get the public IP of the instances on the EC2 instances on AWS console and the placeholder text for IP address.
```php
        <!DOCTYPE html>
        <html>
        <head>
            <title>My EC2 Instance</title>
        </head>
        <body>
            <h1>Welcome to my EC2 instance</h1>
            <p>Public IP: YOUR_PUBLIC_IP</p>
        </body>
        </html>
```

`cat index.html`

<img width="696" alt="Screenshot 2023-11-25 at 8 15 38 AM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/55ca3f68-f5f1-4a9d-86b8-1b6002a3e105">


3. Change file ownership of the index.html file with the command below:

`sudo chown www-data:www-data ./index.html`


- Overriding the default html file of Apache Webserver:

1. Replace the default html file with our new html file with the command:

`sudo cp -f ./index.html /var/www/html/index.html`

<img width="805" alt="Screenshot 2023-11-25 at 8 16 39 AM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/a56f00b6-0420-4654-b886-9aad0a661373">


2. Restart webserver to load the new configuration with the command below:

`sudo systemctl restart apache2`


We have the pages of our two Apache servers below 

<img width="1511" alt="Screenshot 2023-11-25 at 8 18 20 AM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/9c873c6f-72ac-4eb3-830e-31efb47afa1f">


**Step 5**: Configuring Nginx as a load balancer

- Provision a new EC2 instance running ubuntu 22.04.3. We open port 80 and accept traffic from anywhere like step 1 and 2 above.

- SSH in to the instance like step 3.

- Install nginx 

`sudo apt update`

`sudo apt install nginx -y`

<img width="1071" alt="Screenshot 2023-11-25 at 8 25 14 AM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/e2306924-098e-45ea-a43e-ced3a6d243e8">


- Verify that nginx is installed with the command:

`sudo systemctl status nginx`

<img width="1086" alt="Screenshot 2023-11-25 at 8 25 50 AM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/7b91f647-718f-4325-937a-d3f6b46f20da">


- Open nginx configuration file by running:

`sudo vi /etc/nginx/conf.d/loadbalancer.conf`

- Paste and edit the configuration file below making sure we provide the necessary information like the server IP address;

```php
        
        upstream backend_servers {

            # your are to replace the public IP and Port to that of your webservers
            server 127.0.0.1:8000; # public IP and port for webserser 1
            server 127.0.0.1:8000; # public IP and port for webserver 2

        }

        server {
            listen 80;
            server_name <your load balancer's public IP addres>; # provide your load balancers public IP address

            location / {
                proxy_pass http://backend_servers;
                proxy_set_header Host $host;
                proxy_set_header X-Real-IP $remote_addr;
                proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            }
        }
```

`cat /etc/nginx/conf.d/loadbalancer.conf`

<img width="1059" alt="Screenshot 2023-11-25 at 8 29 51 AM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/45a2be09-a599-474c-9b84-b45efe7581de">


- Test your configuration file withe the command:

`sudo nginx -t`

<img width="767" alt="Screenshot 2023-11-25 at 8 30 38 AM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/098936b6-e699-4b90-acba-cfcf3171a6a9">


- If there are no errors, restart Nginx to load the new configuration with the command below:

`sudo systemctl restart nginx`

- Paste the public IP of the Nginx loadbalancer, you should see the same pages served by the webservers titling on the loadbalancer.

<img width="1511" alt="Screenshot 2023-11-25 at 8 31 32 AM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/20e83497-6269-4a23-a41d-c00320c6eb9d">
