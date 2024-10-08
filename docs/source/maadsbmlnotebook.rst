MAADSBML Jupyter Notebook
========================

The MAADSBML jupyter notebook can be downloaded from Github: `MAADSBML Jupyter Notebook: maadsbmlcode.ipynb <https://github.com/smaurice101/raspberrypi/tree/main/maadsbml>`_

Process Your Data File
-----------------------

To process your own data file simply drop it in your local folder: **csvuploads**

.. important::
 
   • You MUST have the MAADSBML docker container running

   • The file must be CSV (comma separated values).  `Example CSVs here: <https://github.com/smaurice101/raspberrypi/tree/main/maadsbml>`_

   • You MUST store your CSV file in your LOCAL **csvuploads** folder

   • The first column MUST be Date in the format: M/D/YYYY.  The Date column is used for seasonality analysis.  If you do not want seasonality analysis, this 
     column is ignored by MAADSBML - but you STILL NEED THE DATE COLUMN.

   • Your CSV must contain column headings
 
   • The Dependent variable MUST be contained in this file

   • ALL DATA IN YOUR CSV MUST BE NUMERIC (with exception of column headers)

MAADSBML Jupyter Notebook Explained
------------------------------

.. code-block::
   :emphasize-lines: 1,11,15,16,17

   # IMPORT MAIN LIBRARIES
   import maadsbml
   import json
   import os
   import time
   # Uncomment IF using jupyter notebook
   import nest_asyncio
   # Uncomment IF using jupyter notebook
   nest_asyncio.apply()

   # SET THE HOST AND PORT WHERE MAADSBML IS LISTENING FOR A CLIENT CONNECTION
   host='http://127.0.0.1'
   port=5595

   # Change these two folders to your local paths that you used for the volume mappings 
   # in Docker Local Paths on Linux/Mac
   # Local Paths on Windows - Change to your local paths
   localstagingfolder = "c:\\maads\\maadsbml\\staging" # change this folder to your local mapped staging folder
   localexceptionfolder = "c:\\maads\\maadsbml\\exception" # change this folder to your local mapped exception folder

.. code-block::
   :emphasize-lines: 1

   # This function is a system function to capture broken pipe network issues - DO NOT MODIFY
   def readifbrokenpipe(jres,hasseasonality):
      # this function is called if there is a broken pipe network issue
      pkey=""
      algofile=""        
      jsonalgostr = ""
    
      pkey= jres.get('AlgoKey')
    
      maadsbmlfile="%s/%s.txt.working" % (localstagingfolder,pkey)
      if hasseasonality == 1:
        algojsonfile="%s/%s_trained_algo_seasons.json" % (localexceptionfolder,pkey)
      else:
        algojsonfile="%s/%s_trained_algo_no_seasons.json" % (localexceptionfolder,pkey)
        
      i=0
      while True:
          time.sleep(5)            
          i = i + 1
          if os.path.isfile(maadsbmlfile): 
               continue
          elif os.path.isfile(algojsonfile):
                # Read the json            
              with open(algojsonfile) as f:
                  jsonalgostr = f.read() 
              break # maadsbml finished
          #elif i > 400:
          #   print("ERROR: Could not find the JSON file - CHECK IF YOUR FILE PATHS ARE CORRECT!")
          #   break   
      return jsonalgostr

