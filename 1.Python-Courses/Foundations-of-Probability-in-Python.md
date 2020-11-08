# [Foundations of Probability in Python](https://learn.datacamp.com/courses/foundations-of-probability-in-python) `10H`

## Course Description
`Probability is the study of regularities that emerge in the outcomes of random experiments. In this course, you'll learn about fundamental probability concepts like random variables (starting with the classic coin flip example) and how to calculate mean and variance, probability distributions, and conditional probability. We'll also explore two very important results in probability: the law of large numbers and the central limit theorem. Since probability is at the core of data science and machine learning, these concepts will help you understand and apply models more robustly. Chances are everywhere, and the study of probability will change the way you see the world. Let’s get random!`

## `Chapter 1` Let's start flipping coins

## Video: Let’s flip a coin in Python
### Flipping coins
- This exercise requires the bernoulli object from the scipy.stats library to simulate the two possible outcomes from a coin flip, 1 ("heads") or 0 ("tails"), and the numpy library (loaded as np) to set the random generator seed.
- You'll use the bernoulli.rvs() function to simulate coin flips using the size argument.
- You will set the random seed so you can reproduce the results for the random experiment in each exercise.
- From each experiment, you will get the values of each coin flip. You can add the coin flips to get the number of heads after flipping 10 coins using the sum() function.
#### Question 1
Import bernoulli from scipy.stats, set the seed with np.random.seed(). Simulate 1 flip, with a 35% chance of heads.
```python
# Import the bernoulli object from scipy.stats
from scipy.stats import bernoulli

# Set the random seed to reproduce the results
np.random.seed(42)

# Simulate one coin flip with 35% chance of getting heads
coin_flip = bernoulli.rvs(p=0.35, size=1)
print(coin_flip)
```
```
[0]
```
#### Question 2
Use bernoulli.rvs() and sum() to get the number of heads after 10 coin flips with 35% chance of getting heads.
```python
# Import the bernoulli object from scipy.stats
from scipy.stats import bernoulli

# Set the random seed to reproduce the results
np.random.seed(42)

# Simulate ten coin flips and get the number of heads
ten_coin_flips = bernoulli.rvs(p=0.35, size=10)
coin_flips_sum = sum(ten_coin_flips)
print(coin_flips_sum)
```
```
4
```
#### Question 3
Using bernoulli.rvs() and sum(), try to get the number of heads after 5 flips with a 50% chance of getting heads.
```python
# Import the bernoulli object from scipy.stats
from scipy.stats import bernoulli

# Set the random seed to reproduce the results
np.random.seed(42)

# Simulate ten coin flips and get the number of heads
five_coin_flips = bernoulli.rvs(p=0.5, size=5)
coin_flips_sum = sum(five_coin_flips)
print(coin_flips_sum)
```
```
3
```
### Using binom to flip even more coins
- Previously, you simulated 10 coin flips with a 35% chance of getting heads using bernoulli.rvs().
- This exercise loads the binom object from scipy.stats so you can use binom.rvs() to simulate 20 trials of 10 coin flips with a 35% chance of getting heads on each coin flip.
#### Question 1
Use the binom.rvs() function to simulate 20 trials of 10 coin flips with a 35% chance of getting heads.
```python
# Set the random seed to reproduce the results
np.random.seed(42)

# Simulate 20 trials of 10 coin flips 
draws = binom.rvs(n=10, p=0.35, size=20)
print(draws)
```
```
[3 6 4 4 2 2 1 5 4 4 1 6 5 2 2 2 3 4 3 3]
```

## Video: Probability mass and distribution functions
### Predicting the probability of defects
- Any situation with exactly two possible outcomes can be modeled with binomial random variables. For example, you could model if someone likes or dislikes a product, or if they voted or not.
- Let's model whether or not a component from a supplier comes with a defect. From the thousands of components that we got from a supplier, we are going to take a sample of 50, selected randomly. The agreed and accepted defect rate is 2%.
- We import the binom object from scipy.stats.
Recall that:
binom.pmf() calculates the probability of having exactly k heads out of n coin flips.
binom.cdf() calculates the probability of having k heads or less out of n coin flips.
binom.sf() calculates the probability of having more than k heads out of n coin flips.
#### Question 1
Let's answer a simple question before we start calculating probabilities:
What is the probability of getting more than 20 heads from a fair coin after 30 coin flips?
```
binom.pmf(k=20, n=30, p=0.5)
1 - binom.pmf(k=20, n=30, p=0.5)
binom.sf(k=20, n=30, p=0.5)
binom.cdf(k=20, n=30, p=0.5)
```
```
binom.sf(k=20, n=30, p=0.5)
```
#### Question 2
Let's get started with our model for defective components.
First, calculate the probability of getting exactly 1 defective component.
```python
# Probability of getting exactly 1 defective component
prob_one_defect = binom.pmf(k=1, n=50, p=0.02)
print(prob_one_defect)
```
```
0.37160171437461204
```
#### Question 3
Next, calculate the probability of not getting any defective components.
```python
# Probability of not getting any defective components
prob_no_defects = binom.pmf(k=0, n=50, p=0.02)
print(prob_no_defects)
```
```
0.3641696800871171
```
#### Question 4
Now calculate the probability of getting 2 or fewer defective components out of 50.
```python
# Probability of getting 2 or less defective components
prob_two_or_less_defects = binom.cdf(k=2, n=50, p=0.02)
print(prob_two_or_less_defects)
```
```
0.9215722516490308
```
### Predicting employment status
- Consider a survey about employment that contains the question "Are you employed?" It is known that 65% of respondents will answer "yes." Eight survey responses have been collected.
- We load the binom object from scipy.stats with the following code: from scipy.stats import binom
- Answer the following questions using pmf(), cdf(), and sf().
#### Question 1
Calculate the probability of getting exactly 5 yes responses.
```python
# Calculate the probability of getting exactly 5 yes responses
prob_five_yes = binom.pmf(k=5, n=8, p=0.65)
print(prob_five_yes)
```
```
0.27858577906250004
```
#### Question 2
Calculate the probability of getting 3 or fewer no responses.
```python
# Calculate the probability of getting 3 or less no responses
prob_three_or_less_no = 1-binom.cdf(k=3, n=8, p=0.65)
print(prob_three_or_less_no)
```
```
0.8939090951171875
```
#### Question 3
Calculate the probability of getting more than 3 yes responses using binom.sf().
```python
# Calculate the probability of getting more than 3 yes responses
prob_more_than_three_yes = binom.sf(k=3, n=8, p=0.65)
print(prob_more_than_three_yes)
```
```
0.8939090951171875
```
### Predicting burglary conviction rate
- There are many situations that can be modeled with only two outcomes: success or failure. This exercise presents a situation that can be modeled with a binomial distribution and gives you the opportunity to calculate probabilities using binom.pmf(), binom.cdf(), and binom.sf().
- The binom object from scipy.stats has been loaded for your convenience.
- Imagine that in your town there are many crimes, including burglaries, but only 20% of them get solved. Last week, there were 9 burglaries. Answer the following questions.
#### Question 1
What is the probability of solving exactly 4 of the 9 total burglaries?
```python
# What is the probability of solving 4 burglaries?
four_solved = binom.pmf(k=4, n=9, p=0.2)
print(four_solved)
```
```
0.06606028799999998
```
#### Question 2
What is the probability of solving more than 3 of the 9 burglaries?
```python
# What is the probability of solving more than 3 burglaries?
more_than_three_solved = binom.sf(k=3, n=9, p=0.2)
print(more_than_three_solved)
```
```
0.08564172800000006
```
#### Question 3
What is the probability of solving exactly 2 or 3 of the 9 burglaries?
```python
# What is the probability of solving 2 or 3 burglaries?
two_or_three_solved = binom.pmf(k=2, n=9, p=0.2) + binom.pmf(k=3, n=9, p=0.2)
print(two_or_three_solved)
```
```
0.47815065599999973
```
#### Question 4
What is the probability of solving 1 or fewer or more than 7 of the 9 burglaries?
```python
# What is the probability of solving 1 or fewer or more than 7 burglaries?
tail_probabilities = binom.cdf(k=1, n=9, p=0.2) + binom.sf(k=7, n=9, p=0.2)
print(tail_probabilities)
```
```
0.43622655999999993
```

