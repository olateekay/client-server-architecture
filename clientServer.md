Create and configure two Linux-based virtual servers (EC2 instances in AWS).
Server A name - `DBserver`
Server B name - `Client`

On `Dbserver` Linux Server install MySQL Server software

`sudo apt update`

![alt text](https://github.com/olateekay/client-server-architecture/blob/main/images/image1.png)

Install mysql-server

`sudo apt install mysql-server -y`

![alt text](https://github.com/olateekay/client-server-architecture/blob/main/images/image2.png

Enable the mysql service

`sudo systemctl enable mysql`

![alt text](https://github.com/olateekay/client-server-architecture/blob/main/images/image3.png)


On `Client` Linux Server install MySQL Client software

`sudo apt update`

![alt text](https://github.com/olateekay/client-server-architecture/blob/main/images/image4.png)

Install mysql-client

`sudo apt install mysql-client -y`

By default, both of your EC2 virtual servers are located in the same local virtual network, so they can communicate to each other using local IP addresses. Use mysql server's local IP address to connect from Client. MySQL server uses TCP port 3306 by default, so you will have to open it by creating a new entry in ‘Inbound rules’ in ‘DbServer’ Security Groups. For extra security, do not allow all IP addresses to reach your ‘DbServer’ - allow access only to the specific local IP address of your ‘Client’.

![alt text](https://github.com/olateekay/client-server-architecture/blob/main/images/image5.png)

Ensure  that mysql installation on `DbServer` is secure by running this;

`sudo mysql_secure_installation`

for this use case, we will not be validating password.Select no when prompted for password validation, then set password. Select yes for  the quetions  that follows afterwards.

![alt text](https://github.com/olateekay/client-server-architecture/blob/main/images/image6.png)

![alt text](https://github.com/olateekay/client-server-architecture/blob/main/images/image7.png)

start mysql 

`sudo mysql`

![alt text](https://github.com/olateekay/client-server-architecture/blob/main/images/image8.png)

Create user
![alt text](https://github.com/olateekay/client-server-architecture/blob/main/images/image9.png)

Create database
![alt text](https://github.com/olateekay/client-server-architecture/blob/main/images/image10.png)

Grant permissions
![alt text](https://github.com/olateekay/client-server-architecture/blob/main/images/image11.png)

Flush privileges
![alt text](https://github.com/olateekay/client-server-architecture/blob/main/images/image12.png)

You might need to configure MySQL server to allow connections from remote hosts.
Run this

`sudo vi /etc/mysql/mysql.conf.d/mysqld.cnf `

Replace ‘127.0.0.1’ to ‘0.0.0.0’ like this:

![alt text](https://github.com/olateekay/client-server-architecture/blob/main/images/image13.png)

Restart mysql 

`sudo systemctl restart mysql`

![alt text](https://github.com/olateekay/client-server-architecture/blob/main/images/image14.png)

From `Client` Linux Server connect remotely to mysql server Database Engine without using SSH. You must use the mysql utility to perform this action.

Run this command;

`sudo mysql -u remote_user -h *DbServer ip*  -p`

![alt text](https://github.com/olateekay/client-server-architecture/blob/main/images/image15.png)

Check that you have successfully connected to a remote MySQL server and can perform SQL queries:

`Show databases;`

![alt text](https://github.com/olateekay/client-server-architecture/blob/main/images/image16.png)

