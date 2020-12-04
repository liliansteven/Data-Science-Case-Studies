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
