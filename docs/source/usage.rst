Usage
=====

.. _installation:

Installation
------------

To use MAADSBML, first install docker engine in your computer:

Setup

1. You will need to have Linux OS installed

• In Windows –you can install WSL (windows subsystem for Linux).  Open Powershell or command prompt in Administrator mode and type:

.. code-block:: console
   wsl --install

Once wsl is installed then update the Linux distro:

.. code-block:: console
   sudo apt update & sudo apt upgrade

• In Mac –Use Terminal

Or get a VM running with Linux Ubuntu installed

2. Install Docker: You can install Docker Desktop (Windows/Mac) Or in linux run: 

.. code-block:: console
   sudoapt install docker.io

3. Pull the maadsbmldocker container:
AMD64 container for Windows/Linux is here: docker pull maadsdocker/maads-batch-automl-otics

ARM64 container for MAC is here: docker pull maadsdocker/maads-batch-automl-otics-arm64

4. Install the MAADSBML Python library:
.. code-block:: console

   (.venv) $ pip install maadsbml

Creating recipes
----------------

To retrieve a list of random ingredients,
you can use the ``lumache.get_random_ingredients()`` function:

.. autofunction:: lumache.get_random_ingredients

The ``kind`` parameter should be either ``"meat"``, ``"fish"``,
or ``"veggies"``. Otherwise, :py:func:`lumache.get_random_ingredients`
will raise an exception.

.. autoexception:: lumache.InvalidKindError

For example:

>>> import lumache
>>> lumache.get_random_ingredients()
['shells', 'gorgonzola', 'parsley']

