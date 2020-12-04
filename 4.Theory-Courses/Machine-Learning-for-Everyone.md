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

## `Chapter 3` Deep Learning

### Video: Deep Learning
### What is deep learning?
- Deep learning applications are everywhere. Think of Google translating large blocks of text in a matter of seconds or your phone's photo gallery automatically recognizing faces.
- Let's see how much you know about deep learning.
#### Question 1
- Here are various statements about deep learning. Some are true, some are false: drag the statements into the correct bucket.
```
You have to figure out the higher-level features yourself while training the data.
More complex problems like image classification can be solved much faster by deep learning than by traditional machine learning.
When there is lack of domain knowledge and you are not sure of the exact features that need to be used, you should use deep learning.
Deep learning is always preferred over traditional machine learning.
The number of neurons in a neural network is limited.
Deep learning  is a subfield of machine learning concerned with algorithms inspired by the structure and function of the brain called neural networks.
```
```
True
More complex problems like image classification can be solved much faster by deep learning than by traditional machine learning.
Deep learning  is a subfield of machine learning concerned with algorithms inspired by the structure and function of the brain called neural networks.
When there is lack of domain knowledge and you are not sure of the exact features that need to be used, you should use deep learning.

False
Deep learning is always preferred over traditional machine learning.
You have to figure out the higher-level features yourself while training the data.
The number of neurons in a neural network is limited.
```
#### Should I use deep learning?
- You work for a bank and want to help your company make smarter loans. You'd like to predict the probability of a borrower defaulting on a loan based on information in their application, such as their credit history, education level, income, and assets. This amount can then be used to determine the interest rate of the loan. You have hundreds of thousands of examples of loans from the past ten years.
- For now, you just want to build a proof of concept on your laptop showing that there is some value in building this model. The performance doesn't have to be perfect just yet.
- Based on this information, how should you solve this problem?
```
Deep Learning
Traditional machine learning
This is not a problem that can be solved with either
```
```
Traditional machine learning
```

### Video: Computer vision
### Image data
- Your friend just texted you an image. However, when you open the message the content seems to be distorted. No worries, you have access to a pre-trained neural network that can restore any image.
- Before you can pass the image to the neural network, it needs to be converted to numbers so that we have features to input. The image's resolution is 284 × 429 pixels. Remember, each color pixel is represented by three color channels (red, green, and blue).
#### Question 1
- How many features will be passed into the model for this color image?
```
121836
429
365508
```
```
365508
```
### The process
- In a bar you strike up a conversation with someone who turns out to be a data scientist at the self-driving car department of Tesla.
- They start talking about one of the deep learning models they built a while ago. It was able to classify images of vehicles as cars or trucks. You discuss the process and at the end of the conversation you have a pretty good idea of what happened.
#### Question 1
- Place the steps that happen inside a neural network in the right order.
```
Neurons will learn to detect shapes of vehicles
The car images are transformed to numbers
Neurons will learn to detect edges
The image is classified as a car or a truck
The pixel intensities are fed into a neural network
Neurons will learn to more complex objects like wheels, doors, and windows
```
```
The car images are transformed to numbers
The pixel intensities are fed into a neural network
Neurons will learn to detect edges
Neurons will learn to more complex objects like wheels, doors, and windows
Neurons will learn to detect shapes of vehicles
The image is classified as a car or a truck
```
### Recognizing handwritten digits
- Remember this from Chapter 1? As a reminder, there's a famous dataset called the MNIST that contains 70,000 images of handwritten digits from 0 to 9. On the right, we have a computer vision model trained on this dataset that attempts to recognize handwritten digits.
- For this exercise, we've added an extra dropdown where you can try different types of machine learning. The first two, logistic regression and random forest, are traditional machine learning models. As you've learned, the third, neural networks, is used in deep learning.
#### Question 1
- Try drawing some digits to see how well each model recognizes your handwriting. Which is the best performing machine learning model?
```
Logistic regression
Random forest
Neural networks
```
```
Neural networks
```

