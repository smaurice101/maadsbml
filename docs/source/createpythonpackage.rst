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

13. The other files in **c:/>pythonpackage/studenttestpackage/**

    a. **requirements.txt** (This is where you can define additional packages you need and Python will automatically download them so users of your package DO NOT have to)

    b. **license.txt** (This is the file you can define any licensing for your package)

    c. **readme.md** (This is the file where you write the documentation for your package. For example, how to use the functions in **myfunctions.py**

Uploading Your Package to Pypi
------------------------------

You are ready to upload your package.  Follow these steps:

14. Goto folder: **c:/>pythonpackage/studenttestpackage/**

    a. Execute the command 1:

       .. code-block::

          python setup.py sdist bdist_wheel

    .. figure:: tp9.png
       :scale: 70%

    b. Execute the command 2:

       .. code-block::

          twine upload dist/*

    .. figure:: tp10.png
       :scale: 70%

    c. Execute the command 3:

       .. figure:: tp12.png
          :scale: 70%

15. See your package on Pypi.org: `studenttestpackage <https://pypi.org/project/studenttestpackage/>`_

       .. figure:: tp11.png
          :scale: 70%

16. Install your package

    .. code-block::

       pip install studenttestpackage==1.0
        
    .. figure:: tp13.png
       :scale: 70%

17. Run your Python function in your Package

    .. figure:: tp14.png
       :scale: 70%

18. SUCCESSFUL RESULT!

    .. figure:: tp15.png
       :scale: 70%

Modify Files to Build Your OWN Python Package
---------------------------------------------

The above files will produce a python package **studenttestpackage** - but you want to create a NEW python package for yourself.  To do this you can easily modify the folders and files.

.. important::

   Everytime you make changes to your package you MUST provide a new version number in the setup.py

   .. figure:: tp16.png
      :scale: 70%

19. You want to create OWN Package.  To the following:

   a. Modify the name of the package: **studenttestpackage**  to your desired name i.e. **bugsbunny** in steps **4.a** and **4.b**

   b. Modify **9.a** and **9.b** to your new package name **bugsbunny**    

      a. name='bugsbunny', (THIS MUST MATCH THE NAME OF YOUR PACKAGE)

      b. packages=['bugsbunny'], (THIS MUST MATCH THE NAME OF YOUR PACKAGE)

   c. Modify 11.a

      a. name = "bugsbunny" (THIS MUST MATCH THE NAME OF YOUR PACKAGE)

20. Install your package

    .. code-block::

       pip install bugsbunny==1.0
        
