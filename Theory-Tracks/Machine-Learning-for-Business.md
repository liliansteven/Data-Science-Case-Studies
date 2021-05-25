<img align="right" width="100" height="100" src="https://github.com/cs-MohamedAyman/DataCamp-Tracks/blob/master/organizations-logos/theory.jpg">

# [Machine Learning for Business](https://learn.datacamp.com/courses/machine-learning-for-business) `10H`

## Course Description
`This course will introduce the key elements of machine learning to the business leaders. We will focus on the key insights and base practices how to structure business questions as modeling projects with the machine learning teams. You will understand the different types of models, what kind of business questions they help answer, or what kind of opportunities they can uncover, also learn to identify situations where machine learning should NOT be applied, which is equally important. You will understand the difference between inference and prediction, predicting probability and amounts, and how using unsupervised learning can help build meaningful customer segmentation strategy.`

## `Chapter 1` Machine learning and data use cases

### Video: Machine learning and data pyramid
#### Terminology clarification
- With all the hype and new phrases being invented each day, it's easy to get lost and misuse some of the terms, adding to the already complex field of machine learning. Identify which of the statements about machine learning and data needs below are incorrect.
```
When machine learning models are prototyped, the teams run experiments to make sure the model is working as intended.
Machine Learning can be done at any point in the data pyramid as its algorithmic power can overcome challenges with data quality.
Machine learning and other data analytics methods will deliver incorrect conclusions if the underlying data is incorrect.
```
```
Machine Learning can be done at any point in the data pyramid as its algorithmic power can overcome challenges with data quality.
```
### Order data pyramid needs
- The data pyramid represents how value gets created with data, and how to ensure there are no gaps in the process. It's important for business leaders to understand which needs should be met first and which later, and structure their organization's data resources accordingly. In this exercise, you will order the needs. What happens first (foundational needs) should be at the bottom, and what happens last (the most advanced analytic methods) should be at the top, just like you saw in the video.
#### Question 1
- Order the needs from the foundational (bottom of the pyramid) to most advanced (top of the pyramid).
```
Analysis
Collection
Preparation & Cleaning
Machine Learning in production
Storage
Prototyping & Testing ML
```
```
Machine Learning in production
Prototyping & Testing ML
Analysis
Preparation & Cleaning
Storage
Collection
```
### Match tasks in data pyramid
- Once a company starts working on their data and analytics roadmap, it's important to understand where these tasks fall within the data needs pyramid, and how many projects there are in different areas. In this exercise, you should match the tasks with the right place in the data needs pyramid.
#### Question 1
- Match the tasks with the right place in the data needs pyramid.
```
Build a weekly customer purchase dashboard broken down by geography and product type.
Analyze customer trends by looking into more granular data points on a customer cohort level and a series of comparative charts.
Build an automated risk scoring model in electronic banking system.
Build a simple churn prediction model and work with a marketing team to test if customers at risk could be saved with certain incentives.
Run an A/B test of three different email templatees to compare customer engagement with each and pick up the most effective version.
Deploy a machine learning model predicting customer purchases into company's CRM system.
```
```
Machine Learning in production
Build an automated risk scoring model in electronic banking system.
Deploy a machine learning model predicting customer purchases into company's CRM system.
Prototyping & Testing ML
Build a simple churn prediction model and work with a marketing team to test if customers at risk could be saved with certain incentives.
Run an A/B test of three different email templatees to compare customer engagement with each and pick up the most effective version.
Analysis
Build a weekly customer purchase dashboard broken down by geography and product type.
Analyze customer trends by looking into more granular data points on a customer cohort level and a series of comparative charts.
```

