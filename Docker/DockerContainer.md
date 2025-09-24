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
```
- Docker creates a container and runs your app inside it.
- To list the running containers
```
docker ps
```
