Data management and cooperation
===============================

In this document, we introduce the basic concepts of data management,
such as browsing, navigating to others’ data, and changing the display
of the images in OMERO. The example here uses OMERO.web, but majority of
the features described here are also present in OMERO.insight.

Description
-----------

We will show:

-  How to browse data in OMERO.web, navigating to yours and other users’ images.


-  How to use the basic layout of OMERO.web for images organized in Projects and Datasets.

-  How to use OMERO.web for viewing of High-Content Screening (HCS) data.

-  How to use the Preview panel.

-  How to adjust the rendering settings of your and other users’ images from the Preview panel.

-  How to move the data between groups if you are data owner.

-  How to move the data between groups if you are an administrator working on behalf of others.

Setup
-----

OMERO.server has been installed and provisioned using an `Ansible playbook <https://github.com/ome/prod-playbooks/blob/master/omero/training-server/playbook.yml>`_.

Resources
---------

-  All data have been pre-imported. For more details, look at `data.md <https://github.com/ome/training-repos/blob/master/data.md>`_.

-  For the HCS data screenshot, the IDR data http://idr.openmicroscopy.org/webclient/?show=well-1420370 were used.

-  To import images and metadata, scripts were used. For more details, check the `maintenance scripts <https://github.com/ome/training-scripts/tree/master/maintenance>`_.

-  For import of images, we use `in_place_import_as.sh <https://github.com/ome/training-scripts/blob/master/maintenance/scripts/in_place_import_as.sh>`_.

-  The cooperation in OMERO is described in `Groups and permissions system <https://docs.openmicroscopy.org/latest/omero/sysadmins/server-permissions.html>`_.

-  To move data between groups using the Command Line Interface see `CLI Moving Objects between Groups <https://docs.openmicroscopy.org/omero/latest/users/cli/chgrp.html>`_.


Step-by-Step
------------

Data layout and ownership, usernames
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

All images for this workshop have been pre-imported for you into the
OMERO.server. For training purposes, we prepared 50 users on the
OMERO.server. Each of these 50 users has their own set of images. These
sets consist of images of the same name, size, shape, form and quality
for each user. Thus, the data of each user appears the same but, in
actual fact, are different and totally independent sets. Thus, small
discrepancies and differences between the users are completely possible.
Further, if one user deletes their own data in OMERO (please do not
delete anything on our server), this will not have any bearing on the
other 49 sets of images belonging to the 49 other users.

The login names of the 50 users are “user-x” where x goes from 1 to 50.
We have given to each of the 50 users in OMERO a unique first name and
surname which we picked from a list of 50 famous scientists e.g. Ada
Lovelace or Francis Crick. This is the name (“your” name) which you will
see in the top-right corner of the OMERO webclient after you log in with your loginname.

In the OMERO webclient the default view shows only your own images.

Browsing and rendering
~~~~~~~~~~~~~~~~~~~~~~

#. In your web browser, go to the server address provided.

#. Log in using the username and password provided.

#. OMERO offers various levels of permissions for groups and users. Depending on the permissions level of each group, a given user might be able to view, annotate or edit data belonging to other users. Permissions are managed by users with admin privileges. For this training session, we will work in a “Read-Annotate” group. This implies that users can view and annotate each other’s data but cannot delete other people’s data.

#. To see other people’s data, click on the (for example``Lab1``) group name in the top-left corner of the webclient. Note that in case you are in a differently named group, the name in the top left corner will accordingly reflect this. Then use the menu to select the name of the group you wish to browse and then the user inside that group whose data you wish to see.

   \ |image0|

#.  You can browse ‘folders’ in the left-hand pane: Image folders are called Datasets and they are within Projects.

#.  When a Dataset is selected, Image thumbnails are shown in the centre panel.\ |image1|

#.  These represent imported Images. The original Images are stored on the server and the generated thumbnails allow us to browse them.

#.  `Bio-Formats <https://www.openmicroscopy.org/bio-formats/>`_ is used to read the pixel-data and metadata from over 150 different image formats, including multi-z timelapse images with many channels, they are referenced as 5D Images. Large pathology and medical images are also supported.

#.  For HCS data, the layout of the OMERO.web is a bit different. The HCS data are usually organized in following manner: ``Images`` are contained in ``Wells``, ``Wells`` are contained in ``Plates`` and ``Plates`` are organized in ``Screens``. The screenshot below shows the typical layout of a ``Plate`` in OMERO.web, where the ``Wells`` are organized in rows and columns. One ``Well`` is selected in central pane and it contains 4 ``Images`` whose thumbnails are displayed below the central pane. The bottom-left corner shows positions of the images inside that ``Well``.

    |image3|

