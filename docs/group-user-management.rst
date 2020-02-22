Administrate Groups and Users
=============================

Administrate using the Web Interface
------------------------------------

Most of following tasks below can only be done by users with some
administrator privileges. The following steps will be done by the
trainer. Below are some useful links to know more about permissions and administrator privileges:

-  https://docs.openmicroscopy.org/latest/omero/sysadmins/server-permissions.html

-  https://docs.openmicroscopy.org/latest/omero/sysadmins/restricted-admins.html

1. In your web browser, go to the server address provided.

2. Login using the username and password provided.

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

      v.   You can add or remove members or group’s owners. Change permissions etc..

      vi.  Make sure that the data owned by a user is moved or transferred to another user before removing the user from the group

      vii. Click Save

5. Managing Users:

   e. Click on the Users tab

   f. You can search for users if desired

   g. How to identify users:

      viii. Users with administrators privileges with \ |image2|

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

      xvii.  You can add or remove the user to/from a group. Modify the roles etc..

      xviii. Click Save

   j. Creating an administrator privileges allow to give some limited rights to some trusted users e.g. to allow a facility manager to import data for other users. It is currently preferable to create users with such role via the Web Interface.

6. Note that a user can manage his/her settings.

   k. In the top-right corner of the webclient, click on your name

   l. In the dropdown menu, click on User settings

   m. In the dialog that pops up, the user can change password, default group i.e. the group he/she will log in by default etc.

Administrate using the Command Line Interface
---------------------------------------------

1. Managing Groups:

   a. By default when creating a group, its permissions level is set to private. To create a new read-annotate group Lab1, run:

..

   $ bin/omero group add Lab1 --type=read-annotate

   Or

   $ bin/omero group add Lab1 --perms='rwra--'

b. To list all the groups and save the output for example in a CSV file:

..

   $ bin/omero group list --style csv > groups.csv

c. To add an existing user user-1 to the Lab1 group and make him/her a group owner (the option --as-owner is not needed when adding a member), run:

..

   $ bin/omero group adduser user-1 --name=Lab1 --as-owner

d. Let’s add trainer-1 as an owner of the group too:

..

   $ bin/omero group adduser trainer-1 --name=Lab1 --as-owner

e. To remove user-1 from the list of owners (user-1 will still be a
      member of the Lab1 group):

..

   $ bin/omero user leavegroup Lab1 --name=user-1 --as-owner

f. To remove user-1 from the Lab1 group, run:

..

   $ bin/omero group removeuser user-1 --name=Lab1

g. To edit the Lab1 group:

   i. First determine its ID:

..

   $ bin/omero group info --group-name Lab1

   id \| name \| perms \| ldap \| # of owners \| # of members

   -----+-------+--------+-------+-------------+--------------

   653 \| Lab1 \| rwra-- \| False \| 0 \| 0

ii. Change its name to "LabN":

$ bin/omero obj update ExperimenterGroup:653 name='LabN'

iii. Let’s reset the name back to “Lab1” to simplify the rest of the workflow

iv.  Change groups permissions to read-write:

$ bin/omero group perms --perms='rwrw--' --name='Lab1'

2. Managing Users:

   h. Create a new user user-lab1 and add the user to the Lab1 group:

..

   $ bin/omero user add user-lab1 Jan Purkyne --group-name Lab1

i. Let’s now add the user to another group:

..

   $ bin/omero user joingroup Lab1 --name=user-lab1

j. To edit the user and for example add an email address

   v. First determine the user’s ID:

..

   $ bin/omero user info --user-name user-lab1

vi. Add an email address:

..

   $ bin/omero obj update Experimenter:123
   email=j\ \ `purkyne@demo.co.uk <mailto:lpasteur@demo.co.uk>`__

k. Make a user inactive:

   vii. User cannot be deleted but it is possible to prevent a user from logging in. For that we need to remove the user from the user group (internal OMERO group).

..

   $ bin/omero user leavegroup user --name=user-lab1

l. To reactivate the user:

..

   $ bin/omero user joingroup user --name=user-lab1

m. LDAP authentication:

   viii. It is possible to convert non LDAP users to LDAP authentication using the command bin/omero ldap setdn

   ix.   When using LDAP as an authentication backend, users when they log in will be added to the internal OMERO group called default unless they have already been added to a given group. To add a user before they have ever logged in to OMERO, run:

         1. First create the user

..

   $ bin/omero ldap create enoether

2. Then add the user to the Lab1 group

..

   $ bin/omero group adduser enoether --name=Lab1

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