### Video: Machine learning principles
#### Modeling types
- There are many differences between supervised and unsupervised machine learning types, and it's important to understand how each can be used in a business setting. Review the following statements about supervised and unsupervised machine learning types and identify which one is correct.
```
Unsupervised learning uses input features to learn patterns and predict the target variable.
Supervised learning uses input features to learn patterns and predict the target variable.
Both supervised and unsupervised learning use input features to learn patterns and predict the target variable.
Target variable is only used in the Data Analysis stage, Machine Learning only works with input features.
```
```
Supervised learning uses input features to learn patterns and predict the target variable.
```
### Find supervised and unsupervised cases
- Supervised and unsupervised machine learning have many use cases in different industries, it's important to understand whether a project belongs to a certain machine learning type. Why is it relevant to a business leader? Because there's a fundamental difference between prediction (supervised) and pattern discovery / clustering (unsupervised) and this will help understanding the expected usage of the project and manage expectations.
#### Question 1
- Assign each of the provided machine learning use case to the correct machine learning type.
```
Group products together based on which are purchased together to inform company's bundling and cross-selling strategy
Predict which customers are likely to purchase an insurance next month
Build customer segmentation to customize marketing and slaes communication
Identify which marketing communications were the most impactful to customers purchasing insurance
Predict which machines in a factory are likely to break and need maintenance
```
```
Supervised machine learning
Predict which customers are likely to purchase an insurance next month
Identify which marketing communications were the most impactful to customers purchasing insurance
Predict which machines in a factory are likely to break and need maintenance
Unsupervised machine learning
Build customer segmentation to customize marketing and slaes communication
Group products together based on which are purchased together to inform company's bundling and cross-selling strategy
```

### Video: Job roles, tools and technologies
#### Job role responsibilities
- In any company, it's very important to hire the right people to work on the existing data needs to make sure their skills and motivations are aligned with the company's data maturity and goals. In this exercise, you will review several data needs and business situations, and will identify which decision is incorrect.
```
Julie is building a centralized data organization for a food delivery start-up. She knows the data is not well captured, so she will hire more people in the infrastructure team and data engineers to build stable data pipelines, and make sure data is flowing and can be used.
Data scientists at the Company ABC have tested a series of prototype models with A/B tests on their website and want to productize the models that worked. They plan to hire machine learning engineers and work closely with the website engineering team to build a machine learning targeting solution based on the findings by the data scientists.
A data analyst at a manufacturing company has spotted weird outlier data points in the readings from the machine sensors. He shared the results with the leadership and their decision is to build a machine learning model right away that will identify any outliers automatically in the operating system of the manufacturing machines and send a signal to the employees operating it.
```
```
A data analyst at a manufacturing company has spotted weird outlier data points in the readings from the machine sensors. He shared the results with the leadership and their decision is to build a machine learning model right away that will identify any outliers automatically in the operating system of the manufacturing machines and send a signal to the employees operating it.
```
### Match data projects with job roles
- Imagine you are building an analytics, engineering, data science and machine learning organization at a large bank with functional managers reporting to you. You have to review the project roadmap to make sure each different function gets the right financing.
#### Question 1
- Review each roadmap project and match it with a job role that should own it.
```
Design a customer risk scoring algorithm from scratch and deploy it on a banking app in real time.
Prototype a machine learning model on a laptop and present results to the bsuiness.
Build a sales dashboard.
Re-write prototype machine learning model into production code and deploy into company's customer facing website.
Create an ad-hoc analysis comparing year over year performance of different business units.
Design an experiment and run A/B test with the fraud prevention team in a bank.
```
```
Data Analyst
Build a sales dashboard.
Create an ad-hoc analysis comparing year over year performance of different business units.
Data Scientist
Prototype a machine learning model on a laptop and present results to the bsuiness.
Design an experiment and run A/B test with the fraud prevention team in a bank.
Machine Learning Engineer
Re-write prototype machine learning model into production code and deploy into company's customer facing website.
Design a customer risk scoring algorithm from scratch and deploy it on a banking app in real time.
```
### Team structure types
- While the data functions can be organized in many different ways, there are three fundamental operating models that the business can start with and adjust based on their corporate structure and business dynamics. In this exercise, you will review a certain data team structure, and identify if this is a centralized, decentralized or a hybrid model.
#### Question 1
- Assign each data team structure to the right model.
```
All data needs and functions are located in one team.
Each geography team owns their own independent data organization.
Critical infrastructure and data storage are owned by one team. Data is analyzed, models prototyped and deployed by different units independently.
Each office have hired their own data analysis and scientists who depend on the central data infrastructure and databases for their data access needs.
Each product department has built their own data collection, storage, preparation, analysis and modeling team.
There is one large department running all data operations and needs for the company.
```
```
Centralized
All data needs and functions are located in one team.
There is one large department running all data operations and needs for the company.
Decentralized
Each geography team owns their own independent data organization.
Each product department has built their own data collection, storage, preparation, analysis and modeling team.
Hybrid
Critical infrastructure and data storage are owned by one team. Data is analyzed, models prototyped and deployed by different units independently.
Each office have hired their own data analysis and scientists who depend on the central data infrastructure and databases for their data access needs.
```

