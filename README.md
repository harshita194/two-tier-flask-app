Two-Tier Flask Application with MySQL, Docker, and Jenkins Integration

This project is a two-tier Flask web application that uses a MySQL database as the backend. The entire setup is containerized using Docker and can be extended for CI/CD automation with Jenkins and Kubernetes (EKS).

It demonstrates modern DevOps practices — containerization, networking, automation, and scalability.

🚀 Features

Flask web application for submitting and displaying messages

MySQL database integration for persistent storage

Docker-based two-tier architecture (frontend + backend)

Multi-stage Docker builds for optimized image size

Jenkins pipeline integration for CI/CD

Kubernetes manifests for cloud deployment (EKS-ready)

🧰 Tech Stack

Flask (Python)

MySQL

Docker & Docker Compose

Jenkins

Kubernetes (EKS)

Makefile (for automation tasks)

⚙️ Setup Instructions
1️⃣ Clone the Repository
git clone https://github.com/harshita194/two-tier-flask-app.git
cd two-tier-flask-app

2️⃣ Create Environment Variables

Create a .env file in the project root directory:

MYSQL_HOST=mysql
MYSQL_USER=root
MYSQL_PASSWORD=admin
MYSQL_DB=mydb

🐳 Run Using Docker Compose

Start both the Flask and MySQL containers:

docker-compose up --build


Access the app:

Frontend: http://localhost

Backend: http://localhost:5000

🧱 Run Without Docker Compose
Create Docker Network
docker network create twotier

Run MySQL Container
docker run -d \
  --name mysql \
  -v mysql-data:/var/lib/mysql \
  --network=twotier \
  -e MYSQL_DATABASE=mydb \
  -e MYSQL_ROOT_PASSWORD=admin \
  -p 3306:3306 \
  mysql:5.7

Build and Run Flask Container
docker build -t flaskapp .
docker run -d \
  --name flaskapp \
  --network=twotier \
  -e MYSQL_HOST=mysql \
  -e MYSQL_USER=root \
  -e MYSQL_PASSWORD=admin \
  -e MYSQL_DB=mydb \
  -p 5000:5000 \
  flaskapp:latest

🧹 Stop and Clean Up
docker-compose down


or manually:

docker stop flaskapp mysql && docker rm flaskapp mysql
docker network rm twotier

📦 Database Setup

Inside MySQL, create the table:

CREATE TABLE messages (
    id INT AUTO_INCREMENT PRIMARY KEY,
    message TEXT
);
