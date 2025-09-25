## Multiple Containers from the Same Image
- You can run more than one container from the same Docker image on your local machine.
- Each container is isolated and has its own filesystem, network stack, and environment.
```
docker run -d --name backend1 -p 5000:5000 mybackend
docker run -d --name backend2 -p 5001:5000 mybackend
```
- Both containers run the same image (mybackend), but are independent and mapped to different host ports that is 5000 and 5001.
- but since the containers are isolated, the backend in each container can run on port 5000.

## Connecting a Container to an External Source
- Containers can connect to resources outside the Docker environment, such as:
  - APIs on the internet
  - External services on your local network
- You just use the external URL or IP in your containerized app: ```fetch("https://api.example.com/data")```
- Docker provides internet access by default via NAT networking.

## Connecting a Container to a Local Database
- If your database is running on your host machine, containers can connect to it:
- Use the special hostname: ```host.docker.internal```
```
DB_HOST=host.docker.internal
DB_PORT=5432
```
- Your container can now communicate with the host DB just like any external server.
