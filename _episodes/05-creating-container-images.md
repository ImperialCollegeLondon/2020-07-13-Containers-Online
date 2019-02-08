---
title: "Creating your own container images"
teaching: 30
exercises: 0
questions:
- "Key question (FIXME)"
objectives:
- "First learning objective. (FIXME)"
keypoints:
- "First key point. Brief Answer to questions. (FIXME)"
---
### Introduction to Dockerfiles

We have seen use of others' Docker container images. Now we move on to describe how you can create your own images.

The specification for how Docker should build images that you design is contained within a file named `Dockerfile`.

Create a new directory named "my-container-spec" and `cd` into it in a terminal window.

Within the new "my-container-spec" directory, use your favourite editor to create a file named "Dockerfile" that contains the following:

~~~
FROM alpine
CMD [ "/bin/echo", "Greetings from my newly minted container." ]
~~~

### Building your Docker image

~~~
$ docker build -t my-container .
~~~
{: .language-bash}
~~~
Sending build context to Docker daemon  2.048kB
Step 1/2 : FROM alpine
latest: Pulling from library/alpine
6c40cc604d8e: Pull complete 
Digest: sha256:b3dbf31b77fd99d9c08f780ce6f5282aba076d70a513a8be859d8d3a4d0c92b8
Status: Downloaded newer image for alpine:latest
 ---> caf27325b298
Step 2/2 : CMD [ "sh", "echo Greetings from my newly minted container." ]
 ---> Running in 08ba4307df31
Removing intermediate container 08ba4307df31
 ---> e8737dae339f
Successfully built e8737dae339f
Successfully tagged my-container:latest
~~~
{: .output}

OK, now let's test that that container does what it's supposed to!

~~~
$ docker run my-container
~~~
{: .language-bash}
~~~
Greetings from my newly minted container.
~~~
{: .output}

While this does not look like much, you have combined a lightweight Linux operating system with your specification to run a given command that can operate reliably on macOS, Microsoft Windows, Linux and on the cloud!

### Copying files into your containers at build time

Let's rework our container to run some code written in the Python programming language.

Open a second terminal window, and change into an empty scratch directory. I will call this the "working shell" and the other terminal window from above the "image building shell".

Open the Dockerfile you created above with your favourite editor, and change its contents to match the following:
~~~
FROM python:3

WORKDIR /usr/src/app

COPY requirements.txt ./
RUN pip install --no-cache-dir -r requirements.txt

COPY test.py .

CMD [ "python", "./test.py" ]
~~~

In your image building shell re-run the command to try to build your container (this will fail!):
~~~
$ docker build -t my-container .
~~~
{: .language-bash}
~~~
Sending build context to Docker daemon  2.048kB
Step 1/6 : FROM python:3
3: Pulling from library/python
741437d97401: Pull complete 
34d8874714d7: Pull complete 
0a108aa26679: Pull complete 
7f0334c36886: Pull complete 
65c95cb8b3be: Pull complete 
9107d7193263: Pull complete 
dd6f212ec984: Pull complete 
43288b101abf: Pull complete 
cbc666ab4a65: Pull complete 
Digest: sha256:d510b850194fab564abc3dfd22e626fa0c4ab3ce81118dab08a084ed3dcd24ac
Status: Downloaded newer image for python:3
 ---> 338b34a7555c
Step 2/6 : WORKDIR /usr/src/app
 ---> Running in 838063c90080
Removing intermediate container 838063c90080
 ---> c350d738dec6
Step 3/6 : COPY requirements.txt ./
COPY failed: stat /var/lib/docker/tmp/docker-builder409382412/requirements.txt: no such file or directory
~~~
{: .output}

Our Dockerfile made reference to a file requirements.txt that should have been in the directory that contained our Dockerfile. It was not present, so the building of the image failed.

For now, create an emtpy file named "requirements.txt" in the same directory as your Dockerfile. That will fix the first error, although an image build would not yet be successful. The "COPY test.py ." command copies the file "test.py" into the working directory of the current image building operation, and will also fail.

Create the file "test.py" in the same directory as your Dockerfile, with the following contents:
~~~
print("Hello world from Python")
~~~
{: .language-python}

~~~
$ docker build -t my-container .
~~~
{: .language-bash}
~~~
Sending build context to Docker daemon  3.584kB
Step 1/6 : FROM python:3
 ---> 338b34a7555c
Step 2/6 : WORKDIR /usr/src/app
 ---> Using cache
 ---> c350d738dec6
Step 3/6 : COPY requirements.txt ./
 ---> Using cache
 ---> c35d15cb3c4a
Step 4/6 : RUN pip install --no-cache-dir -r requirements.txt
 ---> Using cache
 ---> aaa54a230e27
Step 5/6 : COPY test.py .
 ---> 1069b6fcc77c
Step 6/6 : CMD [ "python", "./test.py" ]
 ---> Running in 97fd77f25808
Removing intermediate container 97fd77f25808
 ---> fc145d33ea49
Successfully built fc145d33ea49
Successfully tagged my-container:latest
~~~
{: .output}

In your working shell test your container:
~~~
$ docker run my-container
~~~
{: .language-bash}
~~~
Hello world from Python
~~~
{: .output}


### Sharing files with your containers at run time

- graphing example

### Pushing your container images to the Docker Hub

{% include links.md %}

