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

-  How to use the basic layout of OMERO.web.

-  How to use the Preview panel.

-  How to adjust the rendering settings of yours and other users’ images from the Preview panel.

Setup
-----

OMERO.server has been installed and provisioned using an `Ansible playbook <https://github.com/ome/prod-playbooks/blob/master/omero/training-server/playbook.yml>`_.

Resources
---------

-  All data have been pre-imported. For more details, look at `data.md <https://github.com/ome/training-repos/blob/master/data.md>`_.

-  To import images and metadata, scripts were used. For more details, check the `maintenance scripts <https://github.com/ome/training-scripts/tree/master/maintenance>`_.

-  For import of images, we use `in_place_import_as.sh <https://github.com/ome/training-scripts/blob/master/maintenance/scripts/in_place_import_as.sh>`_.

-  The cooperation in OMERO is described in `Groups and permissions system <https://docs.openmicroscopy.org/latest/omero/sysadmins/server-permissions.html>`_.

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

#. To see other people’s data, click on the Lab1 group name in the top-left corner of the webclient. Then use the menu to select the name of the user whose data you wish to see.

   \ |image0|

#.  You can browse ‘folders’ in the left-hand pane: Image folders are called Datasets and they are within Projects.

#.  When a Dataset is selected, Image thumbnails are shown in the centre panel.\ |image1|

#.  These represent imported Images. The original Images are stored on the server and the generated thumbnails allow us to browse them.

#.  `Bio-Formats <https://www.openmicroscopy.org/bio-formats/>`_ is used to read the pixel-data and metadata from over 150 different image formats, including multi-z timelapse images with many channels, they are referenced as 5D Images. Large pathology and medical images are also supported.

#.  Select an Image. In the right-hand pane, metadata read by Bio-Formats and stored in a relational database is displayed:

    - core metadata in the General tab

    - additional metadata in the Acquisition tab. All the metadata read by Bio-Formats can be downloaded at any time.

#. In the Preview tab in the right-hand panel, you can also view the Image.

#. For multi-plane images, sliders allow you to move through Z or Time dimensions.

#. Viewing Images DOES NOT download the whole Image to the client. Only the viewed Image plane is rendered from the original Image file on the server and sent back to the client.

#. You can adjust the rendering settings for each channel e.g. turn on/off the channels, adjust color settings, look-up tables, etc..

#. The rendering settings can be saved to the server. This NEVER changes the original Image data and can be reverted at any time.

#. The rendering settings can also be copied and pasted between Images. To modify the rendering settings in batch, click on the ``Save to All`` button to apply the same settings to, for example, all Images in a given Dataset.

#. You can use the settings which other users saved on your Images and apply them for your own Image. These settings are highlighted as thumbnails in the lower part of the Preview pane.
  
   \ |image2|

#. Your own settings are highlighted in blue.

#. You can revert to the original settings for an Image or Dataset. For example, using the context menu for a Dataset in the tree, select ``Rendering Settings > Set Imported and Save``.

.. |image0| image:: images/management1.png
   :width: 4.15104in
   :height: 3.4592in
.. |image1| image:: images/management2.png
   :width: 5.69271in
   :height: 2.84137in
.. |image2| image:: images/management3.png
   :width: 3.41667in
   :height: 1.625in
