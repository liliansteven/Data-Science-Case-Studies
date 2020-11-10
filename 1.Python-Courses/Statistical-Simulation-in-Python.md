# [Statistical Simulation in Python](https://learn.datacamp.com/courses/statistical-simulation-in-python) `10H`

## Course Description
`Simulations are a class of computational algorithms that use the relatively simple idea of random sampling to solve increasingly complex problems. Although they have been around for ages, they have gained in popularity recently due to the rise in computational power and have seen applications in multiple domains including Artificial Intelligence, Physics, Computational Biology and Finance just to name a few. Students will use simulations to generate and analyze data over different probability distributions using the important NumPy package. This course will give students hands-on experience with simulations using simple, real-world applications.`

## `Chapter 1` Basics of randomness & simulation

### Video: Introduction to random variables
#### np.random.choice()
- In this exercise, you will be introduced to the np.random.choice() function. This is a remarkably useful function for simulations and you will be making extensive use of it later in the course. As a first step, let's try to understand the basics of this function. Using help(), figure out which of the following input parameters are not optional for the np.random.choice() function:
```
a - input array
size
p - probabilities
replace
```
```
a - input array
```
### Poisson random variable
- The numpy.random module also has a number of useful probability distributions for both discrete and continuous random variables. In this exercise, you will learn how to draw samples from a probability distribution.
- In particular, you will draw samples from a very important discrete probability distribution, the Poisson distribution, which is typically used for modeling the average rate at which events occur.
- Following the exercise, you should be able to apply these steps to any of the probability distributions found in numpy.random. In addition, you will also see how the sample mean changes as we draw more samples from a distribution.
#### Question 1
- Using np.random.poisson() draw samples from a Poisson distribution using lam (lambda) and size_1.
- Repeat the above step, but this time use size_2.
- For each of the above samples, calculate the absolute difference between their mean and lambda using np.mean() and abs().
```python
# Initialize seed and parameters
np.random.seed(123) 
lam, size_1, size_2 = 5, 3, 1000  

# Draw samples & calculate absolute difference between lambda and sample mean
samples_1 = np.random.poisson(lam, size_1)
samples_2 = np.random.poisson(lam, size_2)
answer_1 = abs(lam - samples_1.mean())
answer_2 = abs(lam - samples_2.mean()) 

print("|Lambda - sample mean| with {} samples is {} and with {} samples is {}. ".format(size_1, answer_1, size_2, answer_2))
```
```
|Lambda - sample mean| with 3 samples is 0.33333333333333304 and with 1000 samples is 0.07699999999999996. 
```
### Shuffling a deck of cards
- Often times we are interested in randomizing the order of a set of items. Consider a game of cards where you first shuffle the deck of cards or a game of scrabble where the letters are first mixed in a bag. As the final exercise of this section, you will learn another useful function - np.random.shuffle(). This function allows you to randomly shuffle a sequence in place. At the end of this exercise, you will know how to shuffle a deck of cards or any sequence of items.
- Examine deck_of_cards in the shell.
#### Question 1
- Use the np.random.shuffle() function to shuffle deck_of_cards.
- Select the top three cards from this list by slicing.
```python
# Shuffle the deck
np.random.shuffle(deck_of_cards) 

# Print out the top three cards
card_choices_after_shuffle = deck_of_cards[0:3]
print(card_choices_after_shuffle)
```
```
[('Diamond', 9), ('Spade', 9), ('Spade', 4)]
```