## `Chapter 2` Machine learning types

### Video: Prediction vs. inference dilemma
#### Inference and prediction differences
- The difference between inference and prediction models is mostly in the way the business question or hypothesis is phrased. It's also important to understand the pros and cons of each. There is a trade-off between accuracy and interpretability: some models are easy to understand but do not have optimal predictions; others have excellent predictions but it's unclear how they got there. Below are several statements about the inference and prediction focused models. Select the one that is NOT correct.
```
Inference models are also called causal models.
Prediction models focus on getting the best prediction, no matter the model interpretation.
Inference models are less accurate than prediction machine learning models.
Inference models are more accurate than prediction machine learning models.
```
```
Inference models are more accurate than prediction machine learning models.
```
### Identify inference vs. prediction use cases
- You've learned about the inference vs. prediction dilemma - business leaders do not have to know the algorithmic nuances of the models, but defining the business questions correctly will guide the science team to correctly frame the modeling strategy. Now, you will identify which of these business questions are more likely to be a candidate for an inference (or causal) model, or instead a prediction model.
#### Question 1
- Review each business question and move them to either the "Inference" or "Prediction" bucket.
```
What are the main drivers of high customer satisfaction?
Which of these customers are likely to spend the most in the next 12 months?
Which gaming behaviors are the most predictive of the next month gaming hours?
Which of these transactions are most likely to be fraud?
What are the main indicators of transaction's probability to be fraudulent?
Which of these banknotes are likely to be counterfeit?
```
```
Inference (Causal)
What are the main drivers of high customer satisfaction?
Which gaming behaviors are the most predictive of the next month gaming hours?
What are the main indicators of transaction's probability to be fraudulent?
Prediction
Which of these customers are likely to spend the most in the next 12 months?
Which of these transactions are most likely to be fraud?
Which of these banknotes are likely to be counterfeit?
```

### Video: Inference (causal) models
#### Experiments and causal models
- In the video, we have discussed the importance of experiments such as website or email A/B tests and the role they play when assessing the need of causal models. Read the statements below and identify which of these is incorrect.
```
Whenever possible, causal models are preferred over experiments.
Whenever possible, experiments are preferred over causal models.
Causal models are used when running experiments are not possible e.g. unethical, illegal, or too expensive.
```
```
Whenever possible, causal models are preferred over experiments.
```
### Identify non actionable variables
- Rosie’s machine learning team has deployed a machine learning model on an insurance company’s website. It predicts a purchase probability for a certain insurance type for each customer. Then, the customized recommended product with the highest probability for each customer is shown on the homepage.
- The website team started running AB tests and didn't see any sales increase in the customer group with machine learned recommendation compared with the group that only has generic messages on the main website. Rosie asked to review the model, and provide insights into what are the key driving variables, and how the model was designed.
- In the inferential models, it is important to use variables which the business can affect and has impact on versus the ones that are just correlated but are not useful.
- <image>
#### Question 1
- What conclusion can you draw based on the most impactful variables? Select the most important one.
```
We need to aggressively promote insurance descriptions page visits since they are positively impacting the chances that the customer will buy insurance
The most impactful variables are highly correlated with the desired outcome (interest in a product leads to product purchase) but they are not actionable. The machine learning model needs to be rebuilt using actionable inputs that the business can impact
Weekly behavior is more important than monthly - change the frequency of the product promotional newsletter from monthly to weekly
Nothing, we can’t do anything since the customers are finding the products themselves
```
```
The most impactful variables are highly correlated with the desired outcome (interest in a product leads to product purchase) but they are not actionable. The machine learning model needs to be rebuilt using actionable inputs that the business can impact
```

