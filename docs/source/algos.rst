MAADSBML ALGORITHMS
==================

MAADSBML will perform advanced algorithms for both discreet and continous dependents variable.

It will automatically hypertune the parameters of the linear and non-linear algorithms.  It will also standardize all the variables.

.. important::

   MAADSBML uses a multi-agent framework to find the optimal algorithm for the data.  This is a powerful approach find the optimal algorithm in minutes, when it 
   can normally take days and weeks.

MAADSBML Algorithms
---------------------

MAADSBML will automatically apply the algorithms below to your data.  It will know which algorithms to apply to your data based on whether your dependent variable is continuous or discreet.

.. list-table::

   * - **Algorithm**
     - **Explanation**
   * - Linear Regression
     - This is the standard `linear regression algorithm <https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LinearRegression.html>`_

       using Ordinary Least Squares (OLS).
   * - Adaboosting
     - MAADSBML will apply the `Adaboosting regressor <https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.AdaBoostRegressor.html>`_

       and `Adaboostng classifier <https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.AdaBoostClassifier.html>`_ to your data.
   * - Neural networks
     - 
   * - SVM/SVC
     - 
   * - Logistic
     - 
   * - Gradient boosting
     - 
   * - Multiple layer perceptron
     - 
   * - Ridge regression
     - 
   * - ARIMA
     - 
   * - Gaussian
     - 
   * - Ensemble
     - 
   * - XGboost
     - 
   * - Theilsen Regressor
     - 
   * - Other special algorithms
     - 

  
  