### Video: Simulation basics
### Throwing a fair die
- Once you grasp the basics of designing a simulation, you can apply it to any system or process. Next, we will learn how each step is implemented using some basic examples.
- As we have learned, simulation involves repeated random sampling. The first step then is to get one random sample. Once we have that, all we do is repeat the process multiple times. This exercise will focus on understanding how we get one random sample. We will study this in the context of throwing a fair six-sided die.
- By the end of this exercise, you will be familiar with how to implement the first two steps of running a simulation - defining a random variable and assigning probabilities.
- For the rest of the course, look to the IPython shell to find out what seed has been set.
#### Question 1
- Construct a six-sided die as a list of each of the possible outcomes and assign it to the variable die.
- Define the probability of each of the six sides having an equal chance of showing up and assign it to the variable probabilities.
- Finally, use np.random.choice() to simulate a single throw of the die and record its outcome in the outcome variable.
```python
# Define die outcomes and probabilities
die, probabilities, throws = [1,2,3,4,5,6], [1/6, 1/6, 1/6, 1/6, 1/6, 1/6], 1

# Use np.random.choice to throw the die once and record the outcome
outcome = np.random.choice(die, size=throws, p=probabilities)
print("Outcome of the throw: {}".format(outcome[0]))
```
```
Outcome of the throw: 5
```
### Throwing two fair dice
- We now know how to implement the first two steps of a simulation. Now let's implement the next step - defining the relationship between random variables.
- Often times, our simulation will involve not just one, but multiple random variables. Consider a game where you throw two dice and win if each die shows the same number. Here we have two random variables - the two dice - and a relationship between each of them - we win if they show the same number, lose if they don't. In reality, the relationship between random variables can be much more complex, especially when simulating things like weather patterns.
- By the end of this exercise, you will be familiar with how to implement the third step of running a simulation - defining relationships between random variables.
#### Question 1
- Set num_dice to 2.
- Complete the np.random.choice() function to throw two dice and record the outcomes in the outcomes variable.
- Fill in the Boolean condition to check if the two dice show the same number.
```python
# Initialize number of dice, simulate & record outcome
die, probabilities, num_dice = [1,2,3,4,5,6], [1/6, 1/6, 1/6, 1/6, 1/6, 1/6], 2
outcomes = np.random.choice(die, size=num_dice, p=probabilities) 

# Win if the two dice show the same number
if outcomes[0] == outcomes[1]:
    answer = 'win' 
else: 
    answer = 'lose'

print("The dice show {} and {}. You {}!".format(outcomes[0], outcomes[1], answer))
```
```
The dice show 5 and 5. You win!
```
### Simulating the dice game
- We now know how to implement the first three steps of a simulation. Now let's consider the next step - repeated random sampling.
- Simulating an outcome once doesn't tell us much about how often we can expect to see that outcome. In the case of the dice game from the previous exercise, it's great that we won once. But suppose we want to see how many times we can expect to win if we played this game multiple times, we need to repeat the random sampling process many times. Repeating the process of random sampling is helpful to understand and visualize inherent uncertainty and deciding next steps.
- Following this exercise, you will be familiar with implementing the fourth step of running a simulation - sampling repeatedly and generating outcomes.
#### Question 1
- Set sims to 100 repetitions and initialize wins to 0.
- Write a for loop to repeat throwing the dice.
- Set outcomes to the outcome of throwing two dice.
- If the two dice show the same number, increment wins by 1.
```python
# Initialize model parameters & simulate dice throw
die, probabilities, num_dice = [1,2,3,4,5,6], [1/6, 1/6, 1/6, 1/6, 1/6, 1/6], 2
sims, wins = 100, 0

for i in range(sims):
    outcomes = np.random.choice(die, size=num_dice, p=probabilities) 
    # Increment `wins` by 1 if the dice show same number
    if outcomes[0] == outcomes[1]:
        wins = wins + 1

print("In {} games, you win {} times".format(sims, wins))
```
```
In 100 games, you win 25 times
```

