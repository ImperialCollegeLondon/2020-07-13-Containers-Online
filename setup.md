---
title: Setup
---

Please try to complete the following setup tasks ahead of the workshop. If you run into problems, please contact the workshop leader at the e-mail address on the home page. We will also provide installation and setup help at the workshop if  required, but you will get more out of the training if you can complete them ahead of time.

There are four steps to the setup:

   1. Create a Docker Hub account
   2. Install the Docker software on your system
   3. Ensure that your system is equipped with an SSH client
   4. Setup an account on the HPC system, Cirrus, that we will be using for the workshop
   
These steps are described in more detail below.

> ## Note
> The SSH client and Cirrus account are required to run Singularity containers on a remote
> HPC system. If you are confident, you can attempt to install Singularity on your local
> system. Instructions for this are given below.
{: .callout}

## 1. Create Docker Hub account

You should setup a free account on the Docker Hub ahead of the workshop:

- The [Docker Hub](http://hub.docker.com). We will use the Docker Hub to download pre-built container images, and for you to upload and download container images that you create, as explained in the relevant lesson episodes.

Please seek help at the start of the lesson if you have not been able to setup a Docker Hub account.

### 2. Install the Docker software on your laptop

Please try to install the appropriate software from the list below depending on the operating system that your laptop is running:

- Microsoft Windows, either:
    - Try this first, although it won't work with Windows 10 Home Edition. Install the [Docker Desktop (Windows)](https://hub.docker.com/editions/community/docker-ce-desktop-windows), or failing that;
    - Install the [Docker Toolbox (Windows)](https://docs.docker.com/toolbox/toolbox_install_windows/).
- Apple macOS, either:
    - Try this first, although it will not work with older versions of macOS. Install the [Docker Desktop (Mac)](https://hub.docker.com/editions/community/docker-ce-desktop-mac), or failing that:
    - Install the [Docker Toolbox (Mac)](https://docs.docker.com/toolbox/toolbox_install_mac/).
- Linux: there are too many varieties of Linux to give precise instructions here, but hopefully you can locate documentation for getting Docker installed on your Linux distribution. It may already be installed. If it is not already installed on your system, see:
    - [Docker Engine on CentOS](https://docs.docker.com/install/linux/docker-ce/centos/)
    - [Docker Engine on Debian](https://docs.docker.com/install/linux/docker-ce/debian/)
    - [Docker Engine on Fedora](https://docs.docker.com/install/linux/docker-ce/fedora/)
    - [Docker Engine on Ubuntu](https://docs.docker.com/install/linux/docker-ce/ubuntu/)
    - Note that on Linux, you will either need to run Docker commands as root using `sudo` or [create a docker group to run without sudo](https://docs.docker.com/engine/install/linux-postinstall/#manage-docker-as-a-non-root-user)
    
## 3. SSH client

All attendees should have an SSH client installed.
SSH is a tool that allows us to connect to and use a remote computer as our own.
Please follow the directions below to install an SSH client for your system.

**Windows**

Modern versions of Windows have SSH available in Powershell. You can test if it is available by typing `ssh --help` in Powershell. If it is
installed, you should see some useful output. If it is not installed, you will get an error. If SSH is not available in Powershell, then
you should install MobaXterm as described below.

An alternative is to install MobaXterm from [http://mobaxterm.mobatek.net](http://mobaxterm.mobatek.net). You will want to get the Home edition (Installer edition). However, if Git Bash works, you do not need this.

**macOS**

macOS comes with SSH pre-installed, so you should not need to install anything.

**Linux**

Linux users do not need to install anything, you should be set!

## 4. Account on Cirrus

Please sign up for your account on our HPC machine, Cirrus, which will be available to
you for the duration of the course and for a few days afterwards, to allow you to
complete the practical exercises and put some of what you have learned into practice.

### 4.1 Sign up for a SAFE account

To sign up, you must first register for an account on SAFE (our service administration
web application):

If you are already registered on the ARCHER or Tier-2 SAFE you do not need to re-register. Please proceed to the next step.

1. Go to the [SAFE New User Signup Form](https://safe.epcc.ed.ac.uk/signup.jsp)
2. Fill in your personal details. You can come back later and change them if you wish. Note: you should register using your institutional or company email address - email domains such as gmail.com, outlook.com, etc. are not allowed to be used for access to Cirrus
3. Click “Submit”
4. You are now registered. A single use login link will be emailed to the email address you provided. You can use this link to login and set your password.

### 4.2 Notify the course organisor if your SAFE registration email does not end `.ac.uk`

There are additional restrictions on signing up for accounts which are not from UK academic institutions. If your
registered email address does not end in `.ac.uk` then please let the course organisors know before you attempt
the next step so they can pre-approve your email domain.

### 4.3 Sign up for an account on Cirrus through SAFE

1. [Login to SAFE](https://safe.epcc.ed.ac.uk)
2. Go to the Menu "Login accounts" and select "Request login account"
3. Choose the `tc012` project “Choose Project for Machine Account” box and click "Next"
4. On the next page, the Cirrus system should be selected. Click "Next"
5. Enter the username you would prefer to use on Cirrus. Every username must be unique, so if your chosen name is taken, you will need to choose another

Now you have to wait for the course organiser to accept your request to register. When this has happened, your account will be created on Cirrus.
Once this has been done, you will be sent an email. You can then pick up your one shot initial password for Cirrus from your SAFE account.

### 4.4 Generate an SSH key pair and upload it to SAFE

In addition to your password, you will need an SSH key pair to access Cirrus. There is useful guidance on how
to generate SSH key pairs on the ARCHER website at [http://archer.ac.uk/documentation/getting-started/logging-on.php#generate_key](http://archer.ac.uk/documentation/getting-started/logging-on.php#generate_key).

Once you have generated your key pair, you need to add the public part to your Cirrus account in SAFE:

1. [Login to SAFE](https://safe.epcc.ed.ac.uk)
2. Go to the Menu “Login accounts” and select the Cirrus account you want to add the SSH key to
3. On the subsequent Login account details page click the “Add Credential” button
4. Select “SSH public key” as the Credential Type and click “Next”
5. Either copy and paste the public part of your SSH key into the “SSH Public key” box or use the button to select the public key file on your computer.
6. Click “Add” to associate the public SSH key part with your account

The public SSH key part will now be added to your login account on the Cirrus system.

### 4.5 Log into Cirrus

You should now be able to log into Cirrus by following the [login instructions in the Cirrus documentation](https://cirrus.readthedocs.io/en/master/user-guide/connecting.html#ssh-clients).

## (Optional) Install Singularity on your local system

If you do not wish to use Cirrus to run your Singularity images, you will need to install Singularity on
your local system. These instructions are optional and are not required to complete the course.

If you are running Linux and would like to install Singularity locally on your system, Singularity provide the free, open source [Singularity Community Edition](https://sylabs.io/singularity/). You will need to install various dependencies on your system and then build Singularity from source code.

If you have Linux systems knowledge and would like to attempt a local install of Singularity, you can find details in the [INSTALL.md](https://github.com/sylabs/singularity/blob/master/INSTALL.md) file within the Singularity repository that explains how to install the prerequisites and build and install the software. Singularity is written in the [Go](https://golang.org/) programming language and Go is the main dependency that you'll need to install on your system. The process of installing Go and any other requirements is detailed in the INSTALL.md file.

If you do not have access to a Linux system where you can build and install Singularity but you have administrative privileges on another system, you could look at installing a virtualisation tool such as [VirtualBox](https://www.virtualbox.org/) on which you could run a Linux Virtual Machine (VM) image. Within the Linux VM image, you will be able to install Singularity. Again this is beyond the scope of the course.

If you have a Mac system, you can also try the beta release of [Singularity Desktop for macOS](https://sylabs.io/singularity-desktop-macos/).

{% include links.md %}

{% comment %}
<!--  LocalWords:  myfile kbd links.md md endcomment
-->
{% endcomment %}
