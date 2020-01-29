---
layout: lesson
carpentry: "swc"
venue: "Collingwood College, University of Durham"
address: "Collingwood College, University of Durham, South Road, DH1 3LT (training room on 1st floor above reception)"
country: "UK"
language: "English"
latlng: "54.762968,-1.576440"
humandate: "10:30-16:00, 3 February 2020"
humantime: "10:30 - 16:00"
startdate: 2020-02-03
enddate: 2020-02-03
instructor: ["Andy Turner"]
helper: []
email: ["support@archer.ac.uk"]
collaborative_notes: 
eventbrite: 
root: .
---

<h2>Description</h2>

This session aims to introduce the use of Docker containers with the goal of using them to effect reproducible computational environments. Such environments are useful for ensuring reproducible research outputs, for example.

<h2>Registration</h2>
<p>Please use the <a href="http://archer.ac.uk/training/registration/index.php">ARCHER course registration form</a> to sign up for the workshop.</p>

<p>This course is supported by the <a href="http://www.archer.ac.uk">ARCHER UK national supercomputing service</a> and is free to all academic attendees.</p>

<hr/>

<h2 id="general">General Information</h2>

{% comment %}
  LOCATION

  This block displays the address and links to maps showing directions
  if the latitude and longitude of the workshop have been set.  You
  can use https://itouchmap.com/latlong.html to find the lat/long of an
  address.
{% endcomment %}
{% if page.latlng %}
<p id="where">
  <strong>Where:</strong>
  {{page.address}}.
  Get directions with
  <a href="//www.openstreetmap.org/?mlat={{page.latlng | replace:',','&mlon='}}&zoom=16">OpenStreetMap</a>
  or
  <a href="//maps.google.com/maps?q={{page.latlng}}">Google Maps</a>.
</p>
{% endif %}

{% comment %}
  DATE

  This block displays the date and links to Google Calendar.
{% endcomment %}
{% if page.humandate %}
<p id="when">
  <strong>When:</strong>
  {{page.humandate}}.
  {% include workshop_calendar.html %}
</p>
{% endif %}

{% comment %}
  SPECIAL REQUIREMENTS

  Modify the block below if there are any special requirements.
{% endcomment %}
<p id="requirements">
  <strong>Requirements:</strong> Participants must bring a laptop with a
  Mac, Linux, or Windows operating system (not a tablet, Chromebook, etc.) that they have administrative privileges
  on. They should have a few specific software packages installed (listed
  <a href="#setup">below</a>). They are also required to abide by the <a href="http://archer.ac.uk/training/code-of-conduct/index.php">ARCHER Training Code of Conduct</a>.
</p>

{% comment %}
  ACCESSIBILITY

  Modify the block below if there are any barriers to accessibility or
  special instructions.
{% endcomment %}
<p id="accessibility">
  <strong>Accessibility:</strong> We are committed to making this workshop
  accessible to everybody.
  The workshop organizers have checked that:
</p>
<ul>
  <li>The room is wheelchair / scooter accessible.</li>
  <li>Accessible restrooms are available.</li>
</ul>
<p>
  Materials will be provided in advance of the workshop and
  large-print handouts are available if needed by notifying the
  organizers in advance.  If we can help making learning easier for
  you (e.g. sign-language interpreters, lactation facilities) please
  get in touch (using contact details below) and we will
  attempt to provide them.
</p>

{% comment %}
  CONTACT EMAIL ADDRESS

  Display the contact email address set in the configuration file.
{% endcomment %}
<p id="contact">
  <strong>Contact</strong>:
  Please email
  {% if page.email %}
    {% for email in page.email %}
      {% if forloop.last and page.email.size > 1 %}
        or
      {% else %}
        {% unless forloop.first %}
        ,
        {% endunless %}
      {% endif %}
      <a href='mailto:{{email}}'>{{email}}</a>
    {% endfor %}
  {% else %}
    to-be-announced
  {% endif %}
  for more information.
</p>

<hr/>

> ## Prerequisites
>
> - You should have basic familiarity with using a command shell, and the lesson text will at times request that you "open a shell window", with an assumption that you know what this means.
>   - Under Linux or macOS it is assumed that you will access a `bash` shell (usually the default), using your Terminal application.
>   - Under Windows, Powershell and Git Bash should allow you to use the Unix instructions. We will also try to give command variants for Windows `cmd.exe`.
> - As an item of setup, it is assumed that you have a directory named `container-playground` that you are able to `cd` to using your command shell, *and* are also able to find using your computer's graphical file browser (e.g., Finder on macOS or Windows Explorer). A simple way to achieve this is to create your `container-playground` directory within your computer's `Desktop` folder. (See the Software Carpentry Shell lesson for more details.)
> - The lessons will sometimes request that you use a text editor to create or edit files in particular directories. It is assumed that you either have an editor that you know how to use that runs within the working directory of your shell window (e.g. `nano`), or that if you use a graphical editor, that you can use it to read and write files into the working directory of your shell.
{: .prereq}

<h2 id="setup">Getting Started</h2>

<p>To get started, follow the directions on the <a href="setup/">Setup</a> page to ensure you have a Docker Hub account and the Docker software installed.</p>

<hr/>

{% include links.md %}

{% comment %}

TODO: systematically check for Windows-isms

<!--  LocalWords:  prereq links.md endcomment
 -->
{% endcomment %}
