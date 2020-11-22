<img align="right" width="100" height="100" src="https://github.com/cs-MohamedAyman/DataCamp-Tracks/blob/master/organizations-logos/theory.jpg">

# [Machine Learning for Everyone](https://learn.datacamp.com/courses/machine-learning-for-everyone) `10H`

## Course Description
`What's behind the machine learning hype? In this non-technical course, you’ll learn everything you’ve been too afraid to ask about machine learning. There’s no coding required. Hands-on exercises will help you get past the jargon and learn how this exciting technology powers everything from self-driving cars to your personal Amazon shopping suggestions. How does machine learning work, when can you use it, and what is the difference between AI and machine learning? They’re all covered. Gain skills in this hugely in-demand and influential field, and discover why machine learning is for everyone!`

## `Chapter 1` Let's start flipping coins

### Video: What is machine learning?
#### Recognizing handwritten digits
- In machine learning, there's a famous dataset called the MNIST database of handwritten digits. It contains 70,000 images of handwritten digits from 0 to 9. Many models have been made using this dataset to enable computer recognition of handwritten digits. We have one of those models right here for you!
- On the left-hand box, you can draw a digit (or something else!) and the model will try to infer the intended digit. On the right, you will see the model's output. To draw a digit, click on plot to start drawing, click again to pause. What does the model's output represent?
```
The probabilities that your drawing matches each digit.
The number of images for each digit.
```
```
The probabilities that your drawing matches each digit.
```
#### AI, data science, and machine learning walk into a bar...
- In the age of big data, AI, data science, and machine learning have become buzzwords that are often incorrectly used interchangeably. They are all related in some way but encompass a different range of methods and goals.
- Which of the following statements is FALSE?
```
Machine learning methods can be considered AI methods.
AI and data science share the same goal, but AI uses methods from computer science and data science uses methods from statistics.
Machine learning has become the most prominent subset of AI.
Machine learning is used in data science to make predictions.
```
```
AI and data science share the same goal, but AI uses methods from computer science and data science uses methods from statistics.
```
#### What's true about machine learning?
- As we saw in the video, there are a lot of headlines about machine learning. Always be cautious because some of it can be sensational. What is true about machine learning?
- Classify whether each statement is true or false.
```
To make predictions from a machine learning model, you need data
Machine learning's application is not limited to one type of problem or domain
Machine learning uses methods from computer science, statistics, and physics
Machine learning can only predict what will happen and not explain why something has happened
Machine learning finds patterns is existing data and applies it to new data
```
```
- True
To make predictions from a machine learning model, you need data
Machine learning's application is not limited to one type of problem or domain
Machine learning finds patterns is existing data and applies it to new data

- False
Machine learning uses methods from computer science, statistics, and physics
Machine learning can only predict what will happen and not explain why something has happened
```

### Video: Machine learning concepts
#### Machine learning lingo
- You overhear a group of data scientists discussing their latest machine learning project on predicting whether a tweet is fake or not. Twitter has provided them with a labeled dataset in hopes of improving their spam detection system.
- Here are two observations from the dataset:
- <image>
- Based on this information, classify aspects of their training data as either a feature, label, or target variable.
- Drop each card in the appropriate category.
```
Fake
Number of Twitter followers
Number of likes
Tweet text
True
False
```
```
- Feature
Number of likes
Tweet text
Number of Twitter followers

- Label
True
False

- Target Variable
Fake
```
#### Supervised vs unsupervised
- Have you heard of open data? These are datasets that are freely available and governments especially have been pushing initiatives for open public data. For example, here is a snippet of a dataset from California's Open Data portal that looks at educational attainment (i.e., highest degree of education) and personal income.
- Each row represents a Californian citizen. It contains the year the citizen completed the survey and the citizen's age, gender, educational attainment, and population count of where they live.
- Which of the statements below incorrectly uses the term unsupervised or supervised learning?
```
Train a unsupervised machine learning model to predict a citizen's educational attainment level.
Train a supervised machine learning model to predict personal income with the remaining columns as features.
Use unsupervised learning to segment "no-income" citizens into clusters to try to discover different reasons why someone may be receiving no income.
```
```
Train a unsupervised machine learning model to predict a citizen's educational attainment level.
```

