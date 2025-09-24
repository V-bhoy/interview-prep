## What is a docker container?
- A Docker container is a running instance of a Docker image.
- It’s an isolated environment where your application runs with all its dependencies.

### Things to note:
- Isolated – Containers run separately from each other and from the host system.
- Lightweight – Shares the host OS kernel, so much faster and smaller than a VM.
- Portable – Can run on any machine with Docker installed (dev, test, production).
- Ephemeral – By default, if you delete a container, its changes are lost unless you use volumes.
- Created from images – Every container starts from a Docker image.

## How it works?
- You have a Docker image (blueprint).
- Run a container:
```
docker run -p 3000:3000 myapp:1.0

3000 on left is the port to be exposed on our local machine
3000 pon right is the port exposed inside the container
myapp:1.0 is the image id
```
- Docker creates a container and runs your app inside it.
- To list the running containers
```
docker ps
```
- To list all containers --> ```docker ps -a```
- To remove a particular container --> ```docker rm container-name```
- To stop the container
```
docker stop container-name
```
## Running Containers: Attached vs Detached
### 1. Attached Mode (default)
- When you run a container like this: ```docker run myimage```
- You are attached to the container’s terminal.
- Anything the app prints (logs, console output) appears in your terminal.
- You can interact with the container (if it expects input).
- To stop the container, you press Ctrl + C or above command.
- Logs are streamed to your terminal. Terminal is occupied until you stop the container.
### 2. Detached Mode (-d)
- Run a container in background:
```
docker run -d -p 3000:3000 myimage
```
- Container runs independently in the background.
- You don’t see logs directly in your terminal.
- To check running containers: ```docker ps```
- To see logs: ```docker logs <container_id>```
- Use detached mode for production or long-running apps
- Terminal is free while the container continues running.
### To removw the conatiner when it stops automatically, instead of manually removing the stopped container
```docker run -d --rm -p 3000:3000 myimage```
### If you want to give custom name to the container
```docker run -d --rm --name "my-app" -p 3000:3000 myimage```
- A container with name "my-app" will be running in the background.