### Video: Using simulation for decision-making
### Simulating one lottery drawing
- In the last three exercises of this chapter, we will be bringing together everything you've learned so far. We will run a complete simulation, take a decision based on our observed outcomes, and learn to modify inputs to the simulation model.
- We will use simulations to figure out whether or not we want to buy a lottery ticket. Suppose you have the opportunity to buy a lottery ticket which gives you a shot at a grand prize of $10,000. Since there are 1000 tickets in total, your probability of winning is 1 in 1000. Each ticket costs $10. Let's use our understanding of basic simulations to first simulate one drawing of the lottery.
#### Question 1
- Define chance_of_winning as the probability of winning the lottery. Remember that 1 out of the total number of lottery tickets sold will win.
- Set the probability list to the probabilities of receiving corresponding gains using chance_of_winning.
- Use np.random.choice() to perform one simulation of this lottery drawing.
```python
# Pre-defined constant variables
lottery_ticket_cost, num_tickets, grand_prize = 10, 1000, 10000

# Probability of winning
chance_of_winning = 1/num_tickets

# Simulate a single drawing of the lottery
gains = [-lottery_ticket_cost, grand_prize-lottery_ticket_cost]
probability = [1-chance_of_winning, chance_of_winning]
outcome = np.random.choice(a=gains, size=1, p=probability, replace=True)

print("Outcome of one drawing of the lottery is {}".format(outcome))
```
```
Outcome of one drawing of the lottery is [-10]
```
### Should we buy?
- In the last exercise, we simulated the random drawing of the lottery ticket once. In this exercise, we complete the simulation process by repeating the process multiple times.
- Repeating the process gives us multiple outcomes. We can think of this as multiple universes where the same lottery drawing occurred. We can then determine the average winnings across all these universes. If the average winnings are greater than what we pay for the ticket then it makes sense to buy it, otherwise, we might not want to buy the ticket.
- This is typically how simulations are used for evaluating business investments. After completing this exercise, you will have the basic tools required to use simulations for decision-making.
#### Question 1
- Set the size parameter, which controls the number of simulations, to 2000.
- Set payoffs equal to a list containing how much you could lose and how much you could win.
- Set probs equal to a list of probabilities of losing and winning.
- Calculate the mean of outcomes and assign it to answer.
```python
# Initialize size and simulate outcome
lottery_ticket_cost, num_tickets, grand_prize = 10, 1000, 10000
chance_of_winning = 1/num_tickets
size = 2000
payoffs = [-lottery_ticket_cost, grand_prize-lottery_ticket_cost]
probs = [1-chance_of_winning, chance_of_winning]

outcomes = np.random.choice(a=payoffs, size=size, p=probs, replace=True)

# Mean of outcomes.
answer = outcomes.mean()
print("Average payoff from {} simulations = {}".format(size, answer))
```
```
Average payoff from 2000 simulations = -10.0
```
### Calculating a break-even lottery price
- Simulations allow us to ask more nuanced questions that might not necessarily have an easy analytical solution. Rather than solving a complex mathematical formula, we directly get multiple sample outcomes. We can run experiments by modifying inputs and studying how those changes impact the system. For example, once we have a moderately reasonable model of global weather patterns, we could evaluate the impact of increased greenhouse gas emissions.
- In the lottery example, we might want to know how expensive the ticket needs to be for it to not make sense to buy it. To understand this, we need to modify the ticket cost to see when the expected payoff is negative.
- grand_prize, num_tickets, and chance_of_winning are loaded in the environment.
#### Question 1
- Set sims to 3000 and the lottery_ticket_cost variable to 0.
- If the mean value of outcomes falls below 0, break out of the while loop.
- Else, increment lottery_ticket_cost by 1.
```python
# Initialize simulations and cost of ticket
sims, lottery_ticket_cost = 3000, 0

# Use a while loop to increment `lottery_ticket_cost` till average value of outcomes falls below zero
while 1:
    outcomes = np.random.choice([-lottery_ticket_cost, grand_prize-lottery_ticket_cost],
                 size=sims, p=[1-chance_of_winning, chance_of_winning], replace=True)
    if outcomes.mean() < 0:
        break
    else:
        lottery_ticket_cost += 1
answer = lottery_ticket_cost - 1

print("The highest price at which it makes sense to buy the ticket is {}".format(answer))
```
```
The highest price at which it makes sense to buy the ticket is 9
```
### Calculating a break-even lottery price
- Simulations allow us to ask more nuanced questions that might not necessarily have an easy analytical solution. Rather than solving a complex mathematical formula, we directly get multiple sample outcomes. We can run experiments by modifying inputs and studying how those changes impact the system. For example, once we have a moderately reasonable model of global weather patterns, we could evaluate the impact of increased greenhouse gas emissions.
- In the lottery example, we might want to know how expensive the ticket needs to be for it to not make sense to buy it. To understand this, we need to modify the ticket cost to see when the expected payoff is negative.
- grand_prize, num_tickets, and chance_of_winning are loaded in the environment.
#### Question 1
- Set sims to 3000 and the lottery_ticket_cost variable to 0.
- If the mean value of outcomes falls below 0, break out of the while loop.
- Else, increment lottery_ticket_cost by 1.
```python
# Initialize simulations and cost of ticket
sims, lottery_ticket_cost = 3000, 0

# Use a while loop to increment `lottery_ticket_cost` till average value of outcomes falls below zero
while 1:
    outcomes = np.random.choice([-lottery_ticket_cost, grand_prize-lottery_ticket_cost],
                 size=sims, p=[1-chance_of_winning, chance_of_winning], replace=True)
    if outcomes.mean() < 0:
        break
    else:
        lottery_ticket_cost += 1
answer = lottery_ticket_cost - 1

print("The highest price at which it makes sense to buy the ticket is {}".format(answer))
```
```
The highest price at which it makes sense to buy the ticket is 9
```