### Video: Expected value, mean, and variance
#### Calculating the expected value and variance
How do you calculate the expected value and the variance from a binomial distribution with parameters n=10 and p=0.25?
```
binom.stats(n=10, p=0.25)
binom.pmf(k=5, n=10,p=0.25)
describe(binom.rvs(n=10, p=0.25, size=100)).mean
describe(binom.rvs(n=10, p=0.25, size=100)).variance
```
```
binom.stats(n=10, p=0.25)
```
### Calculating the sample mean
- Simulation involves generating samples and then measuring. In this exercise, we'll generate some samples and calculate the sample mean with the describe() method. See what you observe about the sample mean as the number of samples increases.
- We've preloaded the binom object and the describe() method from scipy.stats for you, so you can calculate some values.
#### Question 1
Generate a sample of 100 fair coin flips using .rvs() and calculate the sample mean using describe().
```python
# Sample mean from a generated sample of 100 fair coin flips
sample_of_100_flips = binom.rvs(n=1, p=0.5, size=100)
sample_mean_100_flips = describe(sample_of_100_flips).mean
print(sample_mean_100_flips)
```
```
0.47
```
#### Question 2
Generate a sample of 1,000 fair coin flips and calculate the sample mean.
```python
# Sample mean from a generated sample of 1,000 fair coin flips
sample_mean_1000_flips = describe(binom.rvs(n=1, p=0.5, size=1000)).mean
print(sample_mean_1000_flips)
```
```
0.497
```
#### Question 3
Generate a sample of 2,000 fair coin flips and calculate the sample mean.
```python
# Sample mean from a generated sample of 2,000 fair coin flips
sample_mean_2000_flips = describe(binom.rvs(n=1, p=0.5, size=2000)).mean
print(sample_mean_2000_flips)
```
```
0.5065
```
### Checking the result
- Now try generating some samples and calculating the expected value and variance yourself, then using the method provided by binom to check if the sample values match the theoretical values.
- The binom object and describe() method from scipy.stats are already loaded, so you can make the calculations.
#### Question 1
Calculate the sample mean and variance of the sample variable.
Calculate the expected value using n=10 and p=0.3, and calculate the variance using mean, and 1 - p.
Use a binom method to get the expected value and variance for 10 coin flips with p=0.3.
```python
sample = binom.rvs(n=10, p=0.3, size=2000)

# Calculate the sample mean and variance from the sample variable
sample_describe = describe(sample)

# Calculate the sample mean using the values of n and p
mean = 10*0.3

# Calculate the sample variance using the value of 1-p
variance = mean*0.7

# Calculate the sample mean and variance for 10 coin flips with p=0.3
binom_stats = binom.stats(n=10, p=0.3)

print(sample_describe.mean, sample_describe.variance, mean, variance, binom_stats)
```
```
2.99 2.1459729864932466 3.0 2.0999999999999996 (array(3.), array(2.1))
```
### Calculating the mean and variance of a sample
- Now that you're familiar with working with coin flips using the binom object and calculating the mean and variance, let's try simulating a larger number of coin flips and calculating the sample mean and variance. Comparing this with the theoretical mean and variance will allow you to check if your simulated data follows the distribution you want.
- We've preloaded the binom object and the describe() method from scipy.stats for you, as well as creating an empty list called averages to store the mean of the sample variable and a variable called variances to store the variance of the sample variable.
#### Question 1
Inside a loop, create a sample variable with 10 trials of 10 coin flips with 25% probability of getting heads.
```python
for i in range(0, 1500):
    # 10 trials of 10 coin flips with 25% probability of heads
    sample = binom.rvs(n=10, p=0.25, size=10)
    # Mean and variance of the values in the sample variable
    averages.append(describe(sample).mean)
    variances.append(describe(sample).variance)
```
#### Question 2
Using the describe() function, calculate the mean of the provided averages array.
Using the describe() function, calculate the mean of the provided variances array.
```python
for i in range(0, 1500):
	# 10 draws of 10 coin flips with 25% probability of heads
    sample = binom.rvs(n=10, p=0.25, size=10)
	# Mean and variance of the values in the sample variable
    averages.append(describe(sample).mean)
    variances.append(describe(sample).variance)
  
# Calculate the mean of the averages variable
print("Mean {}".format(describe(averages).mean))

# Calculate the mean of the variances variable
print("Variance {}".format(describe(variances).mean))
```
```
Mean 2.485066666666667
Variance 1.8856000000000004
```
#### Question 3
Using the binom.stats() function, calculate the theoretical mean and variance using 10 coin flips and a 25% probability of getting heads and compare your results from the previous exercise to the expected values for the mean and variance.
```python
for i in range(0, 1500):
	# 10 draws of 10 coin flips with 25% probability of heads
    sample = binom.rvs(n=10, p=0.25, size=10)
	# Mean and variance of the values in the sample variable
    averages.append(describe(sample).mean)
    variances.append(describe(sample).variance)
  
# Calculate the mean of the averages variable
print("Mean {}".format(describe(averages).mean))

# Calculate the mean of the variances variable
print("Variance {}".format(describe(variances).mean))

# Calculate the mean and variance
print(binom.stats(n=10, p=0.25))
```
```
Mean 2.485066666666667
Variance 1.8856000000000004
(array(2.5), array(1.875))
```
## `Chapter 2` Calculate some probabilities

### Video: Calculating probabilities of two events
#### Any overlap?
When you calculate probabilities for multiple events the most important thing to notice is the relation between the events, in particular, if there is any overlap between any two events.
What would be the formula to calculate the probability of A or B, given that A and B are not mutually exclusive?
```
P(A and B) = P(A) + P(B)
P(A or B) = P(A) - P(B) + P(A and B)
P(A or B) = P(A)P(B) - P(A and B)
P(A or B) = P(A) + P(B) - P(A and B)
```
```
P(A or B) = P(A) + P(B) - P(A and B)
```
### Measuring a sample
- Let's work with a sample of coin flips to calculate some probabilities. You will calculate absolute and relative frequency and check the theoretical value from the distribution of the sample data.
- The array sample_of_two_coin_flips has 1,000 experiments, each consisting of two fair coin flips. For each experiment, we record the number of heads out of the two coin flips: 0, 1, or 2.
- We've preloaded the binom object and the find_repeats() and relfreq() methods from the scipy.stats library for you. You'll need these to calculate the probabilities in this exercise.
#### Question 1
From the provided samples in sample_of_two_coin_flips, get the probability of having 2 heads out of the 1,000 trials.
```python
# Count how many times you got 2 heads from the sample data
count_2_heads = find_repeats(sample_of_two_coin_flips).counts[2]

# Divide the number of heads by the total number of draws
prob_2_heads = count_2_heads / 1000

# Display the result
print(prob_2_heads)
```
```
0.243
```
#### Question 2
Calculate the relative frequency from sample_of_two_coin_flips, set numbins as 3, and extract frequency.
```python
# Get the relative frequency from sample_of_two_coin_flips
# Set numbins as 3
# Extract frequency
rel_freq = relfreq(sample_of_two_coin_flips, numbins=3).frequency
print(rel_freq)
```
```
[0.269 0.488 0.243]
```
#### Question 3
Calculate the probability of getting 0, 1, or 2 from a binomial distribution with n=2 and p=0.5.
```python
# Probability of getting 0, 1, or 2 from the distribution
probabilities = binom.pmf([0,1,2], n=2, p=0.5)
print(probabilities)
```
```
[0.25 0.5  0.25]
```
### Joint probabilities
- In this exercise we're going to calculate joint probabilities using the following table:
		Engine		Gear box