### Video: Machine learning workflow
### Steps for building a model
- Machine learning is integrated in many of the technologies we use everyday. For example, have you noticed that platforms will have personalized recommendations, whether it's another funny video on Youtube or a book by your favorite author on Amazon? These are "recommender systems" and they typically consist of a machine learning model trained on a user's browsing history.
- Imagine the recommender system of your favorite online clothing store. They have data on all the clothes you've viewed and the clothes you ended up buying. This is enough to make a model to output personalized clothing recommendation for you. On the right are tasks to create this model, however, they are incorrectly ordered.
#### Question 1
- Correctly order the tasks.
```
- Train the model using the train dataset and a logistic regression model
- Extract the features for each product in the shop, including brand, number of times viewed, cost, color, and clothing type.
- Evaluate the precentage of products in the test dataset that were accurately predicted as bought
- Split the dataset into 2/3 and 1/3 for the train and test dataset, respectively
```
```
- Extract the features for each product in the shop, including brand, number of times viewed, cost, color, and clothing type.
- Split the dataset into 2/3 and 1/3 for the train and test dataset, respectively
- Train the model using the train dataset and a logistic regression model
- Evaluate the precentage of products in the test dataset that were accurately predicted as bought
```
#### A true step
- Below are four statements about each of the steps in the machine learning workflow. Which of them is true?
```
Extract features: Raw data usually comes organized with features so this step doesn't take much time.
Split dataset: It's important to split the dataset in case one set is lost.
Train model: There are many machine learning models to choose from.
Evaluate: This step happens once.
```
```
Train model: There are many machine learning models to choose from.
```

## `Chapter 2` Machine Learning Models

### Video: Supervised learning
#### Warm up
- What are the two flavors of supervised learning?
```
Features and targets
Carrot and stick
Classification and regression
Training and testing
```
```
Classification and regression
```
### Regressing with class
- You know there are two flavors of supervised learning: classification and regression. Let's see if you can distinguish between these two types of problems.
#### Question 1
- Classify the problems on the right as classification or regression.
```
Based on chemical features (alcohol, pH, chlorides...), predict whether a wine is red, white, or rose.
Based on chemical features (alcohol, pH, chlorides...), predict the price of a wine.
Based on song features (length, key, loudness, tempo...), predict a song's genre.
Based on employee's attributes (seniority, income, department, distance from home...), predict how long until an employee looks for another job.
Based on people's attributes (level of education, area, job title, age...), predict their income.
Based on space object attributes (discovery method, orbit, inclination, mass), predict whether this object is an exoplanet or not.
```
```
Classification
Based on chemical features (alcohol, pH, chlorides...), predict whether a wine is red, white, or rose.
Based on space object attributes (discovery method, orbit, inclination, mass), predict whether this object is an exoplanet or not.
Based on song features (length, key, loudness, tempo...), predict a song's genre.

Regression
Based on chemical features (alcohol, pH, chlorides...), predict the price of a wine.
Based on people's attributes (level of education, area, job title, age...), predict their income.
Based on employee's attributes (seniority, income, department, distance from home...), predict how long until an employee looks for another job.
```

### Video: Unsupervised learning
### We don't need no supervision
- You now know about supervised and unsupervised learning. Let's see if you can distinguish them.
#### Question 1
- Some use cases are presented on the right. Decide if they require a supervised or unsupervised approach and drag them in the correct bucket.
```
Based on email information (sender, topic...), find groups of emails by theme.
Based on customer information (sign up date, ordering frequency, age, marital status), predict their yearly spending amount.
Based on customer information (sign up date, ordering frequency, age, marital status, spending income), find segments of customers.
Based on stock information (open value, highest value, lowest value, close value for each day), predict its future value.
Based on customer's purchase history, find which items they are likely to be interested in next.
Based on email features (sender, topic, ratio of uppercased letter, proportion of money term). predict if an email is spam or not.
```
```
Supervised
Based on customer information (sign up date, ordering frequency, age, marital status), predict their yearly spending amount.
Based on email features (sender, topic, ratio of uppercased letter, proportion of money term). predict if an email is spam or not.
Based on stock information (open value, highest value, lowest value, close value for each day), predict its future value.

Unsupervised
Based on customer information (sign up date, ordering frequency, age, marital status, spending income), find segments of customers.
Based on customer's purchase history, find which items they are likely to be interested in next.
Based on email information (sender, topic...), find groups of emails by theme.
```
### Gotta cluster 'em all!
- Pokemon Go is a popular mobile game where users find, capture, and train virtual Pokemon characters. These characters are scattered throughout real locations and users have to physically travel to find these characters. Pokemon Go users can battle other users at Pokemon Gyms, which are physical locations with high traffic.
- On the right, reported Pokemon sightings in downtown Perth have been plotted according to longitude and latitude. Using clustering and this sighting data, you need to help decide where gyms should open up in downtown Perth.
- According to these sightings, how many gyms do you think should be opened up in downtown Perth?
#### Question 1
```
Seven gyms should be opened.
There's not enough information to decide.
Four gyms should be opened.
```
```
There's not enough information to decide.
```