### Video: Prediction models (supervised learning)
#### Supervised modeling principles
- You have learned the fundamental principles of supervised machine learning models. Now you will read a list of several statements about supervised learning and find one that is incorrect.
```
Supervised machine learning uses inputs features to discover outliers.
Supervised machine learning uses input features to predict the probability of belonging to a certain discrete class.
Supervised machine learning uses input features to predict the amount of a certain outcome.
```
```
Supervised machine learning uses inputs features to discover outliers.
```
### Identify classification and regression models
- You know that supervised machine learning has two types - classification and regression. While the underlying supervised learning principles are the same, they produce different outcomes. Here, you will be presented with a number of machine learning use cases, and try to identify if this is a classification or regression.
#### Question 1
- For each of the machine learning use case - identify if it belongs to classification or regression supervised learning.
```
A car manufacturer wants to use sensor data to identify which of the parts in the production line are potentially faculty and need manual inspection.
A gaming company wants to predict how much time each gamer will likely spend playing video games in the next month.
An online toy shop wants to predict which customers are likely to buy a bike next month.
A bank wants to predict how much money will the customers spend on different services in the next year.
```
```
Classification
An online toy shop wants to predict which customers are likely to buy a bike next month.
A car manufacturer wants to use sensor data to identify which of the parts in the production line are potentially faculty and need manual inspection.
Regression
A gaming company wants to predict how much time each gamer will likely spend playing video games in the next month.
A bank wants to predict how much money will the customers spend on different services in the next year.
```

### Video: Prediction models (unsupervised learning)
#### Unsupervised modeling use cases
- You have reviewed the key principles to unsupervised learning and have gone through a specific example of customer segmentation. In this exercise, you will read a list of statements about unsupervised machine learning and identify which of them is correct.
```
Unsupervised learning is used to predict the probability of an event e.g. whether a machine in a factory will break
Unsupervised learning is used to predict the amount of an outcome e.g. number of purchases next month
Unsupervised learning is used to understand the causal relationship and its strength of input features on the outcome variable
Unsupervised learning is used to identify patterns in data, build clusters or detect outliers
```
```
Unsupervised learning is used to identify patterns in data, build clusters or detect outliers
```
### Classification, regression or unsupervised models
- Now you know a lot about different types of machine learning models. In this case you will see a number of machine learning examples, formulated as a business question or a need e.g. "I want to predict potato prices next month", and will identify if this it belongs with a classification, regression or unsupervised learning.
#### Question 1
- Classify the examples on the right as classification, regression or unsupervised learning problems.
```
Predict our product demand for the next month.
Predict what is the object in the uploaded picture - human, car, animal or other.
Group our customers based on the similarity of their purchasing patterns.
Predict agricultural raw material prices to inform our pricing decisions.
Identify which customers are likely to click on this banner.
Group our products together based on sensor readings, then flag outlier items which don't fall within any cluster for manual inspection.
```
```
Classification
Identify which customers are likely to click on this banner.
Predict what is the object in the uploaded picture - human, car, animal or other.
Regression
Predict our product demand for the next month.
Predict agricultural raw material prices to inform our pricing decisions.
Unsupervised learning
Group our customers based on the similarity of their purchasing patterns.
Group our products together based on sensor readings, then flag outlier items which don't fall within any cluster for manual inspection.
```

## `Chapter 3` Business requirements and model design

