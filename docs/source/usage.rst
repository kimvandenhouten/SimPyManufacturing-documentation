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
   my_factory = Factory(NAME="MyFactory", RESOURCE_NAMES=["Filter", "Mixer"], CAPACITY=[2, 3])


Creating a product
----------------

To generate a product that can be produced in your factory you can use the :class:`~Product` object.

For example

.. code-block:: python

   from classes.classes import Product
   product = Product(NAME="Enzyme_1", ID=0)
   
Then you will need to define the activities that are needed to make your product using the :class:`~Activity` object. These can be added to the product, including optional temporal relations.

.. code-block:: python

   from classes.classes import Activity
   # Make the activites
   activity0 = Activity(ID=0, PROCESSING_TIME=[10, 15], PRODUCT="Enzyme_1",
                        PRODUCT_ID="0", NEEDS=[1, 0])
   activity1 = Activity(ID=1, PROCESSING_TIME=[20, 30], PRODUCT="Enzyme_1",
                        PRODUCT_ID="0", NEEDS=[0, 1])
   # Add the activities to the product
   product.add_activity(activity=activity0)
   product.add_activity(activity=activity1)
   # Set temporal relations, in this case meaning that activity 1 requests
   # resources 10 minutes after start of activity 0.
   product.set_temporal_relations(TEMPORAL_RELATIONS={(0, 1): 10})

This newly defined product can now be added to the products that can be produced in your factory.

.. code-block:: python

   # Add product to factory
   my_factory.add_product(product=product)
  
Creating a production plan
--------------------------

Now we can used the defined factory, and products to make a production plan using the :class:`~ProductionPlan` object. This entails a set of products that should be produced in the factory, including the deadlines.

.. code-block:: python
   
   from classes.classes import ProductionPlan
   my_productionplan = ProductionPlan(ID=0, SIZE=10, NAME="ProductionPlanJanuary", FACTORY=my_factory,
                                   PRODUCT_IDS=[0, 0, 0], DEADLINES=[70, 100, 120])
   my_productionplan.list_products()
 
The user can also define the sequence in which the products will be prioritized in processing:

.. code-block:: python
   
   my_productionplan.set_sequence(sequence=[2, 0, 1])
   
Run a simulation model
----------------------
Now we are all set to run a simulation model. Our library comprises different variants of the simulation model, and more variants could be added. We now showcase for "simulator_3". This simulation model reflects a system that assumes that each product has one starting activity (0), after which a set of downstream processes start. The resources required for activity 0 will first be requested, and once the product retrieves the resources for activity 0, it starts requesting the machines for downstream processing. When the requests for downstream processing should be delayed a bit more, the user can a priori set a temporal relation. 


.. code-block:: python
   
   from classes.simulator_3 import Simulator
   my_simulator = Simulator(plan=my_productionplan, printing=True)
   my_simulator.simulate(SIM_TIME=1000, RANDOM_SEED=1)
   
 
To run this example, use example.py. 


