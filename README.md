# docker_course
Docker Full Documentation

### Install docker in Ubuntu
To install docker in Ubuntu
```
sudo apt update
sudo apt install docker.io
docker version
```
### Install Docker Compose 
```
sudo apt  install docker-compose
```
### Start and enable Docker:
Start the Docker service and enable it to start on boot:
```
sudo systemctl start docker
sudo systemctl enable docker
```

### Install Odoo Using Docker Compose 
```
mkdir my_odoo_app
cd my_odoo_app

```
### To change default Postgres password use this
```
echo "your_postgres_password" > odoo_pg_pass

```
### Create docker-compose.yml file
```
sudo nano docker-compose.yml
```
### Copy and paste the below code
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
### To install odoo please use 
```
sudo docker-compose up -d
```
### Check number container had been created and their status 
```
sudo docker ps
```
If all are up all set if not start the container using the below command to start the container 
```
docker restart container-name-or-id
```
### Upload custom module in Odoo custom addons
```

```