### Video: Business requirements
### Identify situation, opportunity and action
- When scoping out the business requirements for machine learning project, it's very important to follow the right steps. Here, you're presented with a list of statements. You need to match them with different topics of the business requirement scoping process.
#### Question 1
- Match the statements with different topics of the business requirement scoping process.
```
The company started seeing much lower click through rate of its promotion emails.
Increase the engagement and the click through rate of the emails from 2.5% to the previous levels of 5%.
Run a series of AB tests targeting customers with relevant email content based on machine learning predicted product interest.
Reduce the time-to-answer customer requests back to previous levels and potentially even lower.
Build a machine learning solution to guide customers requests with step-by-step customer chat and call process automation.
The number of customer service requests has increased by over 300% driving the time-to-answer up and resulting in more escalations.
```
```
Business situation
The company started seeing much lower click through rate of its promotion emails.
The number of customer service requests has increased by over 300% driving the time-to-answer up and resulting in more escalations.
Business opportunity
Increase the engagement and the click through rate of the emails from 2.5% to the previous levels of 5%.
Reduce the time-to-answer customer requests back to previous levels and potentially even lower.
Business action
Run a series of AB tests targeting customers with relevant email content based on machine learning predicted product interest.
Build a machine learning solution to guide customers requests with step-by-step customer chat and call process automation.
```
#### Identify successful experiments
- Machine learning (ML) outputs have to be tested through experiments in order to make sure the identified opportunity can be achieved. Below you will find a list of three ML initiatives, business scope and their test results. Identify which one has NOT reached the expected opportunity and should NOT be scaled up as the standard way of operating?
```
A manufacturing company has experienced a surge in returns of faulty products from 2% to 5% of total sales. They built a machine learning model to predict faulty items and started manually inspecting them. This was rolled out in half of the products to test the effect. After 3 months, the returns have decreased to 2% for the products with ML, while remained 5% in the other product lines.
A bank has identified a growing number of defaults on credit cards over the last 12 months, going from the standard 7% to 11%. The bank has introduced a stricter application process and built an ML prediction to identify risky customers as one of the decision points in the application review. This was tested in half of the branches. After testing the new process, the default rates have started decreasing in the branches with ML solution while remaining unchanged in the rest.
A beauty products company started seeing a lower number of customers reaching their "Gold Status" which requires meeting certain level of annual spending and other criteria. The competition has been much more active lately. The company decided to build an ML model identifying potential "Gold Status" customers early after they joined the company, and giving them extra discounts, more focused customer service and other incentives. The company ran a test on half of its customers using ML prediction. The conversion rate to "Gold Status" has increased for all customers.
```
```
A beauty products company started seeing a lower number of customers reaching their "Gold Status" which requires meeting certain level of annual spending and other criteria. The competition has been much more active lately. The company decided to build an ML model identifying potential "Gold Status" customers early after they joined the company, and giving them extra discounts, more focused customer service and other incentives. The company ran a test on half of its customers using ML prediction. The conversion rate to "Gold Status" has increased for all customers.
```

### Video: Model training
#### Model training process
- Following the process to train machine learning models is extremely important to ensure the models are generalizable, and don't just memorize the patterns in the data for that specific sample. While the business leaders are not likely to be involved in the details, they will have to understand how the results were obtained, what the results mean, and how they should be interpreted. Which of these statements about the model training process and datasets is correct?
```
Model is built on the training dataset, then its performance is validated on the validation dataset, and finally on the test dataset.
Model is built on the training dataset, then its performance is validated on the test dataset, and finally on the validation dataset.
Training, validation and test datasets are chosen by the machine learning team manually to make sure the best data is in training, and the least accurate in validation and test.
```
```
Model is built on the training dataset, then its performance is validated on the validation dataset, and finally on the test dataset.
```
### Training, validation and test
- You can see a list of machine learning tasks on the right. Your task is to identify if they should be done on the training or test datasets.
#### Question 1
- Identify if these ML tasks should be done on the training or test datasets.
```
This dataset is used to train the model.
Once the final ML model is trained, its performance is measured on this dataset.
This is the last step in the ML process before reporting the final model performance metric.
This dataset contains input features and the target variable for the model to learn the patterns on (model training).
```
```
Training
This dataset is used to train the model.
This dataset contains input features and the target variable for the model to learn the patterns on (model training).
Test
Once the final ML model is trained, its performance is measured on this dataset.
This is the last step in the ML process before reporting the final model performance metric.
```

