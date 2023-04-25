Usage
=====

.. _installation:

Installation
------------

To use SimPyManufacturing, first install it using pip:

.. code-block:: console

   (.venv) $ pip install SimPyManufacturing
   
To install the requirements:

.. code-block:: console

   (.venv) $ pip install -r requirements.txt

Creating a factory
----------------

To generate a simulation tool for a certain factory, you can use the :class:`~Factory` object.

For example

.. code-block:: python

   from classes.classes import Factory
   my_factory = Factory(name="MyFactory", resource_names=["Filter", "Mixer"], capacity=[2, 3])


Creating a product
----------------

To generate a product that can be produced in your factory you can use the :class:`~Product` object.

For example

.. code-block:: python

   from classes.classes import Product
   product = Product(name="Enzyme_1", ID=0)
   
Then you will need to define the activities that are needed to make your product using the :class:`~Activity` object.

.. code-block:: python

   from classes.classes import Activity
   activity = Activity(ID=0, PROCESSING_TIME=10, PRODUCT="Enzyme_1", PRODUCT_ID="0", NEEDS=[1, 0])
   activity = Activity(ID=1, PROCESSING_TIME=20, PRODUCT="Enzyme_1", PRODUCT_ID="0", NEEDS=[0, 1])

