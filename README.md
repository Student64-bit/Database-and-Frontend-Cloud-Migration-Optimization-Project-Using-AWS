# Database and Frontend Cloud Migration & Optimization Project Using AWS

## Overview
This project involves creating a simple React frontend application that includes a submission form, which interacts with a MySQL database initially hosted locally. The objective is to migrate this application to the cloud using various AWS services, enhancing the infrastructure with managed and serverless technologies. The backend will be migrated to an EC2 instance, while the frontend will be hosted in an S3 bucket and served via CloudFront.

## AWS Services Used
- **AWS EC2**: Hosts the initially locally hosted database.
- **AWS CloudFront**: Optimizes the delivery of the migrated React frontend.
- **AWS S3**: Stores and hosts the React frontend.
- **AWS RDS**: Used to enhance the database with features like encrypted security with rotating keys, read replicas for improved availability and performance, and managed backups and OS patches.

## Other Services Used
- **React.js**: Frontend library.
- **Node.js**: JavaScript runtime for the frontend.
- **MySQL WorkBench**: Initial local database creation and management tool.

## Cloud Migration Lifecycle
This project, although not at an enterprise scale with numerous microservices, incorporates typical cloud migration lifecycle practices to gain experience in cloud migration.

### Step 1: Preparation
Preparation typically involves decoupling an infrastructure into microservices for easier cloud migration. For monolithic architectures, this step involves significant restructuring. However, for this project's scope—consisting of a simple frontend and database—the infrastructure does not require decoupling but will be considered in future projects with more complex architectures.

### Step 2: Planning
After preparing the infrastructure, the next step involves organizing the migration phases. Critical services are migrated in later phases to minimize disruption. This project involves a straightforward migration without phase distinctions due to its simplicity.

### Step 3: Migration
- **Database Migration**: The locally hosted MySQL database is migrated to an AWS EC2 instance. This allows the frontend to interact with a cloud-based database.
- **Frontend Migration**: The React application is moved to an AWS S3 bucket configured for static website hosting, making it accessible over the internet.

### Step 4: Monitoring
Given the smaller scope of my current project, this step will be skipped but will be implemented during a larger migration project in the future.

### Step 5: Optimization
After migrating everything to the cloud, the next step will be to utilize various AWS services to enhance aspects such as performance, cost-efficiency, security, and many other valuable features.

## Detailed Migration Steps

### 1. Setting Up Local React Frontend and SQL Database
A simple React frontend is set up where users can enter their first name, last name, and email address, which are stored in a MySQL database.

<p align="center">
  <img src="https://i.imgur.com/nrcZkmI.png" alt="Code commit permissions" width="80%" height="80%">
  <br>
  <strong><small>Figure 1: Screenshot of the React submission form.</small></strong>
</p>
<br>
<br>

<p align="center">
  <img src="https://i.imgur.com/s9vT6D2.png" alt="Code commit permissions" width="80%" height="80%">
  <br>
  <strong><small>Figure 2: Screenshot Demonstrating Database Population from the Frontend Interface.</small></strong>
</p>
<br>

### 2. Migrating the Database
The database is migrated to an AWS EC2 instance. Initially, the database, including its data, tables, and schema, is exported to a MySQL dump file using MySQL WorkBench. This dump file is transferred to the EC2 instance using the `scp` command. Commands are then executed to import this data into MySQL on EC2.

<p align="center">
  <img src="https://i.imgur.com/HGkucGG.png" alt="Code commit permissions" width="80%" height="80%">
  <br>
  <strong><small>Figure 3: Exporting the locally hosted MySQL database to a dump file, which can then be used by an EC2 instance to replicate the database.</small></strong>
</p>
<br>
<br>

<p align="center">
  <img src="https://i.imgur.com/iHbsV15.png" alt="Code commit permissions" width="80%" height="80%">
  <br>
  <strong><small>Figure 4: Successfully transferred the SQL dump file to my virtual EC2 instance using the SCP command from my local machine.</small></strong>
</p>
<br>
<br>

<p align="center">
  <img src="https://i.imgur.com/HAeNqb9.png" alt="Code commit permissions" width="80%" height="80%">
  <br>
  <strong><small>Figure 5: Successfully setup mysql community on my virtual ec2 instance.</small></strong>
</p>
<br>
<br>

