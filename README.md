---

## Web Application Deployment with Podman 🚀

### Project Overview 🌟
This project demonstrates how to deploy a simple web application using Podman. We'll will learn how to containerize an application, run it, and manage it with Podman.

### What we'll learn 🤔
- How to create and containerize a web application using Podman
- Basic Podman commands for building and running containers
- The benefits of using containers for application deployment

### Project Structure 🗂️
```plaintext
Podman_Portfolio_App/
├── app.py
├── Dockerfile
├── README.md
├── requirements.txt
├── static/
│   └── style.css
└── templates/
    └── index.html
```

### Table of Contents
```plaintext
1. Why Use Podman/Docker? 🤔
2. Basic Podman Concepts 📚
3. Podman Commands 📝
4. Project Start 🚀
5. Installations Before Starting 📦
6. Cloning the Repository 📁
7. Dockerfile 📄
8. Building and Running the Image 🚀
9. Checking the Logs 📝
10. License 📜
11. Acknowledgements 🙏
12. Contact 📲
```

### Why Use Podman/Docker? 🤔

Running applications in containers provides several benefits:
- **Isolation:** Containers run in isolated environments, reducing conflicts.
- **Consistency:** Ensures the application behaves the same across different environments.
- **Scalability:** Simplifies horizontal scaling of applications.

### Real-Time Scenario 🕰️
Imagine deploying a web application across development, staging, and production environments. Containers ensure consistent behavior and reduce "works on my machine" issues.

### Basic Podman Concepts 📚

- **Container:** An isolated environment where your application runs.
- **Image:** A snapshot of a container with the application code and runtime environment.
- **Pod:** A group of one or more containers sharing the same network namespace.

Learn more about [Podman concepts here](https://podman.io).

### Podman Commands 📝

Here are some fundamental Podman commands:

| Command                                    | Description                                       |
|--------------------------------------------|---------------------------------------------------|
| `podman pull <image>`                      | Download an image from a registry.               |
| `podman build -t <tag> .`                  | Build a new image from a Dockerfile.             |
| `podman run -d -p <host_port>:<container_port> <image>` | Run a container in detached mode.         |
| `podman ps`                                | List all running containers.                     |
| `podman stop <container_id>`               | Stop a running container.                        |
| `podman rm <container_id>`                 | Remove a stopped container.                      |
| `podman logs <container_id>`               | View the logs of a container.                    |
| `podman rmi <image_id>`                    | Remove an image.                                 |
| `podman exec -it <container_id> /bin/bash` | Execute a command inside a running container.   |

Learn more about [Podman commands here](https://podman.io/getting-started).

### Project Start 🚀

To start with the project, follow the steps below to set up and deploy the web application using Podman.
**Note** - You can pull this source code or repo from  or you can build or use any othe webapp of your choice.

### Installations Before Starting 📦

Ensure you have the following tools installed:

```bash
sudo dnf install git podman python3 python3-pip -y
```

### Cloning the Repository 📁

Clone the repository to get the project files:

```bash
git clone https://github.com/guptajeet/Podman_Portfolio_App.git
```

### Dockerfile 📄

Here is the Dockerfile used to containerize the application:
**Note** - Make sure to remove comments in Dockerfile, here i used comments to explain the file. 

```Dockerfile
# Use the official Python image from Docker Hub
FROM python:3.9-slim

# Set the working directory in the container
WORKDIR /app

# Copy the requirements file to the container
COPY requirements.txt /app/

# Install the Python dependencies
RUN pip install -r requirements.txt

# Copy the rest of the application code to the container
COPY . /app/

# Expose port 5000 for the application
EXPOSE 5000

# Define the command to run the application
CMD ["python", "app.py"]
```

### Building and Running the Image 🚀

Build the Docker image:

```bash
cd Podman_Portfolio_App
sudo podman build -t podman_portfolio_app:1.0 .
```

Run the container:

```bash
sudo podman run -d -p 5000:5000 localhost/podman_portfolio_app:1.0
```

Access the application via [http://server_ip:5000](http://vm_ip:5000) or [http://localhost:5000](http://localhost:5000).

<img width="955" alt="image" src="https://github.com/user-attachments/assets/0ca0cbc3-2b7a-466b-88ce-02de357faa48">

### Checking the Logs 📝

View the container logs:

```bash
sudo podman logs <container_id>
```

### Example Log Output:
```
 * Serving Flask app 'app'
 * Debug mode: on
WARNING: This is a development server. Do not use it in a production deployment. Use a production WSGI server instead.
 * Running on all addresses (0.0.0.0)
 * Running on http://127.0.0.1:5000
 * Running on http://10.88.0.4:5000
```

### License 📜

This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.

### Acknowledgements 🙏

- [Flask](https://flask.palletsprojects.com/): A micro web framework for Python.
- [Podman](https://podman.io): A daemonless container engine for developing, managing, and running OCI containers.
- [GitHub](https://github.com): Hosting and version control platform for the project's repository.

### Contact 📲

Feel free to connect with me on [LinkedIn](https://www.linkedin.com/in/guptajeet).

---
