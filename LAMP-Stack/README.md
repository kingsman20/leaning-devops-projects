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


```php 
VALIDATE PASSWORD PLUGIN can be used to test passwords
and improve security. It checks the strength of password
and allows the users to set only those passwords which are
secure enough. Would you like to setup VALIDATE PASSWORD plugin?

Press y|Y for Yes, any other key for No:
```
If you answer "yes", you'll be asked to select a level of passsword validation. Keep in mind of the levels of password policies below.

```php
There are three levels of password validation policy:

LOW    Length >= 8
MEDIUM Length >= 8, numeric, mixed case, and special characters
STRONG Length >= 8, numeric, mixed case, special characters and dictionary              file

Please enter 0 = LOW, 1 = MEDIUM and 2 = STRONG: 1
```
Regardless of whethr you chose to set up the **VALIDATE PASSWORD PLUGIN**, your server will next ask you to select and confirm a password for the MySQL root user. This is not to be confused with **system root**. The database root user is an administrative user with full privileges over the databse system.

Test if you're able to log in the MySQL system console by typing;

`sudo mysql -p`

<img width="1039" alt="Screenshot 2023-11-05 at 6 26 48 PM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/a514e688-9628-410b-9a31-1190580d14ad">

Notice the `-p` flag in this command, which will prompt for password used after changing the root user password.

Exit MySQL console by typing:

`mysql> exit`


## Installing PHP

`sudo apt install php`

<img width="870" alt="Screenshot 2023-11-05 at 6 30 36 PM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/cdaf3811-f9d0-4fee-983b-3bdbe9075118">


### Enable PHP on the website

In the default **DirectoryIndex** settings in the Apache, a file named `index.html` will take precednce over an `index.php`file. This is useful 
setting up maintainance pages in PHP applications by creating a temporary `index.html`file containing an informative message for visitors. Because this page will take precedence over the index.php page, it will then become the landing pafe for the application. Once maintainance is over, the `index.html` is renamed or removed from the document root bringing back the regular application page.

Finally, we will create a PHP script to test that PHP is correctly installed and configured on your server. This script confirms that Apache is able to handle and process requests for PHP files.

`sudo vim /etc/apache2/mods-enabled/dir.conf`

<img width="1277" alt="Screenshot 2023-11-17 at 2 02 39 PM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/e70eb8b5-eed0-4e75-8065-8bd6b79320c3">


Create a new file named `index.php` inside your custom web root folder.

`vim /var/www/mylamp/index.php`

Enter the following PHP code inside the file:

```php
<?php
phpinfo();
```
When you are finished, save and close the file.

After checking the relevant information about your PHP server through that page, it's best to remove the file you created as it contains sensitive information about your PHP enviroment and your Ubuntu server. Run the code:

`sudo rm /var/www/mylamp/index.php`

you can always recreate this page if you want to access the information again later.



## Creating a Virtual Host for your Website using Apache

In this project, we set up a domain called `projectlamp` 

Apache on Ubuntu 22.0.4 has one server block enabled by default that is configured to serve documents from the /var/www/html directory. We'd leave the configuration as it is and add our own directory next to the default one.

Create directory for the `projectlamp`

`sudo mkdir /var/www/projectlamp`

Next, we assign ownership of the directory with the `$USER` enviroment variable, which will reference with your current system user:

`sudo chown -R $USER:$USER /var/www/projectlamp`

Then, create and open a new configuration file in Apache's `sites-available` directory using your preferred command line editor.

`sudo vi /etc/nginx/site-available/projectlamp.conf`

<img width="1099" alt="Screenshot 2023-11-06 at 3 57 16 PM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/33cfdde4-fca1-4618-bc6d-879b176d71a1">

<img width="989" alt="Screenshot 2023-11-17 at 2 33 25 PM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/c56138f1-270b-402d-be2b-93a4dc1bfaf9">


With this VirtualHost configuration, we are telling Apache to serve `mylamp` using `/var/www/projectlamp`as its web root directory.

Now we use the `a2ensite` command to enable the new virtual host:

`sudo a2ensite projectlamp`

We also need to disable the Apache's default website for it not to overwrite your virtual host. We do that by running the `a2dissite` command:

`sudo a2dissite 000-default`

To make sure your configuration doesn't contain syntax error, run:

`sudo apachectl configtest`

![Alt text](images/a2ensite.png)

Finally, reload Apache so the changes will take effect:

`sudo systemctl reload apache2`


<img width="1409" alt="Screenshot 2023-11-17 at 2 38 29 PM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/f4e67ca1-570b-4a36-89be-91db42b0d504">



Your new website is now active but the web root `/var/www/mylamp` is empty. Create an index.html file in that location so we can test if the virtual host is working.

`sudo echo 'Hello LAMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/mylamp/index.html`


<img width="1461" alt="Screenshot 2023-11-17 at 2 39 35 PM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/8f2da4fe-792c-49d6-936a-3bb42bbbfde8">


Now go tour browser and to open your website url using IP address:

`http://<Public-IP-Address>:80`


<img width="758" alt="Screenshot 2023-11-17 at 2 41 36 PM" src="https://github.com/kingsman20/leaning-devops-projects/assets/20397262/69b3eca3-81d8-46c3-80f7-173ec80b336b">


If you see the `echo` command you wrote in the ***index.html*** file, then it means your Apache virtual host is working as expected. In the output, you'll see your server's public hostname(DNS Name) and public IP address.  

You can leave this file in place as temporary landing page for your applicationn until you setup an `index.php` file to replace it. Once you do, remember to remove or rename the `index.html`file from your document root as it would take precedence over an `index.php` file by default.








