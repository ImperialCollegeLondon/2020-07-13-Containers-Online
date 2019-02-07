---
title: "Containers used in generating this lesson"
teaching: 10
exercises: 0
questions:
- "Key question (FIXME)"
objectives:
- "First learning objective. (FIXME)"
keypoints:
- "The generation of this lesson website can be effected using a container."
---
The website for this lesson is generated mechanically, based on a set of files that specify the configuration of the site, its presentation template, and the content to go on this page. This is far more mangeable than editing each webpage of the lesson separately, for example, if the page header needs to change, this change can be made in one place, and all the pages regenerated. The alternative would be needing to edit each page to repeat the change: this is not productive or suitable work for humans to do!

~~~
$ mkdir ~/tmp/copy-of-docker-intro
$ cd ~/tmp/copy-of-docker-intro
$ # open https://github.com/dme26/docker-introduction/
$ # click green Clone or download for pop-up
$ # click "Download ZIP"
$ # copy files from ZIP into this directory
$ unzip ~/Downloads/docker-introduction-gh-pages.zip 
Archive:  /Users/dme/Downloads/docker-introduction-gh-pages.zip
5bcbba1c5ddc2b19b784f7b872fdb7e6790a953c
   creating: docker-introduction-gh-pages/
  inflating: docker-introduction-gh-pages/.editorconfig  
   creating: docker-introduction-gh-pages/.github/
  inflating: docker-introduction-gh-pages/.github/ISSUE_TEMPLATE.md  
  inflating: docker-introduction-gh-pages/.github/PULL_REQUEST_TEMPLATE.md  
  inflating: docker-introduction-gh-pages/.gitignore  
  inflating: docker-introduction-gh-pages/.travis.yml  
 extracting: docker-introduction-gh-pages/AUTHORS  
  inflating: docker-introduction-gh-pages/CITATION  
  inflating: docker-introduction-gh-pages/CODE_OF_CONDUCT.md  
  inflating: docker-introduction-gh-pages/CONTRIBUTING.md  
  inflating: docker-introduction-gh-pages/LICENSE.md  
  inflating: docker-introduction-gh-pages/Makefile  
  inflating: docker-introduction-gh-pages/README.md  
  inflating: docker-introduction-gh-pages/_config.yml  
   creating: docker-introduction-gh-pages/_episodes/
 extracting: docker-introduction-gh-pages/_episodes/.gitkeep  
  inflating: docker-introduction-gh-pages/_episodes/01-introduction.md  
  inflating: docker-introduction-gh-pages/_episodes/02-meet-docker.md  
  inflating: docker-introduction-gh-pages/_episodes/03-creating-containers.md  
  inflating: docker-introduction-gh-pages/_episodes/04-docker-hub.md  
  inflating: docker-introduction-gh-pages/_episodes/05-creating-container-images.md  
  inflating: docker-introduction-gh-pages/_episodes/06-containers-on-the-cloud.md  
  inflating: docker-introduction-gh-pages/_episodes/07-containers-for-continuous-integration.md  
   creating: docker-introduction-gh-pages/_episodes_rmd/
 extracting: docker-introduction-gh-pages/_episodes_rmd/.gitkeep  
   creating: docker-introduction-gh-pages/_episodes_rmd/data/
 extracting: docker-introduction-gh-pages/_episodes_rmd/data/.gitkeep  
   creating: docker-introduction-gh-pages/_extras/
 extracting: docker-introduction-gh-pages/_extras/.gitkeep  
  inflating: docker-introduction-gh-pages/_extras/about.md  
 extracting: docker-introduction-gh-pages/_extras/discuss.md  
  inflating: docker-introduction-gh-pages/_extras/figures.md  
 extracting: docker-introduction-gh-pages/_extras/guide.md  
   creating: docker-introduction-gh-pages/_includes/
  inflating: docker-introduction-gh-pages/_includes/all_keypoints.html  
  inflating: docker-introduction-gh-pages/_includes/base_path.html  
  inflating: docker-introduction-gh-pages/_includes/carpentries.html  
   creating: docker-introduction-gh-pages/_includes/dc/
  inflating: docker-introduction-gh-pages/_includes/dc/intro.html  
  inflating: docker-introduction-gh-pages/_includes/dc/schedule.html  
  inflating: docker-introduction-gh-pages/_includes/dc/syllabus.html  
  inflating: docker-introduction-gh-pages/_includes/dc/who.html  
  inflating: docker-introduction-gh-pages/_includes/episode_break.html  
  inflating: docker-introduction-gh-pages/_includes/episode_keypoints.html  
  inflating: docker-introduction-gh-pages/_includes/episode_navbar.html  
  inflating: docker-introduction-gh-pages/_includes/episode_overview.html  
  inflating: docker-introduction-gh-pages/_includes/episode_title.html  
  inflating: docker-introduction-gh-pages/_includes/favicons.html  
  inflating: docker-introduction-gh-pages/_includes/gh_variables.html  
  inflating: docker-introduction-gh-pages/_includes/javascript.html  
   creating: docker-introduction-gh-pages/_includes/lc/
  inflating: docker-introduction-gh-pages/_includes/lc/intro.html  
  inflating: docker-introduction-gh-pages/_includes/lc/schedule.html  
  inflating: docker-introduction-gh-pages/_includes/lc/syllabus.html  
  inflating: docker-introduction-gh-pages/_includes/lc/who.html  
  inflating: docker-introduction-gh-pages/_includes/lesson_footer.html  
  inflating: docker-introduction-gh-pages/_includes/life_cycle.html  
  inflating: docker-introduction-gh-pages/_includes/links.md  
  inflating: docker-introduction-gh-pages/_includes/main_title.html  
  inflating: docker-introduction-gh-pages/_includes/navbar.html  
   creating: docker-introduction-gh-pages/_includes/sc/
  inflating: docker-introduction-gh-pages/_includes/sc/intro.html  
  inflating: docker-introduction-gh-pages/_includes/sc/schedule.html  
  inflating: docker-introduction-gh-pages/_includes/sc/syllabus.html  
  inflating: docker-introduction-gh-pages/_includes/sc/who.html  
  inflating: docker-introduction-gh-pages/_includes/syllabus.html  
  inflating: docker-introduction-gh-pages/_includes/workshop_ad.html  
  inflating: docker-introduction-gh-pages/_includes/workshop_calendar.html  
  inflating: docker-introduction-gh-pages/_includes/workshop_footer.html  
   creating: docker-introduction-gh-pages/_layouts/
  inflating: docker-introduction-gh-pages/_layouts/base.html  
  inflating: docker-introduction-gh-pages/_layouts/break.html  
  inflating: docker-introduction-gh-pages/_layouts/episode.html  
  inflating: docker-introduction-gh-pages/_layouts/lesson.html  
  inflating: docker-introduction-gh-pages/_layouts/page.html  
  inflating: docker-introduction-gh-pages/_layouts/reference.html  
  inflating: docker-introduction-gh-pages/_layouts/workshop.html  
  inflating: docker-introduction-gh-pages/aio.md  
   creating: docker-introduction-gh-pages/assets/
   creating: docker-introduction-gh-pages/assets/css/
  inflating: docker-introduction-gh-pages/assets/css/bootstrap-theme.css  
  inflating: docker-introduction-gh-pages/assets/css/bootstrap-theme.css.map  
  inflating: docker-introduction-gh-pages/assets/css/bootstrap.css  
  inflating: docker-introduction-gh-pages/assets/css/bootstrap.css.map  
  inflating: docker-introduction-gh-pages/assets/css/lesson.scss  
  inflating: docker-introduction-gh-pages/assets/css/syntax.css  
   creating: docker-introduction-gh-pages/assets/favicons/
   creating: docker-introduction-gh-pages/assets/favicons/cp/
 extracting: docker-introduction-gh-pages/assets/favicons/cp/apple-touch-icon-114x114.png  
 extracting: docker-introduction-gh-pages/assets/favicons/cp/apple-touch-icon-120x120.png  
 extracting: docker-introduction-gh-pages/assets/favicons/cp/apple-touch-icon-144x144.png  
 extracting: docker-introduction-gh-pages/assets/favicons/cp/apple-touch-icon-152x152.png  
 extracting: docker-introduction-gh-pages/assets/favicons/cp/apple-touch-icon-57x57.png  
 extracting: docker-introduction-gh-pages/assets/favicons/cp/apple-touch-icon-60x60.png  
 extracting: docker-introduction-gh-pages/assets/favicons/cp/apple-touch-icon-72x72.png  
 extracting: docker-introduction-gh-pages/assets/favicons/cp/apple-touch-icon-76x76.png  
 extracting: docker-introduction-gh-pages/assets/favicons/cp/favicon-128.png  
 extracting: docker-introduction-gh-pages/assets/favicons/cp/favicon-16x16.png  
 extracting: docker-introduction-gh-pages/assets/favicons/cp/favicon-196x196.png  
 extracting: docker-introduction-gh-pages/assets/favicons/cp/favicon-32x32.png  
 extracting: docker-introduction-gh-pages/assets/favicons/cp/favicon-96x96.png  
  inflating: docker-introduction-gh-pages/assets/favicons/cp/favicon.ico  
 extracting: docker-introduction-gh-pages/assets/favicons/cp/mstile-144x144.png  
 extracting: docker-introduction-gh-pages/assets/favicons/cp/mstile-150x150.png  
 extracting: docker-introduction-gh-pages/assets/favicons/cp/mstile-310x150.png  
 extracting: docker-introduction-gh-pages/assets/favicons/cp/mstile-310x310.png  
 extracting: docker-introduction-gh-pages/assets/favicons/cp/mstile-70x70.png  
   creating: docker-introduction-gh-pages/assets/favicons/dc/
 extracting: docker-introduction-gh-pages/assets/favicons/dc/apple-touch-icon-114x114.png  
 extracting: docker-introduction-gh-pages/assets/favicons/dc/apple-touch-icon-120x120.png  
 extracting: docker-introduction-gh-pages/assets/favicons/dc/apple-touch-icon-144x144.png  
 extracting: docker-introduction-gh-pages/assets/favicons/dc/apple-touch-icon-152x152.png  
 extracting: docker-introduction-gh-pages/assets/favicons/dc/apple-touch-icon-57x57.png  
 extracting: docker-introduction-gh-pages/assets/favicons/dc/apple-touch-icon-60x60.png  
 extracting: docker-introduction-gh-pages/assets/favicons/dc/apple-touch-icon-72x72.png  
 extracting: docker-introduction-gh-pages/assets/favicons/dc/apple-touch-icon-76x76.png  
 extracting: docker-introduction-gh-pages/assets/favicons/dc/favicon-128.png  
 extracting: docker-introduction-gh-pages/assets/favicons/dc/favicon-16x16.png  
 extracting: docker-introduction-gh-pages/assets/favicons/dc/favicon-196x196.png  
 extracting: docker-introduction-gh-pages/assets/favicons/dc/favicon-32x32.png  
 extracting: docker-introduction-gh-pages/assets/favicons/dc/favicon-96x96.png  
  inflating: docker-introduction-gh-pages/assets/favicons/dc/favicon.ico  
 extracting: docker-introduction-gh-pages/assets/favicons/dc/mstile-144x144.png  
 extracting: docker-introduction-gh-pages/assets/favicons/dc/mstile-150x150.png  
  inflating: docker-introduction-gh-pages/assets/favicons/dc/mstile-310x150.png  
  inflating: docker-introduction-gh-pages/assets/favicons/dc/mstile-310x310.png  
 extracting: docker-introduction-gh-pages/assets/favicons/dc/mstile-70x70.png  
   creating: docker-introduction-gh-pages/assets/favicons/lc/
 extracting: docker-introduction-gh-pages/assets/favicons/lc/apple-touch-icon-114x114.png  
 extracting: docker-introduction-gh-pages/assets/favicons/lc/apple-touch-icon-120x120.png  
 extracting: docker-introduction-gh-pages/assets/favicons/lc/apple-touch-icon-144x144.png  
 extracting: docker-introduction-gh-pages/assets/favicons/lc/apple-touch-icon-152x152.png  
 extracting: docker-introduction-gh-pages/assets/favicons/lc/apple-touch-icon-57x57.png  
 extracting: docker-introduction-gh-pages/assets/favicons/lc/apple-touch-icon-60x60.png  
 extracting: docker-introduction-gh-pages/assets/favicons/lc/apple-touch-icon-72x72.png  
 extracting: docker-introduction-gh-pages/assets/favicons/lc/apple-touch-icon-76x76.png  
  inflating: docker-introduction-gh-pages/assets/favicons/lc/favicon-128.png  
 extracting: docker-introduction-gh-pages/assets/favicons/lc/favicon-16x16.png  
  inflating: docker-introduction-gh-pages/assets/favicons/lc/favicon-196x196.png  
 extracting: docker-introduction-gh-pages/assets/favicons/lc/favicon-32x32.png  
 extracting: docker-introduction-gh-pages/assets/favicons/lc/favicon-96x96.png  
  inflating: docker-introduction-gh-pages/assets/favicons/lc/favicon.ico  
 extracting: docker-introduction-gh-pages/assets/favicons/lc/mstile-144x144.png  
  inflating: docker-introduction-gh-pages/assets/favicons/lc/mstile-150x150.png  
  inflating: docker-introduction-gh-pages/assets/favicons/lc/mstile-310x150.png  
  inflating: docker-introduction-gh-pages/assets/favicons/lc/mstile-310x310.png  
  inflating: docker-introduction-gh-pages/assets/favicons/lc/mstile-70x70.png  
   creating: docker-introduction-gh-pages/assets/favicons/swc/
 extracting: docker-introduction-gh-pages/assets/favicons/swc/apple-touch-icon-114x114.png  
 extracting: docker-introduction-gh-pages/assets/favicons/swc/apple-touch-icon-120x120.png  
 extracting: docker-introduction-gh-pages/assets/favicons/swc/apple-touch-icon-144x144.png  
 extracting: docker-introduction-gh-pages/assets/favicons/swc/apple-touch-icon-152x152.png  
 extracting: docker-introduction-gh-pages/assets/favicons/swc/apple-touch-icon-57x57.png  
 extracting: docker-introduction-gh-pages/assets/favicons/swc/apple-touch-icon-60x60.png  
 extracting: docker-introduction-gh-pages/assets/favicons/swc/apple-touch-icon-72x72.png  
 extracting: docker-introduction-gh-pages/assets/favicons/swc/apple-touch-icon-76x76.png  
 extracting: docker-introduction-gh-pages/assets/favicons/swc/favicon-128.png  
 extracting: docker-introduction-gh-pages/assets/favicons/swc/favicon-16x16.png  
 extracting: docker-introduction-gh-pages/assets/favicons/swc/favicon-196x196.png  
 extracting: docker-introduction-gh-pages/assets/favicons/swc/favicon-32x32.png  
 extracting: docker-introduction-gh-pages/assets/favicons/swc/favicon-96x96.png  
  inflating: docker-introduction-gh-pages/assets/favicons/swc/favicon.ico  
 extracting: docker-introduction-gh-pages/assets/favicons/swc/mstile-144x144.png  
  inflating: docker-introduction-gh-pages/assets/favicons/swc/mstile-150x150.png  
 extracting: docker-introduction-gh-pages/assets/favicons/swc/mstile-310x150.png  
 extracting: docker-introduction-gh-pages/assets/favicons/swc/mstile-310x310.png  
 extracting: docker-introduction-gh-pages/assets/favicons/swc/mstile-70x70.png  
   creating: docker-introduction-gh-pages/assets/fonts/
  inflating: docker-introduction-gh-pages/assets/fonts/glyphicons-halflings-regular.eot  
  inflating: docker-introduction-gh-pages/assets/fonts/glyphicons-halflings-regular.svg  
  inflating: docker-introduction-gh-pages/assets/fonts/glyphicons-halflings-regular.ttf  
  inflating: docker-introduction-gh-pages/assets/fonts/glyphicons-halflings-regular.woff  
 extracting: docker-introduction-gh-pages/assets/fonts/glyphicons-halflings-regular.woff2  
   creating: docker-introduction-gh-pages/assets/img/
  inflating: docker-introduction-gh-pages/assets/img/cp-logo-blue.svg  
  inflating: docker-introduction-gh-pages/assets/img/dc-icon-black.svg  
  inflating: docker-introduction-gh-pages/assets/img/dc-logo-black.svg  
  inflating: docker-introduction-gh-pages/assets/img/lc-icon-black.png  
  inflating: docker-introduction-gh-pages/assets/img/lc-icon-black.svg  
  inflating: docker-introduction-gh-pages/assets/img/lc-logo-black.png  
  inflating: docker-introduction-gh-pages/assets/img/lc-logo-black.svg  
  inflating: docker-introduction-gh-pages/assets/img/swc-icon-blue.svg  
  inflating: docker-introduction-gh-pages/assets/img/swc-logo-blue.png  
  inflating: docker-introduction-gh-pages/assets/img/swc-logo-blue.svg  
  inflating: docker-introduction-gh-pages/assets/img/swc-logo-white.png  
  inflating: docker-introduction-gh-pages/assets/img/swc-logo-white.svg  
   creating: docker-introduction-gh-pages/assets/js/
  inflating: docker-introduction-gh-pages/assets/js/bootstrap.min.js  
  inflating: docker-introduction-gh-pages/assets/js/jquery.min.js  
  inflating: docker-introduction-gh-pages/assets/js/jquery.min.map  
  inflating: docker-introduction-gh-pages/assets/js/lesson.js  
   creating: docker-introduction-gh-pages/bin/
   creating: docker-introduction-gh-pages/bin/boilerplate/
  inflating: docker-introduction-gh-pages/bin/boilerplate/.travis.yml  
 extracting: docker-introduction-gh-pages/bin/boilerplate/AUTHORS  
 extracting: docker-introduction-gh-pages/bin/boilerplate/CITATION  
  inflating: docker-introduction-gh-pages/bin/boilerplate/CONTRIBUTING.md  
  inflating: docker-introduction-gh-pages/bin/boilerplate/README.md  
  inflating: docker-introduction-gh-pages/bin/boilerplate/_config.yml  
   creating: docker-introduction-gh-pages/bin/boilerplate/_episodes/
  inflating: docker-introduction-gh-pages/bin/boilerplate/_episodes/01-introduction.md  
   creating: docker-introduction-gh-pages/bin/boilerplate/_extras/
  inflating: docker-introduction-gh-pages/bin/boilerplate/_extras/about.md  
 extracting: docker-introduction-gh-pages/bin/boilerplate/_extras/discuss.md  
  inflating: docker-introduction-gh-pages/bin/boilerplate/_extras/figures.md  
 extracting: docker-introduction-gh-pages/bin/boilerplate/_extras/guide.md  
  inflating: docker-introduction-gh-pages/bin/boilerplate/aio.md  
  inflating: docker-introduction-gh-pages/bin/boilerplate/index.md  
 extracting: docker-introduction-gh-pages/bin/boilerplate/reference.md  
 extracting: docker-introduction-gh-pages/bin/boilerplate/setup.md  
  inflating: docker-introduction-gh-pages/bin/chunk-options.R  
  inflating: docker-introduction-gh-pages/bin/generate_md_episodes.R  
  inflating: docker-introduction-gh-pages/bin/knit_lessons.sh  
  inflating: docker-introduction-gh-pages/bin/lesson_check.py  
  inflating: docker-introduction-gh-pages/bin/lesson_initialize.py  
  inflating: docker-introduction-gh-pages/bin/markdown_ast.rb  
  inflating: docker-introduction-gh-pages/bin/repo_check.py  
  inflating: docker-introduction-gh-pages/bin/test_lesson_check.py  
  inflating: docker-introduction-gh-pages/bin/util.py  
  inflating: docker-introduction-gh-pages/bin/workshop_check.py  
   creating: docker-introduction-gh-pages/code/
 extracting: docker-introduction-gh-pages/code/.gitkeep  
   creating: docker-introduction-gh-pages/data/
 extracting: docker-introduction-gh-pages/data/.gitkeep  
   creating: docker-introduction-gh-pages/fig/
 extracting: docker-introduction-gh-pages/fig/.gitkeep  
   creating: docker-introduction-gh-pages/files/
 extracting: docker-introduction-gh-pages/files/.gitkeep  
  inflating: docker-introduction-gh-pages/index.md  
 extracting: docker-introduction-gh-pages/reference.md  
  inflating: docker-introduction-gh-pages/setup.md  
