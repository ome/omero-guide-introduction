Administrate Groups and Users
=============================

Description:
------------

This chapter will show how to manage groups and users using the graphical interface in OMERO.web and the command-line interface. Most of following tasks below can only be done by users with some
administrator privileges. We will show:

- How to manage groups, creating and editing a new/existing group
- How to manage users, creating and editing a new/existing user

**Resources:**
--------------

-  Documentation:

   -  https://docs.openmicroscopy.org/latest/omero/sysadmins/server-permissions.html

   -  https://docs.openmicroscopy.org/latest/omero/sysadmins/restricted-admins.html

   -  https://docs.openmicroscopy.org/omero/latest/sysadmins/cli/usergroup.html


Setup:
------

No setup needed for OMERO.web administration panel (see Web Interface chapter below) except working OMERO.web.

**Command Line interface installation**

The installation instructions can be
found at \ https://docs.openmicroscopy.org/latest/omero/users/cli/installation.html\ .


**Step-by-step:**
-----------------

Administrate using the Web Interface
------------------------------------

Below are some useful links to know more about permissions and administrator privileges:

-  https://docs.openmicroscopy.org/latest/omero/sysadmins/server-permissions.html

-  https://docs.openmicroscopy.org/latest/omero/sysadmins/restricted-admins.html

1. In your web browser, go to the server address provided.

2. Log in using the username and password provided.

3. In the top toolbar, click the Admin button |image0|\ .

4. Managing Groups:

   a. Click on the Groups tab.

   b. You can search for groups if desired

   c. To create a new Group:

      i.   Click on the Add new Group button

      ii.  The Name and Permissions fields are mandatory.

      iii. Click Save

   d. To edit a Group:

      iv.  Click on the Pencil button |image1|

      v.   You can add or remove members or group’s owners, change permissions etc..

      vi.  Make sure that the data owned by a user is moved or transferred to another user before removing the user from the group

      vii. Click Save

5. Managing Users:

   e. Click on the Users tab

   f. You can search for users if desired

   g. How to identify users:

      viii. Users with administrator privileges with \ |image2|

      ix.   Active users with\ |image3|

      x.    Inactive users with |image4|

      xi.   LDAP users with |image5|

   h. To create a new User:

      xii.  Click on the Add new User button

      xiii. Mandatory fields are highlighted in red

      xiv.  You can select the role of the user

      xv.   Click Save

   i. To edit a User:

      xvi.   Click on the Pencil button |image6|

      xvii.  You can add or remove the user to/from a group, modify the roles etc..

      xviii. Click Save

   j. Creating an administrator with privileges allows to give some limited rights to some trusted users e.g. to allow a facility manager to import data for other users. It is currently preferable to create users with such roles via the Web Interface.

6. Note that a user can manage his/her settings.

   k. In the top-right corner of the webclient, click on your name

   l. In the dropdown menu, click on User settings

   m. In the dialog that pops up, the user can change password, default group i.e. the group he/she will log in to by default etc.

Administrate using the Command Line Interface
---------------------------------------------

#.  Managing Groups:

    a. By default when creating a group, its permissions level is set to private. To create a new read-annotate group Lab1, run:

       ``$ omero group add Lab1 --type=read-annotate``

       or

       ``$ omero group add Lab1 --perms='rwra--'``

    b. To list all the groups and save the output for example in a CSV file:

       ``$ omero group list --style csv > groups.csv``

    c. To add an existing user user-1 to the Lab1 group and make him/her a group owner (the option ``--as-owner`` is not needed when adding a member), run:

       ``$ omero group adduser user-1 --name=Lab1 --as-owner``

    d. Let’s add trainer-1 as an owner of the group too:

       ``$ omero group adduser trainer-1 --name=Lab1 --as-owner``

    e. To remove user-1 from the list of owners (user-1 will still be a member of the Lab1 group):

       ``$ omero user leavegroup Lab1 --name=user-1 --as-owner``

    f. To remove user-1 from the Lab1 group, run:

       ``$ omero group removeuser user-1 --name=Lab1``

    g. To edit the Lab1 group, first determine its ID:

       ``$ omero group info --group-name Lab1``

       ``id \| name \| perms \| ldap \| # of owners \| # of members``

       ``-----+-------+--------+-------+-------------+--------------``

       ``653 \| Lab1 \| rwra-- \| False \| 0 \| 0``

    h. Change the group name to ``LabN``:

       ``$ omero obj update ExperimenterGroup:653 name='LabN'``

    i. Let’s reset the name back to ``Lab1`` to simplify the rest of the workflow

    j.  Change the group's permissions to read-write:

        ``$ omero group perms --perms='rwrw--' --name='Lab1'``

2. Managing Users:

   a. Create a new user with login name lpasteur and at the same time add this user (with first and last name ``Louis Pasteur``) to the Lab1 group:

      ``$ omero user add lpasteur Louis Pasteur --group-name Lab1``

   b. Let’s now add the user to another group:

      ``$ omero user joingroup Lab1 --name=lpasteur``

   c. To edit the user and for example add an email address, first determine the user’s ID:

      ``$ omero user info --user-name lpasteur``

   d. Add an email address (supposing the ID of the user were ``123``):

      ``$ omero obj update Experimenter:123 email='lpasteur@demo.co.uk'``

   e. Make a user inactive. User cannot be deleted but it is possible to prevent a user from logging in. For that we need to remove the user from the user group (internal OMERO group).

      ``$ omero user leavegroup user --name=lpasteur``

   f. To reactivate the user:

      ``$ omero user joingroup user --name=lpasteur``

   g. LDAP authentication. It is possible to convert non LDAP users to LDAP authentication using the command ``omero ldap setdn``. When using LDAP as an authentication backend, users when they log in will be added to the internal OMERO group called default unless they have already been added to a given group. To add a user before they have ever logged in to OMERO, first create the user (example user name is ``enoether``).

      ``$ omero ldap create enoether``

      Then add the user to the Lab1 group

      ``$ omero group adduser enoether --name=Lab1``

.. |image0| image:: images/groupsusersadm1.png
   :width: 0.75in
   :height: 0.38542in
.. |image1| image:: images/groupsusersadm2.png
   :height: 0.10417in
.. |image2| image:: images/groupsusersadm3.png
   :width: 0.15625in
   :height: 0.15625in
.. |image3| image:: images/groupsusersadm4.png
   :width: 0.15625in
   :height: 0.15625in
.. |image4| image:: images/groupsusersadm5.png
   :width: 0.16667in
   :height: 0.16667in
.. |image5| image:: images/groupsusersadm6.png
   :width: 0.16667in
   :height: 0.1875in
.. |image6| image:: images/groupsusersadm2.png
   :height: 0.10417in