Fails	0.01		0.005
Works	0.99		0.995
- Take the values from the table, create variables, and calculate the probability of the event in each step.
#### Question 1
Calculate the probability that the engine and gear box both work.
```python
# Individual probabilities
P_Eng_works = 0.99
P_GearB_works = 0.995

# Joint probability calculation
P_both_works = P_Eng_works * P_GearB_works

print(P_both_works)
```
```
0.98505
```
#### Question 2
Calculate the probability that one fails -- either engine or gear box -- but not both.
```python
# Individual probabilities
P_Eng_fails = 0.01
P_Eng_works = 0.99
P_GearB_fails = 0.005
P_GearB_works = 0.995

# Joint probability calculation
P_only_GearB_fails = P_GearB_fails * P_Eng_works
P_only_Eng_fails = P_Eng_fails * P_GearB_works

# Calculate result
P_one_fails = P_only_GearB_fails + P_only_Eng_fails

print(P_one_fails)
```
```
0.0149
```
#### Question 3
What is the probability that either both work or both fail?
```python
# Individual probabilities
P_Eng_fails = 0.01
P_Eng_works = 0.99
P_GearB_fails = 0.005
P_GearB_works = 0.995

# Joint probability calculation
P_EngW_GearBW = P_Eng_works * P_GearB_works
P_EngF_GearBF = P_Eng_fails * P_GearB_fails

# Calculate result
P_fails_or_works = P_EngW_GearBW + P_EngF_GearBF

print(P_fails_or_works)
```
```
0.9851
```
### Deck of cards
- In this exercise, you'll use the following deck of cards to calculate some probabilities in each step:
#### Question 1
Calculate the probability of not getting an Ace.
```python
# Ace probability
P_Ace = 4/52

# Not Ace probability
P_not_Ace = 1 - P_Ace

print(P_not_Ace)
```
```
0.9230769230769231
```
#### Question 2
Calculate the probability of getting a red card.
```python
# Figure probabilities
P_Hearts = 13/52
P_Diamonds = 13/52

# Probability of red calculation
P_Red = P_Hearts + P_Diamonds

print(P_Red)
```
```
0.5
```
#### Question 3
Calculate the probability of getting a Jack or a spade.
```python
# Figure probabilities
P_Jack = 4/52
P_Spade = 13/52

# Joint probability
P_Jack_n_Spade = 1/52

# Probability of Jack or spade
P_Jack_or_Spade = P_Jack + P_Spade - P_Jack_n_Spade

print(P_Jack_or_Spade)
```
```
0.3076923076923077
```
#### Question 4
Calculate the probability of getting a King or a Queen.
```python
# Figure probabilities
P_King = 4/52
P_Queen = 4/52

# Joint probability
P_King_n_Queen = 0

# Probability of King or Queen
P_King_or_Queen = P_King + P_Queen - P_King_n_Queen

print(P_King_or_Queen)
```
```
0.15384615384615385
```

### Video: Conditional probabilities
### Delayed flights
- A certain airline offers flights departing to New York on Tuesdays and Fridays, but sometimes the flights are delayed:
			Delayed		On time		Total
Tuesday		24			114			138
Friday		11			127			138
Total		35			241			276
- At the bottom of the Delayed column you have a total of 35, which means there were 35 delayed flights out of the total of 276 departures in the sample. Of these, 24 were on Tuesday and 11 on Friday.
- Given the table, answer the following questions:
#### Question 1
What is the probability of a flight being on time?
```python
# Needed quantities
On_time = 241
Total_departures = 276

# Probability calculation
P_On_time = On_time / Total_departures

print(P_On_time)
```
```
0.8731884057971014
```
#### Question 2
Every departure is on time with probability P_On_time. What is the probability of a flight being delayed?
```python
# Needed quantities
P_On_time = 241 / 276

# Probability calculation
P_Delayed = 1 - P_On_time

print(P_Delayed)
```
```
0.12681159420289856
```
#### Question 3
Given that it's Tuesday, what is the probability of a flight being delayed (P(Delayed|Tuesday))?
```python
# Needed quantities
Delayed_on_Tuesday = 24
On_Tuesday = 138

# Probability calculation
P_Delayed_g_Tuesday = Delayed_on_Tuesday / On_Tuesday

print(P_Delayed_g_Tuesday)
```
```
0.17391304347826086
```
#### Question 4
Given that it's Friday, what is the probability of a flight being delayed (P(Delayed|Friday))?
```python
# Needed quantities
Delayed_on_Friday = 11
On_Friday = 138

# Probability calculation
P_Delayed_g_Friday = Delayed_on_Friday / On_Friday

print(P_Delayed_g_Friday)
```
```
0.07971014492753623
```
### Contingency table
- The following table shows the numbers of red and black cards in a deck that are Aces and non-Aces:
			Red		Black		Total
Ace			2		2			4
Non Ace		24		24			48
Total		26		26			52
- The total in the Red column is 26, which means there are 26 red cards in the deck. Of these, 2 are Aces and 24 are non-Aces. There are 52 cards in a deck. Use the values in the table to calculate some conditional probabilities.
#### Question 1
Calculate P(Ace|Red).
```python
# Individual probabilities
P_Red = 26/52
P_Red_n_Ace = 2/52

# Conditional probability calculation
P_Ace_given_Red = P_Red_n_Ace / P_Red

print(P_Ace_given_Red)
```
```
0.07692307692307693
```
#### Question 2
Calculate P(Black|Ace).
```python
# Individual probabilities
P_Ace = 4/52
P_Ace_n_Black = 2/52

# Conditional probability calculation
P_Black_given_Ace = P_Ace_n_Black / P_Ace

print(P_Black_given_Ace)
```
```
0.5
```
#### Question 3
Calculate P(Non Ace|Black).
```python
# Individual probabilities
P_Black = 26/52
P_Black_n_Non_ace = 24/52

# Conditional probability calculation
P_Non_ace_given_Black = P_Black_n_Non_ace / P_Black

print(P_Non_ace_given_Black)
```
```
0.9230769230769231
```
#### Question 4
Calculate P(Red|Non Ace).
```python
# Individual probabilities
P_Non_ace = 48/52
P_Non_ace_n_Red = 24/52

# Conditional probability calculation
P_Red_given_Non_ace = P_Non_ace_n_Red / P_Non_ace

print(P_Red_given_Non_ace)
```
```
0.5
```
### More cards
- Now let's use the deck of cards to calculate some conditional probabilities.
#### Question 1
Calculate the probability of getting two Jacks (P(Jack and Jack)).
```python
# Needed probabilities
P_first_Jack = 4/52
P_Jack_given_Jack = 3/51

# Joint probability calculation
P_two_Jacks = P_first_Jack * P_Jack_given_Jack

print(P_two_Jacks)
```
```
0.004524886877828055
```
#### Question 2
Calculate P(Ace|Spade).
```python
# Needed probabilities
P_Spade = 13/52
P_Spade_n_Ace = 1/52

# Conditional probability calculation
P_Ace_given_Spade = P_Spade_n_Ace / P_Spade

print(P_Ace_given_Spade)
```
```
0.07692307692307693
```
#### Question 3
Calculate P(Queen|Face card).
```python
# Needed probabilities
P_Face_card = 12/52
P_Face_card_n_Queen = 4/52

# Conditional probability calculation
P_Queen_given_Face_card = P_Face_card_n_Queen / P_Face_card

print(P_Queen_given_Face_card)
```
```
0.3333333333333333
```

