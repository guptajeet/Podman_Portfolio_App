---

## Simple Web Application Deployment with Podman

### 🌟Project Overview

This project demonstrates how to deploy a simple web application using Podman. We'll learn how to containerize an application, run it, and manage it using Podman.

### What I'll Learn

- How to create and containerize a web application using Podman
- Basic Podman commands for building and running containers
- The benefits of using containers for application deployment

### Project Structure

```
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

### Running the Application Without Docker

Before diving into containerization, we might want to check if the application works without Docker:
   ```sh
   sudo dnf install python3 python3-pip -y # Install Python and Required Packages
   pip3 install -r requirements.txt        # Install requirements in this project its FLASK
   python3 app.py                          # Run the Flask Application
   
   ```
   Access the application via `http://localhost:5000/` OR `http://server_ip:5000/`

### Why Use Podman/Docker?

Running application in a container provides several benefits:

- **Isolation:** Containers run in their own isolated environments, reducing conflicts between different applications or services on the same host.
- **Consistency:** Containers ensure that your application runs the same way in different environments, from development to production.
- **Scalability:** Containers make it easier to scale applications horizontally by running multiple instances.

**Real-Time Scenario:**

Imagine you are deploying a web application across different environments: development, staging, and production. Using containers ensures that the application behaves consistently across all environments, reducing the risk of "works on my machine" issues.

### Installations Before Starting

Ensure you have the necessary tools installed:

```sh
sudo dnf install git podman python3 python3-pip -y
```

### Basic Podman Concepts

Before starting the project, it's essential to understand some basic Podman concepts:

- **Container:** An isolated environment where your application runs.
- **Image:** A snapshot of a container that includes the application code and runtime environment.
- **Pod:** A group of one or more containers that share the same network namespace.

[Learn more about Podman concepts here](https://podman.io/docs)

### Podman Commands

Here are some fundamental Podman commands and their uses:

- **`podman pull <image>`**  
  Download an image from a registry.
  ```sh
  podman pull python:3.9-slim
  ```

- **`podman build -t <tag> .`**  
  Build a new image from a Dockerfile in the current directory.
  ```sh
  sudo podman build -t podman_portfolio_app:1.0 .
  ```

- **`podman run -d -p <host_port>:<container_port> <image>`**  
  Run a container in detached mode and map container ports to host ports.
  ```sh
  sudo podman run -d -p 5000:5000 localhost/podman_portfolio_app:1.0
  ```

- **`podman ps`**  
  List all running containers.
  ```sh
  podman ps
  ```

- **`podman stop <container_id>`**  
  Stop a running container.
  ```sh
  sudo podman stop <container_id>
  ```

- **`podman rm <container_id>`**  
  Remove a stopped container.
  ```sh
  sudo podman rm <container_id>
  ```

- **`podman logs <container_id>`**  
  View the logs of a container.
  ```sh
  sudo podman logs <container_id>
  ```

- **`podman rmi <image_id>`**  
  Remove an image.
  ```sh
  sudo podman rmi <image_id>
  ```

- **`podman exec -it <container_id> /bin/bash`**  
  Execute a command inside a running container (e.g., open a shell).
  ```sh
  sudo podman exec -it <container_id> /bin/bash
  ```

[Learn more about Podman commands here](https://docs.podman.io/en/latest/Commands.html)

Lets get started with project now, first step is to pull the source code from github or you can use any other webapp of your choice
### Cloning the Repository

Clone the repository to get the project files:

```sh
git clone https://github.com/guptajeet/Podman_Portfolio_App.git
```

### Dockerfile

Here is the `Dockerfile` used to containerize the application:
Note - Make sure to remove comments in Dockerfile, here i used comments to explain the file. 

```Dockerfile
# Use the official Python image from the Docker Hub
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

### Building and Running the Image

1. **Build the Docker Image:**

   Navigate to the project directory and build the image:

   ```sh
   cd Podman_Portfolio_App
   sudo podman build -t podman_portfolio_app:1.0 .
   ```

2. **Run the Container:**

   Run the container with port mapping:

   ```sh
   sudo podman run -d -p 5000:5000 localhost/podman_portfolio_app:1.0
   ```

   Access the application via `http://vm_ip:5000` or `http://localhost:5000`.

### Checking the Logs

View the container logs to ensure the application is running correctly:

```sh
sudo podman logs <container_id>
```

**Example Log Output:**

```
 * Serving Flask app 'app'
 * Debug mode: on
WARNING: This is a development server. Do not use it in a production deployment. Use a production WSGI server instead.
 * Running on all addresses (0.0.0.0)
 * Running on http://127.0.0.1:5000
 * Running on http://10.88.0.4:5000
```
<img width="955" alt="image" src="https://github.com/user-attachments/assets/41be4070-c760-4ea3-943d-1c54651ad899">


## License

This project is licensed under the [MIT License](LICENSE).

## Acknowledgements

- Flask: A micro web framework for Python.
- Podman: A daemonless container engine for developing, managing, and running OCI containers.

## Contact

Feel free to connect with me on [LinkedIn](https://www.linkedin.com/in/ajeet-g-456333194/).

## Additional

- `.gitignore` file: Excludes unnecessary files from being committed to the repository.

### `app.py`

Here is the `app.py` file used in this project:

```python
from flask import Flask, render_template

app = Flask(__name__)

@app.route('/')
def home():
    return render_template('index.html')

if __name__ == '__main__':
    app.run(host="0.0.0.0", port=5000, debug=True)
```

---


