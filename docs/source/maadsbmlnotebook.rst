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
