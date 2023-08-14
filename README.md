# Docker Full Documentation for Installing and Running Odoo on Ubuntu

This comprehensive documentation provides step-by-step instructions for installing Docker, Docker Compose, and deploying an Odoo instance using Docker Compose on an Ubuntu system.

## Table of Contents
1. [Install Docker on Ubuntu](#install-docker-on-ubuntu)
2. [Install Docker Compose](#install-docker-compose)
3. [Start and Enable Docker](#start-and-enable-docker)
4. [Install Odoo Using Docker Compose](#install-odoo-using-docker-compose)
5. [Customizing PostgreSQL Password](#customizing-postgresql-password)
6. [Create Docker Compose Configuration](#create-docker-compose-yml)
7. [Launch Odoo](#deploy-odoo)
8. [Check Container Status](#check-container-status)
9. [Upload Custom Module to Odoo](#upload-custom-module-to-odoo)
10. [Restart Containers](#restart-containers)
11. [Conclusion](#conclusion)

### 1. Install Docker on Ubuntu
To install Docker on Ubuntu, execute the following commands:

```sh
sudo apt update
sudo apt upgrade
sudo apt install docker.io
docker version
````
### 2. Install Docker Compose
Install Docker Compose using the command:
```sh
sudo apt install docker-compose
```
3. Start and Enable Docker
Start and enable the Docker service to launch on boot:
```
sudo systemctl start docker
sudo systemctl enable docker
```
### 4. Install Odoo Using Docker Compose
Create a directory for your Odoo application and navigate to it:
```
mkdir my_odoo_app
cd my_odoo_app
```
### 5. Customizing PostgreSQL Password
Change the default PostgreSQL password by executing:
```
echo "your_postgres_password" > odoo_pg_pass
```
### 6. Create Docker Compose Configuration
Create and edit the docker-compose.yml file:
```
sudo nano docker-compose.yml
```
Copy and paste the following code into the file:
```
version: '3.1'
services:
  web:
    image: odoo:16.0
    depends_on:
      - db
    ports:
      - "8069:8069"
    volumes:
      - odoo-web-data:/var/lib/odoo
      - ./config:/etc/odoo
      - ./addons:/mnt/extra-addons
    environment:
      - PASSWORD_FILE=/run/secrets/postgresql_password
    secrets:
      - postgresql_password
  db:
    image: postgres:15
    environment:
      - POSTGRES_DB=postgres
      - POSTGRES_PASSWORD_FILE=/run/secrets/postgresql_password
      - POSTGRES_USER=odoo
      - PGDATA=/var/lib/postgresql/data/pgdata
    volumes:
      - odoo-db-data:/var/lib/postgresql/data/pgdata
    secrets:
      - postgresql_password
volumes:
  odoo-web-data:
  odoo-db-data:

secrets:
  postgresql_password:
    file: odoo_pg_pass
```
ctrl + x hit enter to save
### 7. Launch Odoo
Install Odoo by running the following command:
```
sudo docker-compose up -d
```
### 8. Check Container Status
View the status of containers:
```
sudo docker ps
```
If containers are not all up, use the following command to start a specific container:
```
docker restart container-name-or-id
```
### 9. Upload Custom Module to Odoo
Transfer your Odoo module to the container:
```
docker cp /path/to/your/local/file <container-id>:/mnt/custom_addons/
```
### 10. Restart Containers
Restart the containers:
```
docker restart container-name-or-id
```
### 11. Conclusion
Congratulations! You've successfully installed Docker and Docker Compose, deployed an Odoo instance using Docker Compose, and learned how to manage containers and upload custom modules. Your Odoo application is now up and running, ready for your business needs. Enjoy using Docker for efficient and scalable application deployment!

# Docker Full Documentation for Installing and Running Odoo on Ubuntu

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

This comprehensive documentation provides step-by-step instructions for installing Docker, Docker Compose, and deploying an Odoo instance using Docker Compose on an Ubuntu system.

## License

This project is licensed under the terms of the MIT License.