### Video: Total probability law
### Formula 1 engines
- Suppose that two manufacturers, A and B, supply the engines for Formula 1 racing cars, with the following characteristics:
  - 99% of the engines from factory A last more than 5,000 km.
  - Factory B manufactures engines that last more than 5,000 km with 95% probability.
  - 70% of the engines are from manufacturer A, and the rest are produced by manufacturer B.
- What is the chance that an engine will last more than 5,000 km?
#### Question 1
- Calculate the following probabilities:
  - The manufacturer is A (P_A).
  - The engine lasts more than 5,000 km given that manufacturer is A (P_last5000_g_A).
  - The manufacturer is B (P_B).
  - The engine lasts more than 5,000 km given that manufacturer is B (P_last5000_g_B).
- Use the total probability law to calculate the probability that the engine will last more than 5,000 km and store the result into P_last_5000.
```python
# Needed probabilities
P_A = 0.7
P_last5000_g_A = 0.99
P_B = 0.3
P_last5000_g_B = 0.95

# Total probability calculation
P_last_5000 = P_A * P_last5000_g_A + P_B * P_last5000_g_B

print(P_last_5000)
```
```
0.978
```
### Voters
- Of the total population of three states X, Y, and Z, 43% are from state X, 25% are from state Y, and 32% are from state Z. A poll is taken and the result is the following:
  - 53% of the voters support John Doe in state X.
  - 67% of the voters support John Doe in state Y.
  - 32% of the voters support John Doe in state Z.
- Given that a voter supports John Doe, answer the following questions.
#### Question 1
What is the probability that the voter lives in state X and supports John Doe?
```python
# Individual probabilities
P_X = 0.43

# Conditional probabilities
P_Support_g_X = 0.53

# Total probability calculation
P_X_n_Support = P_X * P_Support_g_X
print(P_X_n_Support)
```
```
0.22790000000000002
```
#### Question 2
What is the probability that the voter lives in state Z and does not support John Doe?
```python
# Individual probabilities
P_Z = 0.32

# Conditional probabilities
P_Support_g_Z = 0.32
P_NoSupport_g_Z = 1 - P_Support_g_Z

# Total probability calculation
P_Z_n_NoSupport = P_Z * P_NoSupport_g_Z
print(P_Z_n_NoSupport)
```
```
0.2176
```
#### Question 3
What is the total percentage of voters that support John Doe?
```python
# Individual probabilities
P_X = 0.43
P_Y = 0.25
P_Z = 0.32

# Conditional probabilities
P_Support_g_X = 0.53
P_Support_g_Y = 0.67
P_Support_g_Z = 0.32

# Total probability calculation
P_Support = P_X * P_Support_g_X + P_Y * P_Support_g_Y + P_Z * P_Support_g_Z
print(P_Support)
```
```
0.4978
```

### Video: Bayes' rule
#### Conditioning
- In many situations we find events that depend on other events, and we are interested in calculating probabilities taking into consideration such relations.
- On the other hand, many problems can be studied by classifying the elements in our sample space. It is easier to work with classifications that do not have elements in common -- i.e., that do not overlap. Using this context, please answer the following question:
- Why is Bayes' rule important?
```
It allows you to calculate conditional probabilities.
It allows you to calculate conditional probabilities for events that can be partitions in nonoverlapping parts.
It allows you to calculate joint probabilities.
It was discovered by the Presbyterian minister Thomas Bayes.
```
```
It allows you to calculate conditional probabilities for events that can be partitions in nonoverlapping parts.
```
### Factories and parts
- A certain electronic part is manufactured by three different vendors named V1, V2, and V3.
- Half of the parts are produced by V1, 25% by V2, and the rest by V3. The probability of a part being damaged given that it was produced by V1 is 1%, while it's 2% for V2 and 3% for V3.
- If a part taken at random is damaged, answer the following questions.
#### Question 1
What is the probability that the part was manufactured by V1?
```python
# Individual probabilities & conditional probabilities
P_V1 = 0.5
P_V2 = 0.25
P_V3 = 0.25
P_D_g_V1 = 0.01
P_D_g_V2 = 0.02
P_D_g_V3 = 0.03

# Probability of Damaged
P_Damaged = (P_V1 * P_D_g_V1) + (P_V2 * P_D_g_V2) + (P_V3 * P_D_g_V3)

# Bayes' rule for P(V1|D)
P_V1_g_D = (P_V1 * P_D_g_V1) / P_Damaged

print(P_V1_g_D)
```
```
0.2857142857142857
```
#### Question 2
What is the probability that it was manufactured by V2?
```python
# Individual probabilities & conditional probabilities
P_V1 = 0.5
P_V2 = 0.25
P_V3 = 0.25
P_D_g_V1 = 0.01
P_D_g_V2 = 0.02
P_D_g_V3 = 0.03

# Probability of Damaged
P_Damaged = (P_V1 * P_D_g_V1) + (P_V2 * P_D_g_V2) + (P_V3 * P_D_g_V3)

# Bayes' rule for P(V2|D)
P_V2_g_D = (P_V2 * P_D_g_V2) / P_Damaged

print(P_V2_g_D)
```
```
0.2857142857142857
```
#### Question 3
What is the probability that the part was manufactured by V3?
```python
# Individual probabilities & conditional probabilities
P_V1 = 0.5
P_V2 = 0.25
P_V3 = 0.25
P_D_g_V1 = 0.01
P_D_g_V2 = 0.02
P_D_g_V3 = 0.03

# Probability of Damaged
P_Damaged = (P_V1 * P_D_g_V1) + (P_V2 * P_D_g_V2) + (P_V3 * P_D_g_V3)

# Bayes' rule for P(V3|D)
P_V3_g_D = (P_V3 * P_D_g_V3) / P_Damaged

print(P_V3_g_D)
```
```
0.4285714285714285
```
### Swine flu blood test
- You go to the doctor about a strong headache. The doctor randomly selects you for a blood test for swine flu, which is suspected to affect 1 in 9,000 people in your city. The accuracy of the test is 99%, meaning that the probability of a false positive is 1%. The probability of a false negative is zero.
- Given that you test positive, answer the following questions.
#### Question 1
What is the probability that you have swine flu given that your test outcome is positive?
```python
# Probability of having Swine_flu
P_Swine_flu = 1./9000
# Probability of not having Swine_flu
P_no_Swine_flu = 1 - P_Swine_flu
# Probability of being positive given that you have Swine_flu
P_Positive_g_Swine_flu = 1
# Probability of being positive given that you do not have Swine_flu
P_Positive_g_no_Swine_flu = 0.01

# Probability of Positive
P_Positive = (P_Swine_flu * P_Positive_g_Swine_flu) + (P_no_Swine_flu * P_Positive_g_no_Swine_flu)

# Bayes' rule for P(Swine_flu|Positive)
P_Swine_flu_g_Positive = (P_Swine_flu * P_Positive_g_Swine_flu) / P_Positive

print(P_Swine_flu_g_Positive)
```
```
0.010990218705352238
```
#### Question 2
You went to Miami and 1 in 350 people came back with swine flu. Calculate the new probability that you'll test positive.
```python
# Individual probabilities & conditional probabilities
P_Swine_flu = 1./350
P_no_Swine_flu = 1 - P_Swine_flu
P_Positive_g_Swine_flu = 1
P_Positive_g_no_Swine_flu = 0.01

# Probability of Positive
P_Positive = (P_Swine_flu * P_Positive_g_Swine_flu) + (P_no_Swine_flu * P_Positive_g_no_Swine_flu)

# Bayes' rule for P(Swine_flu|Positive)
P_Swine_flu_g_Positive = (P_Swine_flu * P_Positive_g_Swine_flu) / P_Positive

print(P_Swine_flu_g_Positive)
```
```
0.22271714922048996
```
#### Question 3
If the probability of a false positive is 2%, what is the new probability that you have swine flu after your vacation?
```python
# Individual probabilities & conditional probabilities
P_Swine_flu = 1./350
P_no_Swine_flu = 1 - P_Swine_flu
P_Positive_g_Swine_flu = 1
P_Positive_g_no_Swine_flu = 0.02

# Probability of Positive
P_Positive = P_Swine_flu * P_Positive_g_Swine_flu + P_no_Swine_flu * P_Positive_g_no_Swine_flu

# Bayes' rule for P(Swine_flu|Positive)
P_Swine_flu_g_Positive = (P_Swine_flu * P_Positive_g_Swine_flu) / P_Positive

print(P_Swine_flu_g_Positive)
```
```
0.12531328320802004
```