### Video: Model performance measurement
#### Poor performance examples
- For a business leader it is critical to understand how the model is performing, and where it fails to predict. There is a (in)famous saying about ML models - "All models are wrong but some are useful". The useful part is to understand how it can be leveraged to help the business optimize its operations. Here, you will review several model performance metrics with business conclusions and identify which statement is incorrect.
```
Churn prediction model correctly captures 90% of all churned customers (90% recall), yet it predicts most of the non-churned customers as churned - of all the customers predicted as churned only 5% actually are churners (5% precision). The business asks the ML team to update the model to reduce the number of false positives, as the cost to run any campaigns will be very high if it has to cover almost all customers.
A trading company is starting to use stock price prediction to make trading decisions. The percentage error rate is 25% which means on average the prediction is 25% different than the actual stock price. The traders are concerned. The company tests the model output as one of the rules in an automated rule-based trading system and sees uplift in the returns over the other non-ML rule-based trading system. Based on the positive results, the company is rolling out the prediction as one of the key signals for both the trading systems and the traders.
The manufacturing company wants to predict which items on its production line are faulty. The model is built and it identifies 50% of total faulty products (50% recall), and from the ones identified as faulty around 95% actually are (95% precision). The company decides to continue the manual process as identifying only half of faulty products is not going to help. They need 100% recall and 100% precision.
```
```
The manufacturing company wants to predict which items on its production line are faulty. The model is built and it identifies 50% of total faulty products (50% recall), and from the ones identified as faulty around 95% actually are (95% precision). The company decides to continue the manual process as identifying only half of faulty products is not going to help. They need 100% recall and 100% precision.
```
### Identify performance metrics
- Here you will be given a set of model performance metrics, and will have to identify what kind of performance metrics are they - precision (classification), recall (classification) or error (regression).
- CHEATSHEET: Precision measures how many of the predictions of that class turned out to be true. Recall measures how many of the total observations of that class the prediction was able to capture (or recall). Regression error calculates how far away the prediction is from the observed number.
#### Question 1
Identify what kind of performance metrics are these - precision (classification), recall (classification) or error (regression).
```
The stock price prediction model on average misses the actual stock price by 2.5 USD.
The model predicts a list of patients liekly to suffer from a second heart attack in the next 24 hours. 50% of the predicted patients actually did.
The weekly demand prediction model is on average wrong by 7% compared to the actual demand.
The model gives a list of customer likely to purchase. When the performance is measured, it captures 45% of all the customers that were going to buy.
Of all customers predicted likely to buy, 25% actually bought the product.
The model predict a list of patients likely to suffer from a second heart attack in the next 24 hours. It captures only 20% of all patients at risk.
```
```
Precision
Of all customers predicted likely to buy, 25% actually bought the product.
The model predicts a list of patients liekly to suffer from a second heart attack in the next 24 hours. 50% of the predicted patients actually did.
Recall
The model gives a list of customer likely to purchase. When the performance is measured, it captures 45% of all the customers that were going to buy.
The model predict a list of patients likely to suffer from a second heart attack in the next 24 hours. It captures only 20% of all patients at risk.
Error
The stock price prediction model on average misses the actual stock price by 2.5 USD.
The weekly demand prediction model is on average wrong by 7% compared to the actual demand.
```

