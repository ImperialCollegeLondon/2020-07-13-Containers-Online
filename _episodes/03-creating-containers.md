---
title: "Creating containers"
teaching: 10
exercises: 0
questions:
- "How do I get Docker to perform computation?"
objectives:
- "Demonstrate how to create an instance of a container from an image."
- "Explain how to list (container) images on your laptop."
- "Explain how to list running and completed containers.."
keypoints:
- "Containers are usually created using command line invocations."
- "The `docker run` command creates containers from images."
- "The `docker image` command lists images that are (now) on your computer."
- "The `docker container` command lists containers that have been created."
---

### Creating a "hello world" container

> - Recall that a container "image" is the template from which particular instances of containers will be created.

One of the simplest Docker container images just allows you to create containers that print a welcome message.

Try the following command:
~~~
$ docker run hello-world
~~~
{: .language-bash}
~~~
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
1b930d010525: Pull complete 
Digest: sha256:2557e3c07ed1e38f26e389462d03ed943586f744621577a99efb77324b0fe535
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
~~~
{: .output}

Now try to run the above command again, and observe the difference in the output.

The message from "Hello from Docker!" is what's produced by instances of the hello-world container. It should be identical every time you make an instance of the hello-world container and run it.

 The first time you saw some initial output from the Docker command itself:
~~~
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
1b930d010525: Pull complete 
Digest: sha256:2557e3c07ed1e38f26e389462d03ed943586f744621577a99efb77324b0fe535
Status: Downloaded newer image for hello-world:latest
~~~
{: .output}

What this says is that your laptop didn't have its own local copy of the hello-world container's image.

Docker then connected to the Docker Hub to find and download the (container) image with that name.

The message notes information about the Docker Hub website, but we'll return to that in the next episode.

The "digest" is a secure fingerprint (a "hash") of the particular version of the container image that you now have... (Although of course the usefulness of that hash is minimal if you don't know what to compare it to!)

### Where did that container image go?

You can find out what container images you have local copies of using the following command:
~~~
$ docker image ls
~~~
{: .language-bash}
~~~
REPOSITORY             TAG                 IMAGE ID            CREATED             SIZE
hello-world            latest              fce289e99eb9        4 weeks ago         1.84kB
~~~
{: .output}
(Actually, I had some additional images on my laptop that I've removed from the above, and in live demo I'm likely to end up displaying a great many more lines!)

If you need to reclaim space, you will need to remove image files.
I'm not entirely sure whether uninstalling the Docker client will uninstall your image files.

### What containers are running?
The command to list the containers that are currently running is
~~~
docker container ls
~~~
{: .language-bash}

... although the output should be blank, since the instances of hello-world containers will have been wiped away as soon as they completed. However the container image remains on your computer so that it is quick for you to create future such instances of hello-world containers.

### What containers have run recently?
There is also a way to list running containers, and those that have completed recently
~~~
$ docker container ls --all
~~~
{: .language-bash}
~~~
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                     PORTS               NAMES
9c698655416a        hello-world         "/hello"            2 minutes ago       Exited (0) 2 minutes ago                       zen_dubinsky
6dd822cf6ca9        hello-world         "/hello"            3 minutes ago       Exited (0) 3 minutes ago                       eager_engelbart
~~~
{: .output}

> ## The Docker official documentation is helpful!
> There is lots of great documentation at <https://docs.docker.com/>, for example, detailed reference material and tutorials covering the use of the commands mentioned above.
{: .callout}

{% include links.md %}

{% comment %}
<!--  LocalWords:  keypoints amd64 fce289e99eb9 zen_dubinsky links.md
 -->
<!--  LocalWords:  eager_engelbart endcomment
 -->
{% endcomment %}
