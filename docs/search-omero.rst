Search for Data
===============

In this section, we present the server-wide search in OMERO. This is an additional option for data management, which complements filtering, mining and using annotations to organize your data, which are described elsewhere in :doc:`annotate`.

**Description**
---------------

We will show:

-  How to start a search in OMERO.web

-  How to search for objects annotated with a specific Key-Value Pair

-  How to use Advanced Search

   -  How to search for terms in specific fields e.g. "name"

   -  How to combine search terms using AND

   -  How to combine search terms using AND NOT

**Setup**
---------

-  The data used are from the siRNAi-HeLa folder available at \ https://downloads.openmicroscopy.org/images/DV/siRNAi-HeLa/

-  The Key-Value Pairs were added to the images in the siRNAi-HeLa Dataset for all users using the script \ https://github.com/ome/training-scripts/blob/master/maintenance/scripts/key_value_pairs.py

**Step-by-Step**
----------------

#.  Open a browser and enter the provided URL

#.  Connect using the provided credentials

#.  Enter mitomycin-A into the search box in the top right corner of the webclient |image1|

#.  Press Enter.

#.  The search results will show any objects e.g. Images or Datasets, which have anywhere the string mitomycin-A.

#.  Several images should be found, from two different datasets.

#.  Refine the search now for only Key-Value Pairs which have the key mitomycin-A and value 0mM by entering mitomycin-A:0mM into the search box and pressing Enter.

#.  Now you should find only 21 images.

#.  Click on the “Advanced search” tab in the search results.

#. Enter mitomycin-A:0mM AND name:VRAQ which will narrow down your previous search for mitomycin-A:0mM to objects which also have VRAQ in their name.

#. You should see 5 results now.

#. Enter mitomycin-A:0mM AND NOT name:VRAQ which will reject all objects which have VRAQ in their name and find only the ones which are named differently.

#. You should see 16 results now.

#. Click on the Browse link |image2|\ in one search result line of the last image (in the right-hand part of the centre pane) to navigate back to the main webclient.

.. |image1| image:: images/search1.png
   :width: 2.38542in
   :height: 0.36458in
.. |image2| image:: images/search2.png
   :width: 0.55208in
   :height: 0.27083in
