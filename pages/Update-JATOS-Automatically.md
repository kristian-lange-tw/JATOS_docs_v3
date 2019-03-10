---
title: Update JATOS automatically
keywords: update
tags:
summary:
sidebar: mydoc_sidebar
permalink: Update-JATOS-automatically.html
folder:
toc: true
last_updated: 10 Mar 2019
---

Since version 3.3.5 you can update your JATOS installaion automatically (if you have admin rights, that is).

The process is pretty self-explanatory:

1. If your JATOS version is not the latest one available, you will get a notification in your [home page](http://localhost:9000/). 
1. Click on 'Update' and the latest version will be automatically downloaded from GitHub. (Save some [special cases](#versions-with-newer-Java-required) the variant downloaded will correspond to the one you have already installed, -linux/MacOS/Win, with/withou Java).
1. We expect no problems, but sh&t happens. We recommend that you *backup your result data and study assets folder* before continuing.
1. After donwload is complete, click on Update. 
1. JATOS will automatically backup your H2 database **but not your MySQL database*, should you have one. 
1. JATOS will stop itself, replace the program files, bring back the backed-up database and study assets and start itself again.
1. Restarting should not take long (under a minute). Refresh your JATOS home page after clicking update, to continue working with your updated version.   

## Special cases

### Pre-releases
Pre-releases will not be available as auto-updates by default. If you want to force this to be the case (and you know what you're doing), append the quesry parameter "&pre-relase" to your JATOS home page to get the option.  

### Major updates
Auto-updating might not always be possible (in the unlikely case of a database scheme change, or another major change). JATOS versions will be flagged so that they are not available. You'll have to do a [manual update](Update-JATOS.md).

### Versions with newer Java equired
As of today, JATOS (v.3.3.4) uses Java 8. Future versions will likely require newer Java versions. If you're updating from a JATOS version using Java 8 to (say) another version using JAVA 11, the auto-update process will automatically download JATOS bundled with Java, regardless of wich variant you are currently using.

### Compatibility, feeback and bug reports
The auto-update feature is available for linux and MacOS, but not in windows systems. It works on Docker. 
We tried our best to make this feature as robust and general as possible, and welcome any bug reports if it did not work in your system. In these cases, please [send us](http://www.jatos.org/Contact-us.html) a description of your system along with your [logs](http://www.jatos.org/Troubleshooting.html#read-log-file-in-the-browser). 

