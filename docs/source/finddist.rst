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
        
    # Example File 1
    filename="body_fat.csv"
    # The variable for distributional analysis in body_fat.csv
    varname="%Fat"
    # Example file 2
    filename="weight_height.csv"
    # The variable for distributional analysis in weight_height.csv
    varname="Height"
    # Folder path to save output.  Enter valid path, or it will be saved in current directory.
    folderpath='.'
    # name of file
    imgname="bml"
   
    # We will generate a random array for distributional analysis but we could comment this out and use the above files or any other data
    dataarr = genarray()
    varname="Sample Data"
    # here we are using 1 for FAST distribution analysis using the most common distributions
    # 7 to print the TOP 7 distributions in the image and JSON
    # Use either filename or dataarr NOT both
    filename=""
    try:
     finddist(filename,varname,dataarr,folderpath,imgname,1,7)
    except Exception as e:
      print(e)  

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

2. Image of your distribution curve mapped to your data, as shown below (showing the TOP 7 BEST distributions): See `output image here on GitHub <https://github.com/smaurice101/raspberrypi/blob/main/maadsbml/bml.png>`_

   .. figure:: dist1.png
      :scale: 50%

Outputs: Comprehensive JSON Data File
"""""""""""""""""""""

3. JSON file (same as alldata): See `Output Here on GitHub <https://github.com/smaurice101/raspberrypi/blob/main/maadsbml/bml_data.json>`_

   A summary of the results is also contained in the JSON file.  Specifically, **gamma** is the BEST distribution based on the lowest 
   **sumsquare_error** = **0.0001542284**:

.. code-block:: JSON
                  
      	"bestdistribution": "gamma",
      	"shape": 88622.926,
      	"loc": -3165.175,
      	"scale": 0.036,
      	"summary": {
      		"sumsquare_error": {
      			"gamma": 0.0001542284,
      			"norm": 0.0001548898,
      			"lognorm": 0.0001566958,
      			"chi2": 0.0002046507,
      			"cauchy": 0.0028620826,
      			"rayleigh": 0.0105224588,
      			"powerlaw": 0.0169260703
      		},
      		"aic": {
      			"gamma": 1149.7382825946,
      			"norm": 1147.2692929564,
      			"lognorm": 1159.2415339377,
      			"chi2": 1173.9152701028,
      			"cauchy": 1033.9404491312,
      			"rayleigh": 925.4426473823,
      			"powerlaw": 901.4556624869
      		},
      		"bic": {
      			"gamma": 1171.3693037105,
      			"norm": 1161.6899737004,
      			"lognorm": 1180.8725550537,
      			"chi2": 1195.5462912187,
      			"cauchy": 1048.3611298752,
      			"rayleigh": 939.8633281262,
      			"powerlaw": 923.0866836028
      		},
      		"ks_statistic": {
      			"gamma": 0.0060977192,
      			"norm": 0.0064710822,
      			"lognorm": 0.0072002015,
      			"chi2": 0.0158653357,
      			"cauchy": 0.0748045618,
      			"rayleigh": 0.2564481325,
      			"powerlaw": 0.3170921301
      		},
      		"ks_pvalue": {
      			"gamma": 0.8487981921,
      			"norm": 0.7939223878,
      			"lognorm": 0.6749089697,
      			"chi2": 0.0128838887,
      			"cauchy": 4.130183894e-49,
      			"rayleigh": 0.0,
      			"powerlaw": 0.0
      		}
      	},
      	"filename": "",
      	"varname": "Sample Data",
      	"folderpath": ".",
      	"distimagefilename": "bml.png",
      	"jsondatafilename": "bml.json",
      	"nobs": 10000,
      	"min": -41.54803684864877,
      	"max": 39.4193605288367,
      	"mean": 0.974,
      	"variance": 113.113,
      	"std": 10.635,
      	"skewness": -0.007,
      	"kurtosis": -0.017,
      	"isarray": 1
