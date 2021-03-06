Add Customer / Installation
===========================

Create a new Customer
---------------------

.. figure:: add_customer_or_installation_static/new_customer.png

1. Go to the `Continuous Delivery project settings`_
2. **Create subproject** (screenshot above)

   .. _Continuous Delivery project settings: https://dev.tocco.ch/teamcity/admin/editProject.html?projectId=ContinuousDeliveryNg

.. figure:: add_customer_or_installation_static/new_customer2.png

   Project setting for a new customer

3. Fill in parameters as shown above


.. _create-installation-in-teamcity:

Create a new Installation
-------------------------

.. figure:: add_customer_or_installation_static/new_installation1.png

1. Go to the `Continuous Delivery project settings`_
2. Find the customer you want and click on **edit**. If doesn't exist, it needs to be
   `created <#create-a-new-customer>`_ first.

.. figure:: add_customer_or_installation_static/new_installation2.png

   Build configurations for customers

3. **Create build configuration** (screenshot above)

.. figure:: add_customer_or_installation_static/new_installation3.png

   Template parameters

4. Fill in parameters as shown above
5. Fill in these additional template parameters:

   ============================  =======================================================================================
   CUSTOMER                      Customer name (e.g. agogis or smc but never :strike:`agogistest` or :strike:`smctest`)
   DOCKER_PULL_URL [#f1]_        For prod. systems where a test system exists: [#f3]_

                                    ``registry.appuio.ch/toco-nice-%env.INSTALLATION%test/%env.DOCKER_IMAGE%``

                                 For test systems as well as production system with no test system:

                                    ``""`` (empty)
   DUMP_MODE                     ``dump`` for production systems and ``no_dump`` for test systems [#f2]_
   GIT_TREEISH                   Git branch (e.g. ``releases/2.13``). [#f1]_
   INSTALLATION                  Installation name (e.g. smc or smctest)
   ============================  =======================================================================================

   It shouldn't be necessary to touch any of the other parameters.

|

6. Check again the **DOCKER_PULL_URL** for all the systems of the customer you creating the system for.

   If a test or pilot system already exists and you're creating the production system, make sure that the production system has set DOCKER_PULL_URL right and that is not set on the test or pilot system.

   If you're creating the initial installation e.g. test or pilot make sure DOCKER_PULL_URL isn't set, else it could pull its own image during the deployment.

   Make sure that **GIT_TEEISH** is set right on the test system or pilot system.

.. note::

    The installation needs also to be :doc:`created in OpenShift <../openshift/create_nice_installation>`.


.. rubric:: Footnotes

.. [#f1] If **DOCKER_PULL_URL** is present, the Docker image for the installation is fetched from that URL. Otherwise,
         a new image is built from **GIT_TREEISH**.
.. [#f2] **DUMP_MODE** decides whether a dump is done by default. The user can still override this when deploying.
.. [#f3] This fetches the current image from the test system.
