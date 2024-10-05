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

MAADSBML will also perform cross-validation to hypertune the parameters in the algorithms, where applicable.

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
     - MAADSBML will apply the `neural network <https://scikit-learn.org/stable/modules/neural_networks_supervised.html>`_ algorithm to your data.
   * - SVM/SVC
     - 
   * - Logistic
     - For classification models, MAADS will apply several 

       classification algorithm including `Logistic Regression <https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LogisticRegression.html>`_.
   * - Gradient boosting
     - MAADSBML will apply `gradient boosting regressor <https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.GradientBoostingRegressor.html>`_

       and `gradient boosting classifier <https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.GradientBoostingClassifier.html>`_ to your data.
   * - Multiple layer perceptron (MLP)
     - MAADSBML will apply `MLP regressor <https://scikit-learn.org/stable/modules/generated/sklearn.neural_network.MLPRegressor.html>`_

       and `MLP classifier <https://scikit-learn.org/stable/modules/generated/sklearn.neural_network.MLPClassifier.html>`_ to your data.
   * - Ridge regression
     - MAADSBML will apply the `Ridge regression <https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.Ridge.html>`_ algorithm

       to your data.
   * - ARIMA
     - MAADSBML will apply the `ARIMA <https://www.statsmodels.org/stable/generated/statsmodels.tsa.arima.model.ARIMA.html>`_ algorithm

       to your data.
   * - Gaussian
     - MAADSBML will apply `Gaussian process regression <https://scikit-learn.org/stable/modules/generated/sklearn.gaussian_process.GaussianProcessRegressor.html#sklearn.gaussian_process.GaussianProcessRegressor>`_

       and `Gaussian process classifiers <https://scikit-learn.org/stable/modules/generated/sklearn.gaussian_process.GaussianProcessClassifier.html>`_
   * - Ensemble
     - MAADSBML will also apply advanced `ensemble models <https://scikit-learn.org/stable//api/sklearn.ensemble.html>`_. 
   * - XGboost
     - 
   * - Theilsen Regressor
     - 
   * - Other special algorithms
     - 

  
  
