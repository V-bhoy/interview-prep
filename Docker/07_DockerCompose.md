## What is docker compose?
- Docker Compose is a tool that lets you define and run multi-container Docker applications using a single YAML file (docker-compose.yml).
- It allows you to describe all services, networks, and volumes your application needs in one place.

## Advantages
### Simplifies multi-container setup
- Instead of running multiple docker run commands manually for each container, you define them in a file.
- Example: frontend, backend, and database services all in one file.
### Manages networks and volumes automatically
- Compose creates a custom network so containers can communicate easily by name.
- olumes can be defined and shared across containers.
### Easier environment management
- You can pass environment variables and configuration in the YAML file.
- Makes development, staging, and production setups consistent.
### Single command to manage everything
- Start all containers: ```docker-compose up -d```
- 	Stop all containers: ```docker-compose down```

## Example
```
version: "3.9"
services:
  db:
    image: postgres:15
    environment:
      POSTGRES_USER: user
      POSTGRES_PASSWORD: password
    volumes:
      - db-data:/var/lib/postgresql/data

  backend:
    image: mybackend
    ports:
      - "5000:5000"
    environment:
      DB_HOST: db
      DB_PORT: 5432
    depends_on:
      - db

  frontend:
    image: myfrontend
    ports:
      - "3000:3000"
    depends_on:
      - backend

volumes:
  db-data:
```
- Starts 3 containers (frontend, backend, database).
- Sets up a network automatically.
- Connects backend → db using container name.
- Exposes ports for host access.

## Startup vs Readiness
- When we say “depends_on ensures startup order,” it only means: Container A will start before Container B, doesn’t mean Container A is ready to serve requests.
### Example
- Take a Postgres DB container: The container process starts almost immediately.
- But Postgres takes a few seconds to initialize the database files and start accepting connections.
- So, from Docker’s perspective: Container is running. But it’s not ready (your app might fail to connect if it tries too soon).
- This difference between running and ready is what we mean by actual readiness.
### How to Handle Readiness
- You can use a healthcheck in docker-compose.yml
```
version: "3.9"
services:
  db:
    image: postgres:15
    environment:
      POSTGRES_USER: user
      POSTGRES_PASSWORD: pass
      POSTGRES_DB: mydb
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U user"]
      interval: 10s
      timeout: 5s
      retries: 5
      start_period: 5s

  app:
    build: .
    depends_on:
      db:
        condition: service_healthy
```
- healthcheck: Runs the command pg_isready -U user inside the DB container until Postgres is accepting connections.
- depends_on with condition: service_healthy: Ensures app will only start after the DB container is healthy (ready for connections).
- depends_on only → Order is guaranteed, but readiness isn’t.
- depends_on + healthcheck → Order and readiness both ensured.
