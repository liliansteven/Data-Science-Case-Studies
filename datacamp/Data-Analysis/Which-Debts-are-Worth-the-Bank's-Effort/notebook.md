
## 1. Regression discontinuity: banking recovery
<p>After a debt has been legally declared "uncollectable" by a bank, the account is considered "charged-off." But that doesn't mean the bank <strong><em>walks away</em></strong> from the debt. They still want to collect some of the money they are owed. The bank will score the account to assess the expected recovery amount, that is, the expected amount that the bank may be able to receive from the customer in the future. This amount is a function of the probability of the customer paying, the total debt, and other factors that impact the ability and willingness to pay.</p>
<p>The bank has implemented different recovery strategies at different thresholds (\$1000, \$2000, etc.) where the greater the expected recovery amount, the more effort the bank puts into contacting the customer. For low recovery amounts (Level 0), the bank just adds the customer's contact information to their automatic dialer and emailing system. For higher recovery strategies, the bank incurs more costs as they leverage human resources in more efforts to obtain payments. Each additional level of recovery strategy requires an additional \$50 per customer so that customers in the Recovery Strategy Level 1 cost the company \$50 more than those in Level 0. Customers in Level 2 cost \$50 more than those in Level 1, etc. </p>
<p><strong>The big question</strong>: does the extra amount that is recovered at the higher strategy level exceed the extra \$50 in costs? In other words, was there a jump (also called a "discontinuity") of more than \$50 in the amount recovered at the higher strategy level? We'll find out in this notebook.</p>
<p>![Regression discontinuity graph](https://assets.datacamp.com/production/project_504/img/Regression Discontinuity graph.png)</p>
<p>First, we'll load the banking dataset and look at the first few rows of data. This lets us understand the dataset itself and begin thinking about how to analyze the data.</p>

```python
# Import modules
import pandas as pd
import numpy as np

# Read in dataset
df = pd.read_csv('datasets/bank_data.csv')

# Print the first few rows of the DataFrame
df.head()
```

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>expected_recovery_amount</th>
      <th>actual_recovery_amount</th>
      <th>recovery_strategy</th>
      <th>age</th>
      <th>sex</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2030</td>
      <td>194</td>
      <td>263.540</td>
      <td>Level 0 Recovery</td>
      <td>19</td>
      <td>Male</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1150</td>
      <td>486</td>
      <td>416.090</td>
      <td>Level 0 Recovery</td>
      <td>25</td>
      <td>Female</td>
    </tr>
    <tr>
      <th>2</th>
      <td>380</td>
      <td>527</td>
      <td>429.350</td>
      <td>Level 0 Recovery</td>
      <td>27</td>
      <td>Male</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1838</td>
      <td>536</td>
      <td>296.990</td>
      <td>Level 0 Recovery</td>
      <td>25</td>
      <td>Male</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1995</td>
      <td>541</td>
      <td>346.385</td>
      <td>Level 0 Recovery</td>
      <td>34</td>
      <td>Male</td>
    </tr>
  </tbody>
</table>

```python
first_value = _

def test_pandas_loaded():
    assert pd.__name__ == 'pandas', \
        "pandas should be imported as pd."

def test_numpy_loaded():
    assert np.__name__ == 'numpy', \
        "numpy should be imported as np."

import pandas as pd

def test_df_correctly_loaded():
    correct_df = pd.read_csv('datasets/bank_data.csv')

    assert correct_df.equals(df), \
        "The variable df should contain the data in 'datasets/bank_data.csv'."

# def test_head_output():
#     try:
#         assert "2030" in first_value.to_string()
#     except AttributeError:
#         assert False, \
#             "Please use df.head() as the last line of code in the cell to inspect the data, not the display() or print() functions."
#     except AssertionError:
#         assert False, \
#             "Hmm, the output of the cell is not what we expected. You should see 2030 in the first five rows of the df DataFrame."
```

    3/3 tests passed

## 2. Graphical exploratory data analysis
<p>The bank has implemented different recovery strategies at different thresholds (\$1000, \$2000, \$3000 and \$5000) where the greater the Expected Recovery Amount, the more effort the bank puts into contacting the customer. Zeroing in on the first transition (between Level 0 and Level 1) means we are focused on the population with Expected Recovery Amounts between \$0 and \$2000 where the transition between Levels occurred at \$1000. We know that the customers in Level 1 (expected recovery amounts between \$1001 and \$2000) received more attention from the bank and, by definition, they had higher Expected Recovery Amounts than the customers in Level 0 (between \$1 and \$1000).</p>
<p>Here's a quick summary of the Levels and thresholds again:</p>
<ul>
<li>Level 0: Expected recovery amounts &gt;\$0 and &lt;=\$1000</li>
<li>Level 1: Expected recovery amounts &gt;\$1000 and &lt;=\$2000</li>
<li>The threshold of \$1000 separates Level 0 from Level 1</li>
</ul>
<p>A key question is whether there are other factors besides Expected Recovery Amount that also varied systematically across the \$1000 threshold. For example, does the customer age show a jump (discontinuity) at the \$1000 threshold or does that age vary smoothly? We can examine this by first making a scatter plot of the age as a function of Expected Recovery Amount for a small window of Expected Recovery Amount, \$0 to \$2000. This range covers Levels 0 and 1.</p>

```python
# Scatter plot of Age vs. Expected Recovery Amount
from matplotlib import pyplot as plt
%matplotlib inline
plt.scatter(x=df['expected_recovery_amount'], y=df['age'], c="g", s=2)
plt.xlim(0, 2000)
plt.ylim(0, 60)
plt.xlabel('Expected Recovery Amount')
plt.ylabel('Age')
plt.legend(loc=2)
plt.show()
```

    /usr/local/lib/python3.6/dist-packages/matplotlib/figure.py:2267: UserWarning: This figure includes Axes that are not compatible with tight_layout, so results might be incorrect.
      warnings.warn("This figure includes Axes that are not compatible "

![png](images/output_4_1.png)

```python
# no tests for plots

# def test_nothing():
#     assert True, "Nothing to test."

def test_matplotlib_loaded_2():
    assert 'plt' in globals(), \
    'Did you import the pyplot module from matplotlib under the alias plt?'
```

    1/1 tests passed

## 3. Statistical test:  age vs. expected recovery amount
<p>We want to convince ourselves that variables such as age and sex are similar above and below the \$1000 Expected Recovery Amount threshold. This is important because we want to be able to conclude that differences in the actual recovery amount are due to the higher Recovery Strategy and not due to some other difference like age or sex.</p>
<p>The scatter plot of age versus Expected Recovery Amount did not show an obvious jump around \$1000.  We will now do statistical analysis examining the average age of the customers just above and just below the threshold. We can start by exploring the range from \$900 to \$1100.</p>
<p>For determining if there is a difference in the ages just above and just below the threshold, we will use the Kruskal-Wallis test, a statistical test that makes no distributional assumptions.</p>

```python
# Import stats module
from scipy import stats

# Compute average age just below and above the threshold
era_900_1100 = df.loc[(df['expected_recovery_amount']<1100) &
                      (df['expected_recovery_amount']>=900)]
by_recovery_strategy = era_900_1100.groupby(['recovery_strategy'])
by_recovery_strategy['age'].describe().unstack()

# Perform Kruskal-Wallis test
Level_0_age = era_900_1100.loc[df['recovery_strategy']=="Level 0 Recovery"]['age']
Level_1_age = era_900_1100.loc[df['recovery_strategy']=="Level 1 Recovery"]['age']
stats.kruskal(Level_0_age, Level_1_age)
```

    KruskalResult(statistic=3.4572342749517513, pvalue=0.06297556896097407)

```python
def test_stats_loaded():
    assert 'stats' in globals(), \
    'Did you import the stats module from scipy?'

def test_level_0():
    correct_Level_0_age_mean= df.loc[(df['expected_recovery_amount']<1100) & (df['expected_recovery_amount']>=900) &
                     (df['recovery_strategy']=="Level 0 Recovery")]['age'].mean()
    Level_0_age_mean= Level_0_age.mean()
    assert correct_Level_0_age_mean == Level_0_age_mean, \
        "The mean age for Level_0_age appears to be incorrect. Did you correctly assign Level_0_age?"

def test_level_1():
    correct_Level_1_age_mean= df.loc[(df['expected_recovery_amount']<1100) & (df['expected_recovery_amount']>=900) &
                     (df['recovery_strategy']=="Level 1 Recovery")]['age'].mean()
    Level_1_age_mean= Level_1_age.mean()
    assert correct_Level_1_age_mean == Level_1_age_mean, \
        "The mean age for Level_1_age appears to be incorrect. Did you correctly assign Level_1_age?"
```

    3/3 tests passed

## 4. Statistical test:  sex vs. expected recovery amount
<p>We have seen that there is no major jump in the average customer age just above and just
below the \$1000 threshold by doing a statistical test as well as exploring it graphically with a scatter plot.  </p>
<p>We want to also test that the percentage of customers that are male does not jump across the \$1000 threshold. We can start by exploring the range of \$900 to \$1100 and later adjust this range.</p>
<p>We can examine this question statistically by developing cross-tabs as well as doing chi-square tests of the percentage of customers that are male vs. female.</p>

```python
# Number of customers in each category
crosstab = pd.crosstab(df.loc[(900<=df['expected_recovery_amount']) &
                              (df['expected_recovery_amount']<1100) &
                              (df['expected_recovery_amount']>=0)]['recovery_strategy'],
                       df['sex'])
print(crosstab)

# Chi-square test
chi2_stat, p_val, dof, ex = stats.chi2_contingency(crosstab)
print(p_val)
```

    sex                Female  Male
    recovery_strategy
    Level 0 Recovery       32    57
    Level 1 Recovery       39    55
    0.5377947810444592

```python
def test_crosstab():
    correct_crosstab = pd.crosstab(df.loc[(df['expected_recovery_amount']<1100) & (df['expected_recovery_amount']>=900)]['recovery_strategy'], df['sex'])
    assert correct_crosstab.equals(crosstab), \
    "The crosstab should select the expected_recovery_amount <1100 and >=900."

def test_pval():
    chi2_stat, correct_p_val, dof, ex = stats.chi2_contingency(crosstab)
    assert correct_p_val==p_val, \
    "The chi-square test function should use crosstab as the input variable."
```

    2/2 tests passed

## 5. Exploratory graphical analysis: recovery amount
<p>We are now reasonably confident that customers just above and just below the \$1000 threshold are, on average, similar in their average age and the percentage that are male.  </p>
<p>It is now time to focus on the key outcome of interest, the actual recovery amount.</p>
<p>A first step in examining the relationship between the actual recovery amount and the expected recovery amount is to develop a scatter plot where we want to focus our attention at the range just below and just above the threshold. Specifically, we will develop a scatter plot of  Expected Recovery Amount (X) versus Actual Recovery Amount (Y) for Expected Recovery Amounts between \$900 to \$1100.  This range covers Levels 0 and 1.  A key question is whether or not we see a discontinuity (jump) around the \$1000 threshold.</p>

```python
# Scatter plot of Actual Recovery Amount vs. Expected Recovery Amount
plt.scatter(x=df['expected_recovery_amount'], y=df['actual_recovery_amount'], c="g", s=2)
plt.xlim(900, 1100)
plt.ylim(0, 2000)
plt.xlabel("Expected Recovery Amount")
plt.ylabel("Actual Recovery Amount")
plt.legend(loc=2)
plt.show()
```

    /usr/local/lib/python3.6/dist-packages/matplotlib/figure.py:2267: UserWarning: This figure includes Axes that are not compatible with tight_layout, so results might be incorrect.
      warnings.warn("This figure includes Axes that are not compatible "

![png](images/output_13_1.png)

```python
# no tests for plots

# def test_nothing():
#     assert True, "Nothing to test."

def test_matplotlib_loaded_5():
    assert 'plt' in globals(), \
    'Did you import the pyplot module from matplotlib under the alias plt?'
```

    1/1 tests passed

## 6. Statistical analysis:  recovery amount
<p>As we did with age, we can perform statistical tests to see if the actual recovery amount has a discontinuity above the \$1000 threshold. We are going to do this for two different windows of the expected recovery amount \$900 to \$1100 and for a narrow range of \$950 to \$1050 to see if our results are consistent.</p>
<p>Again, we will use the Kruskal-Wallis test.</p>
<p>We will first compute the average actual recovery amount for those customers just below and just above the threshold using a range from \$900 to \$1100.  Then we will perform a Kruskal-Wallis test to see if the actual recovery amounts are different just above and just below the threshold.  Once we do that, we will repeat these steps for a smaller window of \$950 to \$1050.</p>

```python
# Compute average actual recovery amount just below and above the threshold
by_recovery_strategy['actual_recovery_amount'].describe().unstack()

# Perform Kruskal-Wallis test
Level_0_actual = era_900_1100.loc[df['recovery_strategy']=='Level 0 Recovery']['actual_recovery_amount']
Level_1_actual = era_900_1100.loc[df['recovery_strategy']=='Level 1 Recovery']['actual_recovery_amount']
print(stats.kruskal(Level_0_actual, Level_1_actual))

# Repeat for a smaller range of $950 to $1050
era_950_1050 = df.loc[(df['expected_recovery_amount']<1050) &
                      (df['expected_recovery_amount']>=950)]
Level_0_actual = era_950_1050.loc[df['recovery_strategy']=='Level 0 Recovery']['actual_recovery_amount']
Level_1_actual = era_950_1050.loc[df['recovery_strategy']=='Level 1 Recovery']['actual_recovery_amount']
stats.kruskal(Level_0_actual, Level_1_actual)
```

    KruskalResult(statistic=65.37966302528878, pvalue=6.177308752803109e-16)

    KruskalResult(statistic=30.246000000000038, pvalue=3.80575314300276e-08)

```python
def test_level_0():
    correct_Level_0_actual_mean= df.loc[(df['expected_recovery_amount']<1050) & (df['expected_recovery_amount']>=950) &
                     (df['recovery_strategy']=="Level 0 Recovery")]['actual_recovery_amount'].mean()
    Level_0_actual_mean= Level_0_actual.mean()
    assert correct_Level_0_actual_mean == Level_0_actual_mean, \
        "The mean actual_recovery_amount for Level_0_actual appears to be incorrect. Did you correctly assign Level_0_actual?"

def test_level_1():
    correct_Level_1_actual_mean= df.loc[(df['expected_recovery_amount']<1050) & (df['expected_recovery_amount']>=950) &
                     (df['recovery_strategy']=="Level 1 Recovery")]['actual_recovery_amount'].mean()
    Level_1_actual_mean= Level_1_actual.mean()
    assert correct_Level_1_actual_mean == Level_1_actual_mean, \
        "The mean actual_recovery_amount for Level_1_actual appears to be incorrect. Did you correctly assign Level_1_actual?"
```

    2/2 tests passed

## 7. Regression modeling: no threshold
<p>We now want to take a regression-based approach to estimate the program impact at the \$1000 threshold using data that is just above and below the threshold. </p>
<p>We will build two models. The first model does not have a threshold while the second will include a threshold.</p>
<p>The first model predicts the actual recovery amount (dependent variable) as a function of the expected recovery amount (independent variable). We expect that there will be a strong positive relationship between these two variables.  </p>
<p>We will examine the adjusted R-squared to see the percent of variance explained by the model.  In this model, we are not representing the threshold but simply seeing how the variable used for assigning the customers (expected recovery amount) relates to the outcome variable (actual recovery amount).</p>

```python
# Import statsmodels
import statsmodels.api as sm

# Define X and y
X = era_900_1100['expected_recovery_amount']
y = era_900_1100['actual_recovery_amount']
X = sm.add_constant(X)

# Build linear regression model
model = sm.OLS(y, X).fit()
predictions = model.predict(X)

# Print out the model summary statistics
model.summary()
```

<table class="simpletable">
<caption>OLS Regression Results</caption>
<tr>
  <th>Dep. Variable:</th>    <td>actual_recovery_amount</td> <th>  R-squared:         </th> <td>   0.261</td>
</tr>
<tr>
  <th>Model:</th>                      <td>OLS</td>          <th>  Adj. R-squared:    </th> <td>   0.256</td>
</tr>
<tr>
  <th>Method:</th>                <td>Least Squares</td>     <th>  F-statistic:       </th> <td>   63.78</td>
</tr>
<tr>
  <th>Date:</th>                <td>Fri, 02 Jun 2023</td>    <th>  Prob (F-statistic):</th> <td>1.56e-13</td>
</tr>
<tr>
  <th>Time:</th>                    <td>19:00:52</td>        <th>  Log-Likelihood:    </th> <td> -1278.9</td>
</tr>
<tr>
  <th>No. Observations:</th>         <td>   183</td>         <th>  AIC:               </th> <td>   2562.</td>
</tr>
<tr>
  <th>Df Residuals:</th>             <td>   181</td>         <th>  BIC:               </th> <td>   2568.</td>
</tr>
<tr>
  <th>Df Model:</th>                 <td>     1</td>         <th>                     </th>     <td> </td>
</tr>
<tr>
  <th>Covariance Type:</th>         <td>nonrobust</td>       <th>                     </th>     <td> </td>
</tr>
</table>
<table class="simpletable">
<tr>
              <td></td>                <th>coef</th>     <th>std err</th>      <th>t</th>      <th>P>|t|</th>  <th>[0.025</th>    <th>0.975]</th>
</tr>
<tr>
  <th>const</th>                    <td>-1978.7597</td> <td>  347.741</td> <td>   -5.690</td> <td> 0.000</td> <td>-2664.907</td> <td>-1292.612</td>
</tr>
<tr>
  <th>expected_recovery_amount</th> <td>    2.7577</td> <td>    0.345</td> <td>    7.986</td> <td> 0.000</td> <td>    2.076</td> <td>    3.439</td>
</tr>
</table>
<table class="simpletable">
<tr>
  <th>Omnibus:</th>       <td>64.493</td> <th>  Durbin-Watson:     </th> <td>   1.777</td>
</tr>
<tr>
  <th>Prob(Omnibus):</th> <td> 0.000</td> <th>  Jarque-Bera (JB):  </th> <td> 185.818</td>
</tr>
<tr>
  <th>Skew:</th>          <td> 1.463</td> <th>  Prob(JB):          </th> <td>4.47e-41</td>
</tr>
<tr>
  <th>Kurtosis:</th>      <td> 6.977</td> <th>  Cond. No.          </th> <td>1.80e+04</td>
</tr>
</table><br/><br/>Warnings:<br/>[1] Standard Errors assume that the covariance matrix of the errors is correctly specified.<br/>[2] The condition number is large, 1.8e+04. This might indicate that there are<br/>strong multicollinearity or other numerical problems.

```python
def test_x():
    correct_x= df.loc[(df['expected_recovery_amount']<1100) & (df['expected_recovery_amount']>=900)]['expected_recovery_amount']
    correct_x = sm.add_constant(correct_x)
    assert correct_x['expected_recovery_amount'].mean() == X['expected_recovery_amount'].mean(), \
        "The mean expected_recovery_amount for X appears incorrect. Check your assignment of X.  It should include expected_recovery_amount and indicator_1000 when the expected_recovery_amount is <1100 and >=900."
def test_y():
    correct_y= df.loc[(df['expected_recovery_amount']<1100) & (df['expected_recovery_amount']>=900)]['actual_recovery_amount']
    assert correct_y.mean() == y.mean(), \
        "The mean actual_recovery_amount for y appears incorrect. Check your assignment of y. It should include the actual_recovery_amount when the expected_recovery_amount is <1100 and >=900."

# def test_df_correctly_loaded():
#     correct_model = sm.OLS(y,x).fit()
#     assert correct_model.params[1] == model.params[1], \
#         "Check your assignment of model. It should be equal to sm.OLS(y,X).fit()."
```

    2/2 tests passed

## 8. Regression modeling: adding true threshold
<p>From the first model, we see that the expected recovery amount's regression coefficient is statistically significant. </p>
<p>The second model adds an indicator of the true threshold to the model (in this case at \$1000).  </p>
<p>We will create an indicator variable (either a 0 or a 1) that represents whether or not the expected recovery amount was greater than \$1000. When we add the true threshold to the model, the regression coefficient for the true threshold represents the additional amount recovered due to the higher recovery strategy.  That is to say, the regression coefficient for the true threshold measures the size of the discontinuity for customers just above and just below the threshold.</p>
<p>If the higher recovery strategy helped recovery more money, then the regression coefficient of the true threshold will be greater than zero.  If the higher recovery strategy did not help recovery more money, then the regression coefficient will not be statistically significant.</p>

```python
# Create indicator (0 or 1) for expected recovery amount >= $1000
df['indicator_1000'] = np.where(df['expected_recovery_amount']<1000, 0, 1)
era_900_1100 = df.loc[(df['expected_recovery_amount']<1100) &
                      (df['expected_recovery_amount']>=900)]

# Define X and y
X = era_900_1100['expected_recovery_amount']
y = era_900_1100['actual_recovery_amount']
X = sm.add_constant(X)

# Build linear regression model
model = sm.OLS(y,X).fit()

# Print the model summary
model.summary()
```

<table class="simpletable">
<caption>OLS Regression Results</caption>
<tr>
  <th>Dep. Variable:</th>    <td>actual_recovery_amount</td> <th>  R-squared:         </th> <td>   0.261</td>
</tr>
<tr>
  <th>Model:</th>                      <td>OLS</td>          <th>  Adj. R-squared:    </th> <td>   0.256</td>
</tr>
<tr>
  <th>Method:</th>                <td>Least Squares</td>     <th>  F-statistic:       </th> <td>   63.78</td>
</tr>
<tr>
  <th>Date:</th>                <td>Fri, 02 Jun 2023</td>    <th>  Prob (F-statistic):</th> <td>1.56e-13</td>
</tr>
<tr>
  <th>Time:</th>                    <td>19:00:52</td>        <th>  Log-Likelihood:    </th> <td> -1278.9</td>
</tr>
<tr>
  <th>No. Observations:</th>         <td>   183</td>         <th>  AIC:               </th> <td>   2562.</td>
</tr>
<tr>
  <th>Df Residuals:</th>             <td>   181</td>         <th>  BIC:               </th> <td>   2568.</td>
</tr>
<tr>
  <th>Df Model:</th>                 <td>     1</td>         <th>                     </th>     <td> </td>
</tr>
<tr>
  <th>Covariance Type:</th>         <td>nonrobust</td>       <th>                     </th>     <td> </td>
</tr>
</table>
<table class="simpletable">
<tr>
              <td></td>                <th>coef</th>     <th>std err</th>      <th>t</th>      <th>P>|t|</th>  <th>[0.025</th>    <th>0.975]</th>
</tr>
<tr>
  <th>const</th>                    <td>-1978.7597</td> <td>  347.741</td> <td>   -5.690</td> <td> 0.000</td> <td>-2664.907</td> <td>-1292.612</td>
</tr>
<tr>
  <th>expected_recovery_amount</th> <td>    2.7577</td> <td>    0.345</td> <td>    7.986</td> <td> 0.000</td> <td>    2.076</td> <td>    3.439</td>
</tr>
</table>
<table class="simpletable">
<tr>
  <th>Omnibus:</th>       <td>64.493</td> <th>  Durbin-Watson:     </th> <td>   1.777</td>
</tr>
<tr>
  <th>Prob(Omnibus):</th> <td> 0.000</td> <th>  Jarque-Bera (JB):  </th> <td> 185.818</td>
</tr>
<tr>
  <th>Skew:</th>          <td> 1.463</td> <th>  Prob(JB):          </th> <td>4.47e-41</td>
</tr>
<tr>
  <th>Kurtosis:</th>      <td> 6.977</td> <th>  Cond. No.          </th> <td>1.80e+04</td>
</tr>
</table><br/><br/>Warnings:<br/>[1] Standard Errors assume that the covariance matrix of the errors is correctly specified.<br/>[2] The condition number is large, 1.8e+04. This might indicate that there are<br/>strong multicollinearity or other numerical problems.

```python
def test_x():
    correct_x= df.loc[(df['expected_recovery_amount']<1100) & (df['expected_recovery_amount']>=900),
           ['expected_recovery_amount','indicator_1000']]
    correct_x = sm.add_constant(correct_x)
    assert correct_x['expected_recovery_amount'].mean() == X['expected_recovery_amount'].mean(), \
        "The mean expected_recovery_amount for X appears incorrect. Check your assignment of X.  It should include expected_recovery_amount and indicator_1000 when the expected_recovery_amount is <1100 and >=900."
def test_y():
    correct_y= df.loc[(df['expected_recovery_amount']<1100) & (df['expected_recovery_amount']>=900)]['actual_recovery_amount']
    assert correct_y.mean() == y.mean(), \
        "The mean actual_recovery_amount for y appears incorrect. Check your assignment of y. It should include the actual_recovery_amount when the expected_recovery_amount is <1100 and >=900."

# def test_df_correctly_loaded():
#     correct_model = sm.OLS(y,X).fit()
#     assert correct_model.params[1] == model.params[1], \
#         "Check your assignment of model. It should be equal to sm.OLS(y,X).fit()."
```

    2/2 tests passed

## 9. Regression modeling: adjusting the window
<p>The regression coefficient for the true threshold was statistically significant with an estimated impact of around \$278.  This is much larger than the \$50 per customer needed to run this higher recovery strategy. </p>
<p>Before showing this to our manager, we want to convince ourselves that this result wasn't due to choosing an expected recovery amount window of \$900 to \$1100. Let's repeat this analysis for the window from \$950 to \$1050 to see if we get similar results.</p>
<p>The answer? Whether we use a wide (\$900 to \$1100) or narrower window (\$950 to \$1050), the incremental recovery amount at the higher recovery strategy is much greater than the \$50 per customer it costs for the higher recovery strategy.  So we conclude that the higher recovery strategy is worth the extra cost of \$50 per customer.</p>

```python
# Redefine era_950_1050 so the indicator variable is included
era_950_1050 = df.loc[(df['expected_recovery_amount']<1050) &
                      (df['expected_recovery_amount']>=950)]

# Define X and y
X = era_950_1050[['expected_recovery_amount','indicator_1000']]
y = era_950_1050['actual_recovery_amount']
X = sm.add_constant(X)

# Build linear regression model
model = sm.OLS(y,X).fit()

# Print the model summary
model.summary()
```

<table class="simpletable">
<caption>OLS Regression Results</caption>
<tr>
  <th>Dep. Variable:</th>    <td>actual_recovery_amount</td> <th>  R-squared:         </th> <td>   0.283</td>
</tr>
<tr>
  <th>Model:</th>                      <td>OLS</td>          <th>  Adj. R-squared:    </th> <td>   0.269</td>
</tr>
<tr>
  <th>Method:</th>                <td>Least Squares</td>     <th>  F-statistic:       </th> <td>   18.99</td>
</tr>
<tr>
  <th>Date:</th>                <td>Fri, 02 Jun 2023</td>    <th>  Prob (F-statistic):</th> <td>1.12e-07</td>
</tr>
<tr>
  <th>Time:</th>                    <td>19:00:52</td>        <th>  Log-Likelihood:    </th> <td> -692.92</td>
</tr>
<tr>
  <th>No. Observations:</th>         <td>    99</td>         <th>  AIC:               </th> <td>   1392.</td>
</tr>
<tr>
  <th>Df Residuals:</th>             <td>    96</td>         <th>  BIC:               </th> <td>   1400.</td>
</tr>
<tr>
  <th>Df Model:</th>                 <td>     2</td>         <th>                     </th>     <td> </td>
</tr>
<tr>
  <th>Covariance Type:</th>         <td>nonrobust</td>       <th>                     </th>     <td> </td>
</tr>
</table>
<table class="simpletable">
<tr>
              <td></td>                <th>coef</th>     <th>std err</th>      <th>t</th>      <th>P>|t|</th>  <th>[0.025</th>    <th>0.975]</th>
</tr>
<tr>
  <th>const</th>                    <td> -279.5243</td> <td> 1840.707</td> <td>   -0.152</td> <td> 0.880</td> <td>-3933.298</td> <td> 3374.250</td>
</tr>
<tr>
  <th>expected_recovery_amount</th> <td>    0.9189</td> <td>    1.886</td> <td>    0.487</td> <td> 0.627</td> <td>   -2.825</td> <td>    4.663</td>
</tr>
<tr>
  <th>indicator_1000</th>           <td>  286.5337</td> <td>  111.352</td> <td>    2.573</td> <td> 0.012</td> <td>   65.502</td> <td>  507.566</td>
</tr>
</table>
<table class="simpletable">
<tr>
  <th>Omnibus:</th>       <td>39.302</td> <th>  Durbin-Watson:     </th> <td>   1.955</td>
</tr>
<tr>
  <th>Prob(Omnibus):</th> <td> 0.000</td> <th>  Jarque-Bera (JB):  </th> <td>  82.258</td>
</tr>
<tr>
  <th>Skew:</th>          <td> 1.564</td> <th>  Prob(JB):          </th> <td>1.37e-18</td>
</tr>
<tr>
  <th>Kurtosis:</th>      <td> 6.186</td> <th>  Cond. No.          </th> <td>6.81e+04</td>
</tr>
</table><br/><br/>Warnings:<br/>[1] Standard Errors assume that the covariance matrix of the errors is correctly specified.<br/>[2] The condition number is large, 6.81e+04. This might indicate that there are<br/>strong multicollinearity or other numerical problems.

```python
def test_x():
    correct_x= df.loc[(df['expected_recovery_amount']<1050) & (df['expected_recovery_amount']>=950),['expected_recovery_amount','indicator_1000']]
    correct_x = sm.add_constant(correct_x)
    assert correct_x['expected_recovery_amount'].mean() == X['expected_recovery_amount'].mean(), \
        "The mean expected_recovery_amount for X appears incorrect. Check your assignment of X.  It should include expected_recovery_amount and indicator_1000 when the expected_recovery_amount is <1050 and >=950."
def test_y():
    correct_y= df.loc[(df['expected_recovery_amount']<1050) & (df['expected_recovery_amount']>=950)]['actual_recovery_amount']
    assert correct_y.mean() == y.mean(), \
        "The mean actual_recovery_amount for y appears incorrect. Check your assignment of y. It should include the actual_recovery_amount when the expected_recovery_amount is <1050 and >=950."

# def test_df_correctly_loaded():
#     correct_model = sm.OLS(y,X).fit()
#     assert correct_model.params[1] == model.params[1], \
#         "Check your assignment of model.  It should be equal to sm.OLS(y,X).fit()."
```

    2/2 tests passed
