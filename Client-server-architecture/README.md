# Understanding a client server architecture

Assuming that you go on your browser, and typed in there www.propitixhomes.com. It means that your browser is considered the client, 
Essentially, it is sending request to the remote server, and in turn, would be expecting some kind of response from the remote server.

using curl command
`curl -Iv www.propitixhomes.com`

<img width="1028" alt="Screenshot 2023-11-23 at 7 02 39 PM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/e7200216-d837-4aaf-9961-9361792f59b7">


# Implement a Client Server Architecture using MySQL Database Management System(DBMS)

TASK - Implement a Client Server Architecture using MySQL Database Management System(DBMS)

To demonstrate a basic client-server using MySQL RDBMS, we follow the below instructions 

1. Create and configure two Linux-based virtual servers(EC2 instances in AWS)

Server A name - `mysql-server`

Server B name - `mysql-client`

<img width="1276" alt="Screenshot 2023-11-23 at 7 16 09 PM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/79c82e1a-852f-44ce-938a-17510e3ffbb0">


`sudo hostname mysql-server` & `sudo hostname mysql-client` then `bash`

2. On `mysql-server` Linux Server install MySQL Server software

`sudo apt install mysql-server`

<img width="1184" alt="Screenshot 2023-11-23 at 7 27 36 PM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/37b946a7-c8dc-456a-9c9b-052c8e9ef7a0">


3. On `mysql-client` Linux Server install MySQL Client software.

`sudo apt install mysql-client`

<img width="1189" alt="Screenshot 2023-11-23 at 7 31 58 PM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/b97f4816-effc-4836-b088-e8340ccf4bb6">


4. By default, both of your EC2 virtual servers are located in the same local virtual network, so they can communicate to each other using local IP addresses. Use **mysql-server's** local IP address to connect from **mysql-client**. MySQL server uses TCP port 3306 by default, so you will have to open it by creating a new entry in ‘Inbound rules’ in ‘mysql-server’ Security Groups. For extra security, do not allow all IP addresses to reach your ‘mysql-server’ – allow access only to the specific local IP address of your ‘mysql-client’.

Results:

<img width="1469" alt="Screenshot 2023-11-23 at 7 47 23 PM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/05b3d8fc-ee18-4fab-a5c9-25bcb06d38ad">

<img width="1269" alt="Screenshot 2023-11-23 at 7 47 59 PM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/4e651632-0fd7-4074-b21c-1fa498e5fa5a">



5. We configure **mysql-server** to allow connections from remote hosts.

`sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf`

Replace the following line;

`bind-address = 127.0.0.1`

with the following:

`bind-address = 0.0.0.0`

<img width="1185" alt="Screenshot 2023-11-23 at 7 51 36 PM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/4ab85921-84fe-4e03-9e0d-9302ee1b1030">


6. On mysql-server we create  a user 'kingsley' in MySQL to link with mysql-client. 

Run the command:

`sudo mysql -u root -p`

In your mysql-server ec2 instance allow the ipaddress of the mysql-client ec2 instance with port 3306 to access the mysql-server ec2 instance.

Run the command on the client server to get the public ip:

`sudo curl https://checkip.amazonaws.com`

<img width="719" alt="Screenshot 2023-11-23 at 7 56 57 PM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/2cf7cd4f-c9eb-4b17-946f-a37bb82303e8">


Create a user in MySQL with the command:

`mysql> CREATE USER 'kingsley'@'<ip_address>' IDENTIFIED BY 'password';`

<img width="821" alt="Screenshot 2023-11-23 at 7 58 44 PM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/4162b4ba-3042-4210-82a7-ae4fce3140b2">

`mysql> GRANT ALL PRIVILEGES ON * . * TO 'kingcjay'@'<ip_address>';`

<img width="941" alt="Screenshot 2023-11-23 at 8 00 11 PM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/8c2d62a6-3717-40a3-a98b-df1d622ecb87">


7. To connect to the **mysql-server**, in your **mysql-client** enter the following code.

`mysql -u kingsley -h <ip_address> -p`

Note: The format is 

mysql -u <user> -h <ipaddress-of-the-server> -p (the server here is the mysql-server)

show database:

<img width="1059" alt="Screenshot 2023-11-23 at 8 21 10 PM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/3ec07985-a569-4f43-bfad-d076e2813ee9">