## `Chapter 2` Probability & data generation process

### Video: Probability basics
### Should we buy?
- In the last exercise, we simulated the random drawing of the lottery ticket once. In this exercise, we complete the simulation process by repeating the process multiple times.
- Repeating the process gives us multiple outcomes. We can think of this as multiple universes where the same lottery drawing occurred. We can then determine the average winnings across all these universes. If the average winnings are greater than what we pay for the ticket then it makes sense to buy it, otherwise, we might not want to buy the ticket.
- This is typically how simulations are used for evaluating business investments. After completing this exercise, you will have the basic tools required to use simulations for decision-making.
#### Question 1
- Set the size parameter, which controls the number of simulations, to 2000.
- Set payoffs equal to a list containing how much you could lose and how much you could win.
- Set probs equal to a list of probabilities of losing and winning.
- Calculate the mean of outcomes and assign it to answer.
```python
# Initialize size and simulate outcome
lottery_ticket_cost, num_tickets, grand_prize = 10, 1000, 10000
chance_of_winning = 1/num_tickets
size = 2000
payoffs = [-lottery_ticket_cost, grand_prize-lottery_ticket_cost]
probs = [1-chance_of_winning, chance_of_winning]

outcomes = np.random.choice(a=payoffs, size=size, p=probs, replace=True)

# Mean of outcomes.
answer = outcomes.mean()
print("Average payoff from {} simulations = {}".format(size, answer))
```
```
Average payoff from 2000 simulations = -10.0
```
### Calculating a break-even lottery price
- Simulations allow us to ask more nuanced questions that might not necessarily have an easy analytical solution. Rather than solving a complex mathematical formula, we directly get multiple sample outcomes. We can run experiments by modifying inputs and studying how those changes impact the system. For example, once we have a moderately reasonable model of global weather patterns, we could evaluate the impact of increased greenhouse gas emissions.
- In the lottery example, we might want to know how expensive the ticket needs to be for it to not make sense to buy it. To understand this, we need to modify the ticket cost to see when the expected payoff is negative.
- grand_prize, num_tickets, and chance_of_winning are loaded in the environment.
#### Question 1
- Set sims to 3000 and the lottery_ticket_cost variable to 0.
- If the mean value of outcomes falls below 0, break out of the while loop.
- Else, increment lottery_ticket_cost by 1.
```python
# Initialize simulations and cost of ticket
sims, lottery_ticket_cost = 3000, 0

# Use a while loop to increment `lottery_ticket_cost` till average value of outcomes falls below zero
while 1:
    outcomes = np.random.choice([-lottery_ticket_cost, grand_prize-lottery_ticket_cost],
                 size=sims, p=[1-chance_of_winning, chance_of_winning], replace=True)
    if outcomes.mean() < 0:
        break
    else:
        lottery_ticket_cost += 1
answer = lottery_ticket_cost - 1

print("The highest price at which it makes sense to buy the ticket is {}".format(answer))
```
```
The highest price at which it makes sense to buy the ticket is 9
```

