## What is a Dockerfile?
- a text file that contains a set of instructions to build a Docker image.
- it tells Docker what base OS to use, what files to copy, what commands to run, and what to execute when the container starts.

### Thing to note
- Text file named Dockerfile (no extension)
- Used by ```docker build``` command to create an image
- Each line is an instruction → builds a layer in the Docker image
- Helps automate container setup → no manual installation needed

##  Example Dockerfile (Node.js App)
- Create this file in your project root.
```
# Start from a base Node.js image
FROM node:18-alpine

# Set working directory
WORKDIR /app

# Copy package.json and install dependencies
COPY package*.json ./
RUN npm install

# Copy the rest of the app
COPY . .

# Expose port
EXPOSE 3000

# Command to run the app
CMD ["npm", "start"]
```
- Flow:
  - Docker reads the file line by line → creates layers for the image
	- Builds a ready-to-run image
	- Run docker run myapp → container starts with all dependencies pre-installed
 
 ## .dockerignore
 - we mention all the files here, that we do not want to be included in our image

