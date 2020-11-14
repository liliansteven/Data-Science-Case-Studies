# [Statistical Thinking in Python (Part 2)](https://learn.datacamp.com/courses/statistical-thinking-in-python-part-2) `10H`

## Course Description
`After completing Statistical Thinking in Python (Part 1), you have the probabilistic mindset and foundational hacker stats skills to dive into data sets and extract useful information from them. In this course, you will do just that, expanding and honing your hacker stats toolbox to perform the two key tasks in statistical inference, parameter estimation and hypothesis testing. You will work with real data sets as you learn, culminating with analysis of measurements of the beaks of the Darwin's famous finches. You will emerge from this course with new knowledge and lots of practice under your belt, ready to attack your own inference problems out in the world.`

## `Chapter 1` Parameter estimation by optimization

### Video: Let’s flip a coin in Python
### How often do we get no-hitters?
- The number of games played between each no-hitter in the modern era (1901-2015) of Major League Baseball is stored in the array nohitter_times.
- If you assume that no-hitters are described as a Poisson process, then the time between no-hitters is Exponentially distributed. As you have seen, the Exponential distribution has a single parameter, which we will call τ, the typical interval time. The value of the parameter τ that makes the exponential distribution best match the data is the mean interval time (where time is in units of number of games) between no-hitters.
- Compute the value of this parameter from the data. Then, use np.random.exponential() to "repeat" the history of Major League Baseball by drawing inter-no-hitter times from an exponential distribution with the τ you found and plot the histogram as an approximation to the PDF.
- NumPy, pandas, matlotlib.pyplot, and seaborn have been imported for you as np, pd, plt, and sns, respectively.
```
<class 'numpy.ndarray'> nohitter_times
[ 843 1613 1101  215  684  814  278  324  161  219  545  715  966  624
   29  450  107   20   91 1325  124 1468  104 1309  429   62 1878 1104
  123  251   93  188  983  166   96  702   23  524   26  299   59   39
   12    2  308 1114  813  887  645 2088   42 2090   11  886 1665 1084
 2900 2432  750 4021 1070 1765 1322   26  548 1525   77 2181 2752  127
 2147  211   41 1575  151  479  697  557 2267  542  392   73  603  233
  255  528  397 1529 1023 1194  462  583   37  943  996  480 1497  717
  224  219 1531  498   44  288  267  600   52  269 1086  386  176 2199
  216   54  675 1243  463  650  171  327  110  774  509    8  197  136
   12 1124   64  380  811  232  192  731  715  226  605  539 1491  323
  240  179  702  156   82 1397  354  778  603 1001  385  986  203  149
  576  445  180 1403  252  675 1351 2983 1568   45  899 3260 1025   31
  100 2055 4043   79  238 3931 2351  595  110  215    0  563  206  660
  242  577  179  157  192  192 1848  792 1693   55  388  225 1134 1172
 1555   31 1582 1044  378 1687 2915  280  765 2819  511 1521  745 2491
  580 2072 6450  578  745 1075 1103 1549 1520  138 1202  296  277  351
  391  950  459   62 1056 1128  139  420   87   71  814  603 1349  162
 1027  783  326  101  876  381  905  156  419  239  119  129  467]
```
#### Question 1
- Seed the random number generator with 42.
- Compute the mean time (in units of number of games) between no-hitters.
- Draw 100,000 samples from an Exponential distribution with the parameter you computed from the mean of the inter-no-hitter times.
- Plot the theoretical PDF using plt.hist(). Remember to use keyword arguments bins=50, normed=True, and histtype='step'. Be sure to label your axes.
- Show your plot.
```python
# Seed random number generator
np.random.seed(42)

# Compute mean no-hitter time: tau
tau = np.mean(nohitter_times)

# Draw out of an exponential distribution with parameter tau: inter_nohitter_time
inter_nohitter_time = np.random.exponential(tau, 100000)

# Plot the PDF and label axes
_ = plt.hist(inter_nohitter_time,
             bins=50, normed=True, histtype='step')
_ = plt.xlabel('Games between no-hitters')
_ = plt.ylabel('PDF')

# Show the plot
plt.show()
```
### Do the data follow our story?
- You have modeled no-hitters using an Exponential distribution. Create an ECDF of the real data. Overlay the theoretical CDF with the ECDF from the data. This helps you to verify that the Exponential distribution describes the observed data.
#### Question 1
- Compute an ECDF from the actual time between no-hitters (nohitter_times). Use the ecdf() function you wrote in the prequel course.
- Create a CDF from the theoretical samples you took in the last exercise (inter_nohitter_time).
- Plot x_theor and y_theor as a line using plt.plot(). Then overlay the ECDF of the real data x and y as points. To do this, you have to specify the keyword arguments marker = '.' and linestyle = 'none' in addition to x and y inside plt.plot().
- Set a 2% margin on the plot.
- Show the plot.
```python
# Create an ECDF from real data: x, y
x, y = ecdf(nohitter_times)

# Create a CDF from theoretical samples: x_theor, y_theor
x_theor, y_theor = ecdf(inter_nohitter_time)

# Overlay the plots
plt.plot(x_theor, y_theor)
plt.plot(x, y, marker='.', linestyle='none')

# Margins and axis labels
plt.margins(0.02)
plt.xlabel('Games between no-hitters')
plt.ylabel('CDF')

# Show the plot
plt.show()
```
### How is this parameter optimal?
- Now sample out of an exponential distribution with τ being twice as large as the optimal τ. Do it again for τ half as large. Make CDFs of these samples and overlay them with your data. You can see that they do not reproduce the data as well. Thus, the τ you computed from the mean inter-no-hitter times is optimal in that it best reproduces the data.
- Note: In this and all subsequent exercises, the random number generator is pre-seeded for you to save you some typing.
#### Question 1
- Take 10000 samples out of an Exponential distribution with parameter τ1/2 = tau/2.
- Take 10000 samples out of an Exponential distribution with parameter τ2 = 2*tau.
- Generate CDFs from these two sets of samples using your ecdf() function.
- Add these two CDFs as lines to your plot. This has been done for you, so hit 'Submit Answer' to view the plot!
```python
# Plot the theoretical CDFs
plt.plot(x_theor, y_theor)
plt.plot(x, y, marker='.', linestyle='none')
plt.margins(0.02)
plt.xlabel('Games between no-hitters')
plt.ylabel('CDF')

# Take samples with half tau: samples_half
samples_half = np.random.exponential(tau/2, 10000)

# Take samples with double tau: samples_double
samples_double = np.random.exponential(2*tau, 10000)

# Generate CDFs from these samples
x_half, y_half = ecdf(samples_half)
x_double, y_double = ecdf(samples_double)

# Plot these CDFs as lines
_ = plt.plot(x_half, y_half)
_ = plt.plot(x_double, y_double)

# Show the plot
plt.show()
```

### Video: Linear regression by least squares
### EDA of literacy/fertility data
- In the next few exercises, we will look at the correlation between female literacy and fertility (defined as the average number of children born per woman) throughout the world. For ease of analysis and interpretation, we will work with the illiteracy rate.
- It is always a good idea to do some EDA ahead of our analysis. To this end, plot the fertility versus illiteracy and compute the Pearson correlation coefficient. The Numpy array illiteracy has the illiteracy rate among females for most of the world's nations. The array fertility has the corresponding fertility data.
```
<class 'numpy.ndarray'> illiteracy
[ 9.5 49.2  1.  11.2  9.8 60.  50.2 51.2  0.6  1.   8.5  6.1  9.8  1.
 42.2 77.2 18.7 22.8  8.5 43.9  1.   1.   1.5 10.8 11.9  3.4  0.4  3.1
  6.6 33.7 40.4  2.3 17.2  0.7 36.1  1.  33.2 55.9 30.8 87.4 15.4 54.6
  5.1  1.1 10.2 19.8  0.  40.7 57.2 59.9  3.1 55.7 22.8 10.9 34.7 32.2
 43.   1.3  1.   0.5 78.4 34.2 84.9 29.1 31.3 18.3 81.8 39.  11.2 67.
  4.1  0.2 78.1  1.   7.1  1.  29.   1.1 11.7 73.6 33.9 14.   0.3  1.
  0.8 71.9 40.1  1.   2.1  3.8 16.5  4.1  0.5 44.4 46.3 18.7  6.5 36.8
 18.6 11.1 22.1 71.1  1.   0.   0.9  0.7 45.5  8.4  0.   3.8  8.5  2.
  1.  58.9  0.3  1.  14.  47.   4.1  2.2  7.2  0.3  1.5 50.5  1.3  0.6
 19.1  6.9  9.2  2.2  0.2 12.3  4.9  4.6  0.3 16.5 65.7 63.5 16.8  0.2
  1.8  9.6 15.2 14.4  3.3 10.6 61.3 10.9 32.2  9.3 11.6 20.7  6.5  6.7
  3.5  1.   1.6 20.5  1.5 16.7  2.   0.9]
```
```
<class 'numpy.ndarray'> fertility
[1.769 2.682 2.077 2.132 1.827 3.872 2.288 5.173 1.393 1.262 2.156 3.026
 2.033 1.324 2.816 5.211 2.1   1.781 1.822 5.908 1.881 1.852 1.39  2.281
 2.505 1.224 1.361 1.468 2.404 5.52  4.058 2.223 4.859 1.267 2.342 1.579
 6.254 2.334 3.961 6.505 2.53  2.823 2.498 2.248 2.508 3.04  1.854 4.22
 5.1   4.967 1.325 4.514 3.173 2.308 4.62  4.541 5.637 1.926 1.747 2.294
 5.841 5.455 7.069 2.859 4.018 2.513 5.405 5.737 3.363 4.89  1.385 1.505
 6.081 1.784 1.378 1.45  1.841 1.37  2.612 5.329 5.33  3.371 1.281 1.871
 2.153 5.378 4.45  1.46  1.436 1.612 3.19  2.752 3.35  4.01  4.166 2.642
 2.977 3.415 2.295 3.019 2.683 5.165 1.849 1.836 2.518 2.43  4.528 1.263
 1.885 1.943 1.899 1.442 1.953 4.697 1.582 2.025 1.841 5.011 1.212 1.502
 2.516 1.367 2.089 4.388 1.854 1.748 2.978 2.152 2.362 1.988 1.426 3.29
 3.264 1.436 1.393 2.822 4.969 5.659 3.24  1.693 1.647 2.36  1.792 3.45
 1.516 2.233 2.563 5.283 3.885 0.966 2.373 2.663 1.251 2.052 3.371 2.093
 2.    3.883 3.852 3.718 1.732 3.928]
```
#### Question 1
- Plot fertility (y-axis) versus illiteracy (x-axis) as a scatter plot.
- Set a 2% margin.
- Compute and print the Pearson correlation coefficient between illiteracy and fertility.
```python
# Plot the illiteracy rate versus fertility
_ = plt.plot(illiteracy, fertility, marker='.', linestyle='none')

# Set the margins and label axes
plt.margins(0.02)
_ = plt.xlabel('percent illiterate')
_ = plt.ylabel('fertility')

# Show the plot
plt.show()

# Show the Pearson correlation coefficient
print(pearson_r(illiteracy, fertility))
```
```
0.8041324026815344
```
### Linear regression
- We will assume that fertility is a linear function of the female illiteracy rate. That is, f=ai+b, where a is the slope and b is the intercept. We can think of the intercept as the minimal fertility rate, probably somewhere between one and two. The slope tells us how the fertility rate varies with illiteracy. We can find the best fit line using np.polyfit().
- Plot the data and the best fit line. Print out the slope and intercept. (Think: what are their units?)
#### Question 1
- Compute the slope and intercept of the regression line using np.polyfit(). Remember, fertility is on the y-axis and illiteracy on the x-axis.
- Print out the slope and intercept from the linear regression.
- To plot the best fit line, create an array x that consists of 0 and 100 using np.array(). Then, compute the theoretical values of y based on your regression parameters. I.e., y = a * x + b.
- Plot the data and the regression line on the same plot. Be sure to label your axes.
- Hit 'Submit Answer' to display your plot.
```python
# Plot the illiteracy rate versus fertility
_ = plt.plot(illiteracy, fertility, marker='.', linestyle='none')
plt.margins(0.02)
_ = plt.xlabel('percent illiterate')
_ = plt.ylabel('fertility')

# Perform a linear regression using np.polyfit(): a, b
a, b = np.polyfit(illiteracy, fertility, 1)

# Print the results to the screen
print('slope =', a, 'children per woman / percent illiterate')
print('intercept =', b, 'children per woman')

# Make theoretical line to plot
x = np.array([0, 100])
y = a * x + b

# Add regression line to your plot
_ = plt.plot(x, y)

# Draw the plot
plt.show()
```
```
slope = 0.04979854809063423 children per woman / percent illiterate
intercept = 1.888050610636557 children per woman
```
### How is it optimal?
- The function np.polyfit() that you used to get your regression parameters finds the optimal slope and intercept. It is optimizing the sum of the squares of the residuals, also known as RSS (for residual sum of squares). In this exercise, you will plot the function that is being optimized, the RSS, versus the slope parameter a. To do this, fix the intercept to be what you found in the optimization. Then, plot the RSS vs. the slope. Where is it minimal?
#### Question 1
- Specify the values of the slope to compute the RSS. Use np.linspace() to get 200 points in the range between 0 and 0.1. For example, to get 100 points in the range between 0 and 0.5, you could use np.linspace() like so: np.linspace(0, 0.5, 100).
- Initialize an array, rss, to contain the RSS using np.empty_like() and the array you created above. The empty_like() function returns a new array with the same shape and type as a given array (in this case, a_vals).
- Write a for loop to compute the sum of RSS of the slope. Hint: the RSS is given by np.sum((y_data - a * x_data - b)**2). The variable b you computed in the last exercise is already in your namespace. Here, fertility is the y_data and illiteracy the x_data.
- Plot the RSS (rss) versus slope (a_vals).
- Hit 'Submit Answer' to see the plot!
```python
# Specify slopes to consider: a_vals
a_vals = np.linspace(0, 0.1, 200)

# Initialize sum of square of residuals: rss
rss = np.empty_like(a_vals)

# Compute sum of square of residuals for each value of a_vals
for i, a in enumerate(a_vals):
    rss[i] = np.sum((fertility - a*illiteracy - b)**2)

# Plot the RSS
plt.plot(a_vals, rss, '-')
plt.xlabel('slope (children per woman / percent illiterate)')
plt.ylabel('sum of square of residuals')

plt.show()
```

