##  What is a Volume?
- A volume is Docker’s way of persisting data outside a container’s lifecycle.
- By default, when a container is deleted → all data inside it is lost.
- Volumes solve this by storing data on the host machine, separate from the container.

## Why use Volumes?
- Data Persistence → Data survives even if the container stops or is removed.
- Sharing Data → Multiple containers can access the same volume.
- Performance → Volumes are optimized for Docker (faster than writing inside containers).
- Separation of Concerns → App runs inside container, data is managed outside

## How To Use Volume
- Create volume - ```docker volume create mydata```
- Run a container with a volume - ```docker run -d -v mydata:/app/data myapp```
- Here mydata = volume on host
- /app/data = path inside container
- List volumes - ```docker volume ls```
- Inspect a volume - ```docker volume inspect mydata```

## Bind Mount 
- A bind mount is a way to mount (attach) a specific file or directory from your host machine into a container.
- You explicitly control what file/folder from your host is mounted and where inside the container it is accessible.
- The container sees the exact same content as on the host. Any change made on the host is visible inside the container and vice versa (two-way sync).
- Useful for development, when you want your container to instantly reflect changes you make to code or configs on your machine.
- ```docker run -v /host/path:/container/path myapp```
- /host/path → directory on your local machine.
- /container/path → location inside the container where it will appear.
- If you change files in /host/path, they update immediately in /container/path inside the container.
### When to use bind mounts:
- During local development (mount your code into the container).
- When you want direct control over which host files are available to the container.
- Tightly coupled to the host’s file system → not portable (your teammate’s machine may not have the same paths).
-  Docker volumes (managed by Docker) are preferred for production, while bind mounts are often used in development.
