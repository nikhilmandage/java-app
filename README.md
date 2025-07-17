# Java Application Deployment with Reverse Proxy on AWS

## 📌 Project Overview

This project demonstrates the deployment of a Java-based Student Registration Web Application on Amazon Web Services (AWS). The goal is to securely host the application with MySQL database integration and restrict public access using a reverse proxy architecture.

## 🎯 Objectives

- Deploy a `.war`-based Java application using Apache Tomcat on EC2.
- Set up an Amazon RDS MySQL database for persistent storage.
- Configure a reverse proxy (Nginx or Apache HTTPD) to securely route external traffic.
- Restrict direct public access to the backend EC2 instance.

---

## 🧰 Technology Stack

| Layer               | Technology / Service         |
|---------------------|------------------------------|
| Cloud Infrastructure| AWS EC2, AWS RDS             |
| Application Server  | Apache Tomcat                |
| Reverse Proxy       | Nginx (or Apache HTTPD)      |
| Database            | Amazon RDS (MySQL)           |
| Operating System    | Amazon Linux 2               |
| Java Connector      | MySQL Connector/J            |
| Application         | Java Servlet (student.war)   |

---
## ⚙ Implementation Steps

### 1. Infrastructure Setup
- Launched **two EC2 instances** (Amazon Linux 2):
  - `ec2-backend`: Private instance running Tomcat
  - `ec2-proxy`: Public instance running Nginx
- Launched **Amazon RDS (MySQL)** instance.

### 2. Application Deployment
- Installed Java & Tomcat on backend instance.
- Deployed `student.war` to `webapps/` directory.
- Verified application runs at: `http://<private-ip>:8080/student`

### 3. Database Setup
- Created schema and table:

```sql
CREATE TABLE students (
  id INT AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(100),
  email VARCHAR(100),
  course VARCHAR(50)
);
Configured RDS security group to allow only backend instance.

4. Database Connector
Downloaded and placed mysql-connector.jar in Tomcat's lib/ folder.

Restarted Tomcat to enable JDBC connectivity.

5. Reverse Proxy Setup
Installed and configured Nginx on proxy instance:

nginx
Copy
Edit
server {
    listen 80;
    location /student {
        proxy_pass http://<backend-private-ip>:8080/student;
    }
}
Updated backend security group to allow only proxy access.

6. Access Setup
Application available only at:

arduino
Copy
Edit
http://<Proxy-EC2-Public-IP>/student
Backend port 8080 is blocked from public access.

✅ Results
Application successfully deployed and accessed via reverse proxy.

Student data submitted through the form is stored in Amazon RDS.

Confirmed via MySQL queries from EC2 instance.
📌 Challenges & Solutions
Challenge	Solution
Restricting direct access to backend	Used Security Groups to allow traffic only from proxy
JDBC connectivity errors	Corrected VPC settings and added MySQL Connector to Tomcat
Routing issues via proxy	Configured Nginx with proper proxy_pass rules


name- Nikhil Mandage
fortune clouds
