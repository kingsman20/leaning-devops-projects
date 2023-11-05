# LAMP STACK IMPLEMENTATION

## Linux Apache Mysql Php; where Linux is the operating system, Apache is the web server,Mysql is the database, and Php is the programming language.

## Prerequisites 

- Cloud Service Providers; AWS,Azure,GCP,etc.
- Launch a Linux instance on ubuntu(prefarbly).
- Priot knowledge on how to SSH into virtual host.

## Connection to AWS EC2 Instance
Using ssh client `ssh -i "my-kem.pem" ubuntu@ec2-13-49-241-232.eu-north-1.compute.amazonaws.com`

<img width="1134" alt="Screenshot 2023-11-05 at 5 52 59 PM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/d9ee08ec-8a72-447e-a230-e0b57f317378">

## Installing Apache server

update a list of packages in the package manager
`sudo apt update`

<img width="1008" alt="Screenshot 2023-11-05 at 5 58 48 PM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/ed6fae49-f79c-4ce1-bd0c-12872cc60393">


run apache2 package installation

`sudo apt install apache2` 
`sudo systemctl status apache2` to verify installation

<img width="1104" alt="Screenshot 2023-11-05 at 6 01 48 PM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/14c753b7-9d1b-42f3-8f67-171a36f614a6">

`curl http://localhost:80`
or
`curl http://127.0.0.1:80`

`curl http://<Public-IP-Address>:80`

<img width="1120" alt="Screenshot 2023-11-05 at 6 07 10 PM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/94731f7c-6088-4407-8b11-cf559f4942f5">


## Installing MySQL

`sudo apt install mysql-server -y`

<img width="1107" alt="Screenshot 2023-11-05 at 6 14 42 PM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/6dc3f26d-a431-4ab8-8e67-5fe49af3924f">

`systemctl status mysql`

<img width="1111" alt="Screenshot 2023-11-05 at 6 17 02 PM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/94443beb-c613-4637-bb18-907bca1183c7">

`sudo mysql -p`

<img width="1039" alt="Screenshot 2023-11-05 at 6 26 48 PM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/a514e688-9628-410b-9a31-1190580d14ad">


## Installing PHP

`sudo apt install php`

<img width="870" alt="Screenshot 2023-11-05 at 6 30 36 PM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/cdaf3811-f9d0-4fee-983b-3bdbe9075118">












