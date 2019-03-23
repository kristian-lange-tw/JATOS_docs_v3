---
title: Update JATOS automatically
keywords: update, upgrade, release, install
tags:
summary:
sidebar: mydoc_sidebar
permalink: Update-JATOS-automatically.html
folder:
toc: true
last_updated: 23 Mar 2019
---

Since version 3.3.5 you can update your JATOS automatically (if you have **admin rights** and running on **Mac OS** or **Linux** (including Docker), that is). Windows is not yet supported.

## Normal process

The process is pretty self-explanatory, but anyway, we'll explain it here in detail:

1. If your JATOS version is not the latest one available, you will get a notification in your JATOS' home page.

![Update notification Schreenshot](images/autoupdate-notification.png)

1. We expect no problems, but sh&t happens. We recommend that you **backup your result data and study assets folder** before continuing.
1. Click on _Update_ and after another confirmation the latest version will be downloaded from GitHub and saved in your system's temporary folder. Usually the variant downloaded will be the one without bundled Java. Only in cases where JATOS switches to a newer version of Java a bundled version is required. The download might take a while depending on your internet connection.
1. After dównload is complete, you will be asked again for confirmation. This time you have the option to do a **backup** of your current JATOS installation folder. JATOS will copy the content of its own installation folder into a folder with the name _backup_x.x.x_ (x.x.x is the version before the update). That usually includes your H2 database, your study assets and logs - **but not your MySQL database** (should you have one). If anything goes wrong, you have everything in this backup folder to start the old JATOS again. This backup will use up disk space (therefore you can opt out).

![Update notification Schreenshot](images/autoupdate-update-and-restart.png)

1. After clicking the _Go on_ button, JATOS will stop itself, replace its program files and re-start itself again. This might take up to minute.
1. Refresh your JATOS home page every now and then until you see your updated JATOS' login screen again.


## Special cases

### Pre-releases
Pre-releases will not be available as auto-updates by default. If you want to force this to be the case (and you know what you're doing), append the parameter "&showPreReleases" to your JATOS home page URL.

### Major updates
Auto-updating might not always be possible. JATOS versions will be flagged so that they are not available for auto-update. You'll have to do a [manual update](Update-JATOS.md).

### Versions with newer Java equired
As of today, JATOS (v.3.3.4) uses Java 8. Future versions will likely require newer Java versions. If you're updating from a JATOS version using Java 8 to (say) another version using Java 11, the auto-update process will automatically download JATOS bundled with the new Java, regardless of wich variant you are currently using. If you do not like the bundled Java and use your own version you can always remove the folder _jre_ later on after the update.

### Compatibility, feeback and bug reports
The auto-update feature is available for linux and MacOS, but not for windows systems. It also works on Docker. 
We tried our best to make this feature as robust and general as possible, and welcome any bug reports if it did not work in your system. In these cases, please [send us](http://www.jatos.org/Contact-us.html) a description of your system along with your [logs](http://www.jatos.org/Troubleshooting.html#read-log-file-in-the-browser). 

