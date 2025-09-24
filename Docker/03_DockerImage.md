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
- Run: ```docker build -t myapp:1.0 .```
- It will locate the dockerfile in you current directory and run it to build an image.
- This creates a Docker image called myapp:1.0. My app is the repository for the image whike 1.0, will be the tag referring to the image. A unique image id is attached to it.
- ```docker image ls``` or ```docker images``` will give you a list of all the images linked to your account that you have built.
- To remove a particular image - ```docker rmi myapp:1.0```

## Managing Docker Images
- When you build an image using docker build, Docker stores it on your local machine.
- ```docker images``` shows all the local images.
- Each image has REPOSITORY, TAG, IMAGE ID, CREATED, SIZE.
### What is a repository?
- a storage space for Docker images where you can have multiple versions (tags) of the same image inside a repository.
```
	•	Example:
	•	node → repository
	•	node:18-alpine → specific image (tag/version) in that repository
```
- A repository can be public or private.
- A public repository is where anyone can pull the image for free.
- A private repository is where only authorized users can pull/push. Good for proprietary apps.
- A repositpry lives inside a registry (public / private)
- Namespace groups repositories under a user or organization.
```
	•	Example:
	•	vaishali/myapp:1.0
	•	openai/gpt-app:2.0
	•	Here, vaishali or openai is the namespace.
```
```
Registry (Docker Hub / AWS ECR / Private Registry)
   └── Namespace (user/org)
         └── Repository (image name)
               └── Tags (versions)
```
### Pushing & Pulling Docker Images
- **Pulling an Image**
```docker pull <image-name>:<tag>```
- 	Downloads the image from a registry (like Docker Hub or AWS ECR) to your local machine
- 	use case: Run prebuilt images (databases, programming runtimes, OS images) without building them yourself.
- **Pushing an Image**
- First, you need to build an image locally
```docker build -t vaishali/myapp:1.0 .```
- Login to the registry - ```docker login```
- Push to registry - ```docker push vaishali/myapp:1.0```
- Uploads the image from your local repository to a remote registry.
- Use Case:
    - Share images with team members.
    - Deploy applications to servers or cloud.
    - Store your image versions safely.

