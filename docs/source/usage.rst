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

To generate a simulation tool for a certain factory, you can use the :py:func:`Factory object.

For example
>>> from classes.classes import Factory
>>> my_factory = Factory(name="MyFactory", resource_names=["Filter", "Mixer"], capacity=[2, 3])