.. code-block::
   :emphasize-lines: 1,2,3,4,5,28,29,30,31,32

   # This is the MAIN ML Training function
   # You must enter host, port, filename,dependentvariable,removeoutliers,hasseasonality,deepanalysis,company
   # Deepanalysis will perform advanced algorithms but will take potentially hours to complete based on the 
   # size of your data
   # You can also change the summer, shoulder and winter months
   def hypertraining(host,port,filename,dependentvariable,removeoutliers,hasseasonality,deepanalysis,company):
    #host,port,
    #filename= raw data file in csv format - Note this file is stored on your host machine the DOCKER container needs to be mapped to this volume using -v
    #dependentvariable= dependent variable name - this is the column name in the csv file
    # the file should have a Date column in the format Month/Day/Year
    #username= you can specify a username
    # mode=0
    #timeout=180 - you can modify this in seconds if your data file is large
    #company= change this to the name of your company
    #removeoutliers= specify 1 or 0, 1=remove outliers, 0 do not remove outliers,
    #hasseasonality= specify 1 or 0 to indicate date is affected by seasonaility - 1 = seasonality, 0 = no seasonality,
    #summer= specify the summer months ie. '6,7,8', or set to -1 for no summer
    #winter= specify winter months i.e. '11,12,1,2', or -1 for no winter
    #shoulder= specify shoulder months i.e. '3,4,5,9,10', or -1 for no shoulder season
    #trainingpercentage= specify training percentage i.e. 70, the value represents a percentage to split training and test
    #shuffle= specify 1 or 0 to shuffle the data, 1= shuffle, 0 = no shuffle
    #deepanalysis= specify 1 or 0, 1=deepanalysis, note this will run through deeper algorithms but will take longer, 0 = no deep analysis, this will
    #password='123', - leave as is
    #email='support@otics.ca', - leave as is
    #usereverseproxy=0, - leave as is
    #microserviceid='', leave as is
    #maadstoken='123' leave as is
    summer='6,7,8' # specify -1 if you dont want to analyse summer
    winter='11,12,1,2' # specify -1 if you dont want to analyse winter 
    shoulder='3,4,5,9,10' # specify -1 if you dont want to analyse shoulder 
    trainingpercentage=75
    shuffle=1
    res=maadsbml.hypertraining(host, port, filename, dependentvariable,removeoutliers,hasseasonality, summer,winter,shoulder,trainingpercentage, shuffle, 
    deepanalysis, 'admin', 1200,company)
  
    jres = json.loads(res)

    if jres.get('BrokenPipe') != None: # check if the hypertraining function experienced a brokenpipe - if so wait 
        try:
          res=readifbrokenpipe(jres,hasseasonality)
        except Exception as e:
          print(e)  
           
    print(res)

Call the **hypertraining** to train on your data. 

.. code-block::
   :emphasize-lines: 1,2,8
   
   filename='stockdata.csv'
   dependentvariable='close'
   removeoutliers=0
   hasseasonality=0
   deepanalysis=0
   company='Your company'
   
   hypertraining(host,port,filename,dependentvariable,removeoutliers,hasseasonality,deepanalysis,company)

Here is the output from the hypertraining function.

