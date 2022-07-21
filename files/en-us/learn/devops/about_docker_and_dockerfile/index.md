---
title: Introduction About Docker and Dockerfile
slug: Learn/DevOps/About_Docker_and_Dockerfile
tags:
  - Docker
  - Dockerfile
  - docker tutorial
  - docker build
---
{{LearnSidebar}}


**What is Docker?**

Docker is a configuration management tool that is used to automate the
deployment of software in lightweight containers. These containers help
applications to work efficiently in different environments.

> **Note:**
>
> A Docker Image is a template of instructions used to create containers.

Installation & Configuration of Docker
======================================

Before you install Docker Engine for the first time on a new host
machine, you need to set up the Docker repository. Afterward, you can
install and update Docker from the repository.

CentOS
------

### Set up the repository

Install the yum-utils package (which provides the yum-config-manager
utility) and set up the repository.

``` {.console}
$ sudo yum install -y yum-utils
$ sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo
```

### Install Docker Engine

Install the latest version of Docker Engine, containerd, and Docker
Compose.

``` {.console}
$ yum install docker-ce docker-ce-cli containerd.io docker-compose-plugin
```

Debian
------

### Set up the repository

1.Update the apt package index and install packages to allow apt to use
a repository over HTTPS:

``` {.console}
$ sudo apt-get update

$ sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
```

2.  Add Docker's official GPG key:

``` {.console}
$ sudo mkdir -p /etc/apt/keyrings

$ curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

3.  Use the following command to set up the repository:

``` {.console}
$ echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

### Install Docker Engine

Update the apt package index, and install the latest version of Docker
Engine, containerd, and Docker Compose.

``` {.console}
$ sudo apt-get update
$ sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
```

Dockerfile
==========

**What is a Dockerfile?**

Before we discuss what is a Dockerfile, it is important to know what a
Docker image is. Docker Image:

A Docker Image is a read-only file with a bunch of instructions. When
these instructions are executed, it creates a Docker container.
Dockerfile:

Dockerfile is a simple text file that consists of instructions to build
Docker images.

Mentioned below is the syntax of a Dockerfile:

**Syntax**

    # comments

    command argument argument1...

**Example**

``` {.docker}
# Print "Get Certified. Get Ahead"

Run echo "Get Certified. Get Ahead"
```

Now, let's have a look at how to build a Docker image using a
dockerfile.

List of Docker Commands for Creating a Dockerfile
-------------------------------------------------

Before we create our first Dockerfile, it is important to understand
what makes up the file.

Dockerfile consists of specific commands that guide you on how to build
a specific Docker image.

The specific commands you can use in a dockerfile are:

**FROM**, **PULL**, **RUN**, and **CMD**

-   **FROM** - Creates a layer from the ubuntu:18.04
-   **PULL** - Adds files from your Docker repository
-   **RUN** - Builds your container
-   **CMD** - Specifies what command to run within the container

Mentioned below is an example of the dockerfile with the important
commands

``` {.docker}
FROM ubuntu:18.04

PULL . /file

RUN make /file

CMD python /file/file.py
```

Moving forward, let's go through some of the most common Docker commands
used while creating dockerfiles. Along with the syntax, we are
explaining the commands with examples, so you can start experimenting
with them right away.

-   **ENTRYPOINT** allows specifying a command along with the parameters

``` {.docker}
# Syntax
ENTRYPOINT application "arg, arg1".
# Example
ENTRYPOINT echo "Hello, $name".
```

-   **ADD** command helps in copying data into a Docker image

``` {.docker}
# Syntax
ADD [source] [destination]
# Example
ADD . /home
```

-   **ENV** provides default values for variables that can be accessed
    within the container

``` {.docker}
# Syntax
ENV key=value
# Example
ENV DEBIAN_FRONTEND=noninteractive
```

-   **MAINTAINER** declares the author field of the images

``` {.docker}
# Syntax
MAINTAINER [name]
# Example
MAINTAINER author_name
```

How to Build a Docker Image and Docker Container Using Dockerfile?
------------------------------------------------------------------

First of all, you should create a directory in order to store all the
Docker images you build.

1.  Now, we will create a directory named 'simpledocker' with the
    command:

``` {.console}
$ mkdir simpledocker
```

2.  Move Docker image into that directory and create a new empty file
    (Dockerfile) in it:

``` {.console}
$ cd simpledocker
$ touch Dockerfile
```

3.  Open the file with the editor. In this example, we opened the file
    using vi:

``` {.console}
$ vi Dockerfile
```

4.  Then, add the following content:

``` {.docker}
FROM ubuntu

MAINTAINER simple

RUN apt-get update

CMD ["echo", "Welcome to Simple-learn"]
```

5.  Save and exit the file.

Now, let's build a basic image using a Dockerfile:

``` {.console}
$ docker build [location of your dockerfile]
```

Now, by adding -t flag, the new image can be tagged with a name:

``` {.console}
$ docker build -t simple_image
```

Once the Docker image is created, you can verify by executing the
command:

``` {.console}
$ docker images
```

Create a New Container
----------------------

Now, create a Docker container from the Docker image we created in the
previous step.

Let's name the container "simplelearn" and create it with the command:

``` {.console}
$ docker run --name simplelearn simple_docker
```

The message 'Welcome to Simplelearn' should appear in the command line,
as seen in the image above.
