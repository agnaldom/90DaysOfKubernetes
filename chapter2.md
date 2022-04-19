# Chapeter 2. Creating and Running Containers

Kubernetes is a platform for creating deploying, and managing distributed applications.

In #Chapter 1, we argued strongly for the value of immutable images and infrastructure. This immutability is exactly what the continer image provides. As we will see, it easily solves all the problems of dependency management and encapsulation just decribed.

Contianer images bundle a program and its dependencies into a single artifact unde a root filesystem. The most popular continaer image format is the Docker image format, which has been standardized bu the Open Container Initiative to the OCI image format. Kubernetes supports both Docker- and OCI-compartible images via Docker and other runtimes. Docker images also include additional metadata used by a container runtime to start a running application instance based on the contents os the container image.

## Contianer Images

For nearly everyone, their firts interaction with any container technology is with a container image. A container image is a binary package that encapsulates all of the files necessary to run a program inside of an OS container.

## The Docker Image Format

The most popular and widespread container image format is the Docker image format, which was developed by the Docker open source project for packaging, distributing, and running containers using the docker commang. Subsequently, work has begun by Docker, Inc., and others to standardize the container image format via the Open Container Initiative (OCI) project. The Docker image format continues to be the facto standard, and is made up of a series of filesystem layers. Each layer adds, removes, or modifies files from the preceding layer in the filesystem. 

Containers fall into two main categories:

* System containers
* Application containers

## Building Application Images with Docker

In general, container orchestration system like Kubernetes are focused on building and deploying distributed systems made up of application containers.

### Dockerfiles

A Dockerfile can be used to automate the creation of a Docker container image.

Let's start by building an application image for a simple Node.js program.

1. Every Dockerfile builds on other container images. This line specifies that we are starting from the node:10 image on the Docker Hub. This is a preconfigured image with Node.js 10.
2. This line sets the work directory, in the container image for all follwing commands.
3. These two lines initialize the dependencies for Node.js. First we copy the package files into the image. This will include package.json and package-lock.jso. The RUN command then runs the correct command in the container to install the necessary dependencies.
4. Now we copy the rest of the program files into the image. This will include everything except node_modules, as that is excluded via the .dockerignore file.
5. Finally, we specify the command that should be run when the container is run.

Run the followinf command to create the simpe-node Docker image:

``` $ docker build -t simple-node .```

When you want to run this image, you can do it with the following command. You can navigate to http://localhost:3000 to access the program running in the container:

```$ docker run --rm -p 3000:3000 simple-node```

### Image Security

When it comes to security, there are no shortcuts. When building images that will ultimately run in a production Kubernetes cluster, be sure to follow best practives for packaging and distributing applications. For example, don't build containers with passwords baked in - and this includes not just in the final layer, but any layers int the image. One of the counterintuitive problems introduced by container layers is that deleting a file in one layer doesn;t delete that file from preceding layers. It still takes up spaces, and it can be attacker can simplete an image that only consists of the layers that contain the password.

Secrets and images should never be mixed. If you do so, you will be hacked, and you will bring shame to your entire company or department.

### Multistage Image Builds