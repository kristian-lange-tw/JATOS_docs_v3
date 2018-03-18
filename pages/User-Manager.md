---
title: Manage JATOS users
keywords: user manager, user, member, password, admin rights, admin
tags:
summary:
sidebar: mydoc_sidebar
permalink: User-Manager.html
folder:
toc: true
last_updated: 18 Mar 2018
---

Each experimenter with access to the JATOS server (though the GUI) is a JATOS User. Users can create, modify and delete the studies they are members of.
They can also export and delete results. Users may also have **admin rights**, which lets them control other users' access to JATOS. 

**Manage users**

Only users with admin rights have access to the **User Manager** (located in the header on every GUI page). In the User Manager an admin can create new user, change password of other users, or delete other users. 

![Top Bar screenshot](images/user_manager_header.png)

JATOS comes with one user out-of-box: **Admin** (with user name 'admin'). Admin always has admin rights that cannot be revoked. The initial password for Admin is 'admin' should be changed immediately after installation and kept safe!

Additional to the Admin user every other user can be granted admin rights too (although they can be revoked later).

New users can be granted admin rights, by checking the corresponding box. 

![New User screenshot](images/user_manager_new_user.png)

Admins can see a list of users, to grant or revoke admin rights and to delete them if necessary. **Be careful when deleting users! 
This will delete all studies, along with their result data, that this user is the single member of.**

![User manager screenshot](images/user_manager2.png)

Finally, admins can also change the password of other users. To change the password you'll need to enter your own (admin) password, along with the new desired password for the user.

![Change Password screenshot](images/user_manager_change_pw.png)