## `Chapter 3` Important probability distributions

### Video: Normal distributions
#### Range of values
- Suppose the scores on a given academic test are normally distributed, with a mean of 65 and standard deviation of 10.
- What would be the range of scores two standard deviations from the mean?
```
10 and 65
55 and 75
45 and 85
35 and 95
```
```
45 and 85
```
### Plotting normal distributions
- A certain restaurant chain has been collecting data about customer spending. The data shows that the spending is approximately normally distributed, with a mean of $3.15 and a standard deviation of $1.50 per customer.
#### Question 1
- Import norm from scipy.stats, matplotlib.pyplot as plt, and seaborn as sns.
- Generate a normal distribution sample with mean 3.15 and standard deviation 1.5.
- Plot the sample generated.
```python
# Import norm, matplotlib.pyplot, and seaborn
from scipy.stats import norm
import matplotlib.pyplot as plt 
import seaborn as sns

# Create the sample using norm.rvs()
sample = norm.rvs(loc=3.15, scale=1.5, size=10000, random_state=13)

# Plot the sample
sns.distplot(sample)
plt.show()
```
#### Within three standard deviations
The heights of every employee in a company have been measured, and they are distributed normally with a mean of 168 cm and a standard deviation of 12 cm.
What is the probability of getting a height within three standard deviations of the mean?
```
68%
95%
99.7%
30%
```
```
99.7%
```
### Video: Normal probabilities
### Restaurant spending example
- Let's go back to the example of the restaurant chain that has been collecting data about customer spending. Recall that the data shows that the spending is approximately normally distributed, with a mean of 3.15 and a standard deviation of 1.5 per customer, as pictured in the plot.
- We can use the already imported norm object from scipy.stats to answer several questions about customer spending at this restaurant chain.
#### Question 1
What is the probability that a customer will spend $3 or less?
```python
# Probability of spending $3 or less
spending = norm.cdf(3, loc=3.15, scale=1.5)
print(spending)
```
```
0.46017216272297107
```
#### Question 2
What is the probability that a customer will spend more than $5?
```python
# Probability of spending more than $5
spending = norm.sf(5, loc=3.15, scale=1.5)
print(spending)
```
```
0.10872571321259111
```
#### Question 3
What is the probability that a customer will spend more than $2.15 and $4.15 or less?
```python
# Probability of spending more than $2.15 and $4.15 or less
spending_4 = norm.cdf(4.15, loc=3.15, scale=1.5)
spending_2 = norm.cdf(2.15, loc=3.15, scale=1.5)
print(spending_4 - spending_2)
```
```
0.4950149249061543
```
#### Question 4
What is the probability that a customer will spend $2.15 or less or more than $4.15?
```python
# Probability of spending $2.15 or less or more than $4.15
spending_2 = norm.cdf(2.15, loc=3.15, scale=1.5)
spending_over_4 = norm.sf(4.15, loc=3.15, scale=1.5) 
print(spending_2 + spending_over_4)
```
```
0.5049850750938457
```
### Smartphone battery example
- One of the most important things to consider when buying a smartphone is how long the battery will last.
- Suppose the period of time between charges can be modeled with a normal distribution with a mean of 5 hours and a standard deviation of 1.5 hours.
- A friend wants to buy a smartphone and is asking you the following questions.
norm is already imported from scipy.stats.
#### Question 1
What is the probability that the battery will last less than 3 hours?
```python
# Probability that battery will last less than 3 hours
less_than_3h = norm.cdf(3, loc=5, scale=1.5)
print(less_than_3h)
```
```
0.09121121972586788
```
#### Question 2
What is the probability that the battery will last more than 3 hours?
```python
# Probability that battery will last more than 3 hours
more_than_3h = norm.sf(3, loc=5, scale=1.5)
print(more_than_3h)
```
```
0.9087887802741321
```
#### Question 3
What is the probability that the battery will last between 5 and 7 hours?
```python
# Probability that battery will last between 5 and 7 hours
P_less_than_7h = norm.cdf(7, loc=5, scale=1.5)
P_less_than_5h = norm.cdf(5, loc=5, scale=1.5)
print(P_less_than_7h - P_less_than_5h)
```
```
0.4087887802741321
```
### Adults' heights example
- The heights of adults aged between 18 and 35 years are normally distributed. For males, the mean height is 70 inches with a standard deviation of 4. Adult females have a mean height of 65 inches with a standard deviation of 3.5. You can see how the heights are distributed in this plot:
- Using the previous information, complete the following exercises.
- For your convenience, norm has been imported from the library scipy.stats.
#### Question 1
Print the range of female heights one standard deviation from the mean.
```python
# Values one standard deviation from mean height for females
interval = norm.interval(0.68, loc=65, scale=3.5)
print(interval)
```
```
(61.51939740876586, 68.48060259123413)
```
#### Question 2
Print the value where the tallest males fall with 0.01 probability.
```python
# Value where the tallest males fall with 0.01 probability
tallest = norm.ppf(0.99, loc=70, scale=4)
print(tallest)
```
```
79.30539149616337
```
#### Question 3
Print the probability of being taller than 73 inches for a male and for a female.
```python
# Probability of being taller than 73 inches for males and females
P_taller_male = norm.sf(73, loc=70, scale=4)
P_taller_female = norm.sf(73, loc=65, scale=3.5)
print(P_taller_male, P_taller_female)
```
```
0.2266273523768682 0.011135489479616392
```
#### Question 4
Print the probability of being shorter than 61 inches for a male and for a female.
```python
# Probability of being shorter than 61 inches for males and females
P_shorter_male = norm.cdf(61, loc=70, scale=4)
P_shorter_female = norm.cdf(61, loc=65, scale=3.5)
print(P_shorter_male, P_shorter_female)
```
```
0.012224472655044696 0.12654895447355774
```

