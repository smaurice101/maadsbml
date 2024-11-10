MAADSBML Dashboard
=====================

You can see all of the output from the MAADSBML engine in a dashboard.  

To access the Dashboard simply enter this URL in your browser:

URL: http://localhost:9090/maadsbmllogs.html?topic=bmllogs&append=0

Dashboard URL
------------

.. note::
   This URL accesses the Kafka topic called: bmllogs.  This the topic you set in the Docker Run command field: VIPERLOGNAME (:ref:`MAADSBML Docker Run Parameters Explained`).

   The port 9090 is set using the value in the field: VIPERVIZPORT

   maadsbmllogs.html is the dashboard HTML running in your MAADSBML container.

   append=0 loads new data into the browser - without appending to the old data.

.. figure:: bmldash.png
   :scale: 60%