### Video: The importance of EDA: Anscombe's quartet
#### The importance of EDA
- Why should exploratory data analysis be the first step in an analysis of data (after getting your data imported and cleaned, of course)?
```
You can be protected from misinterpretation of the type demonstrated by Anscombe's quartet.
EDA provides a good starting point for planning the rest of your analysis.
EDA is not really any more difficult than any of the subsequent analysis, so there is no excuse for not exploring the data.
All of these reasons!
```
```
All of these reasons!
```
### Linear regression on appropriate Anscombe data
- For practice, perform a linear regression on the data set from Anscombe's quartet that is most reasonably interpreted with linear regression.
```
<class 'numpy.ndarray'> x
[10.  8. 13.  9. 11. 14.  6.  4. 12.  7.  5.]
```
```
<class 'numpy.ndarray'> y
[ 8.04  6.95  7.58  8.81  8.33  9.96  7.24  4.26 10.84  4.82  5.68]
```
#### Question 1
- Compute the parameters for the slope and intercept using np.polyfit(). The Anscombe data are stored in the arrays x and y.
- Print the slope a and intercept b.
- Generate theoretical x and y data from the linear regression. Your x array, which you can create with np.array(), should consist of 3 and 15. To generate the y data, multiply the slope by x_theor and add the intercept.
- Plot the Anscombe data as a scatter plot and then plot the theoretical line. Remember to include the marker='.' and linestyle='none' keyword arguments in addition to x and y when to plot the Anscombe data as a scatter plot. You do not need these arguments when plotting the theoretical line.
- Hit 'Submit Answer' to see the plot!
```python
# Perform linear regression: a, b
a, b = np.polyfit(x, y, 1)

# Print the slope and intercept
print(a, b)

# Generate theoretical x and y data: x_theor, y_theor
x_theor = np.array([3, 15])
y_theor = a * x_theor + b

# Plot the Anscombe data and theoretical line
_ = plt.plot(x, y, marker='.', linestyle='none')
_ = plt.plot(x_theor, y_theor)

# Label the axes
plt.xlabel('x')
plt.ylabel('y')

# Show the plot
plt.show()
```
```
0.5000909090909095 3.000090909090909
```
### Linear regression on all Anscombe data
- Now, to verify that all four of the Anscombe data sets have the same slope and intercept from a linear regression, you will compute the slope and intercept for each set. The data are stored in lists; anscombe_x = [x1, x2, x3, x4] and anscombe_y = [y1, y2, y3, y4], where, for example, x2 and y2 are the x and y values for the second Anscombe data set.
#### Question 1
- Write a for loop to do the following for each Anscombe data set.
- Compute the slope and intercept.
- Print the slope and intercept.
```python
# Iterate through x,y pairs
for x, y in zip(anscombe_x, anscombe_y):
    # Compute the slope and intercept: a, b
    a, b = np.polyfit(x, y, 1)

    # Print the result
    print('slope:', a, 'intercept:', b)
```
```
slope: 0.5000909090909095 intercept: 3.000090909090909
slope: 0.5000000000000004 intercept: 3.0009090909090896
slope: 0.4997272727272731 intercept: 3.0024545454545453
slope: 0.4999090909090908 intercept: 3.0017272727272735
```

## `Chapter 2` Bootstrap confidence intervals

### Video: Generating bootstrap replicates
#### Getting the terminology down
- Getting tripped up over terminology is a common cause of frustration in students. Unfortunately, you often will read and hear other data scientists using different terminology for bootstrap samples and replicates. This is even more reason why we need everything to be clear and consistent for this course. So, before going forward discussing bootstrapping, let's get our terminology down. If we have a data set with n repeated measurements, a bootstrap sample is an array of length n that was drawn from the original data with replacement. What is a bootstrap replicate?
```
Just another name for a bootstrap sample.
A single value of a statistic computed from a bootstrap sample.
An actual repeat of the measurements.
```
```
A single value of a statistic computed from a bootstrap sample.
```
#### Bootstrapping by hand
- To help you gain intuition about how bootstrapping works, imagine you have a data set that has only three points, [-1, 0, 1]. How many unique bootstrap samples can be drawn (e.g., [-1, 0, 1] and [1, 0, -1] are unique), and what is the maximum mean you can get from a bootstrap sample? It might be useful to jot down the samples on a piece of paper.
- (These are too few data to get meaningful results from bootstrap procedures, but this example is useful for intuition.)
```
There are 3 unique samples, and the maximum mean is 0.
There are 10 unique samples, and the maximum mean is 0.
There are 10 unique samples, and the maximum mean is 1.
There are 27 unique samples, and the maximum mean is 0.
There are 27 unique samples, and the maximum mean is 1.
```
```
There are 27 unique samples, and the maximum mean is 1.
```
### Visualizing bootstrap samples
- In this exercise, you will generate bootstrap samples from the set of annual rainfall data measured at the Sheffield Weather Station in the UK from 1883 to 2015. The data are stored in the NumPy array rainfall in units of millimeters (mm). By graphically displaying the bootstrap samples with an ECDF, you can get a feel for how bootstrap sampling allows probabilistic descriptions of data.
```
<class 'numpy.ndarray'> rainfall
[ 875.5  648.2  788.1  940.3  491.1  743.5  730.1  686.5  878.8  865.6
  654.9  831.5  798.1  681.8  743.8  689.1  752.1  837.2  710.6  749.2
  967.1  701.2  619.   747.6  803.4  645.6  804.1  787.4  646.8  997.1
  774.   734.5  835.   840.7  659.6  828.3  909.7  856.9  578.3  904.2
  883.9  740.1  773.9  741.4  866.8  871.1  712.5  919.2  927.9  809.4
  633.8  626.8  871.3  774.3  898.8  789.6  936.3  765.4  882.1  681.1
  661.3  847.9  683.9  985.7  771.1  736.6  713.2  774.5  937.7  694.5
  598.2  983.8  700.2  901.3  733.5  964.4  609.3 1035.2  718.   688.6
  736.8  643.3 1038.5  969.   802.7  876.6  944.7  786.6  770.4  808.6
  761.3  774.2  559.3  674.2  883.6  823.9  960.4  877.8  940.6  831.8
  906.2  866.5  674.1  998.1  789.3  915.   737.1  763.   666.7  824.5
  913.8  905.1  667.8  747.4  784.7  925.4  880.2 1086.9  764.4 1050.1
  595.2  855.2  726.9  785.2  948.8  970.6  896.   618.4  572.4 1146.4
  728.2  864.2  793. ]
```
#### Question 1
- Write a for loop to acquire 50 bootstrap samples of the rainfall data and plot their ECDF.
- Use np.random.choice() to generate a bootstrap sample from the NumPy array rainfall. Be sure that the size of the resampled array is len(rainfall).
- Use the function ecdf() that you wrote in the prequel to this course to generate the x and y values for the ECDF of the bootstrap sample bs_sample.
- Plot the ECDF values. Specify color='gray' (to make gray dots) and alpha=0.1 (to make them semi-transparent, since we are overlaying so many) in addition to the marker='.' and linestyle='none' keyword arguments.
- Use ecdf() to generate x and y values for the ECDF of the original rainfall data available in the array rainfall.
- Plot the ECDF values of the original data.
- Hit 'Submit Answer' to visualize the samples!
```python
for _ in range(50):
    # Generate bootstrap sample: bs_sample
    bs_sample = np.random.choice(rainfall, size=len(rainfall))

    # Compute and plot ECDF from bootstrap sample
    x, y = ecdf(bs_sample)
    _ = plt.plot(x, y, marker='.', linestyle='none',
                 color='gray', alpha=0.1)

# Compute and plot ECDF from original data
x, y = ecdf(rainfall)
_ = plt.plot(x, y, marker='.')

# Make margins and label axes
plt.margins(0.02)
_ = plt.xlabel('yearly rainfall (mm)')
_ = plt.ylabel('ECDF')

# Show the plot
plt.show()
```

### Video: Bootstrap confidence intervals
### Generating many bootstrap replicates
- The function bootstrap_replicate_1d() from the video is available in your namespace. Now you'll write another function, draw_bs_reps(data, func, size=1), which generates many bootstrap replicates from the data set. This function will come in handy for you again and again as you compute confidence intervals and later when you do hypothesis tests.
- For your reference, the bootstrap_replicate_1d() function is provided below:
```
def bootstrap_replicate_1d(data, func):
    """Generate bootstrap replicate of 1D data."""
    bs_sample = np.random.choice(data, len(data))
    return func(bs_sample)
```
#### Question 1
- Define a function with call signature draw_bs_reps(data, func, size=1).
- Using np.empty(), initialize an array called bs_replicates of size size to hold all of the bootstrap replicates.
- Write a for loop that ranges over size and computes a replicate using bootstrap_replicate_1d(). Refer to the exercise description above to see the function signature of bootstrap_replicate_1d(). Store the replicate in the appropriate index of bs_replicates.
- Return the array of replicates bs_replicates. This has already been done for you.
```python
def draw_bs_reps(data, func, size=1):
    """Draw bootstrap replicates."""

    # Initialize array of replicates: bs_replicates
    bs_replicates = np.empty(size)

    # Generate replicates
    for i in range(size):
        bs_replicates[i] = bootstrap_replicate_1d(data, func)

    return bs_replicates
```
### Bootstrap replicates of the mean and the SEM
- In this exercise, you will compute a bootstrap estimate of the probability density function of the mean annual rainfall at the Sheffield Weather Station. Remember, we are estimating the mean annual rainfall we would get if the Sheffield Weather Station could repeat all of the measurements from 1883 to 2015 over and over again. This is a probabilistic estimate of the mean. You will plot the PDF as a histogram, and you will see that it is Normal.
- In fact, it can be shown theoretically that under not-too-restrictive conditions, the value of the mean will always be Normally distributed. (This does not hold in general, just for the mean and a few other statistics.) The standard deviation of this distribution, called the standard error of the mean, or SEM, is given by the standard deviation of the data divided by the square root of the number of data points. I.e., for a data set, sem = np.std(data) / np.sqrt(len(data)). Using hacker statistics, you get this same result without the need to derive it, but you will verify this result from your bootstrap replicates.
- The dataset has been pre-loaded for you into an array called rainfall.
#### Question 1
- Draw 10000 bootstrap replicates of the mean annual rainfall using your draw_bs_reps() function and the rainfall array. Hint: Pass in np.mean for func to compute the mean.
- As a reminder, draw_bs_reps() accepts 3 arguments: data, func, and size.
- Compute and print the standard error of the mean of rainfall.
- The formula to compute this is np.std(data) / np.sqrt(len(data)).
- Compute and print the standard deviation of your bootstrap replicates bs_replicates.
- Make a histogram of the replicates using the normed=True keyword argument and 50 bins.
- Hit 'Submit Answer' to see the plot!
```python
# Take 10,000 bootstrap replicates of the mean: bs_replicates
bs_replicates = draw_bs_reps(rainfall, np.mean, size=10000)

# Compute and print SEM
sem = np.std(rainfall) / np.sqrt(len(rainfall))
print(sem)

# Compute and print standard deviation of bootstrap replicates
bs_std = np.std(bs_replicates)
print(bs_std)

# Make a histogram of the results
_ = plt.hist(bs_replicates, bins=50, normed=True)
_ = plt.xlabel('mean annual rainfall (mm)')
_ = plt.ylabel('PDF')

# Show the plot
plt.show()
```
```
10.51054915050619
10.465927071184412
```
#### Confidence intervals of rainfall data
- A confidence interval gives upper and lower bounds on the range of parameter values you might expect to get if we repeat our measurements. For named distributions, you can compute them analytically or look them up, but one of the many beautiful properties of the bootstrap method is that you can take percentiles of your bootstrap replicates to get your confidence interval. Conveniently, you can use the np.percentile() function.
- Use the bootstrap replicates you just generated to compute the 95% confidence interval. That is, give the 2.5th and 97.5th percentile of your bootstrap replicates stored as bs_replicates. What is the 95% confidence interval?
```
(765, 776) mm/year
(780, 821) mm/year
(761, 817) mm/year
(761, 841) mm/year
```
```
(780, 821) mm/year
```
### Bootstrap replicates of other statistics
- We saw in a previous exercise that the mean is Normally distributed. This does not necessarily hold for other statistics, but no worry: as hackers, we can always take bootstrap replicates! In this exercise, you'll generate bootstrap replicates for the variance of the annual rainfall at the Sheffield Weather Station and plot the histogram of the replicates.
- Here, you will make use of the draw_bs_reps() function you defined a few exercises ago. It is provided below for your reference:
```
def draw_bs_reps(data, func, size=1):
    """Draw bootstrap replicates."""
    # Initialize array of replicates
    bs_replicates = np.empty(size)
    # Generate replicates
    for i in range(size):
        bs_replicates[i] = bootstrap_replicate_1d(data, func)
    return bs_replicates
```
#### Question 1
- Draw 10000 bootstrap replicates of the variance in annual rainfall, stored in the rainfall dataset, using your draw_bs_reps() function. Hint: Pass in np.var for computing the variance.
- Divide your variance replicates (bs_replicates) by 100 to put the variance in units of square centimeters for convenience.
- Make a histogram of bs_replicates using the normed=True keyword argument and 50 bins.
```python
# Generate 10,000 bootstrap replicates of the variance: bs_replicates
bs_replicates = draw_bs_reps(rainfall, np.var, size=10000)

# Put the variance in units of square centimeters
bs_replicates /= 100

# Make a histogram of the results
_ = plt.hist(bs_replicates, bins=50, normed=True)
_ = plt.xlabel('variance of annual rainfall (sq. cm)')
_ = plt.ylabel('PDF')

# Show the plot
plt.show()
```
### Confidence interval on the rate of no-hitters
- Consider again the inter-no-hitter intervals for the modern era of baseball. Generate 10,000 bootstrap replicates of the optimal parameter τ. Plot a histogram of your replicates and report a 95% confidence interval.
```
<class 'numpy.ndarray'> nohitter_times
[ 843 1613 1101  215  684  814  278  324  161  219  545  715  966  624
   29  450  107   20   91 1325  124 1468  104 1309  429   62 1878 1104
  123  251   93  188  983  166   96  702   23  524   26  299   59   39
   12    2  308 1114  813  887  645 2088   42 2090   11  886 1665 1084
 2900 2432  750 4021 1070 1765 1322   26  548 1525   77 2181 2752  127
 2147  211   41 1575  151  479  697  557 2267  542  392   73  603  233
  255  528  397 1529 1023 1194  462  583   37  943  996  480 1497  717
  224  219 1531  498   44  288  267  600   52  269 1086  386  176 2199
  216   54  675 1243  463  650  171  327  110  774  509    8  197  136
   12 1124   64  380  811  232  192  731  715  226  605  539 1491  323
  240  179  702  156   82 1397  354  778  603 1001  385  986  203  149
  576  445  180 1403  252  675 1351 2983 1568   45  899 3260 1025   31
  100 2055 4043   79  238 3931 2351  595  110  215    0  563  206  660
  242  577  179  157  192  192 1848  792 1693   55  388  225 1134 1172
 1555   31 1582 1044  378 1687 2915  280  765 2819  511 1521  745 2491
  580 2072 6450  578  745 1075 1103 1549 1520  138 1202  296  277  351
  391  950  459   62 1056 1128  139  420   87   71  814  603 1349  162
 1027  783  326  101  876  381  905  156  419  239  119  129  467]
```
#### Question 1
- Generate 10000 bootstrap replicates of τ from the nohitter_times data using your draw_bs_reps() function. Recall that the optimal τ is calculated as the mean of the data.
- Compute the 95% confidence interval using np.percentile() and passing in two arguments: The array bs_replicates, and the list of percentiles - in this case 2.5 and 97.5.
- Print the confidence interval.
- Plot a histogram of your bootstrap replicates. This has been done for you, so hit 'Submit Answer' to see the plot!
```python
# Draw bootstrap replicates of the mean no-hitter time (equal to tau): bs_replicates
bs_replicates = draw_bs_reps(nohitter_times, np.mean, size=10000)

# Compute the 95% confidence interval: conf_int
conf_int = np.percentile(bs_replicates, [2.5, 97.5])

# Print the confidence interval
print('95% confidence interval =', conf_int, 'games')

# Plot the histogram of the replicates
_ = plt.hist(bs_replicates, bins=50, normed=True)
_ = plt.xlabel(r'$\tau$ (games)')
_ = plt.ylabel('PDF')

# Show the plot
plt.show()
```
```
95% confidence interval = [660.67280876 871.63077689] games
```

