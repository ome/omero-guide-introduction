Search for Data
===============

In this section, we present the server-wide search in OMERO. This is an additional option for data management, which complements filtering, mining and using annotations to organize your data, which are described elsewhere in :doc:`annotate`.

Description
-----------

We will show:

-  How to start a search in OMERO.web.

-  How to search for objects annotated with a specific Key-Value Pair.

-  How to use Advanced Search.

   -  How to search for terms in specific fields e.g. "name".

   -  How to combine search terms using AND.

   -  How to combine search terms using AND NOT.

Resources
---------

-  Documentation:

   -  `Search <https://docs.openmicroscopy.org/omero/latest/developers/Modules/Search.html>`_


Setup
-----

-  The data used are from the `siRNAi-HeLa <https://downloads.openmicroscopy.org/images/DV/siRNAi-HeLa>`_ folder.

-  The Key-Value Pairs were added to the images in the siRNAi-HeLa Dataset for all users using the script `key_value_pairs.py <https://github.com/ome/training-scripts/blob/master/maintenance/scripts/key_value_pairs.py>`_.

Step-by-Step
------------

#.  Open a browser and enter the provided URL

#.  Connect using the provided credentials

#.  Enter ``mitomycin-A`` into the search box in the top right corner of the webclient |image1|

#.  Press ``Enter``.

#.  The search results will show any objects e.g. Images or Datasets, which have anywhere the string mitomycin-A.

#.  Several images should be found.

#.  Refine the search now for only Key-Value Pairs which have the key ``mitomycin-A`` and value ``0mM`` by entering ``mitomycin-A:0mM`` into the search box and pressing ``Enter``.

#.  This should narrow down your search and find less results compared with the previous case.

#. Click on the Browse link |image2|\ in one search result line of the last image (in the right-hand part of the centre pane) to navigate back to the main webclient.

Advanced search
---------------

The ``Advanced search`` in OMERO.web gives the opportunity to construct queries with Lucene syntax. These queries will be sent into the OMERO search (which is based on Lucene) unparsed. The possibilities include using logical operators (``AND``, ``OR``, ``NOT``, see workflow below) or fuzzy search (see Search Examples below).

#.  Click on the ``Advanced`` tab in the search results.

#. Enter ``mitomycin-A:0mM AND name:VRAQ`` which will narrow down your previous search for ``mitomycin-A:0mM`` to objects which also have ``VRAQ`` in their name.

#. Enter ``mitomycin-A:0mM AND NOT name:VRAQ`` which will reject all objects which have ``VRAQ`` in their name and find only the ones which are named differently.

.. note::
    Spaces, stars, question marks and ``^`` characters are to be avoided in the Keys.
    If you already have these characters in Keys in your OMERO server,
    then try to replace them with underscores if you want to 
    use the Search functionality on them.
    Spaces, stars, question marks and ``^`` characters in Values 
    are acceptable, but should be avoided if possible, see Search Examples below.

Search examples
---------------

Considering the following setup of 13 separate images:

.. list-table:: Images with Key-Value pairs
   :header-rows: 1

   * - Image ID
     - Image Name
     - Key
     - Value
   * - 1
     - Aurora1
     - GFP H2B
     - 2 uM
   * - 2
     - Aurora2
     - GFP^H2B
     - 2 uM
   * - 3
     - Aurora3
     - H2B
     - 2
   * - 4
     - Aurora4
     - H2B
     - 4
   * - 5
     - Aurora5
     - GFP-H2B
     - 2-uM
   * - 6
     - Aurora6
     - GFP-H2B
     - 2 uM
   * - 7
     - Aurora7
     - GFP_H2B
     - 2_uM
   * - 8
     - Aurora8
     - GFP^H2B
     - 2^uM
   * - 9
     - GFP
     - ``none``
     - ``none``
   * - 10
     - uM
     - ``none``
     - ``none``
   * - 11
     - H2B
     - ``none``
     - ``none``
   * - 12
     - 2
     - ``none``
     - ``none``
   * - 13
     - Aurora13
     - H2B
     - 2 uM

Basic **Search** tab:
   - ``GFP H2B:2 uM`` finds images 1,2,3,5,6,7,8,9,10. In that case, the query is interpreted as ``GFP`` OR ``H2B:2`` OR ``uM``.
   - ``"GFP H2B":2 uM`` throws an error. Do not use quotes around Keys!
   - ``GFP H2B:"2 uM"`` finds images 1,2,5,6,7,8,9. In that case, the query is interpreted as ``GFP`` OR ``H2B:2 uM`` which prevents finding of image 3 with Value ``2``.
   - ``GFP^H2B:2 uM`` finds images 1,2,3,5,6,7,8,9,10. In that case, the query is interpreted as ``GFP`` OR ``H2B:2`` OR ``uM``.
   - ``H2B:2`` finds image 3.
   - ``H2B:4`` finds image 4.
   - ``GFP-H2B:2 uM`` finds images 1,2,5,6,7,8,10.
   - ``GFP-H2B:2-uM`` finds images 5,6.
   - ``GFP-H2B:"2-uM"`` finds images 5,6.
   - ``GFP-H2B:"2 uM"`` finds images 5,6.
   - ``GFP-H2B:"2_uM"`` finds images 5,6.
   - ``GFP_H2B:2_uM`` finds image 7.
   - ``GFP^H2B:2^uM`` finds images 1,2,3,5,6,7,8,9,10.
   - ``GFP`` finds images 1,2,5,6,7,8,9.
   - ``GFP`` with checkbox ``Name`` under ``Restricted by Field`` section checked finds image 9.
   - ``uM`` with checkbox ``Name`` under ``Restricted by Field`` section checked finds image 10.
   - ``H2B`` with checkbox ``Name`` under ``Restricted by Field`` section checked finds image 11.
   - ``2`` with checkbox ``Name`` under ``Restricted by Field`` section checked finds image 12.
   - ``GFP*:2 uM`` throws an error. Do not use wildcards in Keys!
   - ``H2B:*`` finds images 3,4,13. The wildcard can be used in Values.
   - ``H2B:2*`` finds images 3,13.

**Advanced** tab:
   - ``GFP^H2B:2^uM`` and ``GFP^H2B:2 uM`` throw an error in ``Advanced`` tab. This is due to the different interpretation of the ``^`` character between the basic ``Search`` and ``Advanced`` tabs.
   - As there is no ``Name`` checkbox in the ``Advanced`` tab, use ``name:GFP`` instead, which finds image 9.
   - ``Aurora2~0.85`` finds 1,2,3,4,5,6,7,8. The ``~`` denotes a ``fuzzy`` search, which is possible only in ``Advanced`` tab. The number behind the ``~`` indicates the precision with which the result must match the query.
   - ``Aurora2~0.86`` finds image 2.

The behaviour for the rest of the query examples in ``Advanced`` tab is the same as listed above for the basic ``Search`` tab.

.. |image1| image:: images/search1.png
   :width: 2.38542in
   :height: 0.36458in
.. |image2| image:: images/search2.png
   :width: 0.55208in
   :height: 0.27083in
