---
title: "Creating containers in the cloud"
teaching: 10
exercises: 0
questions:
- "Key question (FIXME)"
objectives:
- "First learning objective. (FIXME)"
keypoints:
- "First key point. Brief Answer to questions. (FIXME)"
---
There are lots of ways containers can be created on cloud computing platforms (a.k.a., "in the cloud"). Most commercial cloud providers now offer a container hosting service that will connect to the Docker Hub in order to fetch the container images that you specify, and charge for the time and resources that the containers use. The container hosting will usually be significantly cheaper than full virtualisation services that might be on offer.

Note also that most cloud providers will give you sign-up credit that you can use for free after you first create your account.

For this lesson, though, we instead use an excellent software project repository platform, Bitbucket, that allows users a monthly quota of minutes for which containers of your choice can be run. Bitbucket allows containers to be created in response to the modification of files within your software project.

> - Note that Bitbucket, GitHub and GitLab all achieve similar functions.
> - Bitbucket offers container-based features that are easier to get at than the equivalent functions in GitHub, although GitHub will soon catch up when they release their GitHub Actions functionality publicly.

### BitBucket

Because the ability to use the `git` version management tool is not a prerequisite of this session, we will use Bitbucket in a rather atypical manner. However we should still be able to clearly see it running a container of your choice, under your control.

### Digital Ocean hosting

Cloud providers such as Digital Ocean

{% include links.md %}
