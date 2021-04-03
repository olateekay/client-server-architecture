Create and configure two Linux-based virtual servers (EC2 instances in AWS).
Server A name - `DBserver`
Server B name - `Client`

On `Dbserver` Linux Server install MySQL Server software

`sudo apt update`

![alt text](image1.jpg)

Install mysql-server

`sudo apt install mysql-server -y`

![alt text](image2.jpg)

Enable the mysql service

`sudo systemctl enable mysql`

![alt text](image3.jpg)


On `Client` Linux Server install MySQL Client software

`sudo apt update`

![alt text](image4.jpg)

Install mysql-client

`sudo apt install mysql-client -y`

By default, both of your EC2 virtual servers are located in the same local virtual network, so they can communicate to each other using local IP addresses. Use mysql server's local IP address to connect from Client. MySQL server uses TCP port 3306 by default, so you will have to open it by creating a new entry in ‘Inbound rules’ in ‘DbServer’ Security Groups. For extra security, do not allow all IP addresses to reach your ‘DbServer’ - allow access only to the specific local IP address of your ‘Client’.

![alt text](image5.jpg)

Ensure  that mysql installation on `DbServer` is secure by running this;

`sudo mysql_secure_installation`

![alt text](image6.jpg)

![alt text](image7.jpg)

start mysql 

`sudo mysql`

![alt text](image8.jpg)

Create user
![alt text](image9.jpg)

Create database
![alt text](image10.jpg)

Grant permissions
![alt text](image11.jpg)

Flush privileges
![alt text](image12.jpg)

You might need to configure MySQL server to allow connections from remote hosts.
Run this

`sudo vi /etc/mysql/mysql.conf.d/mysqld.cnf `

Replace ‘127.0.0.1’ to ‘0.0.0.0’ like this:

![alt text](image13.jpg)

Restart mysql 

`sudo systemctl restart mysql`

![alt text](image14.jpg)