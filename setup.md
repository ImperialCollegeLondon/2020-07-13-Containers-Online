---
title: Setup
---
### Website accounts to create
Please seek help at the start of the lesson if you have not been able to establish website accounts on both of:
- The [Docker Hub](http://hub.docker.com). We will use the Docker Hub to download pre-built container images, and for you to upload and download container images that you create, as explained in the relevant lesson episodes.
- [Bitbucket](http://bitbucket.org) is a code project repository site, akin to [GitHub](https://github.org). We will use Bitbucket to create a Docker container from a Docker image that you create.

### Software to install
Please seek help at the start of the lesson if you have not been able to install the appropriate item from the list below, depending on the operating system that your laptop is running:
- macOS: install the [Docker Desktop (Mac)](https://hub.docker.com/editions/community/docker-ce-desktop-mac)
- Microsoft Windows: install the [Docker Desktop (Windows)](https://hub.docker.com/editions/community/docker-ce-desktop-windows)
- Linux: there are too many varieties of Linux to give precise instructions here, but hopefully you can locate documentation for getting Docker installed on your Linux distribution. It may already be installed. Note that Docker do list a number of versions of the Docker Engine for different Linux distributions, at <https://hub.docker.com/search/?type=edition&offering=community>

### Copy/pasting file contents from episodes of the lesson
Let's say you want to copy text off the lesson website and paste it into a file named `myfile` in the current working directory of a shell window. This can be achieved in many ways, depending on your laptop's operating system, but routes I have found work for me:
- macOS and Linux: you are likely to have the `nano` editor installed, which provides you with a very straightforward way to create such a file, just run `nano myfile`, then paste text into the shell window, and press <kbd>control</kbd>+<kbd>x</kbd> to exit: you will be prompted whether you want to save changes to the file, and you can type <kbd>y</kbd> to say "yes".
- Microsoft Windows running `cmd.exe` shells: 
  - `del myfile` to remove `myfile` if it already existed;
  - `copy con myfile` to mean what's typed in your shell window is copied into `myfile`;
  - paste the text you want within `myfile` into the shell window;
  - type <kbd>control</kbd>+<kbd>z</kbd> and then press <kbd>enter</kbd> to finish copying content into `myfile` and return to your shell;
  - you can run the command `type myfile` to check the content of that file, as a double-check.
- Microsoft Windows running PowerShell:
  - The `cmd.exe` method probably works, but another is to paste your file contents between `@'` and `'@` as in this example (the ">" is the prompt indicator):

~~~
> @'
Some hypothetical
file content that is

split over many

lines.
'@ | Set-Contents myfile -encoding ascii
~~~ 

{% include links.md %}

{% comment %}
<!--  LocalWords:  myfile kbd links.md md endcomment
-->
{% endcomment %}
