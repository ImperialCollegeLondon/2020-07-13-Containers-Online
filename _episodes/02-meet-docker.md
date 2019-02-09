---
title: "Introducing the Docker command line"
teaching: 10
exercises: 0
questions:
- "How do I interact with Docker?"
objectives:
- "Explain how to check that Docker is installed and is ready to use."
- "Demonstrate some initial Docker command line interactions."
keypoints:
- "A toolbar icon indicates that Docker is ready to use containers."
- "You will typically interact with Docker using the command line."
---
### Docker command line
- Open browser window on <http://hub.docker.com/>
    - Sign In using email and password (don't tell us what it is)
    - top-right screen will show your _username_ (mine's dme26)
- Start Docker app
- Log in to docker hub using docker.app's menu
    - successful login should un-grey "repositories" in the docker.app menu
- Open terminal window
- Run the following command in shell to check that Docker is installed:

~~~
$ docker --version
~~~
{: .language-bash}
~~~
Docker version 18.09.1, build 4c52b90
~~~
{: .output}

- Run login command in shell
    - (I wasn't prompted for authentication details, but your Docker hub username+password are what's desired.)

~~~
$ docker login
~~~
{: .language-bash}
~~~
Authenticating with existing credentials...
Login Succeeded
~~~
{: .output}

The `Login Succeeded` message means that your `docker` command line tool is ready to access the Docker Hub. We will return to discussion of the Docker Hub soon...

{% include links.md %}

{% comment %}
<!--  LocalWords:  keypoints links.md endcomment
 -->
{% endcomment %}
