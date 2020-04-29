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

This section of the course will build on the experience you've gained with Docker and introduce you to another container platform - [Singularity](https://sylabs.io/singularity/) - demonstrating how to set up, use and work with Singularity.

> ## Prerequisites _(to be added to the main course setup information??)_
> There are two sections to this part of the course, both have slightly different requirements:
>
> **Part I:**
> - Access a local or remote platform with Singularity pre-installed and accessible to you as a user
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
Initially developed within the research community, Singularity is now made available through [Sylabs.io](https://sylabs.io/). We'll be working with Singularity directly on a High Performance Computing (HPC) cluster that has the software pre-installed. You will have been provided with details to access the cluster. 

> ## Installing Singularity on your local system (optional) \[Advanced task\]
>
> If you are running Linux and would like to run Singularity locally on your system, Singularity provide the free, open source [Singularity Community Edition](https://sylabs.io/singularity/). You will need to install various dependencies on your system and then build Singularity from source code.
>
> _This is an advanced task that is beyond the scope of this session, and is not required to participate in the session._
> _However, if you have Linux systems knowledge and would like to attempt a local install of Singularity, you can find details in the [INSTALL.md file](https://github.com/sylabs/singularity/blob/master/INSTALL.md) within the Singularity source that explain how to install the prerequisites and build and install the software._
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

If you recall from learning about Docker, Docker images are formed of a set of _layers_ that make up the complete image. When you pull a Docker image from Docker Hub, you see the different layers being downloaded to your system. They are stored in your local repository on your system and you can see details of the available images using the docker command.

Handling of images is a little different in Singularity. Singularity uses the [Signularity Image Format (SIF)](https://github.com/sylabs/sif) and images are provided as single `SIF` files. Singularity images can be pulled from [Singularity Hub](https://singularity-hub.org/). Singularity is also capable of running containers based on images pulled from [Docker Hub](https://hub.docker.com/), we'll look at this later in the lesson.

> ## Singularity Hub
> Note that in addition to providing a repository that you can pull images from, [Singularity Hub](https://singularity-hub.org/) can also build Singularity images for you from a `recipe` - a configuration file defining the steps to build an image. We'll look at recipes and building images later in this lesson.
{: .callout}

Let's begin by creating a `test` directory, changing into it and pulling a test _Hello World_ image from Singularity Hub:

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

## Singularity's image cache

While singularity doesn't have a local image repository in the same way as Docker, it does cache downloaded image files. Images are simply `.sif` files stored on your local disk. 

If you delete a local `.sif` image that you have pulled from a remote image repository and then pull it again, if the image is unchanged from the version you previously pulled, you will be given a copy of the image file from your local cache rather than the image being downloaded again from the remote source. This removes unnecessary network transfers and is particularly useful for large images which may take some time to transfer over the network. To demonstrate this, remove the `hello-world.sif` file stored in your `test` directory and then issue the `pull` command again:

~~~
$ rm hello-world.sif
$ singularity pull hello-world.sif shub://vsoch/hello-world
~~~
{: .language-bash}

~~~
INFO:    Use image from cache
~~~
{: .output}

As we can see in the above output, the image has been returned from the cache and we don't see the output that we saw previously showing the image being downloaded from Singularity Hub.

How do we know what is stored in the local cache? We can find out using the `singularity cache` command:

~~~
$ singularity cache list
~~~
{: .language-bash}

~~~
There are 1 container file(s) using 62.65 MB and 0 oci blob file(s) using 0.00 kB of space
Total space used: 62.65 MB
~~~
{: .output}

This tells us how many container files are stored in the cache and how much disk space the cache is using but it doesn't tell us _what_ is actually being stored. To find out more information we can add the `-v` verbose flag to the `list` command:

~~~
$ singularity cache list -v
~~~
{: .language-bash}

~~~
NAME                     DATE CREATED           SIZE             TYPE
hello-world_latest.sif   2020-04-03 13:20:44    62.65 MB         shub

There are 1 container file(s) using 62.65 MB and 0 oci blob file(s) using 0.00 kB of space
Total space used: 62.65 MB
~~~
{: .output}

This provides us with some more useful information about the actual images stored in the cache. In the `TYPE` column we can see that our image type is `shub` because it's a `SIF` image that has been pulled from Singularity Hub. 

> ## Cleaning the Singularity image cache
> We can remove images from the cache using the `singularity cache clean` command. Running the command without any options will display a warning and ask you to confirm that you want to remove everything from your cache.
>
> You can also remove specific images or all images of a particular type. Look at the output of `singularity cache clean --help` for more information.
{: .callout}

## Running specific commands within a container

We saw earlier that we can use the `singularity inspect` command to see the run script that a container is configured to run by default. What if we want to run a different command within a container, or we want to open a shell within a container that we can interact with?

If we know the path of an executable that we want to run within a container, we can use the `singularity exec` command. For example, using the `hello-world.sif` container that we've already pulled from Singularity Hub, we can run the following within the `test` directory where the `hello-world.sif` file is located:

~~~
$ singularity exec hello-world.sif /bin/echo Hello World!
~~~
{: .language-bash}

~~~
Hello World!
~~~
{: .output}

Here we see that a container has been started from the `hello-world.sif` image and the `/bin/echo` command has been run within the container, passing the input `Hello World!`. The command has echoed the provided input to the console and the container has terminated.

## Running a shell within a container

If you want to open an interactive shell within a container, Singularity provides the `singularity shell` command. Again, using the `hello-world.sif` image, and within our `test` directory, we can run a shell within a container from the hello-world image:

~~~
$ singularity shell hello-world.sif
~~~
{: .language-bash}

~~~
Singularity> whoami
[<your username>]
Singularity> ls
hello-world.sif
Singularity> 
~~~
{: .output}

As shown above, we have opened a shell in a new container started from the `hello-world.sif` image.

> ## Running a shell inside a Singularity container
>
> Q: What do you notice about the output of the above commands entered within the Singularity container shell?
> 
>
> Q: Does this differ from what you might see within a Docker container?
{: .discussion}

## Users, files and directories within a Singularity container

When you run a Singularity container, Singularity _binds_ some directories from the host system where you are running the `singularity` command into the container that you're starting. There is a default configuration but ultimate control of how things are set up on the system where you're running Singularity is determined by the system administrator. As a result, this section provides an overview but you may find that things are a little different on the system that you're running on.

The first thing to note is that we run `whoami` within the container we should see our own username. For example, if my username is `jc1000`:

~~~
$ singularity shell hello-world.sif
Singularity> whoami
jc1000
~~~
{: .language-bash}

But hang on! We downloaded the `hello-world.sif` image from Singularity Hub. How is it configured with my user details?!

If you have any familiarity with Linux system administration, you may be aware that in Linux, users and their Unix groups are configured in the `/etc/passwd` and `/etc/group` files respectively. In order for the shell within the container to know of my user, the relevant user information needs to be available within these files within the container.

Assuming this feature is enabled on your system, when the container is started, Singularity appends the relevant user and group lines from the host system to the `/etc/passwd` and `/etc/group` files within the container [\[1\]](https://www.intel.com/content/dam/www/public/us/en/documents/presentation/hpc-containers-singularity-advanced.pdf).

Other files and directories are likely to be made available within containers that you start. For example, your _home directory_ is likely to be accessible in the container.

## Using Docker images with Singularity

Singularity can also start containers from Docker images, opening up access to a huge number of existing container images available on [Docker Hub](https://hub.docker.com/) and other registries.

While Singularity doesn't directly support Docker images, it can pull them from Docker Hub and convert them into a suitable format for running via Singularity. When you pull a Docker image, Singularity pulls the slices or _layers_ that make up the Docker image and converts them into a single-file Singularity SIF image.

For example, moving on from the simple _Hello World_ examples that we've looked at so far, let's pull one of the official Docker Python images. We'll use Python 3.8.2 installed on Debian's Buster (v10) Linux distribution:

~~~
$ singularity pull python-3.8.2.sif docker://python:3.8.2-buster
~~~
{: .language-bash}

~~~
INFO:    Converting OCI blobs to SIF format
INFO:    Starting build...
Getting image source signatures
Copying blob f15005b0235f done
Copying blob 41ebfd3d2fd0 done
Copying blob b998346ba308 done
Copying blob f01ec562c947 done
Copying blob 2447a2c11907 done
Copying blob fdd2d569da3e done
Copying blob ac3886b74a9f done
Copying blob 3c783a9b35dd done
Copying blob ce16dda809f6 done
Copying config 983a7273bc done
Writing manifest to image destination
Storing signatures
2020/04/15 16:52:42  info unpack layer: sha256:f15005b0235fa8bd31cc6988c4f2758016fe412d696e81aecf73e52be079f19e
2020/04/15 16:52:45  info unpack layer: sha256:41ebfd3d2fd0de99b1c63aa36a507bf5555481d06e571d84ed84440d30671494
2020/04/15 16:52:45  info unpack layer: sha256:b998346ba308e3362a85c7bf7faed28d0277c68203696134192fe812f809abb2
2020/04/15 16:52:45  info unpack layer: sha256:f01ec562c947a8ca1b168415da6a4a8f8920808f9b5d6f420ef8fa9af249b1f1
2020/04/15 16:52:47  info unpack layer: sha256:2447a2c119076510a07d71cfcec029fceac2e59eea21fc7b39cf0eb234d3798e
2020/04/15 16:52:55  info unpack layer: sha256:fdd2d569da3eb90bae8b2b7b097b369818974f8a4eff48bc06263ea61d44d9f7
2020/04/15 16:52:55  info unpack layer: sha256:ac3886b74a9ff0d174f2a1e6c27cb492d43b3d2b97a5e0ed4c1ae12a82f584da
2020/04/15 16:52:56  info unpack layer: sha256:3c783a9b35ddbae49d3ed42c93ab9710f82ee5633caaca6bedd1074ced380e56
2020/04/15 16:52:56  info unpack layer: sha256:ce16dda809f69733b41448cfc947ab4485da9c1f7481332ad1da436e636891ab
INFO:    Creating SIF file...
INFO:    Build complete: python-3.8.2.sif
~~~
{: .output}

Note how we see singularity saying that it's "_Converting OCI blobs to SIF format_". We then see the layers of the Docker image being downloaded and unpacked and written into a single SIF file. Once the process is complete, we should see the python-3.8.2.sif image file in the current directory.

We can now run a container from this image as we would with any other singularity image:

~~~
$ singularity run python-3.8.2.sif
~~~
{: .language-bash}

~~~
Python 3.8.2 (default, Mar 31 2020, 15:23:55) 
[GCC 8.3.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import math
>>> math.pi
3.141592653589793
>>> 
~~~
{: .language-python}

Running a container from this image has put us straight into a Python prompt where we can run Python code interactively.

> ## Open a shell within the Python container
>
> Try to run a shell within a singularity container based on the `python-3.8.2.sif` image. That is, run a container that opens a shell rather than the default Python console as we saw above.
> See if you can find more than one way to achieve this.
> 
> > ## Solution
> >
> > Recall from the earlier material that we can use the `singularity shell` command to open a shell within a container. To open a regular shell within a container based on the `python-3.8.2.sif` image, we can therefore simply run:
> > ~~~
> > $ singularity shell python-3.8.2.sif
> > ~~~
> > {: .language-bash}
> > 
> > ~~~
> > Singularity> echo $SHELL
> > /bin/bash
> > Singularity> cat /etc/issue
> > Debian GNU/Linux 10 \n \l
> > 
> > Singularity> exit
> > $ 
> > ~~~
> > {: .output}
> > 
> > It is also possible to use the `singularity exec` command to run an executable within a container. We could, therefore, use the `exec` command to run `/bin/bash`:
> > 
> > ~~~
> > $ singularity exec python-3.8.2.sif /bin/bash
> > ~~~
> > {: .language-bash}
> > 
> > ~~~
> > Singularity> echo $SHELL
> > /bin/bash
> > ~~~
> > {: .output}
> {: .solution}
{: .challenge}

# Singularity - Part II

## Brief recap

So far we've seen how Singularity can be used without any administrative privileges on a computing platform, such as a cluster or remote server, where the software has been pre-installed for you and existing images are available. These existing images may be Singularity image files that are already on the platform you're using or they may be images you obtain from a remote image repository such as Singularity Hub or Docker Hub.

What if you want to create your own images or customise existing images?

In this second part of the lesson we'll look at building Singularity images.

This section of the lesson will then conclude with a look at running more advanced, parallel applications from Singularity container.

## Building Singularity images: Introduction

So far you've been able to work with Singularity from your own user account as a non-privileged user. Building Singularity containers requires that you have administrative (root) access on the system where you're building the containers. Bear in mind that this doesn't have to be the system where you intend to run the containers. If, for example, you are intending to build a container that you can subsequently run on a Linux-based cluster, you could build the container on your own Linux-based dekstop or laptop computer. You could then transfer the built image directly to the target platform or upload it to an image repository and pull it onto the target platform from this repository.

> ## Note
> In order undertake the practical aspects of this section of the course you'll need a Linux system where you have administrative privileges and you are able to install Singularity.
>
> If you have administrative privileges on a non-Linux system, you could look at installing a virtualisation tool such as [VirtualBox](https://www.virtualbox.org/) on which you can run a Linux Virtual Machine (VM) image. Within the Linux VM image, you will be able to install Singularity.
>
> If you are not able to access/run Singularity yourself on a system where you have administrative privileges, you can still follow through this material as it is being taught (or read through it in your own time if you're not participating in a taught version of this course) since it will be helpful to have an understanding of how Singularity containers can be built.
{: .callout}

As a platform that is widely used in the scientific/research software and HPC communities, Singularity provides great support for reproducibility. If you build a Singularity container for some scientific software, it's likely that you and/or others will want to be able to reproduce exactly the same environment again. Maybe you want to verify the results of the code or provide a means that others can use to verify the results to support a paper or report. Maybe you're making a tool available to others and want to ensure that they have exactly the right version/configuration of the code.

Similarly to Docker and many other modern software tools, Singularity follows the "Configuration as code" approach where a container configuration can be stored in a file which can then be committed to your version control system alongside other code. Assuming it is suitably configured, this file can then be used by you or other individuals (or by automated build tools) to reproduce a container with the same configuration at some point in the future.

## Building Singularity images: Different approaches

There are various approaches to building Singularity containers. We will highlight two different approaches here and focus on one of them:

 - _Building within a sandbox:_ You can build a container interactively within a sandbox environment. This means you get a shell within the container environment and install and configure packages and code as you wish before exiting the sandbox and converting it into a container image.
- _Building from a [Singularity Definition File](https://sylabs.io/guides/3.5/user-guide/build_a_container.html#creating-writable-sandbox-directories)_: This is Singularity's equivalent to building a Docker container from a Dockerfile and we'll discuss this approach in this section.

You can take a look at Singularity's "[Build a Container](https://sylabs.io/guides/3.5/user-guide/build_a_container.html#creating-writable-sandbox-directories)" documentation for more details on different approaches to building containers.

> ## Why look at Singularity Definition Files?
> Why do you think we might be looking at the _definition file approach_ here rather than the _sandbox approach_?
>
> > ## Discussion
> > The sandbox approach is great for prototyping and testing out an image configuration but it doesn't provide our ultimate goal of reproducibility. If you spend time sitting at your terminal in front of a shell typing different commands to add configuration, maybe you realise you made a mistake so you undo one piece of configuration and change it. This goes on until you have your completed configuration but there's no explicit record of exactly what you did to create that configuration. 
> > 
> > Say your container image file gets deleted by accident, or someone else wants to create an equivalent image to test something. How will they do this and know for sure that they have the same configuration that you had?
> > With a definition file, the configuration steps are explicitly defined and can be easily stored - definition files are small text files, container files may be very large, multi-gigabyte files that are difficult and time consuming to move around.
> {: .solution}
{: .challenge}

## Creating a Singularity Definition File

We'll start with a very simple example:

~~~
Bootstrap: docker
From: ubuntu:20.04

%post
    apt-get -y update && apt-get install -y python

%runscript
    python -c 'print("Hello World! Hello from our custom Singularity image!")'
~~~
{: .language-bash}

The definiton file has a number of sections, specified using the `%` prefix, that are used to define or undertake different configuration during different stages of the build process. You can find full details in Singularity's [Definition Files documentation](https://sylabs.io/guides/3.5/user-guide/definition_files.html). In our very simple example here, we only use the `post` and `runscript` sections.

Let's step through what this definition file does:

~~~
Bootstrap: docker
From: ubuntu:20.04
~~~
{: .language-bash}

These first two lines define where to bootstrap our image from. In this case, we're going to start from a minimal Ubuntu 20.04 docker image. The `Bootstrap: docker` line is similar to prefixing an image path with `docker://` when using, for example, the `singularity pull` command. A range of [different bootstrap options](https://sylabs.io/guides/3.5/user-guide/definition_files.html#preferred-bootstrap-agents) are supported. `From: ubuntu:20.04` says that we want to use the `ubuntu` image with the tag `20.04`.

Next we have the `%post` section of the definition file:

~~~
%post
    apt-get -y update && apt-get install -y python3
~~~
{: .language-bash}

In this section of the file we can do tasks such as package installation, pulling data files from remote locations and undertaking local configuration within the image. Here we use Ubuntu's package manager to update our package indexes and then install the python3 package along with any required dependencies. The `-y` switches are used to accept, by default, interactive prompts that might appear asking you to confirm package updates or installation. This is required because our definition file should be able to run in an unattended, non-interactive environment.

Finally we have the `%runscript` section:

~~~
%runscript
    python3 -c 'print("Hello World! Hello from our custom Singularity image!")'
~~~
{: .language-bash}

This section is used to define a script that should be run when a container is started based on this image using the `singularity run` command. In this simple example we use python3 to print out some text to the console.

We can now save the contents of the simple defintion file shown above to a file and build an image based on it. In the case of this example, the definition file has been named `my_test_image.def`:

~~~
$ sudo singularity build my_test_image.sif my_test_image.def
~~~
{: .language-bash}

The above command requests the building of an image based on the `my_test_image.def` file with the resulting image saved to the `my_test_image.sif` file. Note that we prefix the command with `sudo` because it is necessary to have administrative privileges to build the image. You should see output similar to the following:

~~~
INFO:    Starting build...
Getting image source signatures
Copying blob d51af753c3d3 skipped: already exists
Copying blob fc878cd0a91c skipped: already exists
Copying blob 6154df8ff988 skipped: already exists
Copying blob fee5db0ff82f skipped: already exists
Copying config 95c3f3755f done
Writing manifest to image destination
Storing signatures
2020/04/29 13:36:35  info unpack layer: sha256:d51af753c3d3a984351448ec0f85ddafc580680fd6dfce9f4b09fdb367ee1e3e
2020/04/29 13:36:36  info unpack layer: sha256:fc878cd0a91c7bece56f668b2c79a19d94dd5471dae41fe5a7e14b4ae65251f6
2020/04/29 13:36:36  info unpack layer: sha256:6154df8ff9882934dc5bf265b8b85a3aeadba06387447ffa440f7af7f32b0e1d
2020/04/29 13:36:36  info unpack layer: sha256:fee5db0ff82f7aa5ace63497df4802bbadf8f2779ed3e1858605b791dc449425
INFO:    Running post scriptlet
+ apt-get -y update
Get:1 http://archive.ubuntu.com/ubuntu focal InRelease [265 kB]
...
  [Package update output truncated]
...
Fetched 13.4 MB in 2s (5575 kB/s)                            
Reading package lists... Done
+ apt-get install -y python3
Reading package lists... Done
...
  [Package install output truncated]
...Processing triggers for libc-bin (2.31-0ubuntu9) ...
INFO:    Adding runscript
INFO:    Creating SIF file...
INFO:    Build complete: my_test_image.sif
$ 
~~~
{: .output}

You should now have a `my_test_image.sif` file in the current directory. Note that in the above output, where it says `INFO:  Starting build...` you then see a series of `skipped: already exists` messages for the `Copying blob` lines. This is because the Docker image slices for the Ubuntu 20.04 image have previously been downloaded and are cached on the system where this example is being run. On your system, if the image is not already cached, you will see the slices being downloaded from Docker Hub when these lines of output appear.

We've now built an image and we can attempt to run it:

~~~
$ singularity run my_test_image.sif
~~~
{: .language-bash}

If everything worked successfully, you should see the message printed by Python:

~~~
Hello World! Hello from our custom Singularity image!
~~~
{: .output}

Here we've looked at a very simple example of how to create an image. At this stage, you might want to have a go at creating your own definition file for some code of your own or an application that you work with regularly. If you'd like an more advanced example, take a look at the supplementary material at the end of this lesson where a more advanced example is given that generates a singularity container for running [c-ray](https://github.com/VKoskiv/c-ray), an open source ray-tracing application.

**_Add a note about remote builder capabilities_**

**_Add a note about signing containers_**

## Running MPI parallel codes with Singularity containers

Info about running MPI parallel codes from Singularity containers. 

More about singularity!

* Paragraphs marked "[EDIT]" contain generic text that may benefit from being edited to provide course participants with specific information related to your course environment.

## References

\[1\] Gregory M. Kurzer, Containers for Science, Reproducibility and Mobility: Singularity P2. Intel HPC Developer Conference, 2017. Available at: https://www.intel.com/content/dam/www/public/us/en/documents/presentation/hpc-containers-singularity-advanced.pdf

# Singularity: Supplementary Materials

## Writing a more advanced defintion file

Here we provide a more advanced example of a singularity definition file. This example clones the code for the [c-ray](https://github.com/VKoskiv/c-ray) open source ray-tracing application from GitHub and builds it within the container.

> ## Why [c-ray](https://github.com/VKoskiv/c-ray)?
> We could have chosen any one of a vast number of applications to use for this example but c-ray was selected because it is a lightweight tool that builds quickly while still demonstrating the process of installing multiple dependencies and building the code using CMake. The output of the code also generates something visual that shows you that the code is running correctly within the container.
{: .callout}

