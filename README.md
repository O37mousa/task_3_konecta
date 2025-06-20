# Task_3 KONECTA 

## Running Ubuntu Container with Docker

This guide explains how to run an Ubuntu container using Docker, why it may exit immediately, and how to keep it running.

---

###  Run Ubuntu Container

To run an Ubuntu container:

```bash
# Basic run command
docker run ubuntu

# If permission is denied, use sudo
sudo docker run ubuntu
```

### Check Running Containers

To check all containers (including stopped ones):

```bash
sudo docker ps -a
```

### Why Can't You See the Container?
The Ubuntu container exits immediately because there's no running process inside it.
By default, Docker starts the container, runs the default command (bash), and exits if there's no interaction or ongoing task.

### How to Keep the Container Running
Use the interactive mode to keep the container alive:
```bash
sudo docker run -it ubuntu
```

---

## Create a Dockerfile for the Flask Application
### Docker Compose Summary – Flask + PostgreSQL

This setup defines two services using Docker Compose:

## `web` (Flask App)
- **Builds** from local `Dockerfile`
- **Environment Variables**:
  - `FLASK_APP`, `FLASK_RUN_HOST`, `FLASK_ENV`
  - `DATABASE_URL` for PostgreSQL connection
- **Ports**: Maps `5000` (host) to `5000` (container)
- **Depends on**: `db` service (PostgreSQL)

## `db` (PostgreSQL)
- **Uses** the official `postgres:15` image
- **Environment Variables**:
  - `POSTGRES_USER`, `POSTGRES_PASSWORD`, `POSTGRES_DB`
- **Volume**: Persists data using `db_data`

## Volume
- `db_data`: Stores PostgreSQL data persistently

## Usage
- Start services: `docker-compose up --build -d` & `-d` for running in background
- Stop: `docker-compose down`

### Bulding up docker-compose
- Run docker-compose `sudo docker compose up --build -d`
  
![image](https://github.com/user-attachments/assets/0395fc26-8a4c-4476-b28e-440825872c35)

### Check containers are running
- Run `sudo docker ps -a`

![image](https://github.com/user-attachments/assets/bb932b93-1a43-4347-a90d-ed9c56827d35)

### Access the web container
- Run `sudo docker exec -it c670e9eaece6 bash`
- Change the "_c670e9eaece6_" with your web **CONTAINER ID**

![image](https://github.com/user-attachments/assets/90c8f0b4-716e-4f1f-9899-4a2c067ebee2)

### Updating File & Installing PostgreSQL Client on Ubuntu
- By running `apt update && apt install -y postgresql-client`

### Then, Check Connectivity of the app
- By running `psql -h db -p 5432 -U postgres_user -d mydatabase`

![image](https://github.com/user-attachments/assets/45f69a42-2926-462c-9499-3dccfcb95290)

### To verify the running connection
- Open your browser @ http://localhost:5000/

![image](https://github.com/user-attachments/assets/8ef07111-e296-4934-bfbe-392c803c29bc)

---

## Optional: Bonus
### To add Nginx as a reverse proxy in the setup
- Create create a new folder called **Nginx** for the special page, having a new **Dockerfile**, then make a new file called "**index.html**" that has the design of the _Free Palestine_ page.
- After adding everything, build the new image using `sudo docker build -t free-palestine .`, then run it using `sudo docker run -d -p 8080:80 --name palestine-app free-palestine`

![image](https://github.com/user-attachments/assets/98cec0b2-d8c8-40e9-a308-9ea7df7a31cd)

- Check the container is running

![image](https://github.com/user-attachments/assets/677d48c5-63b6-414b-a2f8-ab04e5b2e8a7)

- Then, run it using `sudo docker run -d -p 8080:80 --name palestine-app free-palestine`

![image](https://github.com/user-attachments/assets/06610cfb-5bd1-4926-bd1f-55ebd042cd82)



