Project Title;

Personal Cloud and Automated Backup Server

Project Overview;

The objective of this project is to deploy a private self hosted photo and video synchronization platform using Immich. The system provides an alternative to commercial cloud services giving full control over personal data.

Project Objectives;

Deploy a stable Dockerized environment on an Ubuntu server.
Configure a storage template for human readable media organization.
Enable automated backups from mobile clients to the local server.
Prepare the infrastructure for a 3 2 1 backup strategy using offline external drives.

Step 1 System Update and Docker Installation

The first step is to ensure the host operating system is up to date and to install the required containerization software. We update the package lists and install docker and docker compose.

sudo apt update

sudo apt upgrade -y

sudo apt install docker.io docker-compose -y

After installation the Docker service is enabled to start automatically on system boot.

sudo systemctl enable docker

sudo systemctl start docker

Step 2 Prepare the Application Directory

A dedicated directory named personal cloud is created to host the configuration files.

mkdir personal-cloud

cd personal-cloud

Inside this directory the official docker compose and environment files are downloaded.

wget -O docker-compose.yml https://github.com/immich-app/immich/releases/latest/download/docker-compose.yml

wget -O .env https://github.com/immich-app/immich/releases/latest/download/example.env

Step 3 Configuration and Container Deployment

Due to a version compatibility with the host docker environment the compose file requires a minor edit.
nano docker-compose.yml
Remove the first line containing name immich and save the file.

The environment file is modified to set the UPLOAD LOCATION to our designated data folder and to configure a secure database password.

nano .env

Change UPLOAD_LOCATION to ./immich-data and set a secure DB_PASSWORD.

Initialize the application in the background.

sudo docker-compose up -d

Step 4 Application Initialization and Admin Setup

Once the Docker containers are successfully running the web interface becomes accessible via the host machine IP address on port 2283.
Navigate to the server IP in a web browser.
Click on the Getting Started button to initialize the platform. The system will prompt for the creation of the primary Administrator account. Fill in the required credentials. This account will have full access to server settings user management and global backup configurations.

Step 5 Storage Template Configuration

During the initial setup wizard the system prompts for the Storage Template configuration. It is highly recommended to enable the storage template engine. This feature organizes the raw physical files on the server into a human readable folder structure based on capture dates like Year and Month. This significantly simplifies manual file retrieval and makes the background backup process much more practical.

Step 6 Mobile Client Configuration

Download the Immich application from the respective app store. Open the app and enter the server endpoint URL.
Log in using the administrator credentials created during the initial setup. Navigate to the backup screen select the relevant local directories and enable the automatic backup switch.

Project Conclusion and Future Hardware Expansion

The core software infrastructure for the personal cloud and photo synchronization service is successfully deployed and operational. Mobile clients can authenticate and automatically offload media to the host server.
The final phase of this project involves the integration of two external storage drives to satisfy the 3 2 1 backup methodology.
Drive A will be mounted as the primary storage volume for the Docker containers.
Drive B will be mounted strictly as an offline backup destination. A scheduled cron job will be implemented to execute a daily synchronization task between Drive A and Drive B ensuring continuous data redundancy without manual intervention.