### Video: Probability basics
#### Queen and spade
- In this example, you'll use the generalized probability formula P(A∪B)=P(A)+P(B)−P(A∩B) to calculate the probability of two events. Consider a deck of cards (13 cards x 4 suites = 52 cards in total). One card is drawn at random. What is the probability of getting a queen or a spade? Here event A is the card being a queen and event B is the card being a spade. Think carefully about whether the two events have anything in common.
```
17/52
16/52
15/52
18/52
```
```
16/52
```
### Two of a kind
- Now let's use simulation to estimate probabilities. Suppose you've been invited to a game of poker at your friend's home. In this variation of the game, you are dealt five cards and the player with the better hand wins. You will use a simulation to estimate the probabilities of getting certain hands. Let's work on estimating the probability of getting at least two of a kind. Two of a kind is when you get two cards of different suites but having the same numeric value (e.g., 2 of hearts, 2 of spades, and 3 other cards).
- By the end of this exercise, you will know how to use simulation to calculate probabilities for card games.
#### Question 1
- Deal the hand: In the for loop, shuffle deck_of_cards. We then select the first 5 cards as our hand.
- Count numeric values: Utilize the get() method to construct the dictionary cards_in_hand which counts the occurrence of each numeric_value in hand.
- Two of a kind? Check if the largest value in cards_in_hand is equal to or greater than 2 to see if we have at least two of a kind. If yes, we increment two_kind.
```python
# Shuffle deck & count card occurrences in the hand
n_sims, two_kind = 10000, 0
for i in range(n_sims):
    np.random.shuffle(deck_of_cards)
    hand, cards_in_hand = deck_of_cards[0:5], {}
    for [suite, numeric_value] in hand:
        # Count occurrences of each numeric value
        cards_in_hand[numeric_value] = cards_in_hand.get(numeric_value, 0) + 1
    
    # Condition for getting at least 2 of a kind
    if max(cards_in_hand.values()) >=2: 
        two_kind += 1

print("Probability of seeing at least two of a kind = {} ".format(two_kind/n_sims))
```
```
Probability of seeing at least two of a kind = 0.4952 
```
### Game of thirteen
- A famous French mathematician Pierre Raymond De Montmart, who was known for his work in combinatorics, proposed a simple game called as Game of Thirteen. You have a deck of 13 cards, each numbered from 1 through 13. Shuffle this deck and draw cards one by one. A coincidence is when the number on the card matches the order in which the card is drawn. For instance, if the 5th card you draw happens to be a 5, it's a coincidence. You win the game if you get through all the cards without any coincidences. Let's calculate the probability of winning at this game using simulation.
- By completing this exercise, you will further strengthen your ability to cast abstract problems into the simulation framework for estimating probabilities.
#### Question 3
- For each drawing, draw all the cards in deck without replacement and assign to draw.
- Check if there are any coincidences in the draw and, if there are, increment the coincidences counter by 1.
- Calculate winning probability as the fraction of games without any coincidences and use prob_of_winning to print your results.
```python
# Pre-set constant variables
deck, sims, coincidences = np.arange(1, 14), 10000, 0

for _ in range(sims):
    # Draw all the cards without replacement to simulate one game
    draw = np.random.choice(deck, size=13, replace=False) 
    # Check if there are any coincidences
    coincidence = (draw == list(np.arange(1, 14))).any()
    if coincidence == True:
        coincidences += 1

# Calculate probability of winning
prob_of_winning = 1-coincidences/sims
print("Probability of winning = {}".format(prob_of_winning))
```
```
Probability of winning = 0.36950000000000005
```

