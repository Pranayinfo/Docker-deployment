# Creation and Deployment of Performance Testing Environment

## Agenda

- GCP Infrastructure
- Creation of GCE
- Database Creation
- 3-Tier Application
- Application Deployment Using Docker Compose
- Conclusion

## GCP Infrastructure

![image](https://github.com/Pranayinfo/Docker-deployment/assets/97338976/497d2e95-7f71-4c00-b894-065580b76368)

### Confidence-Building Strategies

#### GCP Infrastructure Overview

Google Cloud Platform (GCP) provides a robust infrastructure tailored to host various services and applications.

**Services Utilized:**
- **Virtual Private Cloud (VPC):** Offers network isolation and control for resources.
- **Google Compute Engine (GCE):** Provides virtual machine instances for running applications.
- **Snapshot:** Captures the state of a disk at a specific moment, essential for backup and replication.
- **Image:** Represents a bootable OS disk, facilitating replication of system configurations.
- **Database:** Includes managed database services like Cloud SQL for relational databases.

Each service plays a crucial role in building and maintaining our performance testing environment.

## Creation of Google Compute Engine

### Snapshot Creation from UAT Environment

- Begin by taking a snapshot of the existing TEsting environment. This snapshot captures all essential components, including data, configuration files, applications, and dependencies. It serves as the foundation for our performance testing environment.

### Image Creation from GCE UAT Environment

- Create an image from the Google Compute Engine (GCE) instance running in the UAT environment. This image replicates the system configuration of the UAT environment, ensuring consistency in our performance testing setup.

### Creation of Performance Environment Using UAT Image

- Set up the performance testing environment on Google Compute Engine using the UAT image. Update the configuration settings (e.g., ec2-medium, web-vpc, appropriate region). Attach the previously created snapshot to ensure all necessary data is available.

### Firewall Configuration

- Configure firewall rules to allow access through HTTPS, HTTP, and SSH protocols, ensuring secure communication with the performance environment.

## Creation of Postgres Cloud SQL

### Database Creation and Connection

- Set up the database and establish connectivity with our application. We are utilizing both Postgres and Redis databases for our performance testing environment.

### Postgres Database Setup

- Export data from the existing `web-uat-db` to a designated bucket. Create a new Postgres database (`web-perf-db`) with similar configuration parameters.

### Database Import

- Import the exported data from `web-uat-db` stored in the bucket into the performance database.

### User Management

- Create specific users for interacting with the performance database (e.g., `web-user`, `web-uat`, `web-perf`) with necessary privileges.

### Redis Database Overview

- Leverage an existing Redis database for certain functionalities within our application.

## 3-Tier Application
![image](https://github.com/Pranayinfo/Docker-deployment/assets/97338976/692ca5c4-e316-4965-9c41-c252354ec264)

### Explanation of 3-Tier Application

- A 3-tier application architecture divides an application into three separate layers: presentation (frontend), application (backend), and data (database). Each tier serves a specific purpose and can be developed, deployed, and scaled independently.

**Presentation Layer (Frontend):**
- Responsible for user interaction and interface. Technologies like ReactJS are commonly used.

**Application Layer (Backend):**
- Handles business logic and processing of data. Technologies like Express and Node.js are popular choices.

**Data Layer (Database):**
- Stores and manages application data. PostgreSQL for structured data storage, Redis for in-memory data store for caching.

## Application Deployment Using Docker
![image](https://github.com/Pranayinfo/Docker-deployment/assets/97338976/a20f89b1-fc29-4c9d-af76-29a66ff2c64f)

### Overview

- Docker deployment architecture employs containerization to streamline the deployment process and enhance scalability. Nginx proxy server facilitates seamless communication between frontend and backend components.
- Nginx proxy server facilitates seamless communication between frontend and backend components.​
- Frontend consists of three websites: admin, trainer, and student.​
- Backend comprises four services: admin, auth, trainer, and users.​
- Docker Compose simplifies container orchestration, enabling easy integration of multiple services.​
- Cloud SQL PostgreSQL and Redis serve as backend databases, ensuring data persistence and caching functionality.​
- Overall, the architecture offers a robust and scalable solution for deploying Dockerized applications.

**Update the Nginx Proxy Server:​**

- Start Nginx using 'systemctl start nginx' and verify status with 'systemctl status nginx'.​
- Renew update or install new SSL certificate with certbot --nginx and select appropriate options.​
- Certbot is a tool for managing SSL certificates.​
- Select the domain for which the SSL certificate needs to be renewed.​
- Certbot certificates this command will list all the SSL certificates managed by Certbot on your server, along with their expiration dates and associated domain names.​

**Updating Configuration and .env Files:​**
- Navigate to Nginx configuration directory: cd /etc/nginx/sites-available/​
- Create or update the configuration file for the performance environment.​
  Example: vi random.web.com​
- Update the domain and SSL certificate details in the configuration file.​
- Repeat the same process for the /etc/nginx/sites-enabled directory.​
- After updating configuration files, restart Nginx to apply changes.​
Command: systemctl restart nginx

### Docker and Docker-Compose

**Docker:**
- Created a 2-stage Dockerfile for all the services: admin, trainer, and student.

**Docker-Compose:**
- Created the docker-compose manifest file:
  - Manifest files consist of the following services: admin, trainer, student, postgres, and redis.
  - Build the Docker images, specify port numbers, and set environment variables.
Command: docker-compose up -d

## Conclusion

This comprehensive overview covers the creation and deployment of a performance testing environment, encompassing infrastructure setup, application deployment, Docker deployment, database creation, and connection. Each step is detailed, providing insights into the configuration, commands, and scripts involved in the process.

---
Thank You !!