### Video: Evaluating performance
### True or False?
- You just learned how to evaluate your model's performance, and how doing so differs depending on the nature of the problem. Let's check if everything is clear.
#### Question 1
- There are some statements on the right. Assess whether they are True or False.
```
A False Negative is a value that was predicted as positive, when it's actually negative.
Confusion matrices are used to evaluate classification preformance.
Accuracy is always an informative and useful metric.
Assessing an unsupervised learning model's performance is trickier and depends on your original objectives.
A False Positive is a value that was predicted as positive, when it's actually negative.
```
```
True
Confusion matrices are used to evaluate classification preformance.
Assessing an unsupervised learning model's performance is trickier and depends on your original objectives.
A False Positive is a value that was predicted as positive, when it's actually negative.

False
Accuracy is always an informative and useful metric.
A False Negative is a value that was predicted as positive, when it's actually negative.
```
#### Land of confusion
- Your colleague comes to you with the predictions of a model that predicts whether a bank customer will default on their loan or not. They started filling out the matrix, but they got confused about what goes where.
- Can you help your colleague finish their confusion matrix?
```
There are 3 false positives.
There are 4 false positives.
There are 2 false positives.
```
```
There are 2 false positives.
```

### Video: Improving performance
### It's a long way to the top
- As you've seen, there are several ways to improve your model's performance. We focused on hyperparameter tuning, dimensionality reduction and ensemble methods.
#### Question 1
- On the right, you can see some examples of actions you can take to improve a model. Are these actions hyperparameter tuning, dimensionality reduction, or ensemble methods?
```
Use the average prediction from a Linear Regression, a K-Means and a Decision Tree model to assign a category to an observation.
On a dataset of running sessions to assess a treadmill's longevity, with duration, speed, inclination, remove the column calories_burned.
While training a Decision Tree, change the minimum count of observations for what constitutes a branch.
Run an analysis to identify the four main features that give the best predictions, and get rid of the others.
Use the most common prediction from an SVM, a K-Means and a Decision Tree model to assign a category to an observation.
Write a script to try 3 different values of three different hyperparameters of your SVM, and keep the configuration that yields the best results.
```
```
Hyperparameter Tuning
While training a Decision Tree, change the minimum count of observations for what constitutes a branch.
Write a script to try 3 different values of three different hyperparameters of your SVM, and keep the configuration that yields the best results.

Dimensionality Reduction
On a dataset of running sessions to assess a treadmill's longevity, with duration, speed, inclination, remove the column calories_burned.
Run an analysis to identify the four main features that give the best predictions, and get rid of the others.

Ensemble Methods
Use the most common prediction from an SVM, a K-Means and a Decision Tree model to assign a category to an observation.
Use the average prediction from a Linear Regression, a K-Means and a Decision Tree model to assign a category to an observation.
```
### Explore hyperparameter tuning
- hyperparameter is a model parameter that is chosen by you before training begins. (This is in contrast to parameters, which are determined by the model training.) The hyperparameters available to set differ between types of model.
- Here you see the results of a gradient boosting models (GBMs) that tries to predict whether or not people will vote in an election. GBMs are a type of ensemble model that create lots of regression trees. Hyperparameters for GBMs include the number of trees to generate, the complexity of each tree, and the learning rate (how much weight is given to each tree).
- It's usually impossible to know which combination of hyperparameters will result in the best performing model, so you have to try lots of combinations of them.
- Use the dashboard controls to change hyperparameters and find the combination that gives the highest accuracy.
#### Question 1
```
200 trees, 2 levels of complexity, learning rate 0.01
100 trees, 6 levels of complexity, learning rate 0.01
100 trees, 4 levels of complexity, learning rate 0.1
150 trees, 6 levels of complexity, learning rate 0.1
```
```
100 trees, 6 levels of complexity, learning rate 0.01
```
