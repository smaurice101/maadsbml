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

Follow these steps
'''''''''''''''''''

5. Goto folder: **c:/>pythonpackage/studenttestpackage**

6. Download the Github files locally to your computer from here: `studenttestpackage <https://github.com/smaurice101/raspberrypi/tree/main/createpythonpackage/studenttestpackage>`_

   .. figure:: tp2.png
      :scale: 70%

7. Goto folder: **c:/>pythonpackage/studenttestpackage/studenttestpackage**

8. Download the Github files locally to your computer from here: `studenttestpackage/studenttestpackage <https://github.com/smaurice101/raspberrypi/tree/main/createpythonpackage/studenttestpackage/studenttestpackage>`_

   .. figure:: tp3.png
      :scale: 70%

9. In the file **c:/>pythonpackage/studenttestpackage/setup.py**

   You MUST have the following:

   a. name='studenttestpackage', (THIS MUST MATCH THE NAME OF YOUR PACKAGE)

   b. packages=['studenttestpackage'], (THIS MUST MATCH THE NAME OF YOUR PACKAGE)

   .. figure:: tp4.png
      :scale: 70%

10. Goto folder: **c:/>pythonpackage/studenttestpackage/studenttestpackage**

    .. figure:: tp5.png
       :scale: 70%

11. In the file **c:/>pythonpackage/studenttestpackage/studenttestpackage/__init__.py**

    This is the file that EXPORTS your python function that you write.  In this example all functions are defined in file **myfunctions.py**

You MUST have the following:

   a. name = "studenttestpackage" (THIS MUST MATCH THE NAME OF YOUR PACKAGE)

   .. figure:: tp7.png
      :scale: 70%

   b. The function you define are exported in lines:

      1. **from .myfunctions import sayhello**

      2. **from .myfunctions import saygoodbye**

12. In the file **c:/>pythonpackage/studenttestpackage/studenttestpackage/myfunctions.py**

    This is the file that you define your functions.

   .. figure:: tp8.png
      :scale: 70%



Modify Files to Build Your OWN Python Package
---------------------------------------------

The above files will produce a python package **studenttestpackage** - but you want to create a NEW python package for yourself.  To do this you can easily modify the folders and files.

9. Say you want to create
