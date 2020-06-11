---
title: "Running MPI parallel jobs using Singularity containers"
teaching: 30
exercises: 20
questions:
# - "Can I run MPI parallel codes from Singularity containers on a local/institutional/national HPC platform?"
- "How do I set up and run an MPI job from a Singularity container?"
objectives:
- "Learn how MPI applications within Singularity containers can be run on HPC platforms"
- "Understand the challenges and related performance implications when running MPI jobs via Singularity"
keypoints:
- "Singularity images containing MPI applications can be built on one platform and then run on another (e.g. an HPC cluster) if the two platforms have compatible MPI implementations."
- "When running an MPI application within a Singularity container, use the MPI executable on the host system to launch a Singularity container for each process."
- "Think about parallel application performance requirements and how where you build/run your image may affect that."
---

## Running MPI parallel codes with Singularity containers

### MPI overview

MPI - [Message Passing Interface](https://en.wikipedia.org/wiki/Message_Passing_Interface) - is a widely used standard for parallel programming. It is used for exchanging messages/data between processes in a parallel application. If you've been involved in developing or working with computational science software, you may already be familiar with MPI and running MPI applications.

When working with an MPI code on a large-scale cluster, a common approach is to compile the code yourself, within your own user directory on the cluster platform, building against the supported MPI implementation on the cluster. Alternatively, if the code is widely used on the cluster, the platform administrators may build and package the application as a module so that it is easily accessible by all users of the cluster.

### MPI codes with Singularity containers

We've already seen that building Singularity containers can be impractical without root access. Since we're highly unlikely to have root access on a large institutional, regional or national cluster, building a container directly on the target platform is not normally an option.

If our target platform uses [OpenMPI](https://www.open-mpi.org/), one of the two widely used source MPI implementations, we can build/install a compatible OpenMPI version on our local build platform and then build our image and associated code on this platform, either interactively in a sandbox or via a defintion file. Singularity directly supports OpenMPI with support integrated into OpenMPI itself. 

If the target platform uses a version of MPI based on [MPICH](https://www.mpich.org/), the other widely used open source MPI implementation, there is [ABI compatibility between MPICH and several other MPI implementations](https://www.mpich.org/abi/). In this case, you can build your code and image on a local platform against MPICH and you should be able to succesfully run containers based on this image on your target cluster platform.

While this approach does produce a container image with some level of portability, if you're after the best possible performance, it can present some issues. The version of MPI in the container will need to be built and configured to support the hardware on your target platform if the best possible performance is to be achieved. Building on a different platform with different hardware present means that this is not going to be practical, especially if the version of MPI available is different (but compatible). Singularity's [MPI documentation](https://sylabs.io/guides/3.5/user-guide/mpi.html) highlights two different models for working with MPI codes and this is the _[hybrid model](https://sylabs.io/guides/3.5/user-guide/mpi.html#hybrid-model)_. In the following section we'll look at building a Singularity image containing a small MPI application based on the hybrid model.

### Building and running a Singularity image for an MPI code

#### Building and testing an image

This example makes the assumption that you'll be building a container image on a local platform and then deploying it to a cluster with a different but compatbile MPI implementation. See [Singularity and MPI applications](https://sylabs.io/guides/3.5/user-guide/mpi.html#singularity-and-mpi-applications) in the Singularity documentation for further information on how this works.

We'll build an image from a definition file that will be able to run some MPI benchmarks using the [OSU Micro-Benchmarks](https://mvapich.cse.ohio-state.edu/benchmarks/).

In this example, the target platform is a remote HPC cluster that uses [Intel MPI](https://software.intel.com/content/www/us/en/develop/tools/mpi-library.html). The container can be built via the Singularity Docker image that we used in the previous episode of the Singularity material.

Begin by creating a directory and, within that directory, downloading and saving the "tarball" for version 5.6.2 of the OSU Micro-Benchmarks from the [OSU Micro-Benchmarks page](https://mvapich.cse.ohio-state.edu/benchmarks/).

In the same directory, save the following definition file content to a `.def` file, e.g. `osu_benchmarks.def`:

~~~
Bootstrap: docker
From: ubuntu:20.04

%files
    /home/singularity/osu-micro-benchmarks-5.6.3.tar.gz /root/

%post
    apt-get -y update && DEBIAN_FRONTEND=noninteractive apt-get -y install build-essential mpich libmpich-dev
    cd /root
    tar zxvf osu-micro-benchmarks-5.6.3.tar.gz
    cd osu-micro-benchmarks-5.6.3/
    ./configure --prefix=/usr/local/osu CC=/usr/bin/mpicc CXX=/usr/bin/mpicxx
    make && make install

%runscript
    echo "Rank ${PMI_RANK} - About to run: /usr/local/osu/libexec/osu-micro-benchmarks/mpi/$*"
    exec /usr/local/osu/libexec/osu-micro-benchmarks/mpi/$*
~~~
{: .output}

A quick overview of what the above definition file is doing:

 - The image is being bootstrapped from the `ubuntu:20.04` Docker image
 - In the `%files` section: The OSU Micro-Benchmarks tar file is copied from the current directory into the `/root` directory in the image
 - In the `%post` section:
   - Ubuntu's `apt-get` package manager is used to update the package directory and then install the compiler and other required build tools and MPICH
   - The OSU Micro-Benchmarks tar.gz file is extracted and the configure, build and install steps are run to build the benchmark code from source
 - In the `%runscript` section: A runscript is set up that will echo the rank number of the current process and then run the command provided as a command line argument

_Note that base path of the the executable to run is hardcoded in the run script_ so the command line parameter to provide when running a container based on this image is relative to this base path, for example, `startup/osu_hello`, `collective/osu_allgather`, `pt2pt/osu_latency`, `one-sided/osu_put_latency`.

> ## Build and test the OSU Micro-Benchmarks image
>
> Using the above definition file, build a Singularity image named `osu_benchmarks.sif`.
> 
> Once you have built the image, use it to run the `osu_hello` benchmark that is found in the `startup` benchmark folder.
> 
> _NOTE: If you're not using the Singularity Docker image to build your Singularity image, you will need to edit the path to the .tar.gz file in the `%files` section of the definition file._
> 
> > ## Solution
> > 
> > You should be able to build an image from the definition file as follows:
> > 
> > ~~~
> > $ singularity build osu_benchmarks.sif osu_benchmarks.def
> > ~~~
> > {: .language-bash}
> > 
> > Assuming the image builds successfully, you can then try running the container locally and also transfer the SIF file to a cluster platform that you have access to (that has Singularity installed) and run it there.
> > 
> > Let's begin with a single-process run of `osu_hello` on the local system to ensure that we can run the container as expected:
> > 
> > ~~~
> > $ singularity run osu_benchmarks.sif startup/osu_hello
> > ~~~
> > {: .language-bash}
> > 
> > You should see output similar to the following:
> > 
> > ~~~
> > Rank  - About to run: /usr/local/osu/libexec/osu-micro-benchmarks/mpi/startup/osu_hello
> > # OSU MPI Hello World Test v5.6.2
> > This is a test with 1 processes
> > ~~~
> > {: .output}
> > 
> > Note that no rank number is shown since we didn't run the container via mpirun and so the `${PMI_RANK}` environment variable that we'd normally have set in an MPICH run process is not set.
> {: .solution}
{: .challenge}

#### Running Singularity containers via MPI

Assuming the above tests worked, we can now try undertaking a parallel run of one of the OSU benchmarking tools within our container image.

This is where things get interesting and we'll begin by looking at how Singularity containers are run within an MPI environment.

If you're familiar with running MPI codes, you'll know that you use `mpirun`, `mpiexec` or a similar MPI exectuable to start your application. This executable may be run directly on the local system or cluster platform that you're using, or you may run it through a job script submitted to a job scheduler. Your MPI-based application code, which will be linked against the MPI libraries, will make MPI API calls into these MPI libraries which in turn talk to the MPI daemon process running on the host system. This daemon process handles the communication between MPI processes, including talking to the daemons on other nodes to exchange information between processes running on different machines, as necessary.

When running code within a Singularity container, we don't use the MPI executables stored within the container (i.e. we DO NOT run `singularity exec mpirun -np <numprocs> /path/to/my/executable`). Instead we use the MPI installation on the host system to run Singularity and start an instance of our executable from within a container for each MPI process. Without Singularity support in an MPI implementation, this results in starting a separate Singularity container instance within each process. This can present some overhead if a large number of processes are being run on a host. Where Singularity support is built into an MPI implementation this can address this potential issue and reduce the overhead of running code from within a container as part of an MPI job.

Ultimately, this means that our running MPI code is linking to the MPI libraries from the MPI install within our container and these are, in turn, communicating with the MPI daemon on the host system which is part of the host system's MPI installation. These two installations of MPI may be different but as long as there is ABI compatibility between the version of MPI installed in your container image and the version on the host system, your job should run successfully.

We can now try running a 2-process MPI run of a point to point benchmark `osu_latency`. If your local system has both MPI and Singularity installed and has multiple cores, you can run this test on that system. Alternatively you can run on a cluster. Note that you may need to submit this command via a job submission script submitted to a job scheduler if you're running on a cluster. That is beyond the scope of this material but if you're attenting a taught version of this course, some information will be provided at this point in relation to the cluster that you've been provided with access to.


> ## Undertake a parallel run of the `osu_latency` benchmark
>
> Move the `osu_benchmarks.sif` Singularity image onto the cluster (or other suitable) platform where you're going to undertake your benchmark run.
> 
> You should be able to run the benchmark using a command similar to the one shown below. However, if you are running on a cluster, you may need to write and submit a job submission script at this point to initiate running of the benchmark.
>
> ~~~
> $ mpirun -np 2 singularity run osu_benchmarks.sif pt2pt/osu_latency
> ~~~
> {: .language-bash}
> 
> > ## Expected output and discussion
> > 
> > As you can see in the mpirun command shown above, we have called `mpirun` on the host system and are passing to MPI the `singularity` executable for which the parameters are the image file and any parameters we want to pass to the image's run script, in this case the path/name of the benchmark executable to run.
> > 
> > The following shows an example of the output you should expect to see. You should have latency values shown for message sizes up to 4MB.
> > 
> >~~~
> > Rank 1 - About to run: /.../mpi/pt2pt/osu_latency
> > Rank 0 - About to run: /.../mpi/pt2pt/osu_latency
> > # OSU MPI Latency Test v5.6.2
> > # Size          Latency (us)
> > 0                       0.38
> > 1                       0.34
> > ...
> > ~~~
> > {: .output}
> {: .solution}
{: .challenge}

This has demonstrated that we can successfully run a parallel MPI executable from within a Singularity container. However, in this case, the two processes will almost certainly have run on the same physical node so this is not testing the performance of the interconnects between nodes.

You could now try running a larger-scale test. You can also try running a benchmark that uses multiple processes, for example try `collective/osu_gather`.

> ## Investigate performance when using a container image built on a local system and run on a cluster
> 
> To get an idea of any difference in performance between the code within your Singularity image and the same code built natively on the target HPC platform, try building the OSU benchmarks from source, locally on the cluster. Then try running the same benchmark(s) that you ran via the singularity container. Have a look at the outputs you get when running `collective/osu_gather` or one of the other collective benchmarks to get an idea of whether there is a performance difference and how significant it is.
> 
> Try running with enough processes that the processes are spread across different physical nodes so that you're making use of the cluster's network interconnects.
> 
> What do you see?
> 
> > ## Discussion
> > It's likely that you'll find that performance is significantly better with the version of the code built directly on the HPC platform.
> > 
> > Why might this be?
> > 
> > How big is the performance difference between the two builds of the code?
> > 
> {: .solution}
{: .challenge}

If performance is an issue for you then you are advised to take a look at using the _[bind model](https://sylabs.io/guides/3.5/user-guide/mpi.html#bind-model)_ for building/running MPI applications through Singularity.

## Singularity wrap-up

This concludes the 4 episodes of the course covering Singularity. We hope you found this information useful and that it has inspired you to use Singularity to help enhance the way you build/work with research software.

As a new set of material, we appreciate that there are likely to be improvements that can be made to enhance the quality of the material. We welcome your thoughts, suggestions and feedback on improvements that could be made to help others making use of these lessons.