### Video: More probability concepts
### The conditional urn
- As we've learned, conditional probability is defined as the probability of an event given another event. To illustrate this concept, let's turn to an urn problem.
- We have an urn that contains 7 white and 6 black balls. Four balls are drawn at random. We'd like to know the probability that the first and third balls are white, while the second and the fourth balls are black.
- Upon completion, you will learn to manipulate simulations to calculate simple conditional probabilities.
#### Question 1
- Initialize the counter success to 0 and sims to 5000.
- Define a list, urn, with 7 white balls ('w') and 6 black balls ('b').
- Draw 4 balls without replacement and check to see if the first and third are white and second and fourth are black.
- Increment success if the above criterion is met.
```python
# Initialize success, sims and urn
success, sims = 0, 5000
urn = ['w']*7 + ['b']*6

for _ in range(sims):
    # Draw 4 balls without replacement
    draw = np.random.choice(urn, replace=False, size=4)
    # Count the number of successes
    if (draw[0] == 'w') & (draw[1] == 'b') & (draw[2] == 'w') & (draw[3] == 'b'):
        success +=1

print("Probability of success = {}".format(success/sims))
```
```
Probability of success = 0.0722
```
### Birthday problem
- Now we'll use simulation to solve a famous probability puzzle - the birthday problem. It sounds quite straightforward - How many people do you need in a room to ensure at least a 50% chance that two of them share the same birthday?
- With 366 people in a 365-day year, we are 100% sure that at least two have the same birthday, but we only need to be 50% sure. Simulation gives us an elegant way of solving this problem.
- Upon completion of this exercise, you will begin to understand how to cast problems in a simulation framework.
#### Question 1
- Initialize the sample space days which is an array from 1 to 365.
- Define a function birthday_sim() that takes one input people and returns the probability that at least two share the same birthday. Set size of draw to number of people.
```python
# Draw a sample of birthdays & check if each birthday is unique
days = np.arange(1,366)
people = 2

def birthday_sim(people):
    sims, unique_birthdays = 2000, 0 
    for _ in range(sims):
        draw = np.random.choice(days, size=people, replace=True) 
        if len(draw) == len(set(draw)): 
            unique_birthdays += 1
    out = 1 - unique_birthdays / sims
    return out
```
#### Question 2
Call birthday_sim() in a while loop and break when the probability is greater than 0.5.
```python
# Break out of the loop if probability greater than 0.5
while (people > 0):
    prop_bds = birthday_sim(people)
    if prop_bds > 0.5: 
        break
    people += 1

print("With {} people, there's a 50% chance that two share a birthday.".format(people))
```
```
With 23 people, there's a 50% chance that two share a birthday.
```
### Full house
- Let's return to our poker game. Last time, we calculated the probability of getting at least two of a kind. This time we are interested in a full house. A full house is when you get two cards of different suits that share the same numeric value and three other cards that have the same numeric value (e.g., 2 of hearts & spades, jacks of clubs, diamonds, & spades).
- Thus, a full house is the probability of getting exactly three of a kind conditional on getting exactly two of a kind of another value. Using the same code as before, modify the success condition to get the desired output. This exercise will teach you to estimate conditional probabilities in card games and build your foundation in framing abstract problems for simulation.
#### Question 1
- Shuffle deck_of_cards.
- Utilize a dictionary with .get() to count the number of occurrences of each card in the hand.
- Increment the counter full_house when there is a full house in the hand (2 of one kind, 3 of the other).
```python
#Shuffle deck & count card occurrences in the hand
n_sims, full_house, deck_of_cards = 50000, 0, deck.copy()
for i in range(n_sims):
    np.random.shuffle(deck_of_cards)
    hand, cards_in_hand = deck_of_cards[0:5], {}
    for card in hand:
        # Use .get() method to count occurrences of each card
        cards_in_hand[card[1]] = cards_in_hand.get(card[1], 0) + 1
        
    # Condition for getting full house
    condition = (max(cards_in_hand.values()) ==3) & (min(cards_in_hand.values())==2)
    if condition: 
        full_house += 1
print("Probability of seeing a full house = {}".format(full_house/n_sims))
```
```
Probability of seeing a full house = 0.0014
```

