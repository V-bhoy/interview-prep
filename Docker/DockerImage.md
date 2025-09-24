## What is a docker image?
- A Docker image is a read-only template used to create Docker containers.
- Think of it as a blueprint or snapshot of an environment that contains:
   - Application code
   - Runtime (like Node.js, Python, Java)
   - Libraries and dependencies
   - OS-level files needed to run the app
- Containers are created from images.

### Things to note:
- Immutable – Once built, an image does not change.
- Portable – Can run anywhere Docker is installed (your laptop, server, or cloud).
- Layered – Each instruction in a Dockerfile (FROM, COPY, RUN) creates a layer, which makes images lightweight and reusable.
- Versioned – Images can have tags (like node:18-alpine or myapp:v1).

## How it works?
- You write a Dockerfile (instructions to build the image).
- Run: ```docker build -t myapp:1.0```. You can also do ```docker build .``` It will locate the dockerfile in you current directory and run it to build an image.
- This creates a Docker image called myapp:1.0.
- ```docker image ls``` will give you a list of all the images linked to your account that you have built.