### Video: Natural Language Processing
### Sentiment analysis
- Sentiment Analysis is a Natural Language Processing methodology for quantifying how positive or negative the emotion expressed by a segment of text is. It is often used for automatically categorizing customer feedback messages or product reviews.
- Below are four reviews of the movie "The Last Jedi". You can paste them in the Sentiment Analyzer on the right.
#### Question 1
- Which review is scored as the most negative by the sentiment analysis algorithm?
```
I really agree with this comment "Great film, one of the best Star Wars films."
Worst star wars movie ever made. It disrespected the force and everything we love.
A fun exciting, visually striking movie with a great score, great characters, and great action. The Last Jedi is very well directed, but very messy.
This movie was a pointless, ugly, and plot-hole-riddled mess. All it served to do was crush all hope and destroy everything that remained of the Original Trilogy.
```
```
This movie was a pointless, ugly, and plot-hole-riddled mess. All it served to do was crush all hope and destroy everything that remained of the Original Trilogy.
```
### Classifying machine learning tasks
- By this point, you have seen a lot of different applications of machine learning. In this chapter, two special fields were discussed: computer vision and Natural Language Processing (NLP). Deep learning is particularly well-suited to solve these kinds of problems. Let's see if you can identify which use case belongs to which field.
#### Question 1
- Match each task with the correct machine learning field.
```
Predicting the temperature in New York tomorrow.
Searching for images on Google.
Clustering pre-paid telecom customers to identify patterns in terms of money spent in recharging, sending SMS, and browsing the internet.
Parsing all tweets about an artist's latest album to get a feeling for the sentiment toward it.
Google Home understanding that you have asked it to turn on the lights.
Building an application that takes pictures of all the items passing on a conveyor belt and detecting any defects.
```
```
Computer Vision
Searching for images on Google.
Building an application that takes pictures of all the items passing on a conveyor belt and detecting any defects.

NLP
Parsing all tweets about an artist's latest album to get a feeling for the sentiment toward it.
Google Home understanding that you have asked it to turn on the lights.

Traditional Machine Learning
Clustering pre-paid telecom customers to identify patterns in terms of money spent in recharging, sending SMS, and browsing the internet.
Predicting the temperature in New York tomorrow.
```
### Bag of words
- In the field of Natural Language Processing, n-grams are a foundational way to make features from text. n-grams count the sequence of words and n indicates how many word(s) a sequence contains. For example, 2-grams, count the occurrence of two-word sequences.
- In this exercise, you can input text and see what are the top 1-gram, 2-gram, and 3-gram features based on occurrence. If you're not sure what to enter, try some of these restaurant reviews:
```
The food was not great and the service could be faster.
I've seen a lot of bad reviews about this place, but it was not that bad. You get what you pay for!
```
#### Question 1
- Which of the following statements is true?
```
3-grams contain unnecessary information and should be eliminated in effort of dimensionality reduction.
You have to pick between 1-gram, 2-gram, and 3-gram when making your features. You can't use more than one.
As you increase the value of n, the occurrences of n-grams decreases.
```
```
As you increase the value of n, the occurrences of n-grams decreases.
```

### Video: Limits of machine learning
### To black box or not to black box?
- You are interested in machine learning applications in the health sector. You know that some of the tasks require a high accuracy but it's not that important to know what happens inside the model. Others require an Explainable AI approach because the rationale for each classification is important.
#### Question 1
- Sort each task into either the Black Box or Explainable AI category.
```
Extract information from medical journal articles.
Predict whether or not a nurse is likely to quit within the next month.
Classify images from mammograms as cancerous or non-cancerous.
Provide a list of likely diagnoses, given a set of facts about a patient.
```
```
Black Box
Classify images from mammograms as cancerous or non-cancerous.
Extract information from medical journal articles.
Explainable AI
Predict whether or not a nurse is likely to quit within the next month.
Provide a list of likely diagnoses, given a set of facts about a patient.
```
### Spotting bias in machine learning
- In the video, we learned about an AI-enabled recruiting software that preferred men because it learned from historical data when more men were hired. When we have models that affect peoples' lives, we need to carefully evaluate them for any discriminatory behavior that can be learned from historical data.
- On the right, you have a model that attempts to predict whether someone will default on their loan. You can break down the resulting predictions, by different features like demographics and employment status. Play around with these features and see if you can find anything suspicious about who is predicted to default and who isn't.
#### Question 1
- Which feature(s) should be investigated more for potential bias before deploying the model?
```
Race because there is a relatively large difference between African American/ Caucasian proportions in the "No" (32%/68%) and "Yes" (74%/26%) outcomes.
Job because there are a lot more people who are "skilled" in the "No" outcome than the "Yes" outcome.
Purpose because loans for "furniture/appliances" are more often predicted to not default.
```
```
Race because there is a relatively large difference between African American/ Caucasian proportions in the "No" (32%/68%) and "Yes" (74%/26%) outcomes.
```