### Video: Machine learning risks
#### Fixing non performing models
- Once the business runs a number of structured AB tests based on the machine learning predictions and gets negative results, it has to re-group and rethink the strategy again. Which of these is NOT the right action to take in such a situation?
```
Get more data.
Continue using the same machine learning predictions, because it is based on complex algorithms.
Run qualitative research e.g. surveys.
Change the scope of the problem.
```
```
Continue using the same machine learning predictions, because it is based on complex algorithms.
```
#### Non-actionable models
- Identifying failed experiments and models that have not helped with driving the desired business outcomes is important: it helps ensure resources are allocated to the areas with the most business impact. Below are three results from a churn prevention test based on the ML model output. Which one performed the best and should be chosen for the implementation in the main production systems?
```
Half of the customers with a high predicted probability to churn have been targeted with a few retention emails. The churn rates were compared to the other half without email campaigns. The targeted group has seen a 0.2% reduction in the churn rates compared to the control group.
Half of the customers with a high predicted probability to churn have been getting promotions and discounts on the items they were interested in (also predicted by ML). The company has observed a reduction in churn for that group by at least 3% and increase in overall purchase frequency.
Half of the customers with a high predicted probability to churn have been targeted with an increased frequency of multi-channel (email, re-targeting, post etc.) product recommendations. The churn rates were compared to the other half without these recommendations. The targeted group has seen 0.5% increase in the churn rates compared to the control group.
```
```
Half of the customers with a high predicted probability to churn have been getting promotions and discounts on the items they were interested in (also predicted by ML). The company has observed a reduction in churn for that group by at least 3% and increase in overall purchase frequency.
```
### Identify actionable recommendations
- John has built a prototype machine learning model predicting the number of hours the customer will play on the online gaming website next month. He is presenting insights and recommendations. The top 5 most important variables are listed in the barplot, each with a coefficient which shows how much each variable affects the number of active hours for an average customer next month.
- <image>
#### Question 3
- How would you interpret the results and what kind of initiatives would you start? Select one that DOES NOT apply.
```
Work with a website engineering team to reduce the number of errors, track the metric closely to make sure it is decreasing, since it is the thing that is most negatively impacting a player's gaming hours next month.
Run an A/B test with the data science team to explore if reduction in advertising levels would increase the number of gaming hours next month.
Reduce the price for the add-ons to zero.
Raise a question whether the model should be adjusted and the last month hours removed since the variable is not actionable.
```
```
Reduce the price for the add-ons to zero.
```

## `Chapter 4` Managing machine learning projects

### Video: Machine learning mistakes
#### Identify machine learning mistakes
- It's important to identify the situations in the machine learning development process where a mistake might be happening. Below you see a list of situations, identify the one that is NOT a machine learning mistake.
```
Defining business requirements before building the model.
Not having enough data.
Poor target variable definition.
Delaying market testing to push incremental improvements to the model.
```
```
Defining business requirements before building the model.
```
### Data needs pyramid
- The data pyramid represents how value gets created with data, and how to ensure there are no gaps in the process. It's important for business leaders to understand which needs should be met first and which later, and structure their organization's data resources accordingly.
- You're going to order the needs from the first (bottom of the pyramid) to the very last (top of the pyramid). Foundational needs should be in the bottom and the most advanced analytic methods on the top.
#### Question 1
- Order the needs from the first (bottom of the pyramid) to the very last (top of the pyramid).
```
Storage
Analysis
Preparation & Cleaning
Collection
Protoyping & Testing ML
Machine Learning in production
```
```
Machine Learning in production
Protoyping & Testing ML
Analysis
Preparation & Cleaning
Storage
Collection
```
### Match ML mistakes by their types
- It is vital to spot situations where machine learning team might be too focused on the methodology or are just excited about the science behind the project, but the business case is not strong, or the company is not be ready to execute on the ML model outputs. Below you will see a few situations, and will have to identify which of the ML mistake types they belong to.
#### Question 1
- Below you will see a few situations, and will have to identify which of the ML mistake types they belong to.
```
The team wants to get all the possible data before building a prototype. They need 8 months to aggregate data from all different sources.
The team spent 2 months in building the prototype model. They need 8 more months to perfect it before running the A/B test in the market.
The team has reviewed custoomers data: 3% of customers have data captured in a structured format, the rest is sitting in the back-end systems.
The model has been tested in the market and has not shown any results, the team says that they need another 6 months to perfect the model algorithm.
The team said they're going to use all data possible for the inferential model and that they don't need an input from the business team.
The team has reviewed the data source the system are not capturing the data correctly and cannot be used in building the model.
```
```
Not enough data
The team has reviewed the data source the system are not capturing the data correctly and cannot be used in building the model.
The team has reviewed custoomers data: 3% of customers have data captured in a structured format, the rest is sitting in the back-end systems.
Late testing, no impact
The team spent 2 months in building the prototype model. They need 8 more months to perfect it before running the A/B test in the market.
The model has been tested in the market and has not shown any results, the team says that they need another 6 months to perfect the model algorithm.
Feature selection
The team said they're going to use all data possible for the inferential model and that they don't need an input from the business team.
The team wants to get all the possible data before building a prototype. They need 8 months to aggregate data from all different sources.
```

