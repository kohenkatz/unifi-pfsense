unifi-pfsense
=============

A pfSense package that provides the UniFi Controller software.

Purpose
-------

The objective of this project is to develop and maintain a package that provides [Ubiquiti's](http://www.ubnt.com/) UniFi Controller software for the FreeBSD-based [pfSense](http://www.pfsense.org/) firewall project.

Status
------

The project provides the following:

- UniFi 3.2.7, via download from Ubiquiti
- An rc script to start and stop the UniFi controller
- An installation script to automatically download and install the above

Requirements
------------

- pfSense 2.2 BETA

The *will not work* on any version of pfSense older than 2.2.

Dependencies (installed automatically)
--------------------------------------

- OpenJDK 7
- mongodb
- unzip

Milestones
----------

1. ~~An installation script that is automatic, concise, consistent, and reliable.~~
2. ~~An rc script for starting and stopping the UniFi Controller.~~
3. A FreeBSD port and package for installing the UniFi Controller and related scripts.
4. pfSense user interface elements for managing the UniFi Controller.
5. A complete pfSense-style package.

Once the package is stable, we have some other big ideas:

- Detailed UniFi reporting in pfSense.
- Graph data for RRDtool.
- Dashboard widgets: AP status, connected users
- Captive portal integration
- Integrated "wireless" configuration
- Backup and restore integration
- Whatever else we can dig out of the API and mongodb

Challenges
----------

- Because the UniFi Controller software is proprietary, it cannot be built from source and cannot be included directly in a package. To work around this, we can download the UniFi controller software from Ubiquiti during the installation process.
- Because Ubiquiti does not provide a uniform way to identify the latest version, it will be up to the package maintainer to track the Ubiquiti blog and keep the script up to date with the latest software download URL.

Licensing
---------

This project itself is licensed according to the two-clause BSD license.

The UniFi Controller software is licensed as-is with no warranty, according to the README included with the software.

[Ubiquiti has indicated via email](https://github.com/gozoinks/unifi-pfsense/wiki/Tacit-Approval) that acceptance of the EULA on the web site is not required before downloading the software.

Installation
------------

To install the controller software and the rc script:

1. Log in to the pfSense command line shell as root.
2. Run this one-line command, which downloads the install script from Github and executes it with sh:

  ```
    fetch -o - http://git.io/pRYzMA | sh -s
  ```

The install script will install dependencies, download the UniFi controller software, make some adjustments, and start the UniFi controller.

Starting and Stopping
---------------------

To start and stop the controller, use the `service` command from the command line.

- To start the controller:

  ```
    service unifi start
  ```
  The UniFi controller takes a few minutes to start. The 'start' command exits immediately while the startup continues in the background.

- To stop the controller:

  ```
    service unifi stop
  ```
  The the stop command takes a while to execute, and then the shutdown continues for several minutes in the background. The rc script will wait until the command received and the shutdown is finished. The idea is to hold up system shutdown until the UniFi controller has a chance to exit cleanly.

References
----------

These sources of information immediately come to mind:

- [UniFi product information page](http://www.ubnt.com/enterprise/#unifi)
- [UniFi updates blog](https://community.ubnt.com/t5/UniFi-Updates-Blog/bg-p/Blog_UniFi)
- [pfSense: Developing Packages](https://doc.pfsense.org/index.php/Developing_Packages)

A couple of forum posts:

- [Port shar for Unifi by feld](http://community.ubnt.com/t5/UniFi-Wireless/UniFi-wipes-database-every-restart/td-p/382389)
- [Ubiquiti Unifi package for pfSense](https://forum.pfsense.org/index.php?topic=46342.0)
