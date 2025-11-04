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

     a. `Python 3.12 <https://www.python.org/downloads/release/python-3120/>`_ or greater
          
     b. .. code-block::

           pip install twine==6.2.0

     b. .. code-block::

           pip install setuptools==80.9.0

   4. Create local folder on your machine.  You can choose proper name.  For our example, we will create a folder called: **pythonpackage** 

      a. Inside **pythonpackage** create your package.  For our example, we created **studenttestpackage**

      b. Inside **studenttestpackage** create another folder with the SAME name: **studenttestpackage**

      .. figure:: tp1.png
         :scale: 70% 

      .. important::

         You MUST choose your own unique python package name.  You CAN NOT choose: **studenttestpackage** it is already an existing python package under a different username.

Create Your First Python Package
----------------------------------

.. tip::

   All files for this demo are located on `Github <https://github.com/smaurice101/raspberrypi/tree/main/createpythonpackage>`_

Follow these steps.
'''''''''''''''''''

1. Goto folder: **c:/>pythonpackage/studenttestpackage**

2. Download the Github files from here: `studenttestpackage <https://github.com/smaurice101/raspberrypi/tree/main/createpythonpackage/studenttestpackage>`_

   .. figure:: tp2.png
      :scale: 70%
