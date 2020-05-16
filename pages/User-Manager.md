---
title: Manage JATOS users
keywords: user manager, user, member, password, admin rights, admin, LDAP
tags:
summary:
sidebar: mydoc_sidebar
permalink: User-Manager.html
folder:
toc: true
last_updated: 16 May 2020
---

Each experimenter with access to the JATOS server (though the GUI) is a JATOS User. Users can create, modify and delete the studies they are members of.
They can also export and delete results. Users may also have **admin rights**, which lets them control other users' access to JATOS. 


## Manage users

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


## Authentication via LDAP (version >= 3.5.4)

Many institutions use an LDAP server to manage their users centralized in one place. JATOS allows password authentication via LDAP. For this the LDAP server has to be configured in JATOS ([more about this](Configure-JATOS-on-a-Server.html#ldap-authentication-since-jatos--354)). If LDAP is properly configured an additional checkbox 'LDAP' appears in the 'New User' form right under the 'Admin Rights' checkbox. Check this one to enforce authentication by LDAP. Normal JATOS user (locally authenticated) and LDAP user can co-exist in the same JATOS.

At the moment it is not possible to let JATOS create LDAP users automatically - they must be created by an JATOS admin manually.