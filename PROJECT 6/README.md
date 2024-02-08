# UNDERSTANDING CLIENT SERVER ARCHITECTURE

## CLIENT SERVER ARCHITECTURE WITH MySQL

### What is Client-Server Architecture?

Client-server architecture is a distributed computing model in which tasks are divided between the servers and the clients. In this architecture, the client requests services or responses from server, which provides a response. 

# IMPLEMENTING CLIENT-SERVER ARCHITECTURE USING MySQL DATABASE MANAGEMENT SYSTEM (DBMS)

Follow the instruction below to demonstrate a basic client-server using MySQL RDBMS

1. Create and configure two Linux-based virtual servers (EC2 instance on AWS)

Server A name - `mysql server` (To serve information)

Server B name - `mysql client` (To request information)

![alt text](<IMAGES/ec2 instance.PNG>)

2. After connecting the 2 servers to the terminal, run  `sudo apt update` to update the terminal

- Then run `sudo apt install mysql-server` to install mysql on the ubuntu server

![alt text](<IMAGES/sudo apt install mysql.PNG>)

3. On the mysql client terminal, run `sudo apt update` to update the terminal

- Then run `sudo apt install mysql-client` to install mysql on the ubuntu server.

![alt text](<IMAGES/install mysql-client.PNG>)

4. Since the ec2 virtual servers are located in the same local virtual network, they can communicate to each other using local IP addresses. MySQL server uses TCP port 3306 by default so we will have to open it by creating a new entry in inbound rules in your security groups.

![alt text](<IMAGES/mysql port.PNG>)

5. Configure MySQL server to allow connection from remote hosts

Run sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf then change the bind-address from `127.0.0.1` to `0.0.0.0`

![alt text](<IMAGES/sudo nano mysql new.PNG>)

6. To connect MySQL client to MySQL server without using SSH

- open MySQL console on MySQL server

- create new user account using a username and password of your choice by running `CREATE USER 'Shevy'@'16.171.194.116' IDENTIFIED BY 'PassWord@1'` 

Change the shevy to your preferred username, 16.171.194.116 to your public IP address and PassWord@1 to your preferred password

- Then grant priviledges to the account using the command `GRANT ALL PRIVILEGES ON *.* TO 'Shevy'@'16.171.194.116';`

- And flush priviledges using the command `FLUSH PRIVILEDGES`

![alt text](<IMAGES/MYSQL NEW USER.PNG>)

7. From the client server, run `sudo mysql -u Shevy -p -h 51.20.64.51` to connet to mysql server using administrator privileges

![alt text](<IMAGES/mysql -u show databases.PNG>)

If you could see this databases, congratulations. You have successfully connected the client to the mysql server
