### Video: Poisson distributions
### ATM example
- If you know how many specific events occurred per unit of measure, you can assume that the distribution of the random variable follows a Poisson distribution to study the phenomenon.
- Consider an ATM (automatic teller machine) at a very busy shopping mall. The bank wants to avoid making customers wait in line to use the ATM. It has been observed that the average number of customers making withdrawals between 10:00 a.m. and 10:05 a.m. on any given day is 1.
- As a data analyst at the bank, you are asked what the probability is that the bank will need to install another ATM to handle the load.
- To answer the question, you need to calculate the probability of getting more than one customer during that time period.
#### Question 1
- Import poisson from scipy.stats.
- Calculate the probability of having more than one customer visiting the ATM in this 5-minute period.
```python
# Import poisson from scipy.stats
from scipy.stats import poisson

# Probability of more than 1 customer
probability = poisson.sf(k=1, mu=1)

# Print the result
print(probability)
```
```
0.2642411176571153
```
### Highway accidents example
- On a certain turn on a very busy highway, there are 2 accidents per day. Let's assume the number of accidents per day can be modeled as a Poisson random variable and is distributed as in the following plot:
- For your convenience, the poisson object has already been imported from the scipy.stats library.
- Aiming to improve road safety, the transportation agency of the regional government has assigned you the following tasks.
#### Question 1
Determine and print the probability of there being 5 accidents on any day.
```python
# Import the poisson object
from scipy.stats import poisson

# Probability of 5 accidents any day
P_five_accidents = poisson.pmf(k=5, mu=2)

# Print the result
print(P_five_accidents)
```
```
0.03608940886309672
```
#### Question 2
Determine and print the probability of having 4 or 5 accidents on any day.
```python
# Import the poisson object
from scipy.stats import poisson

# Probability of having 4 or 5 accidents on any day
P_less_than_6 = poisson.cdf(k=5, mu=2)
P_less_than_4 = poisson.cdf(k=3, mu=2)

# Print the result
print(P_less_than_6 - P_less_than_4)
```
```
0.12631293102083851
```
#### Question 3
Determine and print the probability of having more than 3 accidents on any day.
```python
# Import the poisson object
from scipy.stats import poisson

# Probability of more than 3 accidents any day
P_more_than_3 = poisson.sf(k=3, mu=2)

# Print the result
print(P_more_than_3)
```
```
0.14287653950145296
```
#### Question 4
Determine and print the number of accidents that is likely to happen with 0.75 probability.
```python
# Import the poisson object
from scipy.stats import poisson

# Number of accidents with 0.75 probability
accidents = poisson.ppf(q=0.75, mu=2)

# Print the result
print(accidents)
```
```
3.0
```
### Generating and plotting Poisson distributions
- In the previous exercise, you calculated some probabilities. Now let's plot that distribution.
- Recall that on a certain highway turn, there are 2 accidents per day on average. Assuming the number of accidents per day can be modeled as a Poisson random variable, let's plot the distribution.
#### Question 1
- Import poisson from scipy.stats, matplotlib.pyplot as plt, and seaborn as sns.
- Generate a Poisson distribution sample with size=10000 and mu=2.
- Plot the sample generated.
```python
# Import poisson, matplotlib.pyplot, and seaborn
from scipy.stats import poisson
import matplotlib.pyplot as plt 
import seaborn as sns

# Create the sample
sample = poisson.rvs(mu=2, size=10000, random_state=13)

# Plot the sample
sns.distplot(sample, kde=False)
plt.show()
```

### Video: Geometric distributions
### Catching salmon example
- Every fall the salmon run occurs -- this is the time when salmon swim back upriver from the ocean to spawn. While swimming back to the upper river (usually to the place where they were spawned), the fish may encounter grizzly bears. Some of these bears can eat 18 salmon in 3 hours, and they have a 0.0333 probability of success in their attempts to catch a fish.
- We can model a grizzly bear catching salmon with a geometric distribution.
- For the following exercises, the geom object from scipy.stats has already been loaded for your convenience.
#### Question 1
Calculate and print the probability that the bear will catch a salmon on its third attempt, after failing two times.
```python
# Getting a salmon on the third attempt
probability = geom.pmf(k=3, p=0.0333)

# Print the result
print(probability)
```
```
0.031119146037000004
```
#### Question 2
Calculate and print the probability that the bear will get a salmon in less than 5 attempts.
```python
# Probability of getting a salmon in less than 5 attempts
probability = geom.cdf(k=4, p=0.0333)

# Print the result
print(probability)
```
```
0.12669313451096792
```
#### Question 3
Calculate and print the probability that the bear will get a salmon in less than 21 attempts.
```python
# Probability of getting a salmon in less than 21 attempts
probability = geom.cdf(k=20, p=0.0333)

# Print the result
print(probability)
```
```
0.4920343187252892
```
#### Question 4
Calculate and print how many attempts the bear has to make to have a 0.9 probability of catching a salmon.
```python
# Attempts for 0.9 probability of catching a salmon
attempts = geom.ppf(q=0.9, p=0.0333)

# Print the result
print(attempts)
```
```
68.0
```
### Free throws example
- Suppose you know that a basketball player has a 0.3 probability of scoring a free throw. What is the probability of them missing with the first throw and scoring with the second?
#### Question 1
- Import geom from scipy.stats.
- Use the probability mass function (pmf()) with p=0.3 and specify the appropriate k value.
```python
# Import geom from scipy.stats
from scipy.stats import geom

# Probability of missing first and scoring on second throw
probability = geom.pmf(k=2, p=0.3)

# Print the result
print(probability)
```
```
0.21
```
### Generating and plotting geometric distributions
- In sports it is common for players to make multiple attempts to score points for themselves or their teams. Each single attempt can have two possible outcomes, scoring or not scoring. Those situations can be modeled with geometric distributions. With scipy.stats you can generate samples using the rvs() function for each distribution.
- Consider the previous example of a basketball player who scores free throws with a probability of 0.3. Generate a sample, and plot it.
numpy has been imported for you with the standard alias np.
#### Question 1
- Import geom from scipy.stats, matplotlib.pyplot as plt, and seaborn as sns.
- Generate a sample with size=10000 from a geometric distribution with a probability of success of 0.3.
- Plot the sample generated.
```python
# Import geom, matplotlib.pyplot, and seaborn
from scipy.stats import geom
import matplotlib.pyplot as plt 
import seaborn as sns

# Create the sample
sample = geom.rvs(p=0.3, size=10000, random_state=13)

# Plot the sample
sns.distplot(sample, bins = np.linspace(0,20,21), kde=False)
plt.show()
```

## `Chapter 4` Probability meets statistics

### Video: From sample mean to population mean
### Generating a sample
- A hospital's planning department is investigating different treatments for newborns. As a data scientist you are hired to simulate the sex of 250 newborn children, and you are told that on average 50.50% are males.
#### Question 1
- Import the binom object from scipy.stats.
- Generate a sample of 250 newborns with 50.50% probability of being male.
- Print the sample.
```python
# Import the binom object
from scipy.stats import binom

# Generate a sample of 250 newborn children
sample = binom.rvs(n=1, p=0.505, size=250, random_state=42)

# Show the sample values
print(sample)
```
```
[1 0 0 0 1 1 1 0 0 0 1 0 0 1 1 1 1 0 1 1 0 1 1 1 1 0 1 0 0 1 0 1 1 0 0 0 1
 1 0 1 1 1 1 0 1 0 1 0 0 1 0 0 0 0 0 0 1 1 1 1 1 1 0 1 1 0 1 0 1 0 0 1 1 0
 0 0 0 1 1 1 0 0 1 1 1 1 0 0 0 1 1 0 0 0 0 1 0 1 1 1 1 0 1 0 0 1 1 0 1 1 1
 1 0 0 0 0 0 1 0 0 0 0 1 1 1 1 0 0 1 0 1 1 1 1 0 1 0 0 1 0 0 1 1 1 1 1 0 1
 1 1 0 1 1 1 0 1 0 0 1 0 1 0 0 0 1 0 1 1 1 0 0 1 0 1 0 1 0 1 0 1 1 1 0 0 1
 0 0 0 0 1 1 0 0 0 1 1 0 0 0 0 0 1 1 0 0 1 1 0 1 1 0 0 0 1 0 1 1 0 0 0 0 0
 1 1 1 1 0 1 0 0 0 1 0 1 1 0 1 1 0 1 0 0 0 1 1 0 1 0 0 0]
```
### Calculating the sample mean
- Now you can calculate the sample mean for this generated sample by taking some elements from the sample.
- Using the sample variable you just created, you'll calculate the sample means of the first 10, 50, and 250 samples.
- The binom object and describe() method from scipy.stats have been imported for your convenience.
#### Question 1
Print the sample mean of the first 10 samples.
```python
# Print the sample mean of the first 10 samples
print(describe(sample[0:10]).mean)
```
```
0.4
```
#### Question 2
Print the sample mean of the first 50 samples.
```python
# Print the sample mean of the first 50 samples
print(describe(sample[0:50]).mean)
```
```
0.56
```
#### Question 3
Print the sample mean of the first 250 samples.
```python
# Print the sample mean of the first 250 samples
print(describe(sample[0:250]).mean)
```
```
0.504
```
### Plotting the sample mean
- Now let's plot the sample mean, so you can see more clearly how it evolves as more data becomes available.
- For this exercise we'll again use the sample you generated earlier, which is available in the sample variable. The binom object and describe() function have already been imported for you from scipy.stats, and matplotlib.pyplot is available as plt.
#### Question 1
In a for statement for i in a range that goes from 2 to 251, do the following:
- Calculate the sample mean for the first i values.
- Use append to add the value to the averages array.
```python
# Calculate sample mean and store it on averages array
averages = []
for i in range(2, 251):
    averages.append(describe(sample[0:i]).mean)
```
#### Question 2
Add a horizontal line at the mean value of the binomial distribution with n=1 and p=0.505.
```python
# Calculate sample mean and store it on averages array
averages = []
for i in range(2, 251):
    averages.append(describe(sample[0:i]).mean)

# Add population mean line and sample mean plot
plt.axhline(binom.mean(n=1, p=0.505), color='red')
plt.plot(averages, '-')
```
#### Question 3
Print the sample mean of the first 250 samples.
```python
# Calculate sample mean and store it on averages array
averages = []
for i in range(2, 251):
    averages.append(describe(sample[0:i]).mean)

# Add population mean line and sample mean plot
plt.axhline(binom.mean(n=1, p=0.505), color='red')
plt.plot(averages, '-')

# Add legend
plt.legend(("Population mean","Sample mean"), loc='upper right')
plt.show()
```

