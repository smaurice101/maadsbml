MAADSBML Jupyter Notebook
========================

The MAADSBML jupyter notebook can be downloaded from Github: `MAADSBML Jupyter Notebook <https://github.com/smaurice101/raspberrypi/tree/main/maadsbml>`_

Process Your Data File
-----------------------

To process your own data file simply drop it in your local folder: **csvuploads**

.. important::

   • The file must be CSV (comma separated values)

   • The first column MUST be Date in the format: M/D/YYYY.  The Date column is used for seasonality analysis.  If you do not want seasonality analysis, this column       is ignored by MAADSBML - but you STILL NEED THE DATE COLUMN.

   • Your CSV must contain column headings
 
   • The Dependent variable MUST be contained in this file

   • ALL DATA IN YOUR CSV MUST BE NUMERIC (with exception of column headers)

MAADSBML Jupyter Notebook Explained
------------------------------

.. code-block::

   import maadsbml
   import json
   import os
   import time
   # Uncomment IF using jupyter notebook
   import nest_asyncio
   # Uncomment IF using jupyter notebook
   nest_asyncio.apply()

   host='http://127.0.0.1'
   port=5595
   ### Change these two folder to your local paths that you used for the volume mappings in Docker Local Paths on Linux/Mac

   # Local Paths on Windows - Change to your local paths
   localstagingfolder = "c:\\maads\\maadsbml\\staging" # change this folder to your local mapped staging folder
   localexceptionfolder = "c:\\maads\\maadsbml\\exception" # change this folder to your local mapped exception folder

.. code-block::
   :emphasize-lines: 8,10,16

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