### Video: Pairs bootstrap
### A function to do pairs bootstrap
- As discussed in the video, pairs bootstrap involves resampling pairs of data. Each collection of pairs fit with a line, in this case using np.polyfit(). We do this again and again, getting bootstrap replicates of the parameter values. To have a useful tool for doing pairs bootstrap, you will write a function to perform pairs bootstrap on a set of x,y data.
#### Question 1
- Define a function with call signature draw_bs_pairs_linreg(x, y, size=1) to perform pairs bootstrap estimates on linear regression parameters.
- Use np.arange() to set up an array of indices going from 0 to len(x). These are what you will resample and use them to pick values out of the x and y arrays.
- Use np.empty() to initialize the slope and intercept replicate arrays to be of size size.
- Write a for loop to:
- Resample the indices inds. Use np.random.choice() to do this.
- Make new x and y arrays bs_x and bs_y using the the resampled indices bs_inds. To do this, slice x and y with bs_inds.
- Use np.polyfit() on the new x and y arrays and store the computed slope and intercept.
- Return the pair bootstrap replicates of the slope and intercept.
```python
def draw_bs_pairs_linreg(x, y, size=1):
    """Perform pairs bootstrap for linear regression."""

    # Set up array of indices to sample from: inds
    inds = np.arange(len(x))

    # Initialize replicates: bs_slope_reps, bs_intercept_reps
    bs_slope_reps = np.empty(size)
    bs_intercept_reps = np.empty(size)

    # Generate replicates
    for i in range(size):
        bs_inds = np.random.choice(inds, size=len(inds))
        bs_x, bs_y = x[bs_inds], y[bs_inds]
        bs_slope_reps[i], bs_intercept_reps[i] = np.polyfit(bs_x, bs_y, 1)

    return bs_slope_reps, bs_intercept_reps
```
### Pairs bootstrap of literacy/fertility data
- Using the function you just wrote, perform pairs bootstrap to plot a histogram describing the estimate of the slope from the illiteracy/fertility data. Also report the 95% confidence interval of the slope. The data is available to you in the NumPy arrays illiteracy and fertility.
- As a reminder, draw_bs_pairs_linreg() has a function signature of draw_bs_pairs_linreg(x, y, size=1), and it returns two values: bs_slope_reps and bs_intercept_reps.
```
<class 'numpy.ndarray'> illiteracy
[ 9.5 49.2  1.  11.2  9.8 60.  50.2 51.2  0.6  1.   8.5  6.1  9.8  1.
 42.2 77.2 18.7 22.8  8.5 43.9  1.   1.   1.5 10.8 11.9  3.4  0.4  3.1
  6.6 33.7 40.4  2.3 17.2  0.7 36.1  1.  33.2 55.9 30.8 87.4 15.4 54.6
  5.1  1.1 10.2 19.8  0.  40.7 57.2 59.9  3.1 55.7 22.8 10.9 34.7 32.2
 43.   1.3  1.   0.5 78.4 34.2 84.9 29.1 31.3 18.3 81.8 39.  11.2 67.
  4.1  0.2 78.1  1.   7.1  1.  29.   1.1 11.7 73.6 33.9 14.   0.3  1.
  0.8 71.9 40.1  1.   2.1  3.8 16.5  4.1  0.5 44.4 46.3 18.7  6.5 36.8
 18.6 11.1 22.1 71.1  1.   0.   0.9  0.7 45.5  8.4  0.   3.8  8.5  2.
  1.  58.9  0.3  1.  14.  47.   4.1  2.2  7.2  0.3  1.5 50.5  1.3  0.6
 19.1  6.9  9.2  2.2  0.2 12.3  4.9  4.6  0.3 16.5 65.7 63.5 16.8  0.2
  1.8  9.6 15.2 14.4  3.3 10.6 61.3 10.9 32.2  9.3 11.6 20.7  6.5  6.7
  3.5  1.   1.6 20.5  1.5 16.7  2.   0.9]
```
```
<class 'numpy.ndarray'> fertility
[1.769 2.682 2.077 2.132 1.827 3.872 2.288 5.173 1.393 1.262 2.156 3.026
 2.033 1.324 2.816 5.211 2.1   1.781 1.822 5.908 1.881 1.852 1.39  2.281
 2.505 1.224 1.361 1.468 2.404 5.52  4.058 2.223 4.859 1.267 2.342 1.579
 6.254 2.334 3.961 6.505 2.53  2.823 2.498 2.248 2.508 3.04  1.854 4.22
 5.1   4.967 1.325 4.514 3.173 2.308 4.62  4.541 5.637 1.926 1.747 2.294
 5.841 5.455 7.069 2.859 4.018 2.513 5.405 5.737 3.363 4.89  1.385 1.505
 6.081 1.784 1.378 1.45  1.841 1.37  2.612 5.329 5.33  3.371 1.281 1.871
 2.153 5.378 4.45  1.46  1.436 1.612 3.19  2.752 3.35  4.01  4.166 2.642
 2.977 3.415 2.295 3.019 2.683 5.165 1.849 1.836 2.518 2.43  4.528 1.263
 1.885 1.943 1.899 1.442 1.953 4.697 1.582 2.025 1.841 5.011 1.212 1.502
 2.516 1.367 2.089 4.388 1.854 1.748 2.978 2.152 2.362 1.988 1.426 3.29
 3.264 1.436 1.393 2.822 4.969 5.659 3.24  1.693 1.647 2.36  1.792 3.45
 1.516 2.233 2.563 5.283 3.885 0.966 2.373 2.663 1.251 2.052 3.371 2.093
 2.    3.883 3.852 3.718 1.732 3.928]
```
#### Question 1
- Use your draw_bs_pairs_linreg() function to take 1000 bootstrap replicates of the slope and intercept. The x-axis data is illiteracy and y-axis data is fertility.
- Compute and print the 95% bootstrap confidence interval for the slope.
- Plot and show a histogram of the slope replicates. Be sure to label your axes. This has been done for you, so click 'Submit Answer' to see your histogram!
```python
# Generate replicates of slope and intercept using pairs bootstrap
bs_slope_reps, bs_intercept_reps = draw_bs_pairs_linreg(
                    illiteracy, fertility, size=1000)

# Compute and print 95% CI for slope
print(np.percentile(bs_slope_reps, [2.5, 97.5]))

# Plot the histogram
_ = plt.hist(bs_slope_reps, bins=50, normed=True)
_ = plt.xlabel('slope')
_ = plt.ylabel('PDF')
plt.show()
```
```
[0.04413953 0.05534094]
```
### Plotting bootstrap regressions
- A nice way to visualize the variability we might expect in a linear regression is to plot the line you would get from each bootstrap replicate of the slope and intercept. Do this for the first 100 of your bootstrap replicates of the slope and intercept (stored as bs_slope_reps and bs_intercept_reps).
#### Question 1
- Generate an array of x-values consisting of 0 and 100 for the plot of the regression lines. Use the np.array() function for this.
- Write a for loop in which you plot a regression line with a slope and intercept given by the pairs bootstrap replicates. Do this for 100 lines.
- When plotting the regression lines in each iteration of the for loop, recall the regression equation y = a*x + b. Here, a is bs_slope_reps[i] and b is bs_intercept_reps[i].
- Specify the keyword arguments linewidth=0.5, alpha=0.2, and color='red' in your call to plt.plot().
- Make a scatter plot with illiteracy on the x-axis and fertility on the y-axis. Remember to specify the marker='.' and linestyle='none' keyword arguments.
- Label the axes, set a 2% margin, and show the plot. This has been done for you, so hit 'Submit Answer' to visualize the bootstrap regressions!
```python
# Generate array of x-values for bootstrap lines: x
x = np.array([0, 100])

# Plot the bootstrap lines
for i in range(100):
    _ = plt.plot(x, 
                 bs_slope_reps[i] * x + bs_intercept_reps[i],
                 linewidth=0.5, alpha=0.2, color='red')

# Plot the data
_ = plt.plot(illiteracy, fertility, marker='.', linestyle='none')

# Label axes, set the margins, and show the plot
_ = plt.xlabel('illiteracy')
_ = plt.ylabel('fertility')
plt.margins(0.02)
plt.show()
```

## `Chapter 3` Introduction to hypothesis testing

### Video: Formulating and simulating a hypothesis
### Generating a permutation sample
- In the video, you learned that permutation sampling is a great way to simulate the hypothesis that two variables have identical probability distributions. This is often a hypothesis you want to test, so in this exercise, you will write a function to generate a permutation sample from two data sets.
- Remember, a permutation sample of two arrays having respectively n1 and n2 entries is constructed by concatenating the arrays together, scrambling the contents of the concatenated array, and then taking the first n1 entries as the permutation sample of the first array and the last n2 entries as the permutation sample of the second array.
#### Question 1
- Concatenate the two input arrays into one using np.concatenate(). Be sure to pass in data1 and data2 as one argument (data1, data2).
- Use np.random.permutation() to permute the concatenated array.
- Store the first len(data1) entries of permuted_data as perm_sample_1 and the last len(data2) entries of permuted_data as perm_sample_2. In practice, this can be achieved by using :len(data1) and len(data1): to slice permuted_data.
- Return perm_sample_1 and perm_sample_2.
```python
def permutation_sample(data1, data2):
    """Generate a permutation sample from two data sets."""

    # Concatenate the data sets: data
    data = np.concatenate((data1, data2))

    # Permute the concatenated array: permuted_data
    permuted_data = np.random.permutation(data)

    # Split the permuted array into two: perm_sample_1, perm_sample_2
    perm_sample_1 = permuted_data[:len(data1)]
    perm_sample_2 = permuted_data[len(data1):]

    return perm_sample_1, perm_sample_2
```
### Visualizing permutation sampling
- To help see how permutation sampling works, in this exercise you will generate permutation samples and look at them graphically.
- We will use the Sheffield Weather Station data again, this time considering the monthly rainfall in June (a dry month) and November (a wet month). We expect these might be differently distributed, so we will take permutation samples to see how their ECDFs would look if they were identically distributed.
- The data are stored in the Numpy arrays rain_june and rain_november.
- As a reminder, permutation_sample() has a function signature of permutation_sample(data_1, data_2) with a return value of permuted_data[:len(data_1)], permuted_data[len(data_1):], where permuted_data = np.random.permutation(np.concatenate((data_1, data_2)))
```
<class 'numpy.ndarray'> rain_june
[ 66.2  39.7  76.4  26.5  11.2  61.8   6.1  48.4  89.2 104.   34.   60.6
  57.1  79.1  90.9  32.3  63.8  78.2  27.5  43.4  30.1  17.3  77.5  44.9
  92.2  39.6  79.4  66.1  53.5  98.5  20.8  55.5  39.6  56.   65.1  14.8
  13.2  88.1   8.4  32.1  19.6  40.4   2.2  77.5 105.4  77.2  38.   27.1
 111.8  17.2  26.7  23.3  77.2  87.2  27.7  50.6  60.3  15.1   6.   29.4
  39.3  56.3  80.4  85.3  68.4  72.5  13.3  28.4  14.7  37.4  49.5  57.2
  85.9  82.1  31.8 126.6  30.7  41.4  33.9  13.5  99.1  70.2  91.8  61.3
  13.7  54.9  62.5  24.2  69.4  83.1  44.   48.5  11.9  16.6  66.4  90.
  34.9 132.8  33.4 225.    7.6  40.9  76.5  48.  140.   55.9  54.1  46.4
  68.6  52.2 108.3  14.6  11.3  29.8 130.9 152.4  61.   46.6  43.9  30.9
 111.1  68.5  42.2   9.8 285.6  56.7 168.2  41.2  47.8 166.6  37.8  45.4
  43.2]
```
```
<class 'numpy.ndarray'> rain_november
[ 83.6  30.9  62.2  37.   41.  160.2  18.2 122.4  71.3  44.2  49.1  37.6
 114.5  28.8  82.5  71.9  50.7  67.7 112.   63.6  42.8  57.2  99.1  86.4
  84.4  38.1  17.7 102.2 101.3  58.   82.  101.4  81.4 100.1  54.6  39.6
  57.5  29.2  48.8  37.3 115.4  55.6  62.   95.   84.2 118.1 153.2  83.4
 104.7  59.   46.4  50.  147.6  76.8  59.9 101.8 136.6 173.   92.5  37.
  59.8 142.1   9.9 158.2  72.6  28.  112.9 119.3 199.2  50.7  44.  170.7
  67.2  21.4  61.3  15.6 106.  116.2  42.3  38.5 132.5  40.8 147.5  93.9
  71.4  87.3 163.7 141.4  62.6  84.9  28.8 121.1  28.6  32.4 112.   50.
  96.9  81.8  70.4 117.5  41.2 124.9  78.2  93.   53.5  50.5  42.6  47.9
  73.1 129.1  56.9 103.3  60.5 134.3  93.1  49.5  48.2 167.9  27.  111.1
  55.4  36.2  57.4  66.8  58.3  60.  161.6 112.7  37.4 110.6  56.6  95.8
 126.8]
```
#### Question 1
- Write a for loop to generate 50 permutation samples, compute their ECDFs, and plot them.
- Generate a permutation sample pair from rain_june and rain_november using your permutation_sample() function.
- Generate the x and y values for an ECDF for each of the two permutation samples for the ECDF using your ecdf() function.
- Plot the ECDF of the first permutation sample (x_1 and y_1) as dots. Do the same for the second permutation sample (x_2 and y_2).
- Generate x and y values for ECDFs for the rain_june and rain_november data and plot the ECDFs using respectively the keyword arguments color='red' and color='blue'.
- Label your axes, set a 2% margin, and show your plot. This has been done for you, so just hit 'Submit Answer' to view the plot!
```python
for _ in range(50):
    # Generate permutation samples
    perm_sample_1, perm_sample_2 = permutation_sample(
                                    rain_june, rain_november)

    # Compute ECDFs
    x_1, y_1 = ecdf(perm_sample_1)
    x_2, y_2 = ecdf(perm_sample_2)

    # Plot ECDFs of permutation sample
    _ = plt.plot(x_1, y_1, marker='.', linestyle='none',
                 color='red', alpha=0.02)
    _ = plt.plot(x_2, y_2, marker='.', linestyle='none',
                 color='blue', alpha=0.02)

# Create and plot ECDFs from original data
x_1, y_1 = ecdf(rain_june)
x_2, y_2 = ecdf(rain_november)
_ = plt.plot(x_1, y_1, marker='.', linestyle='none', color='red')
_ = plt.plot(x_2, y_2, marker='.', linestyle='none', color='blue')

# Label axes, set margin, and show plot
plt.margins(0.02)
_ = plt.xlabel('monthly rainfall (mm)')
_ = plt.ylabel('ECDF')
plt.show()
```

