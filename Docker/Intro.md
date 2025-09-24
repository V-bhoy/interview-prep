## What is a docker?
- containerization platfom for developing, packaging, shipping and running applications.

## Why docker?
- Before Docker, developers faced a big problem:
   - “It works on my machine” issue → An app might work on your laptop but fail on another machine because of differences in OS, dependencies, or configuration.
	 - Setting up environments was slow, manual, and error-prone → You had to install libraries, databases, and dependencies manually.
	 - Virtual Machines (VMs) were a solution, but they are heavy (each VM runs a full operating system) and slow to start.
- So, there was a need for something lightweight, portable, and consistent → That’s where Docker (2013) came in.

## What docker does?
- provides the ability to run an application in a isolated environment called container
- Docker uses containers to package an application with everything it needs (code, libraries, configs, runtime).
   - This makes the app portable → You can run it anywhere (your laptop, a server, cloud).
	 - Containers are lightweight → Unlike VMs, they share the host OS kernel, so they start in milliseconds.
   - makes deployment and devlopment efficient
 
## Benefits
### Consistency across environments
- “Works on my machine” → solved.
- App behaves the same on dev, test, and production.
### Portability
- Package once, run anywhere (Linux, Windows, Cloud, AWS, GCP, Azure, etc.).
### Faster development & deployment
- Containers start quickly (seconds, not minutes).
- Easy to spin up multiple environments.
### Isolation
- Each app runs in its own container, no conflicts (e.g., two apps needing different Node.js versions).
### Microservices-friendly
- Perfect for modern architectures where each service (API, DB, frontend) runs in its own container.
### Resource efficiency
- Much lighter than VMs → better performance on the same hardware.
 
## Docker Architecture
- Docker follows a client–server architecture.
- It has 3 main parts:
  - Docker Client (what you interact with)
	- Docker Daemon (dockerd) (the brain that runs containers)
	- Docker Objects (images, containers, volumes, networks)
### Docker Client (CLI or API)
  - This is what you use when you type commands like docker run, docker build.
	- It talks to the Docker Daemon using REST API over UNIX socket or network.
### Docker Daemon (dockerd)
  - Runs in the background.
	- Responsible for building, running, and managing Docker objects.
  - It listens for requests from the client and does the heavy lifting (like creating containers, pulling images).
### Docker Objects
  - These are the building blocks:
      - Dockerfile - simple text file with instructions to build an image
      - Image → A read-only template with instructions of all deoendencies and libraries to run the program (like Node.js base image).
      - Container → A running instance of an image.
      - Volume → For persisting data.
      - Network → To allow communication between containers.
###  Docker Registries
- cetral repository where images are stored.
- Default is Docker Hub, but companies often use private registries.
- Workflow:
  - docker pull image → download from registry
	- docker push image → upload to registry
```
          +-------------------------+
          |       Docker CLI        |
          |  (docker commands / API)|
          +-----------+-------------+
                      |
                      v
          +-------------------------+
          |     Docker Daemon       |
          |   (dockerd - server)    |
          +----+-------------+------+
               |             |
               v             v
      +---------------+   +----------------+
      | Docker Images |   | Docker Volumes |
      +---------------+   +----------------+
               |
               v
      +-----------------+
      | Docker Container|
      +-----------------+
               |
               v
        Application Running

How It Works (Flow Example)
	1.	You run: docker run node:18-alpine
	2.	Client sends request to daemon.
	3.	Daemon checks if image is available locally. If not → pulls it from registry.
	4.	Daemon creates a container from the image.
	5.	Container runs the application in an isolated environment.
```
## How Docker differs from VMs?
### VM
- A Virtual Machine is like creating a computer inside your computer.
- It uses a hypervisor (software like VMware, VirtualBox, Hyper-V) to divide your system’s CPU, RAM, and storage into parts.
- Each VM runs a full operating system (Windows, Linux, etc.) on top of your actual machine. That makes it heavy (uses a lot of memory, storage, CPU).
- Inside that OS, you can install and run applications just like on a normal computer.
- Starting it is slow (like turning on a full computer).
- performance is slow due to hypervisor overhead
- Stronger isolation (completely separate OS)
- Resource-heavy (CPU, RAM, Disk overhead)
- Use-case: Running multiple OSs, strong isolation, legacy apps
### Docker
- Instead of creating a whole new computer, Docker just makes a separate room inside your existing computer.
- It shares the same operating system but gives each app its own little space, no separate OS needed
- That makes it lightweight (uses very little memory and storage).
- Starting it is fast (just seconds).
- Process-level isolation (secure enough, but shares kernel)
- Efficient, uses fewer resources
- Microservices, CI/CD, fast deployments
```
VM Approach                                         
+----------------------------+                      
|     Hardware               |
+----------------------------+
| Hypervisor (VMware, etc.)  |
+----------------------------+
| Guest OS | Guest OS | Guest OS |
|   App    |   App    |   App    |

Docker Approach
+----------------------------+
|     Hardware               |
+----------------------------+
|   Host OS Kernel           |
+----------------------------+
|   Docker Engine            |
+----------------------------+
| Container | Container | Container |
|   App     |   App     |   App     |

In short:
- Docker is lightweight, faster, and portable, great for microservices and DevOps.
- VMs are heavier but more secure, better when you need to run multiple OSs or very strong isolation.
```
## Docker inside a VM (Real-World Scenario)
### Why run Docker inside a VM?
- Most cloud providers (AWS, Azure, GCP) give you VMs as the basic compute unit.
- Docker itself needs a host OS to run on.
- So, you often run Docker inside a VM instead of directly on physical hardware.
### Benefits:
- Combines isolation of VMs with lightweight containers.
- You can run multiple Docker containers on one VM.
- Easy to move the VM to another server or cloud → your containers move with it.
### How It Works?
```
+------------------------+
|      Physical Server    |
+------------------------+
|        Hypervisor       |
+------------------------+
|        VM #1            |
|   +------------------+  |
|   |   Host OS         |  |
|   |   Docker Engine   |  |
|   | +--------------+ |  |
|   | | Container 1  | |  |
|   | | Container 2  | |  |
|   | +--------------+ |  |
+------------------------+
|        VM #2            |
|   ...                   |
+------------------------+
	•	Physical server: Your actual hardware.
	•	Hypervisor: Creates VMs.
	•	VM: Each VM has its own OS.
	•	Docker Engine inside VM: Runs multiple containers.
	•	Containers: Lightweight apps running inside VM.

Key Points
	•	VM provides hardware-level isolation.
	•	Docker provides app-level isolation.
	•	Together: safe, portable, and efficient.
```

