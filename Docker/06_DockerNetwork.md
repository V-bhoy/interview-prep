## What is a docker network?
- A Docker network allows containers to communicate with each other and/or the outside world.
- By default, Docker containers are isolated, so networking is needed to enable communication.

## Types

### Bridge (default)
- Default network type when you run a container without specifying a network. Docker automatically attaches these containers to the default bridge network.
-  On the default bridge network, containers cannot automatically resolve each other by name. They can only talk using IP addresses.
- So in practice, using default bridge network for container-to-container communication is limited.

### Custom Bridge Network (Recommended)
- Create your own network: ```docker network create my-network```
- Now run containers on this network:
```
docker run -d --name db --network my-network postgres
docker run -d --name backend --network my-network mybackend
docker run -d --name frontend --network my-network myfrontend
```
- Backend can connect to DB using db:5432 (container name acts as hostname).
- Frontend can connect to Backend using backend:5000.
- No need to use IPs — Docker’s internal DNS resolves container names.

### Example Flow
- Imagine your application:
```
Frontend Container (myfrontend)
       │  HTTP request
       ▼
Backend Container (mybackend)
       │  SQL query
       ▼
Database Container (postgres)
```
- All containers are on my-network.
- Communication uses container names as hostnames.
**Environment variables for backend:**
```
DB_HOST=db
DB_PORT=5432
DB_USER=postgres
DB_PASS=mysecret
```
- Backend reads DB_HOST=db → connects to db container.
**Frontend calling backend:**
```fetch("http://backend:5000/api/data")```
- Frontend container can call backend directly because they are on the same network.
  
### Connecting to External Services
- Containers can still connect to the internet (external APIs) via the host machine.
```fetch("https://api.openweathermap.org/data/2.5/weather")```
- Docker automatically routes outgoing requests through the host’s network.

### Connecting to Host Database
- If your database is running on your host machine, not in a container:
```
DB_HOST=host.docker.internal
DB_PORT=5432
```
- Now your container can connect to the database on your local host machine.
