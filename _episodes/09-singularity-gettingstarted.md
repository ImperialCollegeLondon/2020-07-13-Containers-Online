---
title: "Using Singularity to create and run containers: Getting started"
teaching: 20
exercises: 10
questions:
- "What is Singularity and why might it be useful to me?"
- "What is a Singularity container and how do I run one?"
- "What is a Singularity image?"
objectives:
- "Understand what Singularity is and when you might want to use it."
- "Undertake your first run of a simple Singularity container."
keypoints:
- "Singularity is another container platform and it is often used in cluster/HPC/research environments."
- "Singularity has a different security model to other container platforms, one of the key reasons that it is well suited to HPC and cluster environments."
---

***** Add something about terminology - image vs. container *******

This section of the course on Singularity will build on the experience you've gained with Docker and introduce you to another container platform - [Singularity](https://sylabs.io/singularity/) - demonstrating how to set up, use and work with Singularity.

The Singularity material comprises 4 episodes 

> ## Prerequisites _(to be added to the main course setup information??)_
> There are two sections to this part of the course, both have slightly different requirements:
>
> **Part I:**
> - Access a local or remote platform with Singularity pre-installed and accessible to you as a user (i.e. no administrator/root access required).
>   - If you are attending a taught version of this material, it is expected that the course organisers will provide access to a platform (e.g. an institutional HPC cluster) that you can use for the first section of this material.
>
> **Part II:**
> - Access to a local or remote Linux-based system on which you have administrator (root) access and can install the Singularity software.
>
>      OR
>
> - Access to a non-Linux system on which you have administrator (root) access and can install the the VirtualBox virtualisation software under which you can run a Linux virtual machine and install Singularity.
>
> If you have a suitable environment set up for Part II, this could also be used for Part I.
{: .prereq}

> ## Work in progress...
> This section of the course is new material that is under ongoing development. We will introduce singularity and demonstrate how to work with it. As the tools and best practices continue to develop, elements of this material are likely to evolve. We will also aim to add further content to this section of the course and welcome comments/suggestions on how the material can be improved or extended.
{: .callout}

# Singularity - Part I

## What is Singularity?

[Singularity](https://sylabs.io/singularity/) is another container platform. In some ways it appears similar to docker from a user perspective, but in others, particularly in the system's architecture, it is fundamentally different. These differences mean that Singularity is particularly well-suited to running on distributed, High Performance Computing (HPC) infrastructure, as well as your laptop or desktop! 

System administrators will not, generally, install Docker on shared computing platforms such as lab desktops, research clusters or HPC platforms because the design of Docker presents potential security issues for shared platforms with multiple users. Singularity, on the other hand, can be run by end-users entirely within "user space", that is, no special administrative privileges need to be assigned to a user in order for them to run and interact with containers on a platform where Singularity has been installed.

## Getting started with Singularity
[EDIT]*
Initially developed within the research community, Singularity is now made available through [Sylabs.io](https://sylabs.io/). For Part I of this lesson we'll be working with Singularity directly on a High Performance Computing (HPC) cluster that has the software pre-installed. You will have been provided with details to access the cluster. 

> ## Installing Singularity on your local system (optional) \[Advanced task\]
>
> If you are running Linux and would like to run Singularity locally on your system, Singularity provide the free, open source [Singularity Community Edition](https://sylabs.io/singularity/). You will need to install various dependencies on your system and then build Singularity from source code.
>
> _A local installation of Singularity will be useful for Part II of the session. However, you can still learn from the material in Part II without having a local Singularity installation on your system. The installation process is an advanced task that is beyond the scope of this session.
> However, if you have Linux systems knowledge and would like to attempt a local install of Singularity, you can find details in the [INSTALL.md file](https://github.com/sylabs/singularity/blob/master/INSTALL.md) within the Singularity source that explain how to install the prerequisites and build and install the software._
> 
> Singularity also provide a Docker container which enables you to use Docker to run Singularity on other platforms that support Docker. The Singularity Docker container can be pulled from [https://quay.io/repository/singularity/singularity](https://quay.io/repository/singularity/singularity). Use of this container is, again, beyond the scope of this course but once you understand the basics of working with Singularity, this is something you may choose to explore if you wish to experiment with Singularity on your local system.
{: .callout}

Sign in to the HPC cluster, with Singularity installed, that you've been provided with access to. Check that the `singularity` command is available in your terminal:

~~~
$ singularity --version
~~~
{: .language-bash}

~~~
singularity version 3.5.3
~~~
{: .output}

Depending on the version of Singularity installed on your system, you may see a different version. At the time of writing, `v3.5.3` is the latest release of Singularity.

## Accessing and running a Singularity image

If you recall from learning about Docker, Docker images are formed of a set of _layers_ that make up the complete image. When you pull a Docker image from Docker Hub, you see the different layers being downloaded to your system. They are stored in your local Docker repository on your system and you can see details of the available images using the docker command.

Handling of images is a little different in Singularity. Singularity uses the [Signularity Image Format (SIF)](https://github.com/sylabs/sif) and images are provided as single `SIF` files. Singularity images can be pulled from [Singularity Hub](https://singularity-hub.org/). Singularity is also capable of running containers based on images pulled from [Docker Hub](https://hub.docker.com/), we'll look at this later in the lesson.

> ## Singularity Hub
> Note that in addition to providing a repository that you can pull images from, [Singularity Hub](https://singularity-hub.org/) can also build Singularity images for you from a `recipe` - a configuration file defining the steps to build an image. We'll look at recipes and building images later in this lesson.
{: .callout}

Let's begin by creating a `test` directory, changing into it and _pulling_ a test _Hello World_ image from Singularity Hub:

~~~
$ mkdir test
$ cd test
$ singularity pull hello-world.sif shub://vsoch/hello-world
~~~
{: .language-bash}

~~~
INFO:    Downloading shub image
 59.75 MiB / 59.75 MiB [===============================================================================================================] 100.00% 52.03 MiB/s 1s
~~~
{: .output}

What just happened?! We pulled a SIF image from Singularity Hub and asked the `singularity pull` command to store the image file using the name `hello-world.sif`. If you run the `ls` command, you should see this file in your current directory. This is our image and we can now run a container based on this image:

~~~
$ singularity run hello-world.sif
~~~
{: .language-bash}

~~~
RaawwWWWWWRRRR!! Avocado!
~~~
{: .output}

The above command ran the _hello-world_ container from the image we downloaded from Singularity Hub and the resulting output was shown. 


How do we know what command was initiated when we ran the container resulting in this output? We can inspect the image's run script using the `singularity inspect` command:

~~~
$ singularity inspect -r hello-world.sif
~~~
{: .language-bash}

~~~
#!/bin/sh 

exec /bin/bash /rawr.sh

~~~
{: .output}

This shows us the script within the `hello-world.sif` image configured to run by default when we use the `singularity run` command. 