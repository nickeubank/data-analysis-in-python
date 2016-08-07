
Econometrics
=========================

There are two sets of tools for econometrics: `statsmodels`, `quantecon`, and (for bayesians) `stan`.

Stats with StatsModels
^^^^^^^^^^^^^^^^^^^^^^^
`statsmodels` is the go-to library for doing econometrics (linear regression, logit regression, etc.).

You can find a `good tutorial here <http://nbviewer.ipython.org/urls/s3.amazonaws.com/datarobotblog/notebooks/multiple_regression_in_python.ipynb>`_, and a brand new book built around `statsmodels` `here <http://www.springer.com/us/book/9783319283159>`_ (with lots of `example code here <https://github.com/thomas-haslwanter/statsintro_python>`_).

The most important things are also covered on `the statsmodel page here <http://statsmodels.sourceforge.net/devel/>`_, especially the pages on OLS `here <http://statsmodels.sourceforge.net/devel/example_formulas.html>`_ and `here <http://statsmodels.sourceforge.net/devel/examples/notebooks/generated/ols.html>`_.

(If you want to do machine learning, by the way, or want to know the difference between ``statsmodels`` and the machine learning library ``scikit-learn``, head over to :doc:`Machine Learning with scikit-learn </t_scikitlearn>`)

Here are some simple illustrative examples of standard OLS:

On with the show:

.. ipython:: python

   @suppress
   import os
   @suppress
   os.chdir("source/_data")

   # Load pandas and statsmodels
   import pandas as pd
   import statsmodels.formula.api as smf

   # Load a csv dataset of World Development Indicators
   my_data = pd.read_csv('wdi_indicators.csv')

   # Look at first three lines
   my_data.head(3)

   # OLS
   results = smf.ols('life_expectancy ~ population_density + gdp_per_cap',
                     data=my_data).fit()
   print(results.summary())


   # Categorical Vars are easy
      # Make categorical var
   my_data['low_income'] = my_data['gdp_per_cap'] < 4000

   results2 = smf.ols('life_expectancy ~ population_density + gdp_per_cap + C(low_income)', data=my_data).fit()

   print(results2.summary())


   # Heteroskedastic-Robust Standard Errors
   results2_robust = results2.get_robustcov_results()
   print(results2_robust.summary())


   # Output to LaTeX
   latex = results2_robust.summary().as_latex()
   latex

   # Save to disk
   with open("regression_table.tex", "w") as text_file:
       text_file.write(latex)

QuantEcon
^^^^^^^^^^
QuantEcon is a new library specifically for economists with some tools not found in `statsmodels`. `A full index is here <http://quanteconpy.readthedocs.io/en/latest/>`_

PyStan
^^^^^^^^^^
PyStan is the Python interface for the Stan library -- a set of tools for statisticians, especially bayesians. You can find resources on `Stan <http://mc-stan.org/>`_ in general here, and `PyStan in particular here <http://mc-stan.org/interfaces/pystan.html>`_ .
