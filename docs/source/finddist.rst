Find The Best Distribution For Your Data
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

Here are all the distributions it will analyse for your data, and choose the BEST one.
.. code-block::

      [‘alpha’, ‘anglit’, ‘arcsine’, ‘argus’, ‘beta’, ‘betaprime’, ‘bradford’, ‘burr’, ‘burr12’, 
      ‘cauchy’, ‘chi’, ‘chi2’, ‘cosine’, ‘crystalball’, ‘dgamma’, ‘dweibull’, ‘erlang’, ‘expon’, 
      ‘exponnorm’, ‘exponpow’, ‘exponweib’, ‘f’, ‘fatiguelife’, ‘fisk’, ‘foldcauchy’, ‘foldnorm’, 
      ‘frechet_l’, ‘frechet_r’, ‘gamma’, ‘gausshyper’, ‘genexpon’, ‘genextreme’, ‘gengamma’, 
      ‘genhalflogistic’, ‘geninvgauss’, ‘genlogistic’, ‘gennorm’, ‘genpareto’, ‘gilbrat’, ‘gompertz’, 
      ‘gumbel_l’, ‘gumbel_r’, ‘halfcauchy’, ‘halfgennorm’, ‘halflogistic’, ‘halfnorm’,
      ‘hypsecant’, ‘invgamma’, ‘invgauss’, ‘invweibull’, ‘johnsonsb’, ‘johnsonsu’, ‘kappa3’, ‘kappa4’, 
      ‘ksone’, ‘kstwo’, ‘kstwobign’, ‘laplace’, ‘levy’, ‘levy_l’, ‘levy_stable’, ‘loggamma’, ‘logistic’, 
      ‘loglaplace’, ‘lognorm’, ‘loguniform’, ‘lomax’, ‘maxwell’, ‘mielke’, ‘moyal’, ‘nakagami’, ‘ncf’, 
      ‘nct’, ‘ncx2’,‘norm’, ‘norminvgauss’, ‘pareto’, ‘pearson3’, ‘powerlaw’, ‘powerlognorm’, ‘powernorm’, 
      ‘rayleigh’, ‘rdist’, ‘recipinvgauss’, ‘reciprocal’, ‘rice’, ‘rv_continuous’, ‘rv_histogram’, 
      ‘semicircular’, ‘skewnorm’, ‘t’, ‘trapz’, ‘triang’, ‘truncexpon’, ‘truncnorm’, ‘tukeylambda’, 
      ‘uniform’, ‘vonmises’, ‘vonmises_line’, ‘wald’, ‘weibull_max’, ‘weibull_min’, ‘wrapcauchy’]

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
        data = np.random.normal(mu, sigma, 100)
        return data
        
    
    filename="body_fat.csv"
    varname="%Fat"
    filename="weight_height.csv"
    varname="Height"
    folderpath='<specify path to local folder folder>'
    imgname="bml"
    dataarr = []
    dataarr = genarray()
    finddist(filename,varname,dataarr,folderpath,imgname,1,3)
   
The output of the **finddist** function will be:

1. FOUR return variable:

   a. status: will indicate any ERROR success 

   b. dist: distribution dataframe

   c. bestdist: name of best distribution 

   d. alldata: comprehensive JSON data file

2. Image of your distribution curve mapped to your data, as shown below:

   .. figure:: dist1.png
      :scale: 50%

3. JSON file (same as alldata): See `Output Here on GitHub <https://github.com/smaurice101/raspberrypi/blob/main/maadsbml/bml_data.json>`_



