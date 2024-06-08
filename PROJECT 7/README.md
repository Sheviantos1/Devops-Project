# IMPLEMENTING LOADBALANCING ON NGINX

## INTRODUCING LOADBALANCING ON NGINX

 Loadbalancing is a technique used to distribute workloads (tasks or requests) across a group of resources (servers, computers, etc.) to optimize performance, reliability, and efficiency. 

 Imagine a busy restaurant with one overwhelmed waiter and several idle colleagues. That's what happens when a website relies on a single web server – it gets overloaded while others sit idle. Thankfully, load balancing acts like a restaurant manager, efficiently distributing customers (website traffic) among all available servers (waiters). 

 Instead of everyone hitting the first server they see, a load balancer stands as a central access point, receiving all incoming traffic. Using various algorithms, it intelligently routes each request to the most suitable server. This could be the one with the least load, the fastest response time, or even the one best equipped to handle the specific request type.

 By spreading the workload evenly, load balancing prevents any single server from becoming overloaded, ensuring smooth website performance and happy users. 

 Nginx is an incredibly flexible software that can be used in a wide variety of scenarios. It can be configured to act as a web server, reverse proxy, load balancer, and much more. The key is to correctly configure Nginx to meet your specific needs, allowing it to serve your desired purpose seamlessly.

 ## SETTING UP A BASIC LOAD BALANCER

We plan to provision two EC2 instances operating on Ubuntu 22.04, install Apache web server on both, and open port 8000 for unrestricted traffic access. As a final step, we aim to modify the default web page of the servers to showcase their respective public IP addresses.

1. Provisioning an EC2 instance

- On your AWS management console,go to EC2 and create two Ubuntu server, then lauch instances

![alt text](<IMAGES/Launch Instance.PNG>)

2. Open Port 8000

- Go to security group and open port 8000 on the webservers.

![alt text](<IMAGES/Security Group.PNG>)

3. Install Apache Webserver

-  Connect to webserver: Click on connect and copy the ssh 

![alt text](<IMAGES/SSH client.PNG>)

- Then go to your terminal and ssh to connect to the webserver

![alt text](<IMAGES/SSH download.PNG>)

- Next install Apache with the command: `sudo apt update -y && sudo apt install apache2 -y`

![alt text](<IMAGES/Install Apache.PNG>)

- Verify Apache is active by running: `sudo systemctl status apache2`

![alt text](<IMAGES/Check Apache.PNG>)

4. Configure Apache to server a page showing its public IP

- Using a text editor and open the file /etc/apache2/ports.conf by running: `sudo vi /etc/apache2/ports.conf`

![alt text](<IMAGES/File Path.PNG>)

- Add a new listen directive for 8000. Type i to switch to insert mode so you can edit the file, then save the file

![alt text](<IMAGES/Listen Directive.PNG>)

- Next open the file /etc/apache2/sites-availale/000-default.conf and change from port 80 to port 8000 by running: `sudo vi /etc/apache2/sites-availale/000-default.conf`

![alt text](<IMAGES/Virtual Host.PNG>)

- close the file by pressing the esc key and run the command: `:wqa!`

- Restart apache to load the new configuration by running: `sudo systemctl restart apache2`

![alt text](<IMAGES/Restart Apache.PNG>)

5. Create a new html file 

- Open a new index file by running: `sudo vi index.html`

- Switch vi editor to insert mode and paste your html file

![alt text](<IMAGES/File Path.PNG>)

- Change file ownership of the index.html file by running: `sudo chown www-data:www-data ./index.html`

![alt text](<IMAGES/File Ownership.PNG>)

6. Overriding the Default html file of Apache Webserver

- Replace default html file of Apache Webserver by running: `sudo cp -f ./index.html /var/www/html/index.html`

- Restart the Webserver to load the new configuration by running: `sudo systemctl restart apache2`

![alt text](<IMAGES/system restart.PNG>)

- Then run the IP on browser page

![alt text](<IMAGES/Web Page.PNG>)

### Configuring Nginx as a Load Balancer

- Provision an EC2 and open port 80 and connect to ssh

- Then install Nginx into the instance by running: `sudo apt update -y && sudo apt install nginx -y`

![alt text](<IMAGES/Install Nginx.PNG>)

- Verify that Nginx is installed with the command by running: `sudo systemctl status nginx`

![alt text](<IMAGES/Status Nginx.PNG>)

- Open Nginx configuration file by running command: `sudo vi /etc/nginx/conf.d/loadbalancer.conf`

![alt text](IMAGES/Loadbalancer.PNG)

- Paste the file configuration below to configure nginx to act like a load balancer. 

![alt text](<IMAGES/Upstream servers.PNG>)

- Test your configuration by running: `sudo nginx -t`

- Since no error, restart Nginx to load the new configuration by running: `sudo systemctl restart nginx`

- Paste the Public Ip address of Nginx Load Balancer, it should show our configuration

![alt text](<IMAGES/Test Page.PNG>)







































