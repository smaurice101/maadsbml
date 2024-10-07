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

   A summary of the results is also contained in the JSON file.  Specifically, **norm** is the BEST distribution based on the lowest 
   **sumsquare_error** = **0.0081149046**:

.. code-block:: JSON
            
      	"bestdistribution": "norm",
      	"shape": 0,
      	"loc": 0.926,
      	"scale": 10.372,
      	"summary": {
      		"sumsquare_error": {
      			"norm": 0.0001833218,
      			"gamma": 0.0001842996,
      			"lognorm": 0.0008286558,
      			"cauchy": 0.0032124016,
      			"rayleigh": 0.0093685066,
      			"powerlaw": 0.0184203716,
      			"uniform": 0.0187563468
      		},
      		"aic": {
      			"norm": 1080.7122808355,
      			"gamma": 1082.5527638245,
      			"lognorm": 1087.0229562595,
      			"cauchy": 1009.413196322,
      			"rayleigh": 913.1328108475,
      			"powerlaw": 874.1536793632,
      			"uniform": 864.8471332897
      		},
      		"bic": {
      			"norm": 1095.1329615794,
      			"gamma": 1104.1837849405,
      			"lognorm": 1108.6539773755,
      			"cauchy": 1023.833877066,
      			"rayleigh": 927.5534915914,
      			"powerlaw": 895.7847004791,
      			"uniform": 879.2678140336
      		},
      		"ks_statistic": {
      			"norm": 0.0055919778,
      			"gamma": 0.0059054055,
      			"lognorm": 0.0478349235,
      			"cauchy": 0.0733773525,
      			"rayleigh": 0.219349235,
      			"powerlaw": 0.3142887917,
      			"uniform": 0.2392847635
      		},
      		"ks_pvalue": {
      			"norm": 0.9115044119,
      			"gamma": 0.8744437106,
      			"lognorm": 2.527062593e-20,
      			"cauchy": 2.869426062e-47,
      			"rayleigh": 0.0,
      			"powerlaw": 0.0,
      			"uniform": 0.0
      		}
      	},
      	"filename": "",
      	"varname": "Sample Data",
      	"folderpath": ".",
      	"distimagefilename": "bml.png",
      	"jsondatafilename": "bml.json",
      	"isarray": 1      
