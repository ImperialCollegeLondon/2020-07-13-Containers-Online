---
title: "Example: Containers used in generating this lesson"
teaching: 20
exercises: 0
questions:
- "What is a specific example of a container used in practice?"
objectives:
- "Demonstrate how this lesson website is made from files using the Jekyll software in a container."
keypoints:
- "By using the container we avoid all the difficult installation issues of installing Jekyll."
---

The website for this lesson is generated mechanically, based on a set of files that specify the configuration of the site, its presentation template, and the content to go on this page. This is far more manageable than editing each webpage of the lesson separately, for example, if the page header needs to change, this change can be made in one place, and all the pages regenerated. The alternative would be needing to edit each page to repeat the change: this is not productive or suitable work for humans to do!

However, these advantages come with a major disadvantage: we need to install the Jekyll framework to build the website and preview what effect our changes have. Jekyll is written in Ruby, has a large list of dependencies and can be complex to install and maintain. Containers to the rescue!

Now open a web browser window and:
1. Navigate to the GitHub repository that contains the files for this session, at <https://github.com/ARCHER-CSE/2020-02-03-durham-docker>;
2. Click the green "Clone or download" button on the right-hand side of the page;
3. Click "Download ZIP".
4. Expand the downloaded ZIP file. It should contain one directory named `2020-02-03-durham-docker-gh-pages`.

> ## There are many ways to work with ZIP files
> Note that the last two steps can be achieved using a Mac or Windows graphical user interface. There are also ways to effect expanding the ZIP archive on the command line, for example, on my Mac I can achieve the effect of those last two steps through running the command `unzip 2020-02-03-durham-docker-gh-pages.zip`.
{: .callout}

In your shell window, if you `cd` into the `2020-02-03-durham-docker-gh-pages` folder and list the files, you should see something similar to what I see:
~~~
$ cd 2020-02-03-durham-docker-gh-pages
$ ls
~~~
{: .language-bash}
~~~
AUTHORS			_episodes		code
CITATION		_episodes_rmd		data
CODE_OF_CONDUCT.md	_extras			fig
CONTRIBUTING.md		_includes		files
LICENSE.md		_layouts		index.md
Makefile		aio.md			reference.md
README.md		assets			setup.md
_config.yml		bin
~~~
{: .output}

You can now request that a container is created that will compile the files in this set into the lesson website and then run a simple webserver to allow you to view your version of the website locally. Note that this command will be long and fiddly to type, so you probably want to copy-and-paste it into your shell window. This command will continue to (re-)generate and serve up your version of the lesson website, so you will not get your shell prompt back until you type <kbd>control</kbd>+<kbd>c</kbd>. This will stop the webserver, since it cleans away the container.

For macOS, Linux and PowerShell:
~~~
$ docker run --rm -it -v ${PWD}:/srv/jekyll -p 127.0.0.1:4000:4000 jekyll/jekyll:3.7.3 make serve
~~~
{: .language-bash}

For `cmd.exe` shells on Microsoft Windows:
~~~
> docker run --rm -it -v "%CD%":/srv/jekyll -p 127.0.0.1:4000:4000 jekyll/jekyll:3.7.3 make serve
~~~

A quick note on what the different options did here:

   - `--rm` automatically deletes the container once it exits
   - `-it` make the container interactive
   - `-v ${PWD}:/srv/jekyll` mount the current directory in the container at `/srv/jekyll`
   - `-p 127.0.0.1:4000:4000` publish the container port 4000 to port 4000 on the host
   - `jekyll/jekyll:3.7.3` the image to generate the container from 
   - `make serve` the command to run in the container

When I ran the macOS command, the output was as follows:

~~~
Unable to find image 'jekyll/jekyll:3.7.3' locally
3.7.3: Pulling from jekyll/jekyll
ff3a5c916c92: Pull complete 
8e2da6035957: Pull complete 
42e99ed6de92: Pull complete 
70c638bbd0d9: Pull complete 
8f8df9937b34: Pull complete 
Digest: sha256:2b907c5f836ee66d6dde39aa021eebadcadd59dffab693ceecb73be7cfa2808b
Status: Downloaded newer image for jekyll/jekyll:3.7.3
jekyll serve
ruby 2.5.1p57 (2018-03-29 revision 63029) [x86_64-linux-musl]
Configuration file: /srv/jekyll/_config.yml
            Source: /srv/jekyll
       Destination: /srv/jekyll/_site
 Incremental build: disabled. Enable with --incremental
      Generating... 
                    done in 2.647 seconds.
 Auto-regeneration: enabled for '/srv/jekyll'
    Server address: http://0.0.0.0:4000
  Server running... press ctrl-c to stop.
~~~
{: .output}

In the preceding output, you see Docker downloading the image for Jekyll, which is a tool for building websites from specification files such as those used for this lesson. The line `jekyll serve` indicates a command that runs within the Docker container instance. The output below that is from the Jekyll tool itself, highlighting that the website has been built, and indicating that there is a server running.

Open a web browser window and visit the address <http://localhost:4000/>. You should see a site that looks very similar to that at <https://archer-cse.github.io/2020-02-03-durham-docker/>.

Using a new shell window, or using your laptop's GUI, locate the file `index.md` within the `2020-02-03-durham-docker-gh-pages` directory, and open it in your preferred editor program.

Near the top of this file you should see the description starting "This session aims to introduce the use of Docker containers with the goal of using them to effect reproducible computational environments." Make a change to this message, and save the file.

If you reload your web browser, the change that you just made should be visible. This is because the Jekyll container saw that you changed the `index.md` file, and regenerated the website.

You can stop the Jekyll container by clicking in its terminal window and typing <kbd>control</kbd>+<kbd>c</kbd>.

You have now achieved using a reproducible computational environment to reproduce a lesson about reproducible computing environments.

{% include links.md %}

{% comment %}
<!--  LocalWords:  keypoints _episodes_rmd CODE_OF_CONDUCT.md aio.md
 -->
<!--  LocalWords:  CONTRIBUTING.md LICENSE.md index.md reference.md
 -->
<!--  LocalWords:  README.md setup.md _config.yml webserver srv
 -->
<!--  LocalWords:  jekyll x86_64-linux-musl favicons github.io
 -->
<!--  LocalWords:  links.md _episodes_rmd _config.yml endcomment
 -->
{% endcomment %}
