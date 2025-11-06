# **How to use Docker**

Docker is a software that is able to create containers, which can be seen as a lightweight virtual machine, that does not virtualize an entire system but abstract away libraries and software that run on it.  
It initially was only available on Linux based machines but it was then ported to Windows and MacOS.

## **Setting up Docker**

Docker's main usage is based on Linux, and you can find pre-built binaries for the docker basic command line tool, on the following link [https://docs.docker.com/engine/install/](https://docs.docker.com/engine/install/). In case you are on Mac or on Windows, or if you just prefer a good graphical interface, you can install the Docker Desktop, which includes both the engine and the graphical application, and you can find a tutorial for its installation at the following link [https://docs.docker.com/get-started/introduction/get-docker-desktop/](https://docs.docker.com/get-started/introduction/get-docker-desktop/).

## **Working with Docker: Images**

Docker abstracts away the creation of those containers by the use of images. An image is a read-only template that includes all the software and libraries used to define the container. By default, Docker manages a registry of the most used images, called [Docker Hub](https://hub.docker.com/), available to anyone that may want to use them. To download images one can use the command `docker pull`, which will download any image by providing the name from Docker Hub. To manage those downloaded images, you can use the `docker image` command which includes the subcommands `ls` and `rm` respectively to list and remove an image from the system.

```shell
# Download image called image_name with version ver from Docker Hub
docker pull <image_name>:<ver>

docker image ls # List all the downloaded images

docker image rm <image_name> # Remove the image named image_name from the system
```

## **Working with Docker: Containers**

The execution of an image will create a new container, which can be managed by the commands `run`, `ps`, `stop`, `start` and `rm`, which respectively execute a new container, show a list of containers, stop a container, start an existing container, and remove a container.

```shell
# Create a new container base on the image image_name and run it.
docker run <image_name>
# Show all the running docker containers, by adding the -a option you can list also those that are currently stopped
docker ps
# Stop the container identified by container_id
docker stop <container_id>
# Start the previously stopped container container_id
docker start <container_id>
# Remove the container identified by container_id
docker rm <container_id>

```

**NOTE**: The command `docker run` lets you customize how the container is created and run. This is done with the use of the following options:

- `-d`, the container will be detached, which makes the shell usable after the creation of the container  
- `--name name`, this command lets you specify a name for the container, this is useful for simplifying its management and be able to distinguish between different containers created from the same image  
- `-p extern_port:container_port`, map a port that the container listens to, to an external port accessible by the host machine. This can be used when developing applications to access them from outside the container.  
- `-i`, this option makes the container interactive and can be used to debug the behaviour of the container from the inside

## **Working with Docker: Defining new Images**

The main purpose of Docker is not to run any pre-existing images, but the ability to define your own images tailored to the application you are developing.  
To use this feature, you should create a new file called `Dockerfile`, which is used to define the template that will be used to build a new image.  
The main instructions used for the definition of a `Dockerfile` are:

- `FROM image_name:ver`, which specifies the image that will be used as a base for the one you are defining  
- `RUN command`, executes a command to update the content of the image, this is useful when we need to setup the environment  
- `COPY external_directory container_directory`, copies the directory `external_directory` to include it inside the image. The new position of such directory is specified by `container_directory`  
- `WORKDIR directory`, sets up the specified directory as the default one the container will use  
- `CMD [“<executable>”, parameters…]`, this is the last command that will be executed by the docker image, it is usually used to execute the developed application.

Now let’s assume that we have an application created with Python, with the source code contained into the directory `./app`. For this application we want to use an image based on the latest version of Ubuntu available on the Hub and it needs to be run with the command `python3 myapp.py`. We can have a similar `Dockerfile`:

```
# Choose the base image to start the build
FROM ubuntu:latest

# Use RUN to install all the required commands and dependecies
# of the application
RUN apt-get update && apt-get install -y python3 <your_app_dependencies>

COPY . /app

# Set the working directory from which we executes the next instructions
WORKDIR /app

# Define the starting command of the container
CMD ["python3", "myapp.py"]
```

Now that the image is being defined, we need a way to make Docker aware of its existence, and add the image to the list of images. To do this, Docker provides the command `build` which is used to create the new image that we specified in the `Dockerfile`.

```shell
# Creates a new image based on the Dockerfile found in the directory Dockerfile-directory with name:ver as the image identifier
docker build <Dockerfile-directory> -t name:ver
```

**NOTE**: It is not required to specify the `-t` option, but it is recommended to be able to use the image easily.  
