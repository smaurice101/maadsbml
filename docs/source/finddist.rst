Find The Best Distribution for Your Data
=====================================

MAADSBML has a powerful functionality to find the best distribution for your data.  Meaning, it will apply analyse your data and iterate through 
complex distributions to find the one that BEST fits your data.  

.. important::
   Knowing the distribution of your data is critical for machine learning. Specifically, knowing the distribution is important for:
   - calculating the critical regions for hypothesis testing and confidence intervals
   - Machine learning algorithms are often based on distributional assumptions and violating these assumptions can lead to biased results
   - Helps in the choice of algorithms to use 

How To Find The Best Distribution
----------------------------

MAADSBML has a function called: **finddistribution**.  Refer to :ref:`MAADSBML Python Library API`

This is a powerful yet simple function to use.  With ONE-LINE of code, MAADSBML will find the best distribution for your data in seconds.

How To Use finddistribution Function
"""""""""""""""""""""""""""""""""""""""

The best way is to learn this function is by an example.  In the code below, you can test this function for yourself and see its power. 

The code can be found `here on GitHub <https://github.com/smaurice101/raspberrypi/blob/main/maadsbml/finddistribution.py>`_

The data files are also `here on GitHub <https://github.com/smaurice101/raspberrypi/tree/main/maadsbml>`_

.. code-block:: PYTHON

    import maadsbml
    import numpy as np
    
    def finddist(filename,varname,dataarr,folderpath,imgname,fast=1,topdist=6):
        status,dist,bestdist,alldata=maadsbml.finddistribution(filename,varname,dataarr,folderpath,imgname,fast,topdist)
        print(status)
    
    def genarray():
        mu, sigma = 1, 10.5 # mean and standard deviation
        data = np.random.normal(mu, sigma, 10000)
        return data
        
    
    filename="body_fat.csv"
    varname="%Fat"
    filename="weight_height.csv"
    varname="Height"
    folderpath='C:/MAADS/Companies/firstgenesis/probability distribution'
    imgname="bml"
    dataarr = []
    dataarr = genarray()
    finddist(filename,varname,dataarr,folderpath,imgname,1,3)
   



 