### Video: Adding random variables
### Sample means
- An important result in probability and statistics is that the shape of the distribution of the means of random variables tends to a normal distribution, which happens when you add random variables with any distribution with the same expected value and variance.
- For your convenience, we've loaded binom and describe() from the scipy.stats library and imported matplotlib.pyplot as plt and numpy as np. We generated a simulated population with size 1,000 that follows a binomial distribution for 10 fair coin flips and is available in the population variable.
#### Question 1
Select 20 random values from the population using np.random.choice().
```python
# Create list for sample means
sample_means = []
for _ in range(1500):
	# Take 20 values from the population
    sample = np.random.choice(population, 20)
```
#### Question 2
Plot a histogram of the sample_means list.
```python
# Create list for sample means
sample_means = []
for _ in range(1500):
	# Take 20 values from the population
    sample = np.random.choice(population, 20)
    # Calculate the sample mean
    sample_means.append(describe(sample).mean)
```
#### Question 3
Inspecting the plot, what is the distribution of the sample mean?
```
Same as the generated sample
Binomial
Normal
```
```
Normal
```
### Sample means follow a normal distribution
- In the previous exercise, we generated a population that followed a binomial distribution, chose 20 random samples from the population, and calculated the sample mean. Now we're going to test some other probability distributions to see the shape of the sample means.
- From the scipy.stats library, we've loaded the poisson and geom objects and the describe() function. We've also imported matplotlib.pyplot as plt and numpy as np.
- As you'll see, the shape of the distribution of the means is the same even though the samples are generated from different distributions.
#### Question 1
Select 20 values from the population, add the sample mean to the sample_means list, and plot a histogram.
```python
# Generate the population
population = geom.rvs(p=0.5, size=1000)

# Create list for sample means
sample_means = []
for _ in range(3000):
	# Take 20 values from the population
    sample = np.random.choice(population, 20)
    # Calculate the sample mean
    sample_means.append(describe(sample).mean)

# Plot the histogram
plt.hist(sample_means)
plt.show()
```
#### Question 2
Select 20 values from the population, populate the sample_means list, and plot a histogram.
```python
# Generate the population
population = poisson.rvs(mu=2, size=1000)

# Create list for sample means
sample_means = []
for _ in range(1500):
	# Take 20 values from the population
    sample = np.random.choice(population, 20)
    # Calculate the sample mean
    sample_means.append(describe(sample).mean)

# Plot the histogram
plt.hist(sample_means)
plt.show()
```
### Adding dice rolls
- To illustrate the central limit theorem, we are going to work with dice rolls. We'll generate the samples and then add them to plot the outcome.
- You're provided with a function named roll_dice() that will generate the sample dice rolls. numpy is already imported as np for your convenience: you have to use np.add(sample1, sample2) to add samples. Also, matplotlib.pyplot is imported as plt so you can plot the histograms.
#### Question 1
Generate a sample of 2000 dice rolls using roll_dice() and plot a histogram of the sample.
```python
# Configure random generator
np.random.seed(42)

# Generate the sample
sample1 = roll_dice(2000)

# Plot the sample
plt.hist(sample1, bins=range(1, 8), width=0.9)
plt.show()
```
#### Question 2
Add sample1 and sample2 using np.add(), store the result in the variable sum_of_1_and_2, then plot sum_of_1_and_2.
```python
# Configure random generator
np.random.seed(42)

# Generate two samples of 2000 dice rolls
sample1 = roll_dice(2000)
sample2 = roll_dice(2000)

# Add the first two samples
sum_of_1_and_2 = np.add(sample1, sample2)

# Plot the sum
plt.hist(sum_of_1_and_2, bins=range(2, 14), width=0.9)
plt.show()
```
#### Question 3
Add sum_of_1_and_2 and sample3 using np.add() and store the result in sum_of_3_samples. Then plot sum_of_3_samples.
```python
# Configure random generator
np.random.seed(42)

# Generate the samples
sample1 = roll_dice(2000)
sample2 = roll_dice(2000)
sample3 = roll_dice(2000)

# Add the first two samples
sum_of_1_and_2 = np.add(sample1, sample2)

# Add the first two with the third sample
sum_of_3_samples = np.add(sum_of_1_and_2, sample3)

# Plot the result
plt.hist(sum_of_3_samples, bins=range(3, 20), width=0.9)
plt.show() 
```

### Video: Linear regression
### Fitting a model
- A university has provided you with data that shows a relationship between the hours of study and the scores that the students get on a given test.
- You have access to the data through the variables hours_of_study and scores. Use a linear model to learn from the data.
#### Question 1
- Import the linregress() function from scipy.stats.
- Fit a linear model using the provided data in the hours_of_study and scores variables.
- Print the parameters.
```python
# Import the linregress() function
from scipy.stats import linregress

# Get the model parameters
slope, intercept, r_value, p_value, std_err = linregress(hours_of_study, scores)

# Print the linear model parameters
print('slope:', slope)
print('intercept:', intercept)
```
```
slope: 1.715259850957089
intercept: 48.27076128780868
```
### Predicting test scores
- With the relationship between the hours of study and the scores that students got on a given test, you already got the parameters of a linear model, slope and intercept. With those parameters, let's predict the test score for a student who studies for 10 hours.
- For this exercise, the linregress() function has been imported for you from scipy.stats.
#### Question 1
Predict the test score for 10 hours of study using the provided parameters in slope and intercept, then print the score.
```python
# Get the predicted test score for given hours of study
score = slope*10 + intercept
print('score:', score)
```
```
score: 65.42335979737958
```
#### Question 2
Now predict the score for 9 hours of study using the parameters in slope and intercept, then print the score.
```python
# Get the predicted test score for given hours of study
score = slope*9 + intercept
print('score:', score)
```
```
score: 63.708099946422486
```
#### Question 3
Lastly, predict the score for 12 hours of study using the same parameters, and print the score.
```python
# Get the predicted test score for given hours of study
score = slope*12 + intercept
print('score:', score)
```
```
score: 68.85387949929375
```
### Studying residuals
- To implement a linear model you must study the residuals, which are the distances between the predicted outcomes and the data.
- Three conditions must be met:
  - The mean should be 0.
  - The variance must be constant.
  - The distribution must be normal.