#.  Select an Image. In the right-hand pane, metadata read by Bio-Formats and stored in a relational database is displayed:

    - core metadata in the General tab

    - additional metadata in the Acquisition tab. All the metadata read by Bio-Formats can be downloaded at any time.

#. In the ``Preview`` tab in the right-hand panel, you can also view the Image.

#. For multi-plane images, sliders allow you to move through Z or Time dimensions.

#. Viewing Images DOES NOT download the whole Image to the client. Only the viewed Image plane is rendered from the original Image file on the server and sent back to the client.

#. You can adjust the rendering settings for each channel e.g. turn on/off the channels, adjust color settings, look-up tables, etc..

#. The rendering settings can be saved to the server. This NEVER changes the original Image data and can be reverted at any time.

#. The rendering settings can also be copied and pasted between Images. To modify the rendering settings in batch, click on the ``Save to All`` button to apply the same settings to, for example, all Images in a given Dataset.

#. You can use the settings which other users saved on your Images and apply them for your own Image. These settings are highlighted as thumbnails in the lower part of the Preview pane.
  
   \ |image2|

#. Your own settings are highlighted in blue.

#. You can revert to the original settings for an Image or Dataset. For example, using the context menu for a Dataset in the tree, select ``Rendering Settings > Set Imported and Save``.

Move data between groups
~~~~~~~~~~~~~~~~~~~~~~~~

In OMERO, ``Users`` are organized in ``Groups``. The ``Groups`` allow a level of viewing and cooperation between the members of the group which can be adjusted by changing the permissions level on that group. A ``User`` can be a member and have their data in one or more ``Groups``. Thus it is sometimes necessary to move the data between groups. This action can be done by the owners of the data themselves or by an administrator or an administrator with restricted privileges.

Note that caution has to be taken in case the data are linked to other users containers (``Datasets``, ``Projects``). If you move only the contents of those containers (``Datasets`` or ``Images``) and not the containers themselves (``Projects`` or ``Datasets``), the links between such containers and the ``Images`` or ``Datasets`` which are moved will be deleted.

Further, if any objects are moved, the links to any annotations (such as ``Tags`` or attached ``File annotations``) linked to these objects will be severed in case these annotations belong to others or in case these annotations belong to you but are also linked to some other objects in the original group which are not being moved.

Note that except for using OMERO.web described below, it might be worth in some situations to consider moving data between groups using Command Line Interface. See the Resources section for a link to detailed description of the CLI workflow.

Move data between groups: owners of data
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If you are an owner of the data, you can move the data between the groups you are a member of.

#. In OMERO.web, select the data to be moved in the left-hand side tree.

#. Right-click and select ``Move to Group...``.

   |image4|

#. Select the group you want to move the data to.

#. A message ``Checking which linked objects will be moved`` will appear and a spinner to the left of it. Wait until the spinner vanishes and a list of objects to be moved and a list of objects which are not included in the move appears.

   |image5|

#. Check both lists. Please read the note above about which objects are typically not included and reconsider the ``Move`` action again. The ``not included`` objects will not be linked to the ``Moved`` objects anymore if you go ahead with the move, the linkage will be lost.

#. In case you are not happy with the ``Move`` action to go ahead, select a target Dataset or Project or create a new one and click ``OK``.

Move data between groups: administrators
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The administrators can move the data to any group, not only to the group where the owner of the data is a member. Note though that it is not desirable to create a situation where the data belong to someone who is not a member of the group where the data reside.

Typically an administrator works on behalf of other users in a group where the administrator is not a member. For these cases, some features of OMERO.web help to facilitate the moving of data for others (note that these features are not present in the CLI).

#. Navigate to the data of a user in a group where you are not a member of.

#. Select the data in the left-hand tree.

#. Right-click and select ``Move to Group...``.

#. Follow further the steps descibed in the section ``Move data between groups: owners of data`` above, taking note of the ``Not included`` objects.

#. When creating new Datasets or Projects during the move, note that these containers will belong to the owner of the data, not yourself. Also the links between the new containers and the moved data will belong to the owner of the data. This should help to facilitate a smooth workflow, retaining the data handling possibilities such as reorganizing the data, renaming the containers you created for them etc. for the owner of the data. 


.. |image0| image:: images/management1.png
   :width: 4.15104in
   :height: 3.4592in
.. |image1| image:: images/management2.png
   :width: 5.69271in
   :height: 2.84137in
.. |image2| image:: images/management3.png
   :width: 3.41667in
   :height: 1.625in
.. |image3| image:: images/management4.png
   :width: 7.51667in
   :height: 5in
.. |image4| image:: images/management5.png
   :width: 2in
   :height: 2.4592in
.. |image5| image:: images/management6.png
   :width: 4in
   :height: 4.9in
