# learn-docker
These are my notes from learning Docker and its commands

### Introduction
- Solves for matrix hell in development environments
- Containers are completely isolated environments like VMs except they share the underlying OS kernel
- Docker can run software which share the same underlying kernel
- So Windows cannot be run in Linux OS. 
- When we run a Linux container in Windows we use WSL, which runs Linux on Windows
- Docker has less isolation; while VMs have complete isolation
- Container are running instances of Docker images
- Docker images are templates with packages

### Commands
- docker run - will run an image. If not present, it'll pull and then run
- docker ps - list all the containers running locally. 
	- docker ps -a - shows all exited and running containers
- docker stop - stop a container command. Provide an id or container name
- docker rm - remove a stopped or exited container permanently
- docker images - list all the docker images downloaded locally
- docker rmi - Remove an image. The image to be removed must be stopped and deleted'
- docker pull - docker pull will download an image
- Containers are not meant to be run OSes. They are designed to run a specific task. Once the task is complete, it'll exit. This is why if we run ubuntu, it exits immediately
- docker exec - Execute a command on a running container
- docker run runs in the foreground and is attached to the container. It'll not listen to any other commands
- docker run -d - Runs in detached mode and runs the container in background mode
- docker attach - Run the background container as a foreground from background

docker run tag:
- docker run redis:4.0 - 4.0 is the tag. If tag is not given, then latest is use, which is the latest version

docker run stdin: 
- docker run -i : runs in interactive mode
- Need to attach to the prompts terminal
- So command will become: docker run -it - attaches to the current terminal

Map ports:
- use -p to map port in host to that of docker
	- docker run -p 80:5000 kodekloud/webapp
	- It is of the format localPort:containerPort

Persistence of data in docker:
- Each docker container has its own isolated file system
- If we delete the container, the data inside the container is also thrown away
- If we want to persist the data, we need to map to the host volume to that of the container:
	- Use -v
		- docker run -v /opt/datadir:/var/lib/mysql mysql

Docker inspect:
- returns the details of the container

Container logs:
- docker logs <container_id>

Detached and attached mode:
- -d to run as detached
- docker attach <id> to attach to a container

Creating your own image
- Create your own Dockerfile
- Build your image using the docker build command
	- docker build Dockerfile -t <tag>
- Push the image to the registry
	- docker push

Dockerfile:
- Text file written in a specific format with the format:
	Instruction Argument
- Everything on the left is an instruction
	- Example: FROM, RUN, COPY, ENTRYPOINT, EXPOSE, VOLUME, WORKDIR, CMD
	- Every Dockerfile is based on a base image of an OS, or another image created before based on an OS
	- RUN runs a command in the docker image
- Docker builds a instruction using a layered architecture
	- Each layer stores the changes from the previous layer and this reflects in the size of the image
	- All layers built are cached, docker build will reuse the layer from the cache and continue
	- This way rebuilding an image is faster
	- Example with tag:
		-docker build . -t <account_name>/<application_name>
- docker login first to push.
	- Use the command: docker login

Pass env variable: 
- docker run -e APP_COLOR=blue simple-webapp-color
- Inspect env variable of a container:
	- use docker inspect
		- Check the config section

Entrypoint in Dockerfile:
- CMD ["command", "param"]
- ENTRYPOINT is like command which will run when the container starts
	- ENTRYPOINT ["sleep"]
- To override the ENTRYPOINT use --entrypoint argument 