- We will work with data of test scores for two schools, A and B, on the same subject. model_A and model_B were fitted with hours_of_study_A and test_scores_A and hours_of_study_B and test_scores_B, respectively.
matplotlib.pyplot has been imported as plt, numpy as np and LinearRegression from sklearn.linear_model.
#### Question 1
Make a scatter of hours_of_study_A and test_scores_A and plot hours_of_study_values_A and the outcomes from model_A.
```python
# Scatterplot of hours of study and test scores
plt.scatter(hours_of_study_A, test_scores_A)

# Plot of hours_of_study_values_A and predicted values
plt.plot(hours_of_study_values_A, model_A.predict(hours_of_study_values_A))
plt.title("Model A", fontsize=25)
plt.show()
```
#### Question 2
Subtract the predicted values and test_scores_A, then make a scatterplot with hours_of_study_A and residuals_A.
```python
# Calculate the residuals
residuals_A = model_A.predict(hours_of_study_A) - test_scores_A

# Make a scatterplot of residuals of model_A
plt.scatter(hours_of_study_A, residuals_A)

# Add reference line and title and show plot
plt.hlines(0, 0, 30, colors='r', linestyles='--')
plt.title("Residuals plot of Model A", fontsize=25)
plt.show()
```
#### Question 3
Make a scatter of hours_of_study_B and test_scores_B and plot hours_of_study_values_B and the outcomes from model_B.
```python
# Scatterplot of hours of study and test scores
plt.scatter(hours_of_study_B, test_scores_B)

# Plot of hours_of_study_values_B and predicted values
plt.plot(hours_of_study_values_B, model_B.predict(hours_of_study_values_B))
plt.title("Model B", fontsize=25)
plt.show()
```
#### Question 4
Subtract the predicted values and test_scores_B, then make a scatterplot with hours_of_study_B and residuals_B.
```python
# Calculate the residuals
residuals_B = model_B.predict(hours_of_study_B) - test_scores_B

# Make a scatterplot of residuals of model_B
plt.scatter(hours_of_study_B, residuals_B)

# Add reference line and title and show plot
plt.hlines(0, 0, 30, colors='r', linestyles='--')
plt.title("Residuals plot of Model B", fontsize=25)
plt.show()
```
### Video: Logistic regression
### Fitting a logistic model
- The university studying the relationship between hours of study and outcomes on a given test has provided you with a data set containing the number of hours the students studied and whether they failed or passed the test, and asked you to fit a model to predict future performance.
- The data is provided in the variables hours_of_study and outcomes. Use this data to fit a LogisticRegression model. numpy has been imported as np for your convenience.
#### Question 1
- Import LogisticRegression from sklearn.linear_model.
- Create the model using LogisticRegression(C=1e9).
- Pass the data to the model.fit() method.
- Create variables for each parameter, assign the values from the model, and print the parameters beta1 and beta0.
```python
# Import LogisticRegression
from sklearn.linear_model import LogisticRegression

# sklearn logistic model
model = LogisticRegression(C=1e9)
model.fit(hours_of_study, outcomes)

# Get parameters
beta1 = model.coef_[0][0]
beta0 = model.intercept_[0]

# Print parameters
print(beta1, beta0)
```
```
1.2453409925914463 -14.06750028924848
```
### Predicting if students will pass
- In the previous exercise you calculated the parameters of the logistic regression model that fits the data of hours of study and test outcomes.
- With those parameters you can predict the performance of students based on their hours of study. Use model.predict() to get the outcomes based on the logistic regression.
- For your convenience, LogisticRegression has been imported from sklearn.linear_model and numpy has been imported as np.
#### Question 1
- Create an array with the values 10, 11, 12, 13, and 14 to predict the outcomes for a test based on those numbers of hours of study.
- Use model.predict() to get the outcomes from the model, and print the outcomes.
- Use model.predict_proba() to get the probability of passing the test with 11 hours of study.
```python
# Specify values to predict
hours_of_study_test = [[10], [11], [12], [13], [14]]

# Pass values to predict
predicted_outcomes = model.predict(hours_of_study_test)
print(predicted_outcomes)

# Set value in array
value = np.asarray(11).reshape(-1,1)
# Probability of passing the test with 11 hours of study
print("Probability of passing test ", model.predict_proba(value)[:,1])
```
```
[False False  True  True  True]
Probability of passing test  [0.40884325]
```
### Passing two tests
- Put yourself in the shoes of one of the university students. You have two tests coming up in different subjects, and you're running out of time to study. You want to know how much time you have to study each subject to maximize the probability of passing both tests. Fortunately, there's data that you can use.
- For subject A, you already fitted a logistic model in model_A, and for subject B you fitted a model in model_B. As well as preloading LogisticRegression from sklearn.linear_model and numpy as np, expit(), the inverse of the logistic function, has been imported for you from scipy.special.
#### Question 1
Use model_A to predict if you'll pass the test with 6, 7, 8, 9, or 10 hours of study and model_B with 3, 4, 5, or 6.
```python
# Specify values to predict
hours_of_study_test_A = [[6], [7], [8], [9], [10]]

# Pass values to predict
predicted_outcomes_A = model_A.predict(hours_of_study_test_A)
print(predicted_outcomes_A)

# Specify values to predict
hours_of_study_test_B = [[3], [4], [5], [6]]

# Pass values to predict
predicted_outcomes_B = model_B.predict(hours_of_study_test_B)
print(predicted_outcomes_B)
```
```
[False False False  True  True]
[False False  True  True]
```
#### Question 2
Get the probability of passing for test A with 8.6 hours of study and test B with 4.7 hours of study.
```python
# Set value in array
value_A = np.asarray(8.6).reshape(-1,1)
# Probability of passing test A with 8.6 hours of study
print("The probability of passing test A with 8.6 hours of study is ", model_A.predict_proba(value_A)[:,1])

# Set value in array
value_B = np.asarray(4.7).reshape(-1,1)
# Probability of passing test B with 4.7 hours of study
print("The probability of passing test B with 4.7 hours of study is ", model_B.predict_proba(value_B)[:,1])
```
```
The probability of passing test A with 8.6 hours of study is  [0.74226823]
The probability of passing test B with 4.7 hours of study is  [0.9400506]
```
#### Question 3
Calculate the hours you need to study to have 0.5 probability of passing the test using the formula -intercept/slope.
```python
# Print the hours required to have 0.5 probability on model_A
print("Minimum hours of study for test A are ", -model_A.intercept_/model_A.coef_)

# Print the hours required to have 0.5 probability on model_B
print("Minimum hours of study for test B are ", -model_B.intercept_/model_B.coef_)
```
```
Minimum hours of study for test A are  [[8.49401055]]
Minimum hours of study for test B are  [[4.5376007]]
```
#### Question 4
Calculate the joint probability of passing test A and test B.
```python
# Probability calculation for each value of study_hours
prob_passing_A = model_A.predict_proba(study_hours_A.reshape(-1,1))[:,1]
prob_passing_B = model_B.predict_proba(study_hours_B.reshape(-1,1))[:,1]

# Calculate the probability of passing both tests
prob_passing_A_and_B = prob_passing_A * prob_passing_B

# Maximum probability value
max_prob = max(prob_passing_A_and_B)

# Position where we get the maximum value
max_position = np.where(prob_passing_A_and_B == max_prob)[0][0]

# Study hours for each test
prt_msg1 = "Study {:1.0f} hours for the first and {:1.0f} hours for the second test"
prt_msg2 = " and you will pass both tests with {:01.2f} probability."
prt_msg = prt_msg1 + prt_msg2
print(prt_msg.format(study_hours_A[max_position], study_hours_B[max_position], max_prob))
```
```
Study 9 hours for the first and 5 hours for the second test and you will pass both tests with 0.99 probability.
```