$ pwd
/Users/dme/tmp/copy-of-docker-intro
$ cd docker-introduction-gh-pages/
$ less Makefile 
$ docker run --rm -it -v ${PWD}:/srv/jekyll -p 127.0.0.1:4000:4000 jekyll/jekyll:${JEKYLL_VERSION} make serve
$ less Makefile 
$ less Makefile 
$ echo JEKYLL_VERSION=3.7.3
JEKYLL_VERSION=3.7.3
$ docker run --rm -it -v ${PWD}:/srv/jekyll -p 127.0.0.1:4000:4000 jekyll/jekyll:3.7.3 make serve
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
[2019-02-07 15:37:35] ERROR `/assets/favicons/favicon-96x96.png' not found.
[2019-02-07 15:37:35] ERROR `/assets/favicons/favicon-196x196.png' not found.
[2019-02-07 15:37:35] ERROR `/assets/favicons/favicon-16x16.png' not found.
[2019-02-07 15:37:35] ERROR `/assets/favicons/favicon-128.png' not found.
[2019-02-07 15:37:35] ERROR `/assets/favicons/favicon-32x32.png' not found.
^Cmake: *** [Makefile:26: serve] Interrupt
make: *** wait: No child process.  Stop.
$ # change something on home page
$ nano index.md 
$ docker run --rm -it -v ${PWD}:/srv/jekyll -p 127.0.0.1:4000:4000 jekyll/jekyll:3.7.3 make serve
jekyll serve
ruby 2.5.1p57 (2018-03-29 revision 63029) [x86_64-linux-musl]
Configuration file: /srv/jekyll/_config.yml
            Source: /srv/jekyll
       Destination: /srv/jekyll/_site
 Incremental build: disabled. Enable with --incremental
      Generating... 
                    done in 4.438 seconds.
 Auto-regeneration: enabled for '/srv/jekyll'
    Server address: http://0.0.0.0:4000
  Server running... press ctrl-c to stop.
^Cmake: *** [Makefile:26: serve] Interrupt
make: *** wait: No child process.  Stop.
~~~

{% include links.md %}
