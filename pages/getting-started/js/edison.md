---
layout: "page-fullwidth"
title: "Setting Up Your Intel Edison"
subheadline: "Building Connected Things with Node.js, Johnny-Five, and Microsoft Azure"
teaser: "In this lab, you will configure your Intel Edison for use in labs, tutorials, and workshops."
show_meta: true
comments: false
header: no
breadcrumb: true
categories: [intel-edison, node, iot, maker]
permalink: /getting-started/js/edison/
---

> This is premilinary information and is not a complete Getting Started Guide

# Table of Contents
*  Auto generated table of contents
{:toc}

# Bill of Materials (BOM)
To complete the setup and configuration of your Intel Edison you will need the following:

1. [Intel® Edison for Arduino](http://www.seeedstudio.com/depot/Intel-Edison-for-Arduino-p-2149.html)
2. Two (2) USB to micro USB cables.

# Install Drivers
Follow the [Getting Started](https://software.intel.com/en-us/iot/library/edison-getting-started){:target="_blank"} instructions from Intel to install any needed drivers 

## Flash the Edison to the Latest Yocto Image
Yocto is the official Linux image compiled for the Intel Edison. The _Intel® Edison Board Firmware Software Release 3.0_ (Yocto 2.1) includes Node.js v0.10.x.

1. Attach the Edison chip to the Arduino expansion board.

<div id="flash-edison-tabs">
  <ul>
    <li><a href="#windows10"><span>Windows 8/10</span></a></li>
    <li><a href="#windows7"><span>Windows 7</span></a></li>
    <li><a href="#elcapitan"><span>El Capitan</span></a></li>
    <li><a href="#yosemite"><span>Yosemite</span></a></li>
    <li><a href="#linux"><span>Linux</span></a></li>
  </ul>
  <div id="windows10">
    Download and run the <a target="_blank" href="https://software.intel.com/en-us/iot/hardware/edison/downloads">installer from Intel</a>
    
    <p><strong>IMPORTANT:</strong> When running the Windows installer, uncheck everything except for the drivers and the "flash / update" device option.</p>
  </div>
  <div id="windows7">
    Follow the <a target="_blank" href="http://www.intel.com/content/www/us/en/support/boards-and-kits/000005795.html">Instructions from Intel</a>
  </div>
  <div id="elcapitan">
    Follow the <a target="_blank" href="http://rexstjohn.com/intel-edison-el-capitan-setup-process/">Instructions from Rex St. John</a>
  </div>
  <div id="yosemite">
    {% include edison/setup-yosemite.md %}
  </div>
  <div id="linux">
    Follow the <a target="_blank" href="http://www.intel.com/content/www/us/en/support/boards-and-kits/000005990.html">Instructions from Intel</a>
  </div>
</div>

<script>
$( "#flash-edison-tabs" ).tabs();
</script>
 
## Configure Your Edison
Open terminal, type 'screen /dev/cu.usbs' then hit Tab to autocomplete, add '115200 -L' and hit Enter twice at blank screen
 
<div id="config-edison-tabs">
  <ul>
    <li><a href="#windows10"><span>Windows 8/10</span></a></li>
    <li><a href="#windows7"><span>Windows 7</span></a></li>
    <li><a href="#osx"><span>Mac OS X (all)</span></a></li>
    <li><a href="#linux"><span>Linux</span></a></li>
  </ul>
  <div id="windows10">
    <ol>
    <li>Download PuTTy</li> 
    <li>Select 'serial'</li> 
    <li>Set baud rate to 115200</li>
    <li>Use Device Manager to find your COM port (select the COM port that doesn't say "Edison" anywhere in it)</li>
    <li>Press Enter twice at blank screen</li>
    </ol>
  </div>
  <div id="windows7">
    Follow the <a target="_blank" href="http://www.intel.com/content/www/us/en/support/boards-and-kits/000005795.html">Instructions from Intel</a>
  </div>
  <div id="osx">
    Open terminal, type 'screen /dev/cu.usbs' then hit Tab to autocomplete, add '115200 -L' and hit Enter twice at blank screen
  </div>
  <div id="linux">
    Install 'screen,' use "/dev/ttyUSB0 115200" and hit Enter twice at blank screen
  </div>
</div>

<script>
$( "#config-edison-tabs" ).tabs();
</script>


1. Login with __root__ and no password.
2. Run <code>configure_edison --setup</code>
3. Enter a new password for your Edison
4. Give your Edison a unique name.
5. Enter <code>Y</code> to setup Wi-Fi. If scanning fails to discover your Wi-Fi network, enter <code>0</code> to scan again.
6. Enter the numer for the network you want to connect to.
7. Enter the network password.
8. When the new IP address for your Edison is displayed on screen, make a note of it for later use.

## Install Libmraa
Libmraa is a C/C++ library with bindings to Python, Javascript and Java to interface with the I/O on Galileo, Edison & other platforms, with a structured and sane API where port names/numbering matches the board that you are on. Use of libmraa does not tie you to specific hardware with board detection done at runtime you can create portable code that will work across the supported platforms.

Using the screen session to the Edison, run the following

{% highlight text %}
$ echo "src mraa-upm http://iotdk.intel.com/repos/1.1/intelgalactic" > /etc/opkg/mraa-upm.conf
$ opkg update
$ opkg install libmraa0
$ opkg upgrade
$ cd /
$ cd node_app_slot
$ npm install
$ node blink.js
{% endhighlight %}

## Install FileZilla
You can either edit code directly on your Intel Edison or you can edit the code on your computer and copy it to your Edison using SCP or FileZilla! FileZilla Client is a fast and reliable cross-platform FTP, FTPS and SFTP client with lots of useful features and an intuitive graphical user interface. 

Install from [filezilla-project.org](https://filezilla-project.org/)

Deploying code you the Edison is as easy as Drag-n-Drop

1. Open FileZilla
2. Enter the IP address of your Edison in the _Host_ field.
3. Enter __root__ in the _Username_ field
4. ENter the password you created in the _Password field_
5. Enter __22__ in the _Port_ field
6. Click _Quickconnect_
7. Drag & drop files from your machine onto the Edison