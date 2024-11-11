# Ansible Playbooks for Django App Deployment and Configuration


This repository contains a collection of Ansible playbooks for deploying and configuring a Django application along with its dependencies. Each playbook serves a specific purpose in setting up the environment, deploying the app, and configuring services such as Gunicorn, Docker, and GitLab.

  
## Playbooks Overview

  
### 1. `configure_gunicorn.yml`

This playbook configures Gunicorn to serve the Django application.


# Playbook: Configure Gunicorn

This Ansible playbook configures Gunicorn, a Python WSGI HTTP Server for UNIX, to serve a Django application in a virtual environment.

  

### Prerequisites
  

- The playbook assumes that Python 3 is already installed on the target system.

- The target machine should have `apt` package manager (common for Debian-based systems).

- Ensure that the target machine has access to the required Python packages (like `python3-venv` and `gunicorn`).

  

### Playbook Overview



The `configure_gunicorn.yml` playbook performs the following tasks:

  

1. **Install the Python 3 Virtual Environment Package**  

   This task installs the `python3-venv` package, which is needed to create a Python virtual environment.

2. **Create a Python Virtual Environment**  

   It creates a virtual environment in the `/opt/django_app/venv` directory to isolate the Django application and its dependencies.

3. **Install Gunicorn in the Virtual Environment**  

   Gunicorn is installed inside the newly created virtual environment using `pip`, ensuring that it's isolated and compatible with the Django app.

4. **Verify Gunicorn Installation**  

   This task runs `pip list` inside the virtual environment to verify that Gunicorn has been successfully installed.

5. **Display Gunicorn Installation Output**  

   The playbook outputs the result of the `pip list` command, showing all installed Python packages in the virtual environment, confirming that Gunicorn is installed.

  
![alt text](Images/image.png)
![alt text](Images/image-1.png)


### 2. `install_docker.yml`

## Overview

This repository contains Ansible playbooks for automating the deployment of a Django application on a remote server using Docker. The tasks in the playbooks include cloning a GitLab repository, installing Docker, and deploying the Django app via Docker Compose. The playbooks are structured for easy configuration and secure management of credentials.

### Playbooks

1. **`install_docker.yml`**: This playbook installs Docker and Docker Compose on the remote server.
2. **`deploy_django_app.yml`**: This playbook clones the Django application repository, installs the required dependencies, and deploys the application using Docker Compose.

## Playbook Details

#### Purpose

The `install_docker.yml` playbook is designed to automate the installation of Docker and Docker Compose on a remote server. It ensures that Docker and Docker Compose are installed and ready for use.

#### Steps

1. **Install Docker**:
    - The playbook installs Docker from the official Docker repository.
2. **Install Docker Compose**:
    - Docker Compose is installed by downloading the binary from GitHub and placing it in `/usr/local/bin/`.
3. **Start and Enable Docker Service**:
    - The Docker service is started and enabled to run on boot, ensuring that the Docker service is always up when the system restarts.



![alt text](Images/image-2.png)

![alt text](Images/image-3.png)

![alt text](Images/image-4.png)

### 3. `install_python.yml`

## Overview

The `install_python.yml` playbook is designed to automate the installation of Python 3 and pip (Python's package installer) on remote servers. The playbook works with Ansible's `apt` module to update the package list and install the necessary Python packages on a Debian-based system (e.g., Ubuntu).

## Purpose

This playbook ensures that the remote servers, specified in the `dev_vms` group, have Python 3 and pip 3 installed and ready for use. These tools are essential for managing Python applications and dependencies.

## Playbook Details

### Steps

1. **Update Package List**:
    
    - The playbook starts by updating the system's package list to ensure the latest versions of available packages are installed.
2. **Install Python3 and pip3**:
    
    - The playbook installs both Python 3 and pip 3 in a single task. It uses a loop to install both packages: `python3` (the core Python 3 interpreter) and `python3-pip` (the Python package installer).

### Playbook Operation

![alt text](Images/image-5.png)

![alt text](Images/image-6.png)

![alt text](Images/image-7.png)

### 4. `install_gitlab.yml`

# Playbook: Install GitLab Runner

This Ansible playbook installs and configures GitLab Runner on a remote server, allowing you to register and run jobs for your GitLab CI/CD pipelines.

### Prerequisites

- The target machine should be running a Linux-based operating system (e.g., Ubuntu, Debian).
- Ensure that the target machine has internet access to download the GitLab Runner binary.
- The `dev_vms` host group should be defined in your Ansible inventory file.

### Playbook Overview

The `install_gitlab.yml` playbook performs the following tasks:

1. **Download the GitLab Runner Binary**  
   This task downloads the latest GitLab Runner binary from GitLab’s official repository and places it in the `/usr/local/bin` directory.

2. **Register GitLab Runner as a Service**  
   Registers the GitLab Runner as a service so it can be managed using systemd. This task ensures that the runner is ready to start and join the GitLab instance.

3. **Start GitLab Runner Service**  
   Starts the GitLab Runner service and ensures it is enabled to start on boot.

### Playbook Breakdown

![alt text](/Images/image-9.png)

![alt text](/Images/image-8.png)


# Playbook: Install GitLab Runner

This Ansible playbook installs and configures GitLab Runner on a remote server, allowing you to register and run jobs for your GitLab CI/CD pipelines.

### Prerequisites

- The target machine should be running a Linux-based operating system (e.g., Ubuntu, Debian).
- Ensure that the target machine has internet access to download the GitLab Runner binary.
- The `dev_vms` host group should be defined in your Ansible inventory file.

### Playbook Overview

The `install_gitlab.yml` playbook performs the following tasks:

1. **Download the GitLab Runner Binary**  
   This task downloads the latest GitLab Runner binary from GitLab’s official repository and places it in the `/usr/local/bin` directory.

2. **Register GitLab Runner as a Service**  
   Registers the GitLab Runner as a service so it can be managed using systemd. This task ensures that the runner is ready to start and join the GitLab instance.

3. **Start GitLab Runner Service**  
   Starts the GitLab Runner service and ensures it is enabled to start on boot.

### Playbook Breakdown

![alt text](Images/image-10.png)


### 5. `install_dependencies.yml`

# Playbook: Install Application Dependencies

This Ansible playbook automates the installation of the necessary dependencies for a Django application. It ensures that the Python virtual environment is created, the required packages are installed, and the `requirements.txt` file is copied to the server.

### Prerequisites

- The target machine should be running a Linux-based operating system (e.g., Ubuntu, Debian).
- Ensure the target machine has internet access for downloading the required packages.
- The `dev_vms` host group should be defined in your Ansible inventory file.

### Playbook Overview

The `install_dependencies.yml` playbook performs the following tasks:

1. **Gather Facts**  
   Collects system information, which is useful for making decisions about system configuration.

2. **Install Python 3 venv Package**  
   Ensures that the Python 3 virtual environment package (`python3-venv`) is installed.

3. **Create a Virtual Environment**  
   Creates a Python virtual environment at `/opt/django_app/venv` to isolate dependencies from the system Python installation.

4. **Copy `requirements.txt` to the VM**  
   Copies the `requirements.txt` file containing the list of Python dependencies to the server.

5. **Install Python Dependencies**  
   Installs the required Python packages in the virtual environment using `pip` and the `requirements.txt` file.

### Playbook Breakdown

![alt text](Images/image-12.png)

![alt text](Images/image-11.png)