### Video: Data generating process
### Driving test
- Through the next exercises, we will learn how to build a data generating process (DGP) through progressively complex examples.
- In this exercise, you will simulate a very simple DGP. Suppose that you are about to take a driving test tomorrow. Based on your own practice and based on data you have gathered, you know that the probability of you passing the test is 90% when it's sunny and only 30% when it's raining. Your local weather station forecasts that there's a 40% chance of rain tomorrow. Based on this information, you want to know what is the probability of you passing the driving test tomorrow.
- This is a simple problem and can be solved analytically. Here, you will learn how to model a simple DGP and see how it can be used for simulation.
#### Question 1
- Write a function test_outcome().
- Set weather as 'rain' or 'sun' depending on the input argument p_rain (the probability of rain).
- Set the appropriate probabilities of 'pass' and 'fail' in test_result using weather & the dictionary p_pass.
```python
sims, outcomes, p_rain, p_pass = 1000, [], 0.40, {'sun':0.9, 'rain':0.3}

def test_outcome(p_rain):
    # Simulate whether it will rain or not
    weather = np.random.choice(['rain', 'sun'], p=[p_rain, 1-p_rain])
    # Simulate and return whether you will pass or fail
    test_result = np.random.choice(['pass', 'fail'], p=[p_pass[weather], 1-p_pass[weather]])
    return test_result
```
#### Question 2
- Now let's compute the probability of passing the test.
- First to count the number of times you pass using the collected results in outcomes.
- Use this to calculate pass_outcomes_frac as fraction of pass outcomes.
- Print pass_outcomes_frac.
```python
for _ in range(sims):
    outcomes.append(test_outcome(p_rain))

# Calculate fraction of outcomes where you pass
pass_outcomes_frac = sum([x == 'pass' for x in outcomes])/len(outcomes)
print("Probability of Passing the driving test = {}".format(pass_outcomes_frac))
```
```
Probability of Passing the driving test = 0.654
```
### National elections
- This exercise will give you a taste of how you can model a DGP at different levels of complexity.
- Consider national elections in a country with two political parties - Red and Blue. This country has 50 states and the party that wins the most states wins the elections. You have the probability p of Red winning in each individual state and want to know the probability of Red winning nationally.
- Let's model the DGP to understand the distribution. Suppose the election outcome in each state follows a binomial distribution with probability p such that 0 indicates a loss for Red and 1 indicates a win. We then simulate a number of election outcomes. Finally, we can ask rich questions like what is the probability of Red winning less than 45% of the states?
#### Question 1
- Simulate one election using np.random.binomial() with p = probs and n=1. Assign it to election.
- Append the average of Red's wins in election to outcomes.
- Calculate the fraction of outcomes where Red won less than 45% of the states. Save it as prob_red_wins and use it to print your results.
```python
outcomes, sims, probs = [], 1000, p

for _ in range(sims):
    # Simulate elections in the 50 states
    election = np.random.binomial(p=probs, n=1)
    # Get average of Red wins and add to `outcomes`
    outcomes.append(election.mean())

# Calculate probability of Red winning in less than 45% of the states
prob_red_wins = sum([(x < 0.45) for x in outcomes])/len(outcomes)
print("Probability of Red winning in less than 45% of the states = {}".format(prob_red_wins))
```
```
Probability of Red winning in less than 45% of the states = 0.196
```
### Fitness goals
- Let's model how activity levels impact weight loss using modern fitness trackers. On days when you go to the gym, you average around 15k steps, and around 5k steps otherwise. You go to the gym 40% of the time. Let's model the step counts in a day as a Poisson random variable with a mean λ dependent on whether or not you go to the gym.
- For simplicity, let’s say you have an 80% chance of losing 1lb and a 20% chance of gaining 1lb when you get more than 10k steps. The probabilities are reversed when you get less than 8k steps. Otherwise, there's an even chance of gaining or losing 1lb. Given all this information, find the probability of losing weight in a month.
#### Question 1
- Simulate steps as a Poisson random variable for a given day based on the value of lam.
- Set prob to [0.2, 0.8] if steps > 10000 or to [0.8, 0.2] if steps < 8000. Sum up all the weight lost or gained in a month stored in w.
- Calculate and print the fraction of simulations where total weight for a month in outcomes is less than 0. Save as weight_loss_outcomes_frac and use that to print your results.
```python
# Simulate steps & choose prob 
for _ in range(sims):
    w = []
    for i in range(days):
        lam = np.random.choice([5000, 15000], p=[0.6, 0.4], size=1)
        steps = np.random.poisson(lam)
        if steps > 10000: 
            prob = [0.2, 0.8]
        elif steps < 8000: 
            prob = [0.8, 0.2]
        else:
            prob = [0.5, 0.5]
        w.append(np.random.choice([1, -1], p=prob))
    outcomes.append(sum(w))

# Calculate fraction of outcomes where there was a weight loss
weight_loss_outcomes_frac = sum([x < 0 for x in outcomes])/len(outcomes)
print("Probability of Weight Loss = {}".format(weight_loss_outcomes_frac))
```
```
Probability of Weight Loss = 0.215
```