### Video: Test statistics and p-values
#### Test statistics
- When performing hypothesis tests, your choice of test statistic should be:
```
something well-known, like the mean or median.
be a parameter that can be estimated.
be pertinent to the question you are seeking to answer in your hypothesis test.
```
```
be pertinent to the question you are seeking to answer in your hypothesis test.
```
#### What is a p-value?
- The p-value is generally a measure of:
```
the probability that the hypothesis you are testing is true.
the probability of observing your data if the hypothesis you are testing is true.
the probability of observing a test statistic equally or more extreme than the one you observed, given that the null hypothesis is true.
```
```
the probability of observing a test statistic equally or more extreme than the one you observed, given that the null hypothesis is true.
```
### Generating permutation replicates
- As discussed in the video, a permutation replicate is a single value of a statistic computed from a permutation sample. As the draw_bs_reps() function you wrote in chapter 2 is useful for you to generate bootstrap replicates, it is useful to have a similar function, draw_perm_reps(), to generate permutation replicates. You will write this useful function in this exercise.
- The function has call signature draw_perm_reps(data_1, data_2, func, size=1). Importantly, func must be a function that takes two arrays as arguments. In most circumstances, func will be a function you write yourself.
#### Question 1
- Define a function with this signature: draw_perm_reps(data_1, data_2, func, size=1).
- Initialize an array to hold the permutation replicates using np.empty().
- Write a for loop to:
- Compute a permutation sample using your permutation_sample() function
- Pass the samples into func() to compute the replicate and store the result in your array of replicates.
- Return the array of replicates.
```python
def draw_perm_reps(data_1, data_2, func, size=1):
    """Generate multiple permutation replicates."""

    # Initialize array of replicates: perm_replicates
    perm_replicates = np.empty(size)

    for i in range(size):
        # Generate permutation sample
        perm_sample_1, perm_sample_2 = permutation_sample(data_1, data_2)

        # Compute the test statistic
        perm_replicates[i] = func(perm_sample_1, perm_sample_2)

    return perm_replicates
```
### Look before you leap: EDA before hypothesis testing
- Kleinteich and Gorb (Sci. Rep., 4, 5225, 2014) performed an interesting experiment with South American horned frogs. They held a plate connected to a force transducer, along with a bait fly, in front of them. They then measured the impact force and adhesive force of the frog's tongue when it struck the target.
- Frog A is an adult and Frog B is a juvenile. The researchers measured the impact force of 20 strikes for each frog. In the next exercise, we will test the hypothesis that the two frogs have the same distribution of impact forces. But, remember, it is important to do EDA first! Let's make a bee swarm plot for the data. They are stored in a Pandas data frame, df, where column ID is the identity of the frog and column impact_force is the impact force in Newtons (N).
#### Data File (df.csv)
#### Question 1
- Use sns.swarmplot() to make a bee swarm plot of the data by specifying the x, y, and data keyword arguments.
- Label your axes.
- Show the plot.
```python
# Make bee swarm plot
_ = sns.swarmplot(x='ID', y='impact_force', data=df)

# Label axes
_ = plt.xlabel('frog')
_ = plt.ylabel('impact force (N)')

# Show the plot
plt.show()
```
### Permutation test on frog data
- The average strike force of Frog A was 0.71 Newtons (N), and that of Frog B was 0.42 N for a difference of 0.29 N. It is possible the frogs strike with the same force and this observed difference was by chance. You will compute the probability of getting at least a 0.29 N difference in mean strike force under the hypothesis that the distributions of strike forces for the two frogs are identical. We use a permutation test with a test statistic of the difference of means to test this hypothesis.
- For your convenience, the data has been stored in the arrays force_a and force_b.
#### Question 1
- Define a function with call signature diff_of_means(data_1, data_2) that returns the differences in means between two data sets, mean of data_1 minus mean of data_2.
- Use this function to compute the empirical difference of means that was observed in the frogs.
- Draw 10,000 permutation replicates of the difference of means.
- Compute the p-value.
- Print the p-value.
```python
def diff_of_means(data_1, data_2):
    """Difference in means of two arrays."""

    # The difference of means of data_1, data_2: diff
    diff = np.mean(data_1) - np.mean(data_2)

    return diff

# Compute difference of mean impact force from experiment: empirical_diff_means
empirical_diff_means = diff_of_means(force_a, force_b)

# Draw 10,000 permutation replicates: perm_replicates
perm_replicates = draw_perm_reps(force_a, force_b,
                                 diff_of_means, size=10000)

# Compute p-value: p
p = np.sum(perm_replicates >= empirical_diff_means) / len(perm_replicates)

# Print the result
print('p-value =', p)
```
```
p-value = 0.0063
```

### Video: Bootstrap hypothesis tests
### A one-sample bootstrap hypothesis test
- Another juvenile frog was studied, Frog C, and you want to see if Frog B and Frog C have similar impact forces. Unfortunately, you do not have Frog C's impact forces available, but you know they have a mean of 0.55 N. Because you don't have the original data, you cannot do a permutation test, and you cannot assess the hypothesis that the forces from Frog B and Frog C come from the same distribution. You will therefore test another, less restrictive hypothesis: The mean strike force of Frog B is equal to that of Frog C.
- To set up the bootstrap hypothesis test, you will take the mean as our test statistic. Remember, your goal is to calculate the probability of getting a mean impact force less than or equal to what was observed for Frog B if the hypothesis that the true mean of Frog B's impact forces is equal to that of Frog C is true. You first translate all of the data of Frog B such that the mean is 0.55 N. This involves adding the mean force of Frog C and subtracting the mean force of Frog B from each measurement of Frog B. This leaves other properties of Frog B's distribution, such as the variance, unchanged.
```
<class 'numpy.ndarray'> force_b
[0.172 0.142 0.037 0.453 0.355 0.022 0.502 0.273 0.72  0.582 0.198 0.198
 0.597 0.516 0.815 0.402 0.605 0.711 0.614 0.468]
```
#### Question 1
- Translate the impact forces of Frog B such that its mean is 0.55 N.
- Use your draw_bs_reps() function to take 10,000 bootstrap replicates of the mean of your translated forces.
- Compute the p-value by finding the fraction of your bootstrap replicates that are less than the observed mean impact force of Frog B. Note that the variable of interest here is force_b.
- Print your p-value.
```python
# Make an array of translated impact forces: translated_force_b
translated_force_b = force_b - np.mean(force_b) + 0.55

# Take bootstrap replicates of Frog B's translated impact forces: bs_replicates
bs_replicates = draw_bs_reps(translated_force_b, np.mean, 10000)

# Compute fraction of replicates that are less than the observed Frog B force: p
p = np.sum(bs_replicates <= np.mean(force_b)) / 10000

# Print the p-value
print('p = ', p)
```
```
p =  0.0046
```
### A two-sample bootstrap hypothesis test for difference of means
- We now want to test the hypothesis that Frog A and Frog B have the same mean impact force, but not necessarily the same distribution, which is also impossible with a permutation test.
- To do the two-sample bootstrap test, we shift both arrays to have the same mean, since we are simulating the hypothesis that their means are, in fact, equal. We then draw bootstrap samples out of the shifted arrays and compute the difference in means. This constitutes a bootstrap replicate, and we generate many of them. The p-value is the fraction of replicates with a difference in means greater than or equal to what was observed.
- The objects forces_concat and empirical_diff_means are already in your namespace.
```
<class 'numpy.ndarray'> forces_concat
[1.612 0.605 0.327 0.946 0.541 1.539 0.529 0.628 1.453 0.297 0.703 0.269
 0.751 0.245 1.182 0.515 0.435 0.383 0.457 0.73  0.172 0.142 0.037 0.453
 0.355 0.022 0.502 0.273 0.72  0.582 0.198 0.198 0.597 0.516 0.815 0.402
 0.605 0.711 0.614 0.468]
```
```
<class 'numpy.float64'> empirical_diff_means
0.28825000000000006
```
```
<class 'numpy.ndarray'> force_a
[1.612 0.605 0.327 0.946 0.541 1.539 0.529 0.628 1.453 0.297 0.703 0.269
 0.751 0.245 1.182 0.515 0.435 0.383 0.457 0.73 ]
```
```
<class 'numpy.ndarray'> force_b
[0.172 0.142 0.037 0.453 0.355 0.022 0.502 0.273 0.72  0.582 0.198 0.198
 0.597 0.516 0.815 0.402 0.605 0.711 0.614 0.468]
```
#### Question 1
- Compute the mean of all forces (from forces_concat) using np.mean().
- Generate shifted data sets for both force_a and force_b such that the mean of each is the mean of the concatenated array of impact forces.
- Generate 10,000 bootstrap replicates of the mean each for the two shifted arrays.
- Compute the bootstrap replicates of the difference of means by subtracting the replicates of the shifted impact force of Frog B from those of Frog A.
- Compute and print the p-value from your bootstrap replicates.
```python
# Compute mean of all forces: mean_force
mean_force = np.mean(forces_concat)

# Generate shifted arrays
force_a_shifted = force_a - np.mean(force_a) + mean_force
force_b_shifted = force_b - np.mean(force_b) + mean_force

# Compute 10,000 bootstrap replicates from shifted arrays
bs_replicates_a = draw_bs_reps(force_a_shifted, np.mean, size=10000)
bs_replicates_b = draw_bs_reps(force_b_shifted, np.mean, size=10000)

# Get replicates of difference of means: bs_replicates
bs_replicates = bs_replicates_a - bs_replicates_b

# Compute and print p-value: p
p = np.sum(bs_replicates >= empirical_diff_means) / len(bs_replicates)
print('p-value =', p)
```
```
p-value = 0.0045
```

## `Chapter 4` Hypothesis test examples

