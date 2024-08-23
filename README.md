
---

# Docker Containerization of a Django Application

This guide will walk you through the steps to run a Django application using Docker on an AWS EC2 instance.

## Prerequisites

- AWS account
- Basic knowledge of AWS EC2 and Docker

## Steps to Get Started

### 1. Create an EC2 Instance

1. Log in to your AWS account and create an EC2 instance.
2. Choose an appropriate instance type (e.g., t2.micro for free tier) and an Ubuntu AMI.

### 2. Install Docker

SSH into your EC2 instance and run the following commands to install Docker:

```sh
sudo apt update
sudo apt install docker.io -y
```

### 3. Start Docker and Grant Access

#### Check Docker Installation

Run a test Docker container:

```sh
docker run hello-world
```

#### Troubleshooting

If you encounter a permission denied error:

```sh
docker: Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Post "http://%2Fvar%2Frun%2Fdocker.sock/v1.24/containers/create": dial unix /var/run/docker.sock: connect: permission denied.
See 'docker run --help'.
```

It could mean:

1. The Docker daemon is not running.
2. Your user does not have access to run Docker commands.

#### Start Docker Daemon

Check the status of the Docker daemon:

```sh
sudo systemctl status docker
```

If it's not running, start it:

```sh
sudo systemctl start docker
```

#### Grant User Access

Add your user to the Docker group to run Docker commands without `sudo`:

```sh
sudo usermod -aG docker ubuntu
```

Replace `ubuntu` with your username.

Log out and log back in for the changes to take effect.

#### Verify Docker Installation

```sh
docker run hello-world
```

You should see the message "Hello from Docker!".

### 4. Clone the Repository

Clone the project repository:

```sh
git clone https://github.com/Abdulwasay10/Docker-Containerization-of-a-Django-Application.git
```

Navigate to the project directory where the Dockerfile is located:

```sh
cd Docker-Containerization-of-a-Django-Application
```

### 5. Build the Docker Image

Initialize the Docker build:

```sh
docker build -t django-app .
```

### 6. Run the Docker Container

Get the image ID:

```sh
docker images
```

Run the project:

```sh
docker run -p 8000:8000 -it <imageid>
```

Replace `<imageid>` with the actual image ID.

### 7. Access the Application

1. Update the inbound security rules for your EC2 instance to allow traffic on port 8000.
2. Access the application using your EC2 instance's public IP address: `http://<your-ec2-ip>:8000`

## Notes

- Ensure your EC2 instance's security group allows inbound traffic on port 8000.
- For production use, consider using a more secure setup, including SSL/TLS and firewall configurations.

---