### Video: eCommerce Ad Simulation
### Sign up Flow
- We will now model the DGP of an eCommerce ad flow starting with sign-ups.
- On any day, we get many ad impressions, which can be modeled as Poisson random variables (RV). You are told that λ is normally distributed with a mean of 100k visitors and standard deviation 2000.
- During the signup journey, the customer sees an ad, decides whether or not to click, and then whether or not to signup. Thus both clicks and signups are binary, modeled using binomial RVs. What about probability p of success? Our current low-cost option gives us a click-through rate of 1% and a sign-up rate of 20%. A higher cost option could increase the clickthrough and signup rate by up to 20%, but we are unsure of the level of improvement, so we model it as a uniform RV.
#### Question 1
- Initialize ct_rate and su_rate dictionaries such that the high values are uniformly distributed between the low value and 1.2× the low value.
- Model impressions as a Poisson random variable with a mean value lam.
- Model clicks and signups as binomial random variables with n as impressions and clicks and p as ct_rate[cost] and su_rate[cost], respectively.
- We then print the simulated signups for the 'high' cost option.
```python
# Initialize click-through rate and signup rate dictionaries
ct_rate = {'low':0.01, 'high':np.random.uniform(low=0.01, high=1.2*0.01)}
su_rate = {'low':0.2, 'high':np.random.uniform(low=0.2, high=1.2*0.2)}

def get_signups(cost, ct_rate, su_rate, sims):
    lam = np.random.normal(loc=100000, scale=2000, size=sims)
    # Simulate impressions(poisson), clicks(binomial) and signups(binomial)
    impressions = np.random.poisson(lam=lam)
    clicks = np.random.binomial(impressions, p=ct_rate[cost])
    signups = np.random.binomial(clicks, p=su_rate[cost])
    return signups

print("Simulated Signups = {}".format(get_signups('high', ct_rate, su_rate, 1)))
```
```
Simulated Signups = [268]
```
### Purchase Flow
- After signups, let's model the revenue generation process. Once the customer has signed up, they decide whether or not to purchase - a natural candidate for a binomial RV. Let's assume that 10% of signups result in a purchase.
- Although customers can make many purchases, let's assume one purchase. The purchase value could be modeled by any continuous RV, but one nice candidate is the exponential RV. Suppose we know that purchase value per customer has averaged around $1000. We use this information to create the purchase_values RV. The revenue, then, is simply the sum of all purchase values.
- The variables ct_rate, su_rate and the function get_signups() from the last exercise are pre-loaded for you.
#### Question 1
- Model purchases as a binomial RV with p=0.1.
- Model purchase_values as an exponential RV scale=1000 and the appropriate size.
- Append rev with the sum of purchase_values.
```python
def get_revenue(signups):
    rev = []
    np.random.seed(123)
    for s in signups:
        # Model purchases as binomial, purchase_values as exponential
        purchases = np.random.binomial(s, p=0.1)
        purchase_values = np.random.exponential(scale=1000, size=purchases)
        
        # Append to revenue the sum of all purchase values.
        rev.append(purchase_values.sum())
    return rev

print("Simulated Revenue = ${}".format(get_revenue(get_signups('low', ct_rate, su_rate, 1))[0]))
```
```
Simulated Revenue = $22404.217742298042
```
### Probability of losing money
- In this exercise, we will use the DGP model to estimate probability.
- As seen earlier, this company has the option of spending extra money, let's say $3000, to redesign the ad. This could potentially get them higher clickthrough and signup rates, but this is not guaranteed. We would like to know whether or not to spend this extra $3000 by calculating the probability of losing money. In other words, the probability that the revenue from the high-cost option minus the revenue from the low-cost option is lesser than the cost.
- Once we have simulated revenue outcomes, we can ask a rich set of questions that might not have been accessible using traditional analytical methods.
- This simple yet powerful framework forms the basis of Bayesian methods for getting probabilities.
#### Question 1
- Initialize cost_diff, the difference between the 'high' and 'low' cost options, to 3000.
- Get the revenue for the high-cost option and assign it to rev_high.
- Calculate the fraction of times when rev_high - rev_low is less than cost_diff. Call it frac and use it to print your results.
```python
# Initialize sims
sims, cost_diff = 10000, 3000

# Get revenue when the cost is 'low' and when the cost is 'high'
rev_low = get_revenue(get_signups('low', ct_rate, su_rate, sims))
rev_high = get_revenue(get_signups('high', ct_rate, su_rate, sims))

# calculate fraction of times rev_high - rev_low is less than cost_diff
frac = sum([rev_high[i] - rev_low[i] < cost_diff for i in range(len(rev_low))])/len(rev_low)
print("Probability of losing money = {}".format(frac))
```
```
Probability of losing money = 0.4659
```

