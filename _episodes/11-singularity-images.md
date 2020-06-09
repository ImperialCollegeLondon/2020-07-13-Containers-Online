---
title: "Building Singularity images"
teaching: 25
exercises: 15
questions:
- "I now know how to run a Singularity image, how do I create one?"
objectives:
- "Understand the different Singularity container file formats."
- "Understand how to build and share your own Singularity containers."
keypoints:
- "Singularity has its own container image format (SIF) but it can also run containers directly from Docker Hub."
- ""
- ""
---

# Singularity - Part II

## Brief recap

So far we've seen how Singularity can be used without any administrative privileges on a computing platform, such as a cluster or remote server, where the software has been pre-installed for you and existing images are available. These existing images may be Singularity image files that are already on the platform you're using or they may be images you obtain from a remote image repository such as Singularity Hub or Docker Hub.

What if you want to create your own images or customise existing images?

In this second part of the lesson we'll look at building Singularity images.

This section of the lesson will then conclude with a look at running more advanced, parallel applications from a Singularity container.

## Building Singularity images

### Introduction

So far you've been able to work with Singularity from your own user account as a non-privileged user. This section of the lesson requires that you have administrative (root) access on the system where you'll be building containers. While it is possible to build Singularity containers without root access, it is highly recommended that you use root, as highlighted in [this section](https://sylabs.io/guides/3.5/user-guide/build_a_container.html#creating-writable-sandbox-directories) of the Singularity documentation. Bear in mind that the system that you use doesn't have to be the system where you intend to run the containers. If, for example, you are intending to build a container that you can subsequently run on a Linux-based cluster, you could build the container on your own Linux-based dekstop or laptop computer. You could then transfer the built image directly to the target platform or upload it to an image repository and pull it onto the target platform from this repository.

> ## Note
> In order undertake the practical aspects of this section of the lesson you'll need a Linux system where you have administrative privileges and you are able to install Singularity.
>
> If you have administrative privileges on a non-Linux system, you could look at installing a virtualisation tool such as [VirtualBox](https://www.virtualbox.org/) on which you can run a Linux Virtual Machine (VM) image. Within the Linux VM image, you will be able to install Singularity.
>
> If you are not able to access/run Singularity yourself on a system where you have administrative privileges, you can still follow through this material as it is being taught (or read through it in your own time if you're not participating in a taught version of this course) since it will be helpful to have an understanding of how Singularity containers can be built.
> 
> You could also attempt to follow this section of the lesson without using root and instead using the `singularity` command's [`--fakeroot`](https://sylabs.io/guides/3.5/user-guide/fakeroot.html) option. However, you may encounter issues with permissions when trying to build and run your containers and this is why running the commands as root is strongly recommended and is the approach described in this lesson.
{: .callout}

As a platform that is widely used in the scientific/research software and HPC communities, Singularity provides great support for reproducibility. If you build a Singularity container for some scientific software, it's likely that you and/or others will want to be able to reproduce exactly the same environment again. Maybe you want to verify the results of the code or provide a means that others can use to verify the results to support a paper or report. Maybe you're making a tool available to others and want to ensure that they have exactly the right version/configuration of the code.

Similarly to Docker and many other modern software tools, Singularity follows the "Configuration as code" approach and a container configuration can be stored in a file which can then be committed to your version control system alongside other code. Assuming it is suitably configured, this file can then be used by you or other individuals (or by automated build tools) to reproduce a container with the same configuration at some point in the future.

### Different approaches to building images

There are various approaches to building Singularity containers. We highlight two different approaches here and focus on one of them:

 - _Building within a sandbox:_ You can build a container interactively within a sandbox environment. This means you get a shell within the container environment and install and configure packages and code as you wish before exiting the sandbox and converting it into a container image.
- _Building from a [Singularity Definition File](https://sylabs.io/guides/3.5/user-guide/build_a_container.html#creating-writable-sandbox-directories)_: This is Singularity's equivalent to building a Docker container from a Dockerfile and we'll discuss this approach in this section.

You can take a look at Singularity's "[Build a Container](https://sylabs.io/guides/3.5/user-guide/build_a_container.html#creating-writable-sandbox-directories)" documentation for more details on different approaches to building containers.

> ## Why look at Singularity Definition Files?
> Why do you think we might be looking at the _definition file approach_ here rather than the _sandbox approach_?
>
> > ## Discussion
> > The sandbox approach is great for prototyping and testing out an image configuration but it doesn't provide the best support for our ultimate goal of reproducibility. If you spend time sitting at your terminal in front of a shell typing different commands to add configuration, maybe you realise you made a mistake so you undo one piece of configuration and change it. This goes on until you have your completed configuration but there's no explicit record of exactly what you did to create that configuration. 
> > 
> > Say your container image file gets deleted by accident, or someone else wants to create an equivalent image to test something. How will they do this and know for sure that they have the same configuration that you had?
> > With a definition file, the configuration steps are explicitly defined and can be easily stored.
> > 
> > Definition files are small text files while container files may be very large, multi-gigabyte files that are difficult and time consuming to move around. This makes definition files ideal for storing in a version control system along with their revisions.
> {: .solution}
{: .challenge}

### Creating a Singularity Definition File

As highlighted above, a Singularity Definition File is a text file that contains a series of statements that are used to create a container image. The definition file can be stored in your code repository as part of your code and used to create a reproducible image. For a given commit in your repository, the definition file present at that commit can be used to reproduce a container with a known state. It was pointed out earlier in the course, when covering Docker, that this property also applies for Dockerfiles.

We'll know look at a very simple example of a definition file:

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

Let's step through this definition file and look at the lines in more detail:

~~~
Bootstrap: docker
From: ubuntu:20.04
~~~
{: .language-bash}

These first two lines define where to bootstrap our image from. Rather than starting completely from scratch and having to install our operating system into an empty image, it's much easier to start from some existing base image. In this case, we're going to start from a minimal Ubuntu 20.04 docker image. The `Bootstrap: docker` line is similar to prefixing an image path with `docker://` when using, for example, the `singularity pull` command. A range of [different bootstrap options](https://sylabs.io/guides/3.5/user-guide/definition_files.html#preferred-bootstrap-agents) are supported. `From: ubuntu:20.04` says that we want to use the `ubuntu` image with the tag `20.04`.

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

The above command requests the building of an image based on the `my_test_image.def` file with the resulting image saved to the `my_test_image.sif` file. Note that we prefix the command with `sudo` because it is necessary to have administrative privileges to build the image - you may be asked to enter your password when running this command in order to gain administrator privileges. You should see output similar to the following:

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

### More advanced definition files

Here we've looked at a very simple example of how to create an image. At this stage, you might want to have a go at creating your own definition file for some code of your own or an application that you work with regularly. There are several definition file sections that were _not_ used in the above example, these are:

 - `%setup`
 - `%files`
 - `%environment`
 - `%startscript`
 - `%test`
 - `%labels`
 - `%help`

The [`Sections` part of the definition file documentation](https://sylabs.io/guides/3.5/user-guide/definition_files.html#sections) details all the sections and provides an example definition file that makes use of all the sections.

### Additional Singularity features

Singularity has a wide range of features. You can find full details in the [Singularity User Guide](https://sylabs.io/guides/3.5/user-guide/index.html) and we highlight a couple of key features here that may be of use/interest:

**Remote Builder Capabilities:** If you have access to a platform with Singularity installed but you don't have root access to create containers, you may be able to use the [Remote Builder](https://cloud.sylabs.io/builder) functionality to offload the process of building an image to remote cloud resources. You'll need to register for a _cloud token_ via the link on the [Remote Builder](https://cloud.sylabs.io/builder) page.

**Signing containers:** If you do want to share container image (`.sif`) files directly with colleagues or collaborators, how can the people you send an image to be sure that they have received the file without tampering or corruption? And how can you be sure that the same goes for any container image file you receive from others? Singularity supports signing containers which allows a digital signature to be linked to an image file. This signature can be used to verify that an image file has been signed by the holder of a specific key and that the file is unchanged from when it was signed. You can find full details of how to use this functionality in the Singularity documentation on [Signing and Verifying Containers](https://sylabs.io/guides/3.0/user-guide/signNverify.html).