### Video: A/B testing
### The vote for the Civil Rights Act in 1964
- The Civil Rights Act of 1964 was one of the most important pieces of legislation ever passed in the USA. Excluding "present" and "abstain" votes, 153 House Democrats and 136 Republicans voted yea. However, 91 Democrats and 35 Republicans voted nay. Did party affiliation make a difference in the vote?
- To answer this question, you will evaluate the hypothesis that the party of a House member has no bearing on his or her vote. You will use the fraction of Democrats voting in favor as your test statistic and evaluate the probability of observing a fraction of Democrats voting in favor at least as small as the observed fraction of 153/244. (That's right, at least as small as. In 1964, it was the Democrats who were less progressive on civil rights issues.) To do this, permute the party labels of the House voters and then arbitrarily divide them into "Democrats" and "Republicans" and compute the fraction of Democrats voting yea.
#### Question 1
- Construct Boolean arrays, dems and reps that contain the votes of the respective parties; e.g., dems has 153 True entries and 91 False entries.
- Write a function, frac_yea_dems(dems, reps) that returns the fraction of Democrats that voted yea. The first input is an array of Booleans, Two inputs are required to use your draw_perm_reps() function, but the second is not used.
- Use your draw_perm_reps() function to draw 10,000 permutation replicates of the fraction of Democrat yea votes.
- Compute and print the p-value.
```python
# Construct arrays of data: dems, reps
dems = np.array([True] * 153 + [False] * 91)
reps = np.array([True] * 136 + [False] * 35)

def frac_yea_dems(dems, reps):
    """Compute fraction of Democrat yea votes."""
    frac = np.sum(dems) / len(dems)
    return frac

# Acquire permutation samples: perm_replicates
perm_replicates = draw_perm_reps(dems, reps, frac_yea_dems, 10000)

# Compute and print p-value: p
p = np.sum(perm_replicates <= 153/244) / len(perm_replicates)
print('p-value =', p)
```
```
p-value = 0.0002
```
#### What is equivalent?
- You have experience matching stories to probability distributions. Similarly, you use the same procedure for two different A/B tests if their stories match. In the Civil Rights Act example you just did, you performed an A/B test on voting data, which has a Yes/No type of outcome for each subject (in that case, a voter). Which of the following situations involving testing by a web-based company has an equivalent set up for an A/B test as the one you just did with the Civil Rights Act of 1964?
```
You measure how much time each customer spends on your website before and after an advertising campaign.
You measure the number of people who click on an ad on your company's website before and after changing its color.
You measure how many clicks each person has on your company's website before and after changing the header layout.
```
```
You measure the number of people who click on an ad on your company's website before and after changing its color.
```
### A time-on-website analog
- It turns out that you already did a hypothesis test analogous to an A/B test where you are interested in how much time is spent on the website before and after an ad campaign. The frog tongue force (a continuous quantity like time on the website) is an analog. "Before" = Frog A and "after" = Frog B. Let's practice this again with something that actually is a before/after scenario.
- We return to the no-hitter data set. In 1920, Major League Baseball implemented important rule changes that ended the so-called dead ball era. Importantly, the pitcher was no longer allowed to spit on or scuff the ball, an activity that greatly favors pitchers. In this problem you will perform an A/B test to determine if these rule changes resulted in a slower rate of no-hitters (i.e., longer average time between no-hitters) using the difference in mean inter-no-hitter time as your test statistic. The inter-no-hitter times for the respective eras are stored in the arrays nht_dead and nht_live, where "nht" is meant to stand for "no-hitter time."
- Since you will be using your draw_perm_reps() function in this exercise, it may be useful to remind yourself of its call signature: draw_perm_reps(d1, d2, func, size=1) or even referring back to the chapter 3 exercise in which you defined it.
```
<class 'numpy.ndarray'> nht_dead
[  -1  894   10  130    1  934   29    6  485  254  372   81  191  355
  180  286   47  269  361  173  246  492  462 1319   58  297   31 2970
  640  237  434  570   77  271  563 3365   89    0  379  221  479  367
  628  843 1613 1101  215  684  814  278  324  161  219  545  715  966
  624   29  450  107   20   91 1325  124 1468  104 1309  429   62 1878
 1104  123  251   93  188  983  166   96  702   23  524   26  299   59
   39   12    2  308 1114  813  887]
```
```
<class 'numpy.ndarray'> nht_live
[ 645 2088   42 2090   11  886 1665 1084 2900 2432  750 4021 1070 1765
 1322   26  548 1525   77 2181 2752  127 2147  211   41 1575  151  479
  697  557 2267  542  392   73  603  233  255  528  397 1529 1023 1194
  462  583   37  943  996  480 1497  717  224  219 1531  498   44  288
  267  600   52  269 1086  386  176 2199  216   54  675 1243  463  650
  171  327  110  774  509    8  197  136   12 1124   64  380  811  232
  192  731  715  226  605  539 1491  323  240  179  702  156   82 1397
  354  778  603 1001  385  986  203  149  576  445  180 1403  252  675
 1351 2983 1568   45  899 3260 1025   31  100 2055 4043   79  238 3931
 2351  595  110  215    0  563  206  660  242  577  179  157  192  192
 1848  792 1693   55  388  225 1134 1172 1555   31 1582 1044  378 1687
 2915  280  765 2819  511 1521  745 2491  580 2072 6450  578  745 1075
 1103 1549 1520  138 1202  296  277  351  391  950  459   62 1056 1128
  139  420   87   71  814  603 1349  162 1027  783  326  101  876  381
  905  156  419  239  119  129  467]
```
#### Question 1
- Compute the observed difference in mean inter-nohitter time using diff_of_means().
- Generate 10,000 permutation replicates of the difference of means using draw_perm_reps().
- Compute and print the p-value.
```python
# Compute the observed difference in mean inter-no-hitter times: nht_diff_obs
nht_diff_obs = diff_of_means(nht_dead, nht_live)

# Acquire 10,000 permutation replicates of difference in mean no-hitter time: perm_replicates
perm_replicates = draw_perm_reps(nht_dead, nht_live,
                                 diff_of_means, size=10000)

# Compute and print the p-value: p
p = np.sum(perm_replicates <= nht_diff_obs) / len(perm_replicates)
print('p-val =', p)
```
```
p-val = 0.0001
```
#### What should you have done first?
- That was a nice hypothesis test you just did to check out whether the rule changes in 1920 changed the rate of no-hitters. But what should you have done with the data first?
```
Performed EDA, perhaps plotting the ECDFs of inter-no-hitter times in the dead ball and live ball eras.
Nothing. The hypothesis test was only a few lines of code.
```
```
Performed EDA, perhaps plotting the ECDFs of inter-no-hitter times in the dead ball and live ball eras.
```

### Video: Test of correlation
#### Simulating a null hypothesis concerning correlation
- The observed correlation between female illiteracy and fertility in the data set of 162 countries may just be by chance; the fertility of a given country may actually be totally independent of its illiteracy. You will test this null hypothesis in the next exercise.
- To do the test, you need to simulate the data assuming the null hypothesis is true. Of the following choices, which is the best way to do it?
```
Choose 162 random numbers to represent the illiteracy rate and 162 random numbers to represent the corresponding fertility rate.
Do a pairs bootstrap: Sample pairs of observed data with replacement to generate a new set of (illiteracy, fertility) data.
Do a bootstrap sampling in which you sample 162 illiteracy values with replacement and then 162 fertility values with replacement.
Do a permutation test: Permute the illiteracy values but leave the fertility values fixed to generate a new set of (illiteracy, fertility) data.
Do a permutation test: Permute both the illiteracy and fertility values to generate a new set of (illiteracy, fertility data).
```
```
Do a permutation test: Permute the illiteracy values but leave the fertility values fixed to generate a new set of (illiteracy, fertility) data.
```
### Hypothesis test on Pearson correlation
- The observed correlation between female illiteracy and fertility may just be by chance; the fertility of a given country may actually be totally independent of its illiteracy. You will test this hypothesis. To do so, permute the illiteracy values but leave the fertility values fixed. This simulates the hypothesis that they are totally independent of each other. For each permutation, compute the Pearson correlation coefficient and assess how many of your permutation replicates have a Pearson correlation coefficient greater than the observed one.
- The function pearson_r() that you wrote in the prequel to this course for computing the Pearson correlation coefficient is already in your name space.
```
<class 'numpy.ndarray'> illiteracy
[ 9.5 49.2  1.  11.2  9.8 60.  50.2 51.2  0.6  1.   8.5  6.1  9.8  1.
 42.2 77.2 18.7 22.8  8.5 43.9  1.   1.   1.5 10.8 11.9  3.4  0.4  3.1
  6.6 33.7 40.4  2.3 17.2  0.7 36.1  1.  33.2 55.9 30.8 87.4 15.4 54.6
  5.1  1.1 10.2 19.8  0.  40.7 57.2 59.9  3.1 55.7 22.8 10.9 34.7 32.2
 43.   1.3  1.   0.5 78.4 34.2 84.9 29.1 31.3 18.3 81.8 39.  11.2 67.
  4.1  0.2 78.1  1.   7.1  1.  29.   1.1 11.7 73.6 33.9 14.   0.3  1.
  0.8 71.9 40.1  1.   2.1  3.8 16.5  4.1  0.5 44.4 46.3 18.7  6.5 36.8
 18.6 11.1 22.1 71.1  1.   0.   0.9  0.7 45.5  8.4  0.   3.8  8.5  2.
  1.  58.9  0.3  1.  14.  47.   4.1  2.2  7.2  0.3  1.5 50.5  1.3  0.6
 19.1  6.9  9.2  2.2  0.2 12.3  4.9  4.6  0.3 16.5 65.7 63.5 16.8  0.2
  1.8  9.6 15.2 14.4  3.3 10.6 61.3 10.9 32.2  9.3 11.6 20.7  6.5  6.7
  3.5  1.   1.6 20.5  1.5 16.7  2.   0.9]
```
```
<class 'numpy.ndarray'> fertility
[1.769 2.682 2.077 2.132 1.827 3.872 2.288 5.173 1.393 1.262 2.156 3.026
 2.033 1.324 2.816 5.211 2.1   1.781 1.822 5.908 1.881 1.852 1.39  2.281
 2.505 1.224 1.361 1.468 2.404 5.52  4.058 2.223 4.859 1.267 2.342 1.579
 6.254 2.334 3.961 6.505 2.53  2.823 2.498 2.248 2.508 3.04  1.854 4.22
 5.1   4.967 1.325 4.514 3.173 2.308 4.62  4.541 5.637 1.926 1.747 2.294
 5.841 5.455 7.069 2.859 4.018 2.513 5.405 5.737 3.363 4.89  1.385 1.505
 6.081 1.784 1.378 1.45  1.841 1.37  2.612 5.329 5.33  3.371 1.281 1.871
 2.153 5.378 4.45  1.46  1.436 1.612 3.19  2.752 3.35  4.01  4.166 2.642
 2.977 3.415 2.295 3.019 2.683 5.165 1.849 1.836 2.518 2.43  4.528 1.263
 1.885 1.943 1.899 1.442 1.953 4.697 1.582 2.025 1.841 5.011 1.212 1.502
 2.516 1.367 2.089 4.388 1.854 1.748 2.978 2.152 2.362 1.988 1.426 3.29
 3.264 1.436 1.393 2.822 4.969 5.659 3.24  1.693 1.647 2.36  1.792 3.45
 1.516 2.233 2.563 5.283 3.885 0.966 2.373 2.663 1.251 2.052 3.371 2.093
 2.    3.883 3.852 3.718 1.732 3.928]
```
#### Question 1
- Compute the observed Pearson correlation between illiteracy and fertility.
- Initialize an array to store your permutation replicates.
- Write a for loop to draw 10,000 replicates:
- Permute the illiteracy measurements using np.random.permutation().
- Compute the Pearson correlation between the permuted illiteracy array, illiteracy_permuted, and fertility.
- Compute and print the p-value from the replicates.
```python
# Compute observed correlation: r_obs
r_obs = pearson_r(illiteracy, fertility)

# Initialize permutation replicates: perm_replicates
perm_replicates = np.empty(10000)

# Draw replicates
for i in range(10000):
    # Permute illiteracy measurments: illiteracy_permuted
    illiteracy_permuted = np.random.permutation(illiteracy)

    # Compute Pearson correlation
    perm_replicates[i] = pearson_r(illiteracy_permuted, fertility)

# Compute p-value: p
p = np.sum(perm_replicates >= r_obs) / len(perm_replicates)
print('p-val =', p)
```
```
p-val = 0.0
```
### Do neonicotinoid insecticides have unintended consequences?
- As a final exercise in hypothesis testing before we put everything together in our case study in the next chapter, you will investigate the effects of neonicotinoid insecticides on bee reproduction. These insecticides are very widely used in the United States to combat aphids and other pests that damage plants.
- In a recent study, Straub, et al. (Proc. Roy. Soc. B, 2016) investigated the effects of neonicotinoids on the sperm of pollinating bees. In this and the next exercise, you will study how the pesticide treatment affected the count of live sperm per half milliliter of semen.
- First, we will do EDA, as usual. Plot ECDFs of the alive sperm count for untreated bees (stored in the Numpy array control) and bees treated with pesticide (stored in the Numpy array treated).
```
<class 'numpy.ndarray'> control
[ 4.159234  4.408002  0.172812  3.498278  3.104912  5.164174  6.615262
  4.633066  0.170408  2.65      0.0875    1.997148  6.92668   4.574932
  3.896466  5.209814  3.70625   0.        4.62545   3.01444   0.732652
  0.4       6.518382  5.225     6.218742  6.840358  1.211308  0.368252
  3.59937   4.212158  6.052364  2.115532  6.60413   5.26074   6.05695
  6.481172  3.171522  3.057228  0.218808  5.215112  4.465168  2.28909
  3.732572  2.17087   1.834326  6.074862  5.841978  8.524892  4.698492
  2.965624  2.324206  3.409412  4.830726  0.1       0.        4.101432
  3.478162  1.009688  4.999296  4.32196   0.299592  3.606032  7.54026
  4.284024  0.057494  6.036668  2.924084  4.150144  1.256926  4.666502
  4.806594  2.52478   2.027654  2.52283   4.735598  2.033236  0.
  6.177294  2.601834  3.544408  3.6045    5.520346  4.80698   3.002478
  3.559816  7.075844 10.        0.139772  6.17171   3.201232  8.459546
  0.17857   7.088276  5.496662  5.415086  1.932282  3.02838   7.47996
  1.86259   7.838498  2.242718  3.292958  6.363644  4.386898  8.47533
  4.156304  1.463956  4.533628  5.573922  1.29454   7.547504  3.92466
  5.820258  4.118522  4.125     2.286698  0.591882  1.273124  0.
  0.        0.       12.22502   7.601604  5.56798   1.679914  8.77096
  5.823942  0.258374  0.        5.899236  5.486354  2.053148  3.25541
  2.72564   3.364066  2.43427   5.282548  3.963666  0.24851   0.347916
  4.046862  5.461436  4.066104  0.        0.065   ]
```
```
<class 'numpy.ndarray'> treated
[1.342686 1.058476 3.793784 0.40428  4.528388 2.142966 3.937742 0.1375
 6.919164 0.       3.597812 5.196538 2.78955  2.3229   1.090636 5.323916
 1.021618 0.931836 2.78     0.412202 1.180934 2.8674   0.       0.064354
 3.008348 0.876634 0.       4.971712 7.280658 4.79732  2.084956 3.251514
 1.9405   1.566192 0.58894  5.219658 0.977976 3.124584 1.297564 1.433328
 4.24337  0.880964 2.376566 3.763658 1.918426 3.74     3.841726 4.69964
 4.386876 0.       1.127432 1.845452 0.690314 4.185602 2.284732 7.237594
 2.185148 2.799124 3.43218  0.63354  1.142496 0.586    2.372858 1.80032
 3.329306 4.028804 3.474156 7.508752 2.032824 1.336556 1.906496 1.396046
 2.488104 4.759114 1.07853  3.19927  3.814252 4.275962 2.817056 0.552198
 3.27194  5.11525  2.064628 0.       3.34101  6.177322 0.       3.66415
 2.352582 1.531696]
```
#### Question 1
- Use your ecdf() function to generate x,y values from the control and treated arrays for plotting the ECDFs.
- Plot the ECDFs on the same plot.
- The margins have been set for you, along with the legend and axis labels. Hit 'Submit Answer' to see the result!
```python
# Compute x,y values for ECDFs
x_control, y_control = ecdf(control)
x_treated, y_treated = ecdf(treated)

# Plot the ECDFs
plt.plot(x_control, y_control, marker='.', linestyle='none')
plt.plot(x_treated, y_treated, marker='.', linestyle='none')

# Set the margins
plt.margins(0.02)

# Add a legend
plt.legend(('control', 'treated'), loc='lower right')

# Label axes and show plot
plt.xlabel('millions of alive sperm per mL')
plt.ylabel('ECDF')
plt.show()
```
### Bootstrap hypothesis test on bee sperm counts
- Now, you will test the following hypothesis: On average, male bees treated with neonicotinoid insecticide have the same number of active sperm per milliliter of semen than do untreated male bees. You will use the difference of means as your test statistic.
- For your reference, the call signature for the draw_bs_reps() function you wrote in chapter 2 is draw_bs_reps(data, func, size=1).
#### Question 1
- Compute the mean alive sperm count of control minus that of treated.
- Compute the mean of all alive sperm counts. To do this, first concatenate control and treated and take the mean of the concatenated array.
- Generate shifted data sets for both control and treated such that the shifted data sets have the same mean. This has already been done for you.
- Generate 10,000 bootstrap replicates of the mean each for the two shifted arrays. Use your draw_bs_reps() function.
- Compute the bootstrap replicates of the difference of means.
- The code to compute and print the p-value has been written for you. Hit 'Submit Answer' to see the result!
```python
# Compute the difference in mean sperm count: diff_means
diff_means = np.mean(control) - np.mean(treated)

# Compute mean of pooled data: mean_count
mean_count = np.mean(np.concatenate((control, treated)))

# Generate shifted data sets
control_shifted = control - np.mean(control) + mean_count
treated_shifted = treated - np.mean(treated) + mean_count

# Generate bootstrap replicates
bs_reps_control = draw_bs_reps(control_shifted,
                               np.mean, size=10000)
bs_reps_treated = draw_bs_reps(treated_shifted,
                               np.mean, size=10000)

# Get replicates of difference of means: bs_replicates
bs_replicates = bs_reps_control - bs_reps_treated

# Compute and print p-value: p
p = np.sum(bs_replicates >= np.mean(control) - np.mean(treated)) \
            / len(bs_replicates)
print('p-value =', p)
```
```
p-value = 0.0
```

## `Chapter 5` Putting it all together a case study

### Video: Finch beaks and the need for statistics
### EDA of beak depths of Darwin's finches
- For your first foray into the Darwin finch data, you will study how the beak depth (the distance, top to bottom, of a closed beak) of the finch species Geospiza scandens has changed over time. The Grants have noticed some changes of beak geometry depending on the types of seeds available on the island, and they also noticed that there was some interbreeding with another major species on Daphne Major, Geospiza fortis. These effects can lead to changes in the species over time.
- In the next few problems, you will look at the beak depth of G. scandens on Daphne Major in 1975 and in 2012. To start with, let's plot all of the beak depth measurements in 1975 and 2012 in a bee swarm plot.
- The data are stored in a pandas DataFrame called df with columns 'year' and 'beak_depth'. The units of beak depth are millimeters (mm).
#### Data File (df.csv)
#### Question 1
- Create the beeswarm plot.
- Label the axes.
- Show the plot.
```python
# Create bee swarm plot
_ = sns.swarmplot(data=df, x='year', y='beak_depth')

# Label the axes
_ = plt.xlabel('year')
_ = plt.ylabel('beak depth (mm)')

# Show the plot
plt.show()
```
### ECDFs of beak depths
- While bee swarm plots are useful, we found that ECDFs are often even better when doing EDA. Plot the ECDFs for the 1975 and 2012 beak depth measurements on the same plot.
- For your convenience, the beak depths for the respective years has been stored in the NumPy arrays bd_1975 and bd_2012.
```
<class 'numpy.ndarray'> bd_2012
[ 9.4   8.9   9.5  11.    8.7   8.4   9.1   8.7  10.2   9.6   8.85  8.8
  9.5   9.2   9.    9.8   9.3   9.   10.2   7.7   9.    9.5   9.4   8.
  8.9   9.4   9.5   8.   10.    8.95  8.2   8.8   9.2   9.4   9.5   8.1
  9.5   8.4   9.3   9.3   9.6   9.2  10.    8.9  10.5   8.9   8.6   8.8
  9.15  9.5   9.1  10.2   8.4  10.   10.2   9.3  10.8   8.3   7.8   9.8
  7.9   8.9   7.7   8.9   9.4   9.4   8.5   8.5   9.6  10.2   8.8   9.5
  9.3   9.    9.2   8.7   9.    9.1   8.7   9.4   9.8   8.6  10.6   9.
  9.5   8.1   9.3   9.6   8.5   8.2   8.    9.5   9.7   9.9   9.1   9.5
  9.8   8.4   8.3   9.6   9.4  10.    8.9   9.1   9.8   9.3   9.9   8.9
  8.5  10.6   9.3   8.9   8.9   9.7   9.8  10.5   8.4  10.    9.    8.7
  8.8   8.4   9.3   9.8   8.9   9.8   9.1 ]
```
```
<class 'numpy.ndarray'> bd_1975
[ 8.4   8.8   8.4   8.    7.9   8.9   8.6   8.5   8.9   9.1   8.6   9.8
  8.2   9.    9.7   8.6   8.2   9.    8.4   8.6   8.9   9.1   8.3   8.7
  9.6   8.5   9.1   9.    9.2   9.9   8.6   9.2   8.4   8.9   8.5  10.4
  9.6   9.1   9.3   9.3   8.8   8.3   8.8   9.1  10.1   8.9   9.2   8.5
 10.2  10.1   9.2   9.7   9.1   8.5   8.2   9.    9.3   8.    9.1   8.1
  8.3   8.7   8.8   8.6   8.7   8.    8.8   9.    9.1   9.74  9.1   9.8
 10.4   8.3   9.44  9.04  9.    9.05  9.65  9.45  8.65  9.45  9.45  9.05
  8.75  9.45  8.35]
```
#### Question 1
- Compute the ECDF for the 1975 and 2012 data.
- Plot the two ECDFs.
- Set a 2% margin and add axis labels and a legend to the plot.
- Hit 'Submit Answer' to view the plot!
```python
# Compute ECDFs
x_1975, y_1975 = ecdf(bd_1975)
x_2012, y_2012 = ecdf(bd_2012)

# Plot the ECDFs
_ = plt.plot(x_1975, y_1975, marker='.', linestyle='none')
_ = plt.plot(x_2012, y_2012, marker='.', linestyle='none')

# Set margins
plt.margins(0.02)

# Add axis labels and legend
_ = plt.xlabel('beak depth (mm)')
_ = plt.ylabel('ECDF')
_ = plt.legend(('1975', '2012'), loc='lower right')

# Show the plot
plt.show()
```
```
### Parameter estimates of beak depths
- Estimate the difference of the mean beak depth of the G. scandens samples from 1975 and 2012 and report a 95% confidence interval.
- Since in this exercise you will use the draw_bs_reps() function you wrote in chapter 2, it may be helpful to refer back to it.
```
#### Question 1
- Compute the difference of the sample means.
- Take 10,000 bootstrap replicates of the mean for the 1975 beak depths using your draw_bs_reps() function. Also get 10,000 bootstrap replicates of the mean for the 2012 beak depths.
- Subtract the 1975 replicates from the 2012 replicates to get bootstrap replicates of the difference of means.
- Use the replicates to compute the 95% confidence interval.
- Hit 'Submit Answer' to view the results!
```python
# Compute the difference of the sample means: mean_diff
mean_diff = np.mean(bd_2012) - np.mean(bd_1975)

# Get bootstrap replicates of means
bs_replicates_1975 = draw_bs_reps(bd_1975, np.mean, 10000)
bs_replicates_2012 = draw_bs_reps(bd_2012, np.mean, 10000)

# Compute samples of difference of means: bs_diff_replicates
bs_diff_replicates = bs_replicates_2012 - bs_replicates_1975

# Compute 95% confidence interval: conf_int
conf_int = np.percentile(bs_diff_replicates, [2.5, 97.5])

# Print the results
print('difference of means =', mean_diff, 'mm')
print('95% confidence interval =', conf_int, 'mm')
```
```
difference of means = 0.22622047244094645 mm
95% confidence interval = [0.05633521 0.39190544] mm
```
### Hypothesis test: Are beaks deeper in 2012?
- Your plot of the ECDF and determination of the confidence interval make it pretty clear that the beaks of G. scandens on Daphne Major have gotten deeper. But is it possible that this effect is just due to random chance? In other words, what is the probability that we would get the observed difference in mean beak depth if the means were the same?
- Be careful! The hypothesis we are testing is not that the beak depths come from the same distribution. For that we could use a permutation test. The hypothesis is that the means are equal. To perform this hypothesis test, we need to shift the two data sets so that they have the same mean and then use bootstrap sampling to compute the difference of means.
#### Question 1
- Make a concatenated array of the 1975 and 2012 beak depths and compute and store its mean.
- Shift bd_1975 and bd_2012 such that their means are equal to the one you just computed for the combined data set.
- Take 10,000 bootstrap replicates of the mean each for the 1975 and 2012 beak depths.
- Subtract the 1975 replicates from the 2012 replicates to get bootstrap replicates of the difference.
- Compute and print the p-value. The observed difference in means you computed in the last exercise is still in your namespace as mean_diff.
```python
# Compute mean of combined data set: combined_mean
combined_mean = np.mean(np.concatenate((bd_1975, bd_2012)))

# Shift the samples
bd_1975_shifted = bd_1975 - np.mean(bd_1975) + combined_mean
bd_2012_shifted = bd_2012 - np.mean(bd_2012) + combined_mean

# Get bootstrap replicates of shifted data sets
bs_replicates_1975 = draw_bs_reps(bd_1975_shifted, np.mean, 10000)
bs_replicates_2012 = draw_bs_reps(bd_2012_shifted, np.mean, 10000)

# Compute replicates of difference of means: bs_diff_replicates
bs_diff_replicates = bs_replicates_2012 - bs_replicates_1975

# Compute the p-value: p
p = np.sum(bs_diff_replicates >= mean_diff) / len(bs_diff_replicates)

# Print p-value
print('p =', p)
```
```
p = 0.0034
```

### Video: Variation in beak shapes
### EDA of beak length and depth
- The beak length data are stored as bl_1975 and bl_2012, again with units of millimeters (mm). You still have the beak depth data stored in bd_1975 and bd_2012. Make scatter plots of beak depth (y-axis) versus beak length (x-axis) for the 1975 and 2012 specimens.
```
<class 'numpy.ndarray'> bl_1975
[13.9  14.   12.9  13.5  12.9  14.6  13.   14.2  14.   14.2  13.1  15.1
 13.5  14.4  14.9  12.9  13.   14.9  14.   13.8  13.   14.75 13.7  13.8
 14.   14.6  15.2  13.5  15.1  15.   12.8  14.9  15.3  13.4  14.2  15.1
 15.1  14.   13.6  14.   14.   13.9  14.   14.9  15.6  13.8  14.4  12.8
 14.2  13.4  14.   14.8  14.2  13.5  13.4  14.6  13.5  13.7  13.9  13.1
 13.4  13.8  13.6  14.   13.5  12.8  14.   13.4  14.9  15.54 14.63 14.73
 15.73 14.83 15.94 15.14 14.23 14.15 14.35 14.95 13.95 14.05 14.55 14.05
 14.45 15.05 13.25]
```
```
<class 'numpy.ndarray'> bd_1975
[ 8.4   8.8   8.4   8.    7.9   8.9   8.6   8.5   8.9   9.1   8.6   9.8
  8.2   9.    9.7   8.6   8.2   9.    8.4   8.6   8.9   9.1   8.3   8.7
  9.6   8.5   9.1   9.    9.2   9.9   8.6   9.2   8.4   8.9   8.5  10.4
  9.6   9.1   9.3   9.3   8.8   8.3   8.8   9.1  10.1   8.9   9.2   8.5
 10.2  10.1   9.2   9.7   9.1   8.5   8.2   9.    9.3   8.    9.1   8.1
  8.3   8.7   8.8   8.6   8.7   8.    8.8   9.    9.1   9.74  9.1   9.8
 10.4   8.3   9.44  9.04  9.    9.05  9.65  9.45  8.65  9.45  9.45  9.05
  8.75  9.45  8.35]
```
```
<class 'numpy.ndarray'> bl_2012
[14.3  12.5  13.7  13.8  12.   13.   13.   13.6  12.8  13.6  12.95 13.1
 13.4  13.9  12.3  14.   12.5  12.3  13.9  13.1  12.5  13.9  13.7  12.
 14.4  13.5  13.8  13.   14.9  12.5  12.3  12.8  13.4  13.8  13.5  13.5
 13.4  12.3  14.35 13.2  13.8  14.6  14.3  13.8  13.6  12.9  13.   13.5
 13.2  13.7  13.1  13.2  12.6  13.   13.9  13.2  15.   13.37 11.4  13.8
 13.   13.   13.1  12.8  13.3  13.5  12.4  13.1  14.   13.5  11.8  13.7
 13.2  12.2  13.   13.1  14.7  13.7  13.5  13.3  14.1  12.5  13.7  14.6
 14.1  12.9  13.9  13.4  13.   12.7  12.1  14.   14.9  13.9  12.9  14.6
 14.   13.   12.7  14.   14.1  14.1  13.   13.5  13.4  13.9  13.1  12.9
 14.   14.   14.1  14.7  13.4  13.8  13.4  13.8  12.4  14.1  12.9  13.9
 14.3  13.2  14.2  13.   14.6  13.1  15.2 ]
```
```
<class 'numpy.ndarray'> bd_2012
[ 9.4   8.9   9.5  11.    8.7   8.4   9.1   8.7  10.2   9.6   8.85  8.8
  9.5   9.2   9.    9.8   9.3   9.   10.2   7.7   9.    9.5   9.4   8.
  8.9   9.4   9.5   8.   10.    8.95  8.2   8.8   9.2   9.4   9.5   8.1
  9.5   8.4   9.3   9.3   9.6   9.2  10.    8.9  10.5   8.9   8.6   8.8
  9.15  9.5   9.1  10.2   8.4  10.   10.2   9.3  10.8   8.3   7.8   9.8
  7.9   8.9   7.7   8.9   9.4   9.4   8.5   8.5   9.6  10.2   8.8   9.5
  9.3   9.    9.2   8.7   9.    9.1   8.7   9.4   9.8   8.6  10.6   9.
  9.5   8.1   9.3   9.6   8.5   8.2   8.    9.5   9.7   9.9   9.1   9.5
  9.8   8.4   8.3   9.6   9.4  10.    8.9   9.1   9.8   9.3   9.9   8.9
  8.5  10.6   9.3   8.9   8.9   9.7   9.8  10.5   8.4  10.    9.    8.7
  8.8   8.4   9.3   9.8   8.9   9.8   9.1 ]
```
#### Question 1
- Make a scatter plot of the 1975 data. Use the color='blue' keyword argument. Also use an alpha=0.5 keyword argument to have transparency in case data points overlap.
- Do the same for the 2012 data, but use the color='red' keyword argument.
- Add a legend and label the axes.
- Show your plot.
```python
# Make scatter plot of 1975 data
_ = plt.plot(bl_1975, bd_1975, marker='.',
             linestyle='None', color='blue', alpha=0.5)

# Make scatter plot of 2012 data
_ = plt.plot(bl_2012, bd_2012, marker='.',
             linestyle='None', color='red', alpha=0.5)

# Label axes and make legend
_ = plt.xlabel('beak length (mm)')
_ = plt.ylabel('beak depth (mm)')
_ = plt.legend(('1975', '2012'), loc='upper left')

# Show the plot
plt.show()
```
### Linear regressions
- Perform a linear regression for both the 1975 and 2012 data. Then, perform pairs bootstrap estimates for the regression parameters. Report 95% confidence intervals on the slope and intercept of the regression line.
- You will use the draw_bs_pairs_linreg() function you wrote back in chapter 2.
- As a reminder, its call signature is draw_bs_pairs_linreg(x, y, size=1), and it returns bs_slope_reps and bs_intercept_reps. The beak length data are stored as bl_1975 and bl_2012, and the beak depth data is stored in bd_1975 and bd_2012.
#### Question 1
- Compute the slope and intercept for both the 1975 and 2012 data sets.
- Obtain 1000 pairs bootstrap samples for the linear regressions using your draw_bs_pairs_linreg() function.
- Compute 95% confidence intervals for the slopes and the intercepts.
```python
# Compute the linear regressions
slope_1975, intercept_1975 = np.polyfit(bl_1975, bd_1975, 1)
slope_2012, intercept_2012 = np.polyfit(bl_2012, bd_2012, 1)

# Perform pairs bootstrap for the linear regressions
bs_slope_reps_1975, bs_intercept_reps_1975 = \
        draw_bs_pairs_linreg(bl_1975, bd_1975, 1000)
bs_slope_reps_2012, bs_intercept_reps_2012 = \
        draw_bs_pairs_linreg(bl_2012, bd_2012, 1000)

# Compute confidence intervals of slopes
slope_conf_int_1975 = np.percentile(bs_slope_reps_1975, [2.5, 97.5])
slope_conf_int_2012 = np.percentile(bs_slope_reps_2012, [2.5, 97.5])
intercept_conf_int_1975 = np.percentile(
                            bs_intercept_reps_1975, [2.5, 97.5])
intercept_conf_int_2012 = np.percentile(
                            bs_intercept_reps_2012, [2.5, 97.5])

# Print the results
print('1975: slope =', slope_1975,
      'conf int =', slope_conf_int_1975)
print('1975: intercept =', intercept_1975,
      'conf int =', intercept_conf_int_1975)
print('2012: slope =', slope_2012,
      'conf int =', slope_conf_int_2012)
print('2012: intercept =', intercept_2012,
      'conf int =', intercept_conf_int_2012)
```
```
1975: slope = 0.4652051691605937 conf int = [0.33851226 0.59306491]
1975: intercept = 2.3908752365842263 conf int = [0.64892945 4.18037063]
2012: slope = 0.462630358835313 conf int = [0.33137479 0.60695527]
2012: intercept = 2.977247498236019 conf int = [1.06792753 4.70599387]
```
### Displaying the linear regression results
- Now, you will display your linear regression results on the scatter plot, the code for which is already pre-written for you from your previous exercise. To do this, take the first 100 bootstrap samples (stored in bs_slope_reps_1975, bs_intercept_reps_1975, bs_slope_reps_2012, and bs_intercept_reps_2012) and plot the lines with alpha=0.2 and linewidth=0.5 keyword arguments to plt.plot().
#### Question 1
- Generate the x-values for the bootstrap lines using np.array(). They should consist of 10 mm and 17 mm.
- Write a for loop to plot 100 of the bootstrap lines for the 1975 and 2012 data sets. The lines for the 1975 data set should be 'blue' and those for the 2012 data set should be 'red'.
- Hit 'Submit Answer' to view the plot!
```python
# Make scatter plot of 1975 data
_ = plt.plot(bl_1975, bd_1975, marker='.',
             linestyle='none', color='blue', alpha=0.5)

# Make scatter plot of 2012 data
_ = plt.plot(bl_2012, bd_2012, marker='.',
             linestyle='none', color='red', alpha=0.5)

# Label axes and make legend
_ = plt.xlabel('beak length (mm)')
_ = plt.ylabel('beak depth (mm)')
_ = plt.legend(('1975', '2012'), loc='upper left')

# Generate x-values for bootstrap lines: x
x = np.array([10, 17])

# Plot the bootstrap lines
for i in range(100):
    plt.plot(x, bs_slope_reps_1975[i] * x + bs_intercept_reps_1975[i],
             linewidth=0.5, alpha=0.2, color='blue')
    plt.plot(x, bs_slope_reps_2012[i] * x + bs_intercept_reps_2012[i],
             linewidth=0.5, alpha=0.2, color='red')

# Draw the plot again
plt.show()
```
### Beak length to depth ratio
- The linear regressions showed interesting information about the beak geometry. The slope was the same in 1975 and 2012, suggesting that for every millimeter gained in beak length, the birds gained about half a millimeter in depth in both years. However, if we are interested in the shape of the beak, we want to compare the ratio of beak length to beak depth. Let's make that comparison.
- Remember, the data are stored in bd_1975, bd_2012, bl_1975, and bl_2012.
#### Question 1
- Make arrays of the beak length to depth ratio of each bird for 1975 and for 2012.
- Compute the mean of the length to depth ratio for 1975 and for 2012.
- Generate 10,000 bootstrap replicates each for the mean ratio for 1975 and 2012 using your draw_bs_reps() function.
- Get a 99% bootstrap confidence interval for the length to depth ratio for 1975 and 2012.
- Print the results.
```python
# Compute length-to-depth ratios
ratio_1975 = bl_1975 / bd_1975
ratio_2012 = bl_2012 / bd_2012

# Compute means
mean_ratio_1975 = np.mean(ratio_1975)
mean_ratio_2012 = np.mean(ratio_2012)

# Generate bootstrap replicates of the means
bs_replicates_1975 = draw_bs_reps(ratio_1975, np.mean, size=10000)
bs_replicates_2012 = draw_bs_reps(ratio_2012, np.mean, size=10000)

# Compute the 99% confidence intervals
conf_int_1975 = np.percentile(bs_replicates_1975, [0.5, 99.5])
conf_int_2012 = np.percentile(bs_replicates_2012, [0.5, 99.5])

# Print the results
print('1975: mean ratio =', mean_ratio_1975,
      'conf int =', conf_int_1975)
print('2012: mean ratio =', mean_ratio_2012,
      'conf int =', conf_int_2012)
```
```
1975: mean ratio = 1.5788823771858533 conf int = [1.55668803 1.60073509]
2012: mean ratio = 1.4658342276847767 conf int = [1.44363932 1.48729149]
```
#### How different is the ratio?
- In the previous exercise, you computed the mean beak length to depth ratio with 99% confidence intervals for 1975 and for 2012. The results of that calculation are shown graphically in the plot accompanying this problem. In addition to these results, what would you say about the ratio of beak length to depth?
- <image>
```
- The mean beak length-to-depth ratio decreased by about 0.1, or 7%, from 1975 to 2012. The 99% confidence intervals are not even close to overlapping, so this is a real change. The beak shape changed.
- It is impossible to say if this is a real effect or just due to noise without computing a p-value. Let me compute the p-value and get back to you.
```
```
- The mean beak length-to-depth ratio decreased by about 0.1, or 7%, from 1975 to 2012. The 99% confidence intervals are not even close to overlapping, so this is a real change. The beak shape changed.
```

### Video: Calculation of heritability
### EDA of heritability
- The array bd_parent_scandens contains the average beak depth (in mm) of two parents of the species G. scandens. The array bd_offspring_scandens contains the average beak depth of the offspring of the respective parents. The arrays bd_parent_fortis and bd_offspring_fortis contain the same information about measurements from G. fortis birds.
- Make a scatter plot of the average offspring beak depth (y-axis) versus average parental beak depth (x-axis) for both species. Use the alpha=0.5 keyword argument to help you see overlapping points.
```
<class 'numpy.ndarray'> bd_parent_fortis
[10.1    9.55   9.4   10.25  10.125  9.7    9.05   7.4    9.     8.65
  9.625  9.9    9.55   9.05   8.35  10.1   10.1    9.9   10.225 10.
 10.55  10.45   9.2   10.2    8.95  10.05  10.2    9.5    9.925  9.95
 10.05   8.75   9.2   10.15   9.8   10.7   10.5    9.55  10.55  10.475
  8.65  10.7    9.1    9.4   10.3    9.65   9.5    9.7   10.525  9.95
 10.1    9.75  10.05   9.9   10.     9.1    9.45   9.25   9.5   10.
 10.525  9.9   10.4    8.95   9.4   10.95  10.75  10.1    8.05   9.1
  9.55   9.05  10.2   10.    10.55  10.75   8.175  9.7    8.8   10.75
  9.3    9.7    9.6    9.75   9.6   10.45  11.    10.85  10.15  10.35
 10.4    9.95   9.1   10.1    9.85   9.625  9.475  9.     9.25   9.1
  9.25   9.2    9.95   8.65   9.8    9.4    9.     8.55   8.75   9.65
  8.95   9.15   9.85  10.225  9.825 10.     9.425 10.4    9.875  8.95
  8.9    9.35  10.425 10.    10.175  9.875  9.875  9.15   9.45   9.025
  9.7    9.7   10.05  10.3    9.6   10.     9.8   10.05   8.75  10.55
  9.7   10.     9.85   9.8    9.175  9.65   9.55   9.9   11.55  11.3
 10.4   10.8    9.8   10.45  10.    10.75   9.35  10.75   9.175  9.65
  8.8   10.55  10.675  9.95   9.55   8.825  9.7    9.85   9.8    9.55
  9.275 10.325  9.15   9.35   9.15   9.65  10.575  9.975  9.55   9.2
  9.925  9.2    9.3    8.775  9.325  9.175  9.325  8.975  9.7    9.5
 10.225 10.025  8.2    8.2    9.55   9.05   9.6    9.6   10.15   9.875
 10.485 11.485 10.985  9.7    9.65   9.35  10.05  10.1    9.9    8.95
  9.3    9.95   9.45   9.5    8.45   8.8    8.525  9.375 10.2    7.625
  8.375  9.25   9.4   10.55   8.9    8.8    9.     8.575  8.575  9.6
  9.375  9.6    9.95   9.6   10.2    9.85   9.625  9.025 10.375 10.25
  9.3    9.5    9.55   8.55   9.05   9.9    9.8    9.75  10.25   9.1
  9.65  10.3    8.9    9.95   9.5    9.775  9.425  7.75   7.55   9.1
  9.6    9.575  8.95   9.65   9.65   9.65   9.525  9.85   9.05   9.3
  8.9    9.45  10.     9.85   9.25  10.1    9.125  9.65   9.1    8.05
  7.4    8.85   9.075  9.     9.7    8.7    9.45   9.7    8.35   8.85
  9.7    9.45  10.3   10.    10.45   9.45   8.5    8.3   10.     9.225
  9.75   9.15   9.55   9.     9.275  9.35   8.95   9.875  8.45   8.6
  9.7    8.55   9.05   9.6    8.65   9.2    8.95   9.6    9.15   9.4
  8.95   9.95  10.55   9.7    8.85   8.8   10.     9.05   8.2    8.1
  7.25   8.3    9.15   8.6    9.5    8.05   9.425  9.3    9.8    9.3
  9.85   9.5    8.65   9.825  9.    10.45   9.1    9.55   9.05  10.
  9.35   8.375  8.3    8.8   10.1    9.5    9.75  10.1    9.575  9.425
  9.65   8.725  9.025  8.5    8.95   9.3    8.85   8.95   9.8    9.5
  8.65   9.1    9.4    8.475  9.35   7.95   9.35   8.575  9.05   8.175
  9.85   7.85   9.85  10.1    9.35   8.85   8.75   9.625  9.25   9.55
 10.325  8.55   9.675  9.15   9.     9.65   8.6    8.8    9.     9.95
  8.4    9.35  10.3    9.05   9.975  9.975  8.65   8.725  8.2    7.85
  8.775  8.5    9.4  ]
```
```
<class 'numpy.ndarray'> bd_offspring_fortis
[10.7   9.78  9.48  9.6  10.27  9.5   9.    7.46  7.65  8.63  9.81  9.4
  9.48  8.75  7.6  10.   10.09  9.74  9.64  8.49 10.15 10.28  9.2  10.01
  9.03  9.94 10.5   9.7  10.02 10.04  9.43  8.1   9.5   9.9   9.48 10.18
 10.16  9.08 10.39  9.9   8.4  10.6   8.75  9.46  9.6   9.6   9.95 10.05
 10.16 10.1   9.83  9.46  9.7   9.82 10.34  8.02  9.65  9.87  9.   11.14
  9.25  8.14 10.23  8.7   9.8  10.54 11.19  9.85  8.1   9.3   9.34  9.19
  9.52  9.36  8.8   8.6   8.    8.5   8.3  10.38  8.54  8.94 10.    9.76
  9.45  9.89 10.9   9.91  9.39  9.86  9.74  9.9   9.09  9.69 10.24  8.9
  9.67  8.93  9.3   8.67  9.15  9.23  9.59  9.03  9.58  8.97  8.57  8.47
  8.71  9.21  9.13  8.5   9.58  9.21  9.6   9.32  8.7  10.46  9.29  9.24
  9.45  9.35 10.19  9.91  9.18  9.89  9.6  10.3   9.45  8.79  9.2   8.8
  9.69 10.61  9.6   9.9   9.26 10.2   8.79  9.28  8.83  9.76 10.2   9.43
  9.4   9.9   9.5   8.95  9.98  9.72  9.86 11.1   9.14 10.49  9.75 10.35
  9.73  9.83  8.69  9.58  8.42  9.25 10.12  9.31  9.99  8.59  8.74  8.79
  9.6   9.52  8.93 10.23  9.35  9.35  9.09  9.04  9.75 10.5   9.09  9.05
  9.54  9.3   9.06  8.7   9.32  8.4   8.67  8.6   9.53  9.77  9.65  9.43
  8.35  8.26  9.5   8.6   9.57  9.14 10.79  8.91  9.93 10.7   9.3   9.93
  9.51  9.44 10.05 10.13  9.24  8.21  8.9   9.34  8.77  9.4   8.82  8.83
  8.6   9.5  10.2   8.09  9.07  9.29  9.1  10.19  9.25  8.98  9.02  8.6
  8.25  8.7   9.9   9.65  9.45  9.38 10.4   9.96  9.46  8.26 10.05  8.92
  9.5   9.43  8.97  8.44  8.92 10.3   8.4   9.37  9.91 10.    9.21  9.95
  8.84  9.82  9.5  10.29  8.4   8.31  9.29  8.86  9.4   9.62  8.62  8.3
  9.8   8.48  9.61  9.5   9.37  8.74  9.31  9.5   9.49  9.74  9.2   9.24
  9.7   9.64  9.2   7.5   7.5   8.7   8.31  9.    9.74  9.31 10.5   9.3
  8.12  9.34  9.72  9.    9.65  9.9  10.   10.1   8.    9.07  9.75  9.33
  8.11  9.36  9.74  9.9   9.23  9.7   8.2   9.35  9.49  9.34  8.87  9.03
  9.07  9.43  8.2   9.19  9.    9.2   9.06  9.81  8.89  9.4  10.45  9.64
  9.03  8.71  9.91  8.33  8.2   7.83  7.14  8.91  9.18  8.8   9.9   7.73
  9.25  8.7   9.5   9.3   9.05 10.18  8.85  9.24  9.15  9.98  8.77  9.8
  8.65 10.    8.81  8.01  7.9   9.41 10.18  9.55  9.08  8.4   9.75  8.9
  9.07  9.35  8.9   8.19  8.65  9.19  8.9   9.28 10.58  9.    9.4   8.91
  9.93 10.    9.37  7.4   9.    8.8   9.18  8.3  10.08  7.9   9.96 10.4
  9.65  8.8   8.65  9.7   9.23  9.43  9.93  8.47  9.55  9.28  8.85  8.9
  8.75  8.63  9.    9.43  8.28  9.23 10.4   9.    9.8   9.77  8.97  8.37
  7.7   7.9   9.5   8.2   8.8 ]
```
```
<class 'numpy.ndarray'> bd_parent_scandens
[ 8.3318  8.4035  8.5317  8.7202  8.7089  8.7541  8.773   8.8107  8.7919
  8.8069  8.6523  8.6146  8.6938  8.7127  8.7466  8.7504  8.7805  8.7428
  8.7164  8.8032  8.8258  8.856   8.9012  8.9125  8.8635  8.8258  8.8522
  8.8974  8.9427  8.9879  8.9615  8.9238  8.9351  9.0143  9.0558  9.0596
  8.9917  8.905   8.9314  8.9465  8.9879  8.9804  9.0219  9.052   9.0407
  9.0407  8.9955  8.9992  8.9992  9.0747  9.0747  9.5385  9.4781  9.4517
  9.3537  9.2707  9.1199  9.1689  9.1425  9.135   9.1011  9.1727  9.2217
  9.2255  9.2821  9.3235  9.3198  9.3198  9.3198  9.3273  9.3725  9.3989
  9.4253  9.4593  9.4442  9.4291  9.2632  9.2293  9.1878  9.1425  9.1275
  9.1802  9.1765  9.2481  9.2481  9.1991  9.1689  9.1765  9.2406  9.3198
  9.3235  9.1991  9.2971  9.2443  9.316   9.2934  9.3914  9.3989  9.5121
  9.6176  9.5535  9.4668  9.3725  9.3348  9.3763  9.3839  9.4216  9.4065
  9.3348  9.4442  9.4367  9.5083  9.448   9.4781  9.595   9.6101  9.5686
  9.6365  9.7119  9.8213  9.825   9.7609  9.6516  9.5988  9.546   9.6516
  9.7572  9.8854 10.0023  9.3914]
```
```
<class 'numpy.ndarray'> bd_offspring_scandens
[ 8.419   9.2468  8.1532  8.0089  8.2215  8.3734  8.5025  8.6392  8.7684
  8.8139  8.7911  8.9051  8.9203  8.8747  8.943   9.0038  8.981   9.0949
  9.2696  9.1633  9.1785  9.1937  9.2772  9.0722  8.9658  8.9658  8.5025
  8.4949  8.4949  8.5633  8.6013  8.6468  8.1532  8.3734  8.662   8.6924
  8.7456  8.8367  8.8595  8.9658  8.9582  8.8671  8.8671  8.943   9.0646
  9.1405  9.2089  9.2848  9.3759  9.4899  9.4519  8.1228  8.2595  8.3127
  8.4949  8.6013  8.4646  8.5329  8.7532  8.8823  9.0342  8.6392  8.6772
  8.6316  8.7532  8.8291  8.8975  8.9734  9.0494  9.1253  9.1253  9.1253
  9.1785  9.2848  9.4595  9.3608  9.2089  9.2544  9.3684  9.3684  9.2316
  9.1709  9.2316  9.0342  8.8899  8.8291  8.981   8.8975 10.4089 10.1886
  9.7633  9.7329  9.6114  9.5051  9.5127  9.3684  9.6266  9.5354 10.0215
 10.0215  9.6266  9.6038  9.4063  9.2316  9.338   9.262   9.262   9.4063
  9.4367  9.0342  8.943   8.9203  8.7835  8.7835  9.057   8.9354  8.8975
  8.8139  8.8671  9.0873  9.2848  9.2392  9.2924  9.4063  9.3152  9.4899
  9.5962  9.6873  9.5203  9.6646]
```
#### Question 1
- Generate scatter plots for both species. Display the data for G. fortis in blue and G. scandens in red.
- Set the axis labels, make a legend, and show the plot.
```python
# Make scatter plots
_ = plt.plot(bd_parent_fortis, bd_offspring_fortis,
             marker='.', linestyle='none', color='blue', alpha=0.5)
_ = plt.plot(bd_parent_scandens, bd_offspring_scandens,
             marker='.', linestyle='none', color='red', alpha=0.5)

# Label axes
_ = plt.xlabel('parental beak depth (mm)')
_ = plt.ylabel('offspring beak depth (mm)')

# Add legend
_ = plt.legend(('G. fortis', 'G. scandens'), loc='lower right')

# Show plot
plt.show()
```
### Correlation of offspring and parental data
- In an effort to quantify the correlation between offspring and parent beak depths, we would like to compute statistics, such as the Pearson correlation coefficient, between parents and offspring. To get confidence intervals on this, we need to do a pairs bootstrap.
- You have already written a function to do pairs bootstrap to get estimates for parameters derived from linear regression. Your task in this exercise is to make a new function with call signature draw_bs_pairs(x, y, func, size=1) that performs pairs bootstrap and computes a single statistic on pairs samples defined. The statistic of interest is computed by calling func(bs_x, bs_y). In the next exercise, you will use pearson_r for func.
#### Question 1
- Set up an array of indices to sample from. (Remember, when doing pairs bootstrap, we randomly choose indices and use those to get the pairs.)
- Initialize the array of bootstrap replicates. This should be a one-dimensional array of length size.
- Write a for loop to draw the samples.
- Randomly choose indices from the array of indices you previously set up.
- Extract x values and y values from the input array using the indices you just chose to generate a bootstrap sample.
- Use func to compute the statistic of interest from the bootstrap samples of x and y and store it in your array of bootstrap replicates.
- Return the array of bootstrap replicates.
```python
def draw_bs_pairs(x, y, func, size=1):
    """Perform pairs bootstrap for a single statistic."""

    # Set up array of indices to sample from: inds
    inds = np.arange(len(x))

    # Initialize replicates: bs_replicates
    bs_replicates = np.empty(size)

    # Generate replicates
    for i in range(size):
        bs_inds = np.random.choice(inds, len(inds))
        bs_x, bs_y = x[bs_inds], y[bs_inds]
        bs_replicates[i] = func(bs_x, bs_y)

    return bs_replicates
```
### Pearson correlation of offspring and parental data
- The Pearson correlation coefficient seems like a useful measure of how strongly the beak depth of parents are inherited by their offspring. Compute the Pearson correlation coefficient between parental and offspring beak depths for G. scandens. Do the same for G. fortis. Then, use the function you wrote in the last exercise to compute a 95% confidence interval using pairs bootstrap.
- Remember, the data are stored in bd_parent_scandens, bd_offspring_scandens, bd_parent_fortis, and bd_offspring_fortis.
#### Question 1
- Use the pearson_r() function you wrote in the prequel to this course to compute the Pearson correlation coefficient for G. scandens and G. fortis.
- Acquire 1000 pairs bootstrap replicates of the Pearson correlation coefficient using the draw_bs_pairs() function you wrote in the previous exercise for G. scandens and G. fortis.
- Compute the 95% confidence interval for both using your bootstrap replicates.
```python
# Compute the Pearson correlation coefficients
r_scandens = pearson_r(bd_parent_scandens, bd_offspring_scandens)
r_fortis = pearson_r(bd_parent_fortis, bd_offspring_fortis)

# Acquire 1000 bootstrap replicates of Pearson r
bs_replicates_scandens = draw_bs_pairs(
        bd_parent_scandens, bd_offspring_scandens, pearson_r, size=1000)
bs_replicates_fortis = draw_bs_pairs(
        bd_parent_fortis, bd_offspring_fortis, pearson_r, size=1000)

# Compute 95% confidence intervals
conf_int_scandens = np.percentile(bs_replicates_scandens, [2.5, 97.5])
conf_int_fortis = np.percentile(bs_replicates_fortis, [2.5, 97.5])

# Print results
print('G. scandens:', r_scandens, conf_int_scandens)
print('G. fortis:', r_fortis, conf_int_fortis)
```
```
G. scandens: 0.4117063629401258 [0.26564228 0.54388972]
G. fortis: 0.7283412395518487 [0.6694112  0.77840616]
```
### Measuring heritability
- Remember that the Pearson correlation coefficient is the ratio of the covariance to the geometric mean of the variances of the two data sets. This is a measure of the correlation between parents and offspring, but might not be the best estimate of heritability. If we stop and think, it makes more sense to define heritability as the ratio of the covariance between parent and offspring to the variance of the parents alone. In this exercise, you will estimate the heritability and perform a pairs bootstrap calculation to get the 95% confidence interval.
- This exercise highlights a very important point. Statistical inference (and data analysis in general) is not a plug-n-chug enterprise. You need to think carefully about the questions you are seeking to answer with your data and analyze them appropriately. If you are interested in how heritable traits are, the quantity we defined as the heritability is more apt than the off-the-shelf statistic, the Pearson correlation coefficient.
- Remember, the data are stored in bd_parent_scandens, bd_offspring_scandens, bd_parent_fortis, and bd_offspring_fortis.
#### Question 1
- Write a function heritability(parents, offspring) that computes heritability defined as the ratio of the covariance of the trait in parents and offspring divided by the variance of the trait in the parents. Hint: Remind yourself of the np.cov() function we covered in the prequel to this course.
- Use this function to compute the heritability for G. scandens and G. fortis.
- Acquire 1000 bootstrap replicates of the heritability using pairs bootstrap for G. scandens and G. fortis.
- Compute the 95% confidence interval for both using your bootstrap replicates.
- Print the results.
```python
def heritability(parents, offspring):
    """Compute the heritability from parent and offspring samples."""
    covariance_matrix = np.cov(parents, offspring)
    return covariance_matrix[0,1] / covariance_matrix[0,0]

# Compute the heritability
heritability_scandens = heritability(bd_parent_scandens,
                                     bd_offspring_scandens)
heritability_fortis = heritability(bd_parent_fortis,
                                   bd_offspring_fortis)

# Acquire 1000 bootstrap replicates of heritability
replicates_scandens = draw_bs_pairs(
        bd_parent_scandens, bd_offspring_scandens, heritability, size=1000)
replicates_fortis = draw_bs_pairs(
        bd_parent_fortis, bd_offspring_fortis, heritability, size=1000)

# Compute 95% confidence intervals
conf_int_scandens = np.percentile(replicates_scandens, [2.5, 97.5])
conf_int_fortis = np.percentile(replicates_fortis, [2.5, 97.5])

# Print results
print('G. scandens:', heritability_scandens, conf_int_scandens)
print('G. fortis:', heritability_fortis, conf_int_fortis)
```
```
G. scandens: 0.5485340868685982 [0.34395487 0.75638267]
G. fortis: 0.7229051911438159 [0.64655013 0.79688342]
```
### Is beak depth heritable at all in G. scandens?
- The heritability of beak depth in G. scandens seems low. It could be that this observed heritability was just achieved by chance and beak depth is actually not really heritable in the species. You will test that hypothesis here. To do this, you will do a pairs permutation test.
#### Question 1
- Initialize your array of replicates of heritability. We will take 10,000 pairs permutation replicates.
- Write a for loop to generate your replicates.
- Permute the bd_parent_scandens array using np.random.permutation().
- Compute the heritability between the permuted array and the bd_offspring_scandens array using the heritability() function you wrote in the last exercise. Store the result in the replicates array.
- Compute the p-value as the number of replicates that are greater than the observed heritability_scandens you computed in the last exercise.
```python
# Initialize array of replicates: perm_replicates
perm_replicates = np.empty(10000)

# Draw replicates
for i in range(10000):
    # Permute parent beak depths
    bd_parent_permuted = np.random.permutation(bd_parent_scandens)
    perm_replicates[i] = heritability(bd_parent_permuted,
                                      bd_offspring_scandens)

# Compute p-value: p
p = np.sum(perm_replicates >= heritability_scandens) / len(perm_replicates)

# Print the p-value
print('p-val =', p)
```
```
p-val = 0.0
```