### Video: Communication management
#### Business communication focus
- It's important to focus the business and machine learning communication on the right things. Below you will see a list of topics that are included in the proposed weekly machine learning model agenda. Which of these topics is NOT relevant for the business audience and should be decided by the ML team only?
```
Defining the business requirements.
Reviewing machine learning model concept and its product proposal.
Discussing machine learning algorithm nuances.
Defining market testing tactics.
```
```
Discussing machine learning algorithm nuances.
```
### Market testing
- Market testing is extremely important to ensure that the model is useful and can drive desired business outcomes. The way to do this is through running structured experiments - they could be experiments with customers, systems, or even machines e.g. testing if preventive maintenance of manufacturing machines identified to be at risk of failure by ML would extend their lifetime and maintenance costs.
- Here, you will sort the market testing steps from first to the last.
#### Question 1
- You see a number of steps for ML market testing - identify their order and sort them from first (top) to last (bottom).
```
Build a machine learning model predicting the outcome
Run certain actions e.g. marketing campaign, for group A and no actions for group B
Select customers with the predicted values and split into 2 groups (A/B)
Measure group A performance vs. group B and conclude if there was an impact on the desired outcome
Define the target
```
```
Define the target
Build a machine learning model predicting the outcome
Select customers with the predicted values and split into 2 groups (A/B)
Run certain actions e.g. marketing campaign, for group A and no actions for group B
Measure group A performance vs. group B and conclude if there was an impact on the desired outcome
```

### Video: Machine learning in production
#### Production systems
- There are thousands of different production systems in the world, but there are certain nuances that separate them, as they are live, customer facing and critical to the business.
- Below is a list of examples of production systems. Identify which of these items is NOT a production system.
```
Customer Relationship Management (CRM).
Fraud detection system.
Online banking platform.
Weekly business report stored as a spreadsheet file in company's shared drive.
```
```
Weekly business report stored as a spreadsheet file in company's shared drive.
```
### Production systems ML use cases
- We have seen multiple types of production systems. Now, we will look into some specific machine learning in production examples, and you will have to match them with appropriate types of production systems.
#### Question 1
- Match the machine learning in production examples with the production systems they are likely implemented in.
```
A transaction is passed to the team for a manual review after the system it as 'risky'
The snesor readings predict a potential collision and automatically hit the car brakes of the car to avoid it.
An automated product promotion email is triggered by a real time machine learning model predicting which product the customer might be interested in.
A high-value customers get a number of promotional discounts when the system predicts they are at risk of churning.
The customer receives an email requesting information about their money transfer. The system identified a potentially risky transaction.
The car should turn right at the next crossing. The road is closed; the system automatically re-calculates the journey to offer an alternative path.
```
```
Customer relationship management
An automated product promotion email is triggered by a real time machine learning model predicting which product the customer might be interested in.
A high-value customers get a number of promotional discounts when the system predicts they are at risk of churning.
Fraud prevention system
A transaction is passed to the team for a manual review after the system it as 'risky'
The customer receives an email requesting information about their money transfer. The system identified a potentially risky transaction.
Autonomous car
The snesor readings predict a potential collision and automatically hit the car brakes of the car to avoid it.
The car should turn right at the next crossing. The road is closed; the system automatically re-calculates the journey to offer an alternative path.
```
### ML in production launch
- Deploying machine learning models into production systems is a complex task, and requires caution and close business involvement to make sure customers are not negatively affected. Releasing slowly and to a limited audience, tracking results and feedback is critical to ensure a smooth launch and early detection of any possible issues.
#### Question 1
- Order the implementation steps of launching machine learning in production from first (top) to last (bottom).
```
Make sure the results are consistent over time
Launch to a small of customers
Scale up the model coverage
Track initial results
```
```
Launch to a small of customers
Track initial results
Make sure the results are consistent over time
Scale up the model coverage
```
