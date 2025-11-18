# Nginx–Apache Load Balancer

## Objective

This project demonstrates the deployment of a complete load-balanced web infrastructure using **NGINX as a reverse proxy** with two Fedora-based **Apache web servers** as backend nodes.

It includes:

- Building and configuring the servers  
- Deploying custom web content  
- Implementing **.htaccess** authentication  
- Setting up the **NGINX load balancer**  
- Applying firewall rules  
- Performing security testing using **OWASP ZAP**

The environment simulates real-world scenarios involving:

- High availability and redundancy  
- Traffic routing and distribution  
- Disaster recovery concepts  
- Basic web server security practices

## Skills Learned

- Linux server setup & configuration  
- Apache web server deployment  
- NGINX reverse proxy & load balancing  
- Basic authentication using `.htaccess`  
- Firewall configuration  
- Security testing with OWASP ZAP  


## Tools Used

- Fedora Linux  
- Apache HTTPD  
- NGINX  
- firewalld  
- VirtualBox  
- OWASP ZAP

## 🎥 Full Project Demonstration Video

🔗 **Project Walkthrough:**  
  
https://github.com/user-attachments/assets/9bf2b30c-a8f2-4d3e-8c38-de586bf38bc1

This single video includes:

- ✔️ Web Server 1 setup  
- ✔️ Web Server 2 setup  
- ✔️ NGINX Load Balancer configuration  
- ✔️ Firewall setup  
- ✔️ HTAccess authentication  
- ✔️ ZAP scanning
  
## 🏗️ Architecture Overview


               Client (Browser / ZAP)
                         |
                         v
               +----------------------+
               |     NGINX LB VM      |
               |     Reverse Proxy    |
               +----------------------+
                     /            \
                    /              \
                   v                v
        +------------------+   +------------------+
        | Fedora WebServer1|   | Fedora WebServer2|
        | Apache + HTAccess|   | Apache + HTAccess|
        +------------------+   +------------------+

## Project Steps

### 1. Web Server 1 Setup (Apache HTTPD)
    
  - Installed Apache using dnf install httpd -y

  - Enabled service with systemctl

  - Created HTML test page with external dog image

  - Added identifier: “This page is served from Node 1”

  - Implemented .htaccess authentication using .htpasswd

  - Opened firewall port 80
 
### 2. Web Server 2 Setup (Apache HTTPD)

  - Installed & configured Apache

  - Custom index.html

  - Added identifier: “This page is served from Node 2”

  - Implemented .htaccess authentication

  - Opened port 80 with firewalld

### 3. NGINX Load Balancer Setup

  - Installed NGINX on a separate Fedora VM

  - Configured upstream servers inside nginx.conf

- Reverse proxy + load balancing using:

```nginx
upstream backend {
    server 10.0.0.158;
    server 10.0.0.130;
}

server {
    listen 80;
    location / {
        proxy_pass http://backend;
    }
}
```

  - Restarted & enabled NGINX

### 4. Testing Load Balancing

  - Accessed load balancer IP from internal browser

  - Accessed from Windows host browser

  - Verified round-robin switching between Node 1 and Node 2
