---
title: "Introducing containers"
teaching: 10
exercises: 0
questions:
- "What are containers, and why might they be useful to me?"
objectives:
- "Explain the notion of virtualisation in computing."
- "Explain the ways in which virtualisation may be useful."
- "Explain how containers streamline ."
keypoints:
- "Virtualisation is an old technology that container technology makes more practical."
- "Docker is just one software platform that can create containers and the resources they use."
---
### Background: virtualisation in computing

Some uses of computers and the software they run should be deterministic, particularly when building reproducible computational environments. The meaning of "deterministic" is: if you feed in the same input, to the same computer, then the same output will appear.

However a computer running deterministic software, let's call it the "guest", should *itself* be able to be simulated as a deterministic computational process running on a computer we will call the "host". The guest computer can be said to have been virtualised: and will often be referred to a "virtual machine" (or VM): it is no longer a physical computer. 

> Note that this description elides many details and complexities that are not particularly relevant to this lesson, for example:
> - Thinking with analogy to movies such as Inception, The Matrix, etc., can the guest computer figure out that it's not actually a physical computer, and that it's running as software inside a host physical computer? Yes, it probably can... but let's not go there.
> - Can you run a host as a guest itself within another host? Sometimes... but let's not go there, either!

### Motivation for virtualisation

What features does virtualisation offer?
- Isolation: the VM is self-contained, so you can create and destroy it without affecting the host computer.
- Reproducibility: the VM can be "wound-back" to a known-good situation, much as you might revert a document you are editing to the last saved state.
- Manageability: the VM is software, so can be saved and restored as you might a document file (albeit a *much* larger file than your typical document file!).
- Migration: the VM is software, so can be transmitted to another physical host and run in the same way from there.

Downsides of "full" virtualisation:
- The file describing a VM has to contain its entire simulated hard-disk, so this leads to very large files.
- A host needs *lots* of RAM to run large numbers of virtual machines, as the strong isolation means that the VMs do not share any resources.

### Containers are a type of lightweight virtualisation

Containers are cut-down virtual machines. Containers sacrifice the strong isolation that full virtualisation provides in order to vastly reduce the resource requirements on the virtualisation host.

The term "container" can be usefully considered with reference to shipping containers. Before shipping containers were developed, packing and unpacking cargo ships was time consuming, and error prone, with high potential for different clients' goods to become mixed up. Software containers standardise the packaging of a complete software system (the lightweight virtual machine): you can drop a container into a container host, and it should "just work".

Hopefully this lesson will demonstrate the portability aspect of containers, showing the *same* containers running on:
- macOS;
- Microsoft Windows;
- (any Linux users out there?); and
- in the cloud.

### Docker is a popular container platform

Docker is software that manages containers and the resources that containers need. While Docker is a clear leader in the container space, there are many similar technologies available... we just need to pick one to use for this workshop.

### Docker's terminology

- **Image**: this is the term that Docker uses to describe the template from which live instances of containers will be created. The term "container image" may sometimes be used to emphasise that the "image" relates to software containers and not, say, cute kitten pictures.
- **Container**: this is an instance of a lightweight virtual machine created by Docker from a (container) image.
- **Hub**: the Docker hub is a storage resource and associated website where a vast collection of preexisting container images are documented, and are made available for your use.

{% include links.md %}

