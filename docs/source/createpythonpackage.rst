Creating Python Packages
=========================

This site will inform you how to create your own Python Packages on `Pypi.org <https://pypi.org/>`_ .  This is a global public site that is accessible to anyone around the world.  It allows anyone to **pip install <yourpackage>**

Pre-requisite
--------------

You must perform the following pre-requistes.

.. important::

   1. Create an account on `Pypi.org <https://pypi.org/>`_

   2. You must also generate a token. This token should start with **pypi-**.  SAVE THIS TOKEN.  You will need it to upload your package to Pypi.org

   3. Install the following packages:

     a. .. code-block::

           pip install twine==6.2.0

     b. .. code-block::

           pip install setuptools==80.9.0