.. code-block::

   {"AlgoKey":"admin_stockdata_csv","AlgoDetails":"RidgeRegression,0.996,allseason;LassoCV,0.995864, 
   allseason;VotingRegressor,0.995778,allseason;LinearSVR,0.995763,allseason;HuberRegressor,0.99503, 
   allseason;simpleregression_reg,0.995,allseason;ARDRegression,0.994911,allseason;BayesianRidge,0.994905, 
   allseason;Lars,0.994774,allseason;LarsCV,0.994774,allseason;", "PDF":"/maads/agentfilesdocker/dist/maadsweb/pdfreports/admin_stockdata_csv_no_seasons.pdf", 
   "Hasseasonality":"No","Deep Analysis":"No","Shuffled":"Yes","Outliers Removed":"No", "Generated On":"2024-04-25 00:28:37", 
   "Timezone":"UTC","Username":"admin","Dependentvariable":"close", "Filename":"/maads/agentfilesdocker/dist/maadsweb/csvuploads/stockdata.csv", 
   "Host":"127.0.0.1","Port":5595,"AlgoJson":"/maads/agentfilesdocker/dist/maadsweb/exception/admin_stockdata_csv_trained_algo_no_seasons.json", 
   "MainSortedAlgosInfoWeighted":"The numbers in the main sorted algorithms represent the average of the MAPE, R-Square, Explained Variance and Model 
   Accuracy","BESTALGO-ALLSEASON":"RidgeRegression", "MainSortedAlgos-Weighted- 
   Allseason":"VotingRegressor,0.998;LinearSVR,0.998;HuberRegressor,0.998;RidgeRegression,0.997;LassoCV,0.997; 
   simpleregression_reg,0.996;ARDRegression,0.996;BayesianRidge,0.996;RANSACRegressor,0.996;LassoLarsIC,0.996", "BESTALGOWEIGHTED-ALLSEASON":"VotingRegressor"}
   Once you have executed hypertraining - the output will be the pkey (or AlgoKey) use this this AlgoKey to as input into hyperprediction.

.. list-table::

   * - **JSON Field**
     - **JSON Value**
   * - AlgoKey
     - Key for your optimal algorithm.  This is main key.
   * - AlgoDetails
     - Details about the algorithms. For example, 

       RidgeRegression,0.996, allseason, means RidgeRegression 

       has a MAPE (Mean Absolute Percentage Error) of 0.996 
       
       with allseason (seasonality ignored).
   * - PDF
     - Path where the PDF report is saved.
   * - Hasseasonality
     - Yes for seasonlity, No for no seasonality.
   * - Deep Analysis
     - Yes for deepanalysis, No for no deep analysis.
   * - Shuffled
     - Yes for shuffled, No for no shuffling.  Shuffling, 

       shuffles the training datatset.
   * - Outliers Removed
     - Yes for outliers removed, No for no outliers removed.
   * - Generated On
     - UTC time when training completed.
   * - Timezone
     - UTC timezone.
   * - Username
     - username.
   * - Dependentvariable
     - Dependent variable in the ML model.
   * - Filename
     - Training data filename used.
   * - Host
     - Host IP for maadsbml.
   * - Port
     - Port for Maadsbml.
   * - Algojson
     - Path for the algorithm JSON.
   * - MainSortedAlgosInfoWeighted
     - Description.
   * - BESTALGO-ALLSEASON
     - Best algorithm.
   * - MainSortedAlgos-Weighted-Allseason
     - All the main algorithms.
   * - BESTALGOWEIGHTED-ALLSEASON
     - Best weighted algorithm.

Once you have executed hypertraining - the output will be the AlgoKey (or pkey) use this this AlgoKey to as input into hyperprediction.

.. code-block::

   def hyperprediction(pkey,host,port,inputdata,username):
  
     res=maadsbml.hyperpredictions(pkey,inputdata,host,port,username)
     print(res)

.. important::

   Once you have executed hypertraining - the output will be the pkey (or **AlgoKey**) use this this AlgoKey to as input into hyperpredictioncustom and specify 
   the algorithm and season you want to use for hyperpredictions.

.. code-block::

   # This is the main function to perform predictions from the trained algo.
   def hyperpredictioncustom(pkey,host,port,inputdata,username,algoname,season):
    res=maadsbml.hyperpredictions(pkey,inputdata,host,port,username,algoname,season)
    print(res)

Here is the output from the hyperprediction or hyperpredictioncustom functions:

.. code-block::

   {"hyperprediction":45.14,"AlgoKey":"admin_stockdata_csv","Season":"allseason","Algorithm":"RidgeRegression","Dependent 
   Variable":"close","Fields":"Date,Open,High,Low,Volume","Trained Model Accuracy":"0.996","Pickle Files":"/maads/agentfilesdocker/networks/Alberta-Electric- 
   System-Operator_AESO)_ADMIN_STOCKDATA_CSVALLSEASON_AG1_4_RidgeRegression_normal_1.00000000_946_.pkl, /maads/agentfilesdocker/networks/Alberta-Electric-System- 
   Operator_AESO)_ADMIN_STOCKDATA_CSVALLSEASON_AG1_4_RidgeRegression_normal_1.00000000_946_scalerx_.pkl, /maads/agentfilesdocker/networks/Alberta-Electric-System- 
   Operator_AESO)_ADMIN_STOCKDATA_CSVALLSEASON_AG1_4_RidgeRegression_normal_1.00000000_946_scalery_.pkl","CreatedOn":"2024-04-25, 
   00:29:27","InputData":"5/21/2013,52.650002,83.330002,2.120003,2674600","MicroService":"PREDICTIONSERVICE","Host":"127.0.0.1","Port":5495}

.. list-table::

   * - **JSON Field**
     - **JSON Value**
   * - hyperprediction
     - The prediction.
   * - AlgoKey
     - The AlgoKey
   * - Season
     - The AlgoKey
   * - Algorithm
     - This is the BEST algorithm determined by MAADSBML.
   * - Dependent Variable
     - The AlgoKey
   * - Fields
     - These are the independent variables.
   * - Trained Model Accuracy
     - MAPE value for the trained algorithm.
   * - Pickle Files
     - The Python pickle files for the algorithms and standardization.
   * - CreatedOn
     - The date and time prediction was generated.
   * - InputData
     - The input data used for the predictions.
   * - MicroService
     - microservice.
   * - Host
     - The IP address of MAADSBML
   * - Port
     - The prediction port.

Use the **AlgoKey** to find details on the algorithm.

.. code-block::

   def algoinfo(pk):
     res=maadsbml.algodescription(host,port,pk)
     print(res)

