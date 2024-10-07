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

Here are all the distributions it will analyse for your data, and choose the BEST one using the **sumsquare_error** method, see :ref:`Outputs: Comprehensive JSON Data File`

.. important::
   The distribution with the lowest **sumsquare_error** is the BEST one. using the **sumsquare_error** method, see :ref:`Outputs: Comprehensive JSON Data File`

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
    dataarr = genarray()
    varname="Sample Data"
    finddist("",varname,dataarr,folderpath,imgname,1,7)

Outputs From finddistribution
----------------------------

The output of the **finddist** function will be:

Outputs: Four Returned Variables
"""""""""""""""""""""

1. FOUR return variable:

   a. status: will indicate any ERROR success 

   b. dist: distribution dataframe

   c. bestdist: name of best distribution 

   d. alldata: comprehensive JSON data file

Outputs: Distribution Image
"""""""""""""""""""""

2. Image of your distribution curve mapped to your data, as shown below (showing the TOP 7 BEST distributions):

   .. figure:: dist1.png
      :scale: 50%

Outputs: Comprehensive JSON Data File
"""""""""""""""""""""

3. JSON file (same as alldata): See `Output Here on GitHub <https://github.com/smaurice101/raspberrypi/blob/main/maadsbml/bml_data.json>`_

   A summary of the results is also contained in the JSON file.  Specifically, **norm** is the BEST distribution based on the lowest 
   **sumsquare_error** = **0.0081149046**:

.. code-block:: JSON
      
      "bestdistribution": "norm",
      	"shape": 0,
      	"loc": 0.029,
      	"scale": 1.497,
      	"summary": {
      		"sumsquare_error": {
      			"norm": 0.0081149046,
      			"gamma": 0.0082625558,
      			"lognorm": 0.0087592562,
      			"exponpow": 0.084470161,
      			"cauchy": 0.1269541688,
      			"rayleigh": 0.4482579119,
      			"powerlaw": 0.8826028833
      		},
      		"aic": {
      			"norm": 806.08450877,
      			"gamma": 804.6052961259,
      			"lognorm": 801.9580285437,
      			"exponpow": 1211.378442525,
      			"cauchy": 657.8834702006,
      			"rayleigh": 556.6037629452,
      			"powerlaw": 505.8212509523
      		},
      		"bic": {
      			"norm": 820.505189514,
      			"gamma": 826.2363172418,
      			"lognorm": 823.5890496596,
      			"exponpow": 1233.0094636409,
      			"cauchy": 672.3041509446,
      			"rayleigh": 571.0244436891,
      			"powerlaw": 527.4522720682
      		},
      		"ks_statistic": {
      			"norm": 0.0062391598,
      			"gamma": 0.0074117257,
      			"lognorm": 0.0096569495,
      			"exponpow": 0.0618710113,
      			"cauchy": 0.0737015036,
      			"rayleigh": 0.2312575944,
      			"powerlaw": 0.3468426483
      		},
      		"ks_pvalue": {
      			"norm": 0.8287219803,
      			"gamma": 0.6392443451,
      			"lognorm": 0.3066432281,
      			"exponpow": 1.013247951e-33,
      			"cauchy": 1.103071858e-47,
      			"rayleigh": 0.0,
      			"powerlaw": 0.0
      		}
      	},
      	"filename": "",
      	"varname": "Sample Data",
      	"folderpath": "C:/MAADS/Companies/firstgenesis/probability distribution",
      	"distimagefilename": "bml.png",
      	"jsondatafilename": "bml.json",
      	"isarray": 1
      