<p align="center">
  <img src="https://i.imgur.com/WJjTsNG.png" alt="Code commit permissions" width="80%" height="80%">
  <br>
  <strong><small>Figure 6: Successfully replicated my local database to the virtual EC2 instance, thereby migrating it to the cloud where it can utilize a wide range of AWS services.</small></strong>
</p>
<br>
<br>

### 3. Migrating the Frontend
The React application files are moved to an AWS S3 bucket. The `npm run build` command is used to create a production-ready build of the application, reducing the number of files that need to be uploaded.

<p align="center">
  <img src="https://i.imgur.com/pBaiFC8.png" alt="Code commit permissions" width="80%" height="80%">
  <br>
  <strong><small>Figure 7: React applications can have thousands of files, which can be troublesome when moving them to an S3 bucket. Therefore, I created a build folder that condenses only the critical and necessary files needed to host my frontend.</small></strong>
</p>
<br>
<br>

<p align="center">
  <img src="https://i.imgur.com/Ul9LOlO.png" alt="Code commit permissions" width="80%" height="80%">
  <br>
  <strong><small>Figure 8: S3 bucket after the build files have been transferred.</small></strong>
</p>
<br>
<br>

<p align="center">
  <img src="https://i.imgur.com/DQVu9R7.png" alt="Code commit permissions" width="80%" height="80%">
  <br>
  <strong><small>Figure 9: The frontend can now be accessed from the internet using the EC2 instance's IP address, although it does not yet have a custom domain name or CNAME. This will be addressed later with the implementation of CloudFront distribution services for optimization.</small></strong>
</p>
<br>
<br>

### 4. Optimizing the Frontend with AWS Services
AWS CloudFront is used to manage the CDN, caching, and security aspects of the frontend service. This setup includes default SSL/TLS encryption provided by CloudFront, enhancing security and performance.

<p align="center">
  <img src="https://i.imgur.com/VHPh4Ha.png" alt="Code commit permissions" width="80%" height="80%">
  <br>
  <strong><small>Figure 10: As mentioned earlier, although my frontend is now hosted in the cloud, additional measures, such as in-flight encryption, can be implemented to address security issues. In the next figure, I will demonstrate what the application looks like after using the AWS CloudFront service.</small></strong>
</p>
<br>
<br>

<p align="center">
  <img src="https://i.imgur.com/pgNr4vw.png" alt="Code commit permissions" width="80%" height="80%">
  <br>
  <strong><small>Figure 11: After using CloudFront to distribute my frontend application online, it now incorporates several security features including SSL for in-flight encryption, a WAF (Web Application Firewall) for private access, and ORN Shield to protect against malicious website attacks.</small></strong>
</p>
<br>
<br>

<p align="center">
  <img src="https://i.imgur.com/X3rlyvC.png" alt="Code commit permissions" width="80%" height="80%">
  <br>
  <strong><small>Figure 12: WAF (Web Application Firewall).</small></strong>
</p>
<br>
<br>


### 5. Optimizing the Backend Database with AWS RDS
The backend MySQL database on EC2 is further optimized by migrating it to AWS RDS. This service improves management by automating backups, patching, and scaling. Features like read replicas help in distributing the load and improving query performance.
<p align="center">
  <img src="https://i.imgur.com/D2LW2jp.png" alt="Code commit permissions" width="80%" height="80%">
  <br>
  <strong><small>Figure 13: Creating a backup of my database for good security practices which I will download locally.</small></strong>
</p>
<br>
<br>

<p align="center">
  <img src="https://i.imgur.com/sTXyRcm.png" alt="Code commit permissions" width="80%" height="80%">
  <br>
  <strong><small>Figure 14: Configuring the RDS database for preformance optimization.</small></strong>
</p>
<br>
<br>

<p align="center">
  <img src="https://i.imgur.com/Traao6X.png" alt="Code commit permissions" width="80%" height="80%">
  <br>
  <strong><small>Figure 15:After setting up my RDS cloud database, I was able to replicate it from my EC2 instance. This process was similar to how I migrated my local database to the cloud, but it was somewhat simpler. I only needed the RDS endpoint, master username, and master password to accomplish this with a single shell command.</small></strong>
</p>
<br>
<br>

By following these steps and utilizing the described AWS services, the project demonstrates a successful cloud migration strategy for a simple web application.
