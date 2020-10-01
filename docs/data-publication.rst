Prepare data for publication using OMERO
========================================

Users can publish Image data to the world using OMERO. Here we describe some steps to facilitate that. The steps are to be done by an administrator or restricted administrator in OMERO. 


Description
-----------

We will show:

-  How to set up configurations in OMERO.web for establishing of a ``public user``.

-  How to set up a ``public group``.

-  How to get the data into the ``public group``.

-  How to open the ``public group`` to the outer world.

Setup
-----

OMERO.server has been installed and provisioned using an `Ansible playbook <https://github.com/ome/prod-playbooks/blob/master/omero/training-server/playbook.yml>`_.

OMERO.server configurations for publication are described in the following chapters of `the publication in OMERO documentation <https://docs.openmicroscopy.org/omero/latest/sysadmins/public.html>`_:

- `Configuring public user <https://docs.openmicroscopy.org/omero/latest/sysadmins/public.html#configuring-public-user>`_.
- `Reusing OMERO sessions <https://docs.openmicroscopy.org/omero/latest/sysadmins/public.html#reusing-omero-sessions>`_.

Resources
---------

-  The publication in OMERO is described in `the documentation <https://docs.openmicroscopy.org/omero/latest/sysadmins/public.html>`_.

Step-by-Step
------------

#. Consult with the system administrator of your OMERO.server the `configuring of public user on the server <https://docs.openmicroscopy.org/omero/latest/sysadmins/public.html>`_. Read the possibilities about how to restrict the access to the data in public group using url filtering in `the publication with OMERO documentation <https://docs.openmicroscopy.org/omero/latest/sysadmins/public.html>`_

#. Establish a ``public group`` with read-only permissions. See the `publication example documentation <https://docs.openmicroscopy.org/omero/5.6.1/sysadmins/public.html#full-example-of-hosting-data-for-a-publication>`_ and the :doc:`group-user-management` for how to do it. Note: The ``public group`` is just an ordinary read-only group, only a subsequent addition of the ``public user`` to this group makes it public.

#. Think about the best strategy of data layout in the ``public group``, see suggestions about it in the `Group setup part of publication example documentation <https://docs.openmicroscopy.org/omero/latest/sysadmins/public.html#group-setup>`_.

#. Duplicate the data to be published as described in :doc:`data-management` either yourself, or instruct the lead scientist on the publication to do this. It is recommended to duplicate the annotations as well, which is done by the duplication plugin by the default, as this will facilitate the preservation of the linkage between the data and annotations during the subsequent move to the public group.

#. Consult with the scientists intending to publish their data about how to Move the data into the ``public group``, or move them yourself. Some helpful hints about the data Move can be found in the `Data migration chapter of the documentation <https://docs.openmicroscopy.org/omero/latest/sysadmins/public.html#data-migration>`_. The move between groups is made easier by making duplicates of the data prior to the move and then moving these duplicates (see previous step). Also see the chapter ``Move data between groups`` in :doc:`data-management` for how to Move the data between groups. The other option is to import the data afresh into the ``public group``. Note: there is no possiblity to copy or link the data in a single step into ``public group`` from another group in OMERO at the moment. The duplication of the data and subsequent move of the duplicate into the public group is the recommended workflow.

#. Once you are happy with the setup of the ``public group``, add the ``public user`` into the ``public group`` as described in `the documentation <https://docs.openmicroscopy.org/omero/latest/sysadmins/public.html>`_. See :doc:`group-user-management` for how to add users into groups in OMERO. The additon of the ``public user`` will make the data in the ``public group`` visible to the world.
