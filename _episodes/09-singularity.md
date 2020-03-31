---
title: "Using Singularity to create and run containers"
teaching: 40
exercises: 30
questions:
- "What is Singularity, why might it be useful and how do I use it?"
objectives:
- "Understand what Singularity is and when you might want to use it."
- "Understand how to run containers using Singularity and how to create them."
keypoints:
- "Singularity is another container platform and it is often used in cluster/HPC/research environments."
- "Singularity has its own container image format (SIF) but it can also run containers directly from Docker Hub."
- "Singularity has a different security model to other container platforms, one of the key reasons that it is well suited to HPC and cluster environments."
---

This section of the course will build on the experience you've gained with Docker and introduce you to another container platform - [Singularity](https://sylabs.io/singularity/) - demonstrating how to set up, use and work Singularity.

> ## Work in progress...
> This section of the course is new material that is under ongoing development. We will introduce singularity and demonstrate how to work with it. As the tools and best practices continue to develop, elements of this material are likely to evolve. We will also aim to add further content to this section of the course and welcome comments/suggestions on how the material can be improved or extended.
{: .callout}

## Singularity

[Singularity](https://sylabs.io/singularity/) is another container platform. In some ways it appears similar to docker from a user perspective, but in others, particularly in the system's architecture, it is fundamentally different. These differences mean that Singularity is particularly well-suited to running on distributed, High Performance Computing (HPC) infrastructure, as well as your laptop or desktop! 

System administrators will not, generally, install Docker on shared computing platforms such as lab desktops, research clusters or HPC platforms because the design of Docker presents potential security issues for shared platforms with multiple users. Singularity, on the other hand, can be run by end-users entirely within "user space", that is, no special administrative privileges need to be assigned to a user in order for them to run and interact with containers on a platform where Singularity has been installed.

## Getting started with Singularity

Initially developed within the research community, Singularity is now made available through [Sylabs.io](https://sylabs.io/). We'll be working with the free, open source [Singularity Community Edition](https://sylabs.io/singularity/). Singularity supports Linux platforms. For the purpose of this session, we'll be leveraging the Docker skills that you've already learnt and running Singularity within a Docker container. This ensures that you can follow this session on a Linux, Mac or Windows platform.


> ## Installing Singularity from source code (optional) \[Advanced task\]
>
> If you are running on a Linux system and would like to run Singularity natively on your system (i.e. not within a Docker container), you can build a [SingularityCE release](https://www.github.com/sylabs/singularity/releases) from source code.
>
> _This is an advanced task that is beyond the scope of this session, and is not required to participate in the session._
> _However, if you have Linux systems knowledge and would like to attempt a local install of Singularity, you can find details in the [INSTALL.md file](https://github.com/sylabs/singularity/blob/master/INSTALL.md) within the Singularity source that explain how to install the prerequisites and build and install the software._
> 
{: .callout}

Singularity containers are stored in a Docker container repository. Instead of using Docker Hub, Singularity containers are distributed through [Quay.io](https://quay.io), an alternative container repository. We can see the list of tags/containers on the [Singularity - Repository Tags](https://quay.io/repository/singularity/singularity?tab=tags) on Quay.io.

We'll begin by pulling the Docker container for the latest version of Singularity. _At the time of writing, this is v3.5.3._

~~~
$ docker pull quay.io/singularity/singularity:v3.5.3
~~~
{: .language-bash}

~~~
v3.5.3: Pulling from singularity/singularity
4167d3e14976: Pull complete 
... (additional lines truncated)
6c16b46e7b9f: Pull complete 
Digest: sha256:14c0705bda549b28ea604c7de17f2dc063c35d82be850f0b508a39a07912a3bf
Status: Downloaded newer image for quay.io/singularity/singularity:v3.5.3
quay.io/singularity/singularity:v3.5.3
~~~
{: .output}

If you recall from learning about Docker, the above output says that Docker has pulled the various _layers_ that make up the Docker image containing Singularity v3.5.3 into the local container repository on your system. You can see that the image is available by looking at the list of docker images on your system:

~~~
$ docker image ls
~~~
{: .language-bash}
~~~
REPOSITORY                           TAG                      IMAGE ID            CREATED             SIZE
quay.io/singularity/singularity      v3.5.3                   fb8d1bd5b4e7        5 weeks ago         966MB
~~~
{: .output}

Using the same approach demonstrated in the _[Creating containers](/03-creating-containers/index.html)_ section of the course, we'll now run a container based on the Singularity image and open a shell within the container so we can proceed with learning about Singularity. Note that in addition to the two flags used previously, we add a couple of additional flags:

   - `-t` flag:           Allocate a psuedo-tty to allow us to access the container interactively
   - `-d` flag:           Detach the container and run in the background
   - `--privileged` flag: Allow the container to have enhanced system access privileges
   - `--entrypoint` flag: Override the default entrypoint for the container to instead run a shell
   - `--name` flag:       Assign a name to the container to make it easier to reference in subsequent commands

~~~
$ docker run -t -d --privileged --entrypoint /bin/bash --name singularity quay.io/singularity/singularity:v3.5.3
~~~
{: .language-bash}

Note that the use of the `--name` flag in the `docker run` command above means that our running container has the name _"singularity"_ rather than a container name autogenerated by Docker. The `--privileged` flag is required to ensure that Singularity has sufficient privileges to run within the Docker container.

Also note the `--entrypoint` flag that was used when starting the container. This flag overrides any pre-configured container entrypoint. The entrypoint is the executable that the container is configured to run by default. For this container, it is `/usr/local/bin/singularity`. Therefore, if we don't override the entry point, when the `docker run` command is issued, the container starts, runs the `singularity` command and, without any additional parameters, the command exits straight away, causing the container to exit. We override the original entrypoint, directing the container to start a bash shell on startup instead. This ensures that the container remains in a running state and we can interact with it.

We can verify that the container has started successfully and is running with the `docker ps -a` command (or `docker container ls`):

~~~
$ docker container ls
~~~
{: .language-bash}
~~~
CONTAINER ID        IMAGE                                    COMMAND                  CREATED             STATUS              PORTS                                                                                 NAMES
2e373f5e7050        quay.io/singularity/singularity:v3.5.3   "/bin/bash"              3 minutes ago       Up 3 minutes                                                                                              singularity
~~~
{: .output}

For the purposes of this lesson, we'll use the `docker exec` command to start another bash shell within the container that we can connect to and interact with to work with singularity in the subsequent parts of this lesson. To do this, run the following command:

~~~
$ docker exec -i -t singularity /bin/bash
~~~
{: .language-bash}
~~~
bash-5.0# 
~~~
{: .output}


More about singularity!

