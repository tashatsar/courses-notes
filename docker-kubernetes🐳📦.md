# [Docker, kubernetes, and openshift course🐳📦](https://www.coursera.org/learn/ibm-containers-docker-kubernetes-openshift/)

👍Pros: 

👎Cons: 

⌚Duration: 

## Introduction

A **container** is a unit of software that encapsulates everything needed to build, ship, and run applications.

Why containers📦:
- lower deployment time and costs
- better utilization
- automate processes
- microservices support
- operating system, programming language, and platform-independent

Major container vendors:
- Docker is a robust platform and the most popular container platform, flexible scaling and portability
- Podman is a daemon-less container engine that is more secure than Docker
- LXC for data-intensive applications and operations
- Vagrant for the highest levels of isolation on the running physical machine

### Docker 📦🚢

Docker: open platform used for developing, shipping, and running applications as containers. Docker containers are **not a good fit** for applications based on monolithic architecture or applications that require high performance or security. 

**Docker architecture**: 
- client (docker build, docker push, docker run)
- host (Dockerfiles, images (copies), containers, networks, storage volumes, and other objects, such as plugins and add-ons)
- container registry (image)

Docker uses networks to isolate container communications. Docker uses volumes and binds mounts to persist data even after a container stops running. Docker container is runnable instance of an image.

Steps used to create and run containers:
1. create a Dockerfile
2. use it to create a container image
3. use the container image to create a running container

## Cheat Sheet: Docker CLI
| Command	| Description |
|-|-|
`curl localhost`	| Pings the application
`docker build` |	Builds an image from a Dockerfile
`docker build . -t` |	Builds the image and tags the image id
`docker CLI` |	Start the Docker command line interface.
`docker container rm` |	Removes a container
`docker images` |	Lists the images
`docker ps` |	Lists the containers
`docker ps -a` |	Lists the containers that ran and exited successfully
`docker pull` |	Pulls the latest image or repository from a registry
`docker push` |	Pushes an image or a repository to a registry
`docker run` |	Runs a command in a new container
`docker run -p` |	Runs the container by publishing the ports
`docker stop` |	Stops one or more running containers
`docker stop $(docker ps -q)` |	Stops all running containers
`docker tag` |	Creates a tag for a target image that refers to a source image
`docker --version` |	Displays the version of the Docker CLI
`exit` |	Closes the terminal session
`export MY_NAMESPACE` |	Exports a namespace as an environment variable
`git clone` |	Clones the git repository that contains the artifacts needed
`ibmcloud cr` | images	Lists images in the IBM Cloud Container Registry
`ibmcloud cr login` |	Logs your local Docker daemon into IBM Cloud Container Registry
`ibmcloud cr namespaces` |	Views the namespaces you have access to
`ibmcloud cr region-set` |	Ensures that you are targeting the region appropriate to your cloud account
`ibmcloud target` |	Provides information about the account you’re targeting
`ibmcloud version` |	Displays the version of the IBM Cloud CLI
