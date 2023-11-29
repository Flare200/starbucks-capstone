### Table of Contents

1. [Installation](#installation)
2. [File Descriptions](#files)
3. [Problem Statement](#problem)
4. [Business Understanding](#business)
5. [Solution to Problem](#solution)
6. [Results](#results)
7. [Licensing, Authors, and Acknowledgements](#licensing)

## Installation <a name="installation"></a>

Should include python packages: 'numpy', 'pandas', 'matplotlib', and 'seaborn'.  The code should run with no issues using Python versions 3.*.

You can install the libraries with the following commands:
1. `pandas`: Command to install is `pip install pandas`.
2. `numpy`: Command to install is `pip install numpy`.
3. `matplotlib`: Command to install is `pip install matplotlib`.
4. `seaborn`: Command to install is `pip install seaborn`.

## File Descriptions <a name="files"></a>

There is one notebook available, `Starbucks_Capstone_notebook.ipynb`, which was initially provided by Udacity.  This notebook showcases a lot of skills I've garnered up to this point which includes data inspection, data cleaning, exploratory data analysis, matrix factorization, and recommendation systems.  Markdown cells were used when trying to explain the findings and thought process of the analysis. Comments were also used throughout the code to make it easier to follow.

The json files, `portfolio.json`, `profile.json`, and `transcript.json` are the initial datasets provided by Udacity and Starbucks that are used in the notebook.
* `portfolio.json` - contains offer ids and meta data about each offer (duration, type, etc.)
* `profile.json` - demographic data for each customer
* `transcript.json` - records for transactions, offers received, offers viewed, and offers completed

The pickle files, `complete_user_item_matrix.pkl`, `train_user_item_matrix.pkl`, and `test_user_item_matrix.pkl` are the user-item matrices that are created to be used for the recommendation systems.  These files are provided in case you don't want to run the function to manually get them as they do take some time to run.
* `complete_user_item_matrix.pkl` - Full user-item matrix created using the `clean_transcript` dataframe
* `train_user_item_matrix.pkl` - User-item matrix used for training in FunkSVD; it makes up the first 70% of the data and contains older transactions
* `test_user_item_matrix.pkl` - User-item matrix used for predicting and validating the user and item matrices; it makes up the last 30% of the data and contains newer transactions

## Problem Statement<a name="problem"></a>

The problem that I am trying to solve is how can we provide the best offers to customers given their transaction history in relation to the offers we give them.  If they are an existing customers, how likely are they going to make a purchase with a given offer?  If they are a new customer, then we will recommend the best offers.

## Business Understanding<a name="business"></a>

For this study, we use three types of promotional offers:

1. Buy-one-get-one (BOGO): Customers must spend a certain amount to receive a reward equal to that threshold.
2. Discount: Customers receive a reward equivalent to a portion of the amount they spend.
3. Informational: This type doesn't provide a reward or require any minimum spending on the customer's part.

Please note that if a customer completes an offer without actually seeing the offer, it will not be considered successful as it cannot be directly linked to the offer's effect.

## Solution to Problem<a name="solution"></a>

I feel that the best way to tackle this is to use matrix factorization and FunkSVD to create the best recommendations for existing users, assuming that they recieved an offer, viewed it, and completed it.  With this sequence, we can more certainly say that a specific offer was the reason for a purchase.  Since there would be a lot of missing data, FunkSVD is the best way to approach this problem as it uses gradient descent to lead to a lower mean squared error over multiple iterations.  Existing users could get reccommendations based on this method.  New users, however, would have no transaction history.  To compensate for this in the cold start problem, we can give new users the top offers until they build up more history.

## Results<a name="results"></a>

The main findings of the code can be found at the post available [here](https://medium.com/@elijah_89308/creating-a-win-win-personalized-offers-for-maximized-customer-satisfaction-c27180feb122).

## Licensing, Authors, and Acknowledgements<a name="licensing"></a>

Credit goes to Udacity and Starbucks for providing the following datasets from Starbucks.

