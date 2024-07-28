# 🍽️ Restaurant Tips Analysis

![](https://estrategia.vepormas.com/wp-content/uploads/2018/04/21DIC_1630_BLOG_RETAIL_2.png)

This project aims to use the restaurant tips dataset to practice creating composition plots and visualizations.

We will examine the relationship between different variables and the tips given.

The dataset consists of information from 244 restaurant bills, collected in the US in 1987.

It includes details about the tips given to restaurant staff, such as the total bill, tip amount, gender of the person paying, smoking status, day of the week, time of day, and party size.

# 1. Access data
You can get the analysis in the attachment "Restaurant_tips_analysis.ipynbin" this  repository

If you can not load the analysis in this repository, you can get the analysis on your notebook in https://colab.research.google.com by following these steps:
 
 📥 ### Data import

 First, Open the Colab and let’s import the needed libraries: Pandas & Matplotlib, then import data from (https://raw.githubusercontent.com/RusAbk/sca_datasets/main/tips.csv)

```
import pandas as pd
import matplotlib.pyplot as plt
data = pd.read_csv('https://raw.githubusercontent.com/RusAbk/sca_datasets/main/tips.csv')
```

🔍 ### Data exploration

Let's take a look at the first 5 rows, you can see each observation represents a customer who left a tip at a restaurant.

```
data.head()
```
![image](https://github.com/user-attachments/assets/08f8ea55-fd9d-47f9-9ee9-4ad4f6a18b56)

We can see information about:

- the day it occurred
- if it was at lunch or dinner
- the total bill
- the sex of the person
- if they were a smoker or not
- the size of the party

Before continuing take a look at a few rows of the data and use info and describe to analyze dataset column types and values.

### Column types checking
Show the columns of the dataframe and their types:
```
data.info()
```
![image](https://github.com/user-attachments/assets/7c9280f8-16c6-4b13-b1b1-a4d2ae124656)

We have string columns considered as objects. Let's fix their types and make them string:

```
data=data.convert_dtypes()
data.info()
```
![image](https://github.com/user-attachments/assets/bcdf38f1-2f7e-49b3-8bb6-d4567e5386cf)

### Basic descriptive statistics

![image](https://github.com/user-attachments/assets/fbb6080d-1fcc-449e-a0c2-72abc9c85c4f)


#### Other measures of central tendency for the whole dataset

```
common_tip_min=data['tip'].min()
common_tip_max=data['tip'].max()
common_tip_mean=data['tip'].mean()
common_tip_median=data['tip'].median()

### Make a list of values:

common_values = [common_tip_min, common_tip_max, common_tip_mean, common_tip_median]
common_values = map(lambda x: round(x, 4), common_values)
common_mct = pd.DataFrame(common_values, index=['min', 'max', 'mean', 'median'])
common_mct
```

![image](https://github.com/user-attachments/assets/cf4c8094-9168-4331-99d6-9225b307ae2c)

# 2. Tip value influencers

In the research, I analyse some factors that may affect to tip values:
- Smokers and Non-smokers
- Male and female
- Dinner and Lunch

## A. 🚬 Do people who smoke give more tips?
For this analysis, I collect data of tip value for smokers and non-smokes, and calculate some measurements

```
smoker_df=data[data['smoker']=='Yes']
non_smoker_df=data[data['smoker']=='No']

smoker_tip_min=smoker_df['tip'].min()
smoker_tip_max=smoker_df['tip'].max()
smoker_tip_mean=smoker_df['tip'].mean()
smoker_tip_median=smoker_df['tip'].median()

non_smokers_tip_min=non_smoker_df['tip'].min()
non_smokers_tip_max=non_smoker_df['tip'].max()
non_smokers_tip_mean=non_smoker_df['tip'].mean()
non_smokers_tip_median=non_smoker_df['tip'].median()

all_vals_dict = {
    'Common': {'min': common_tip_min, 'max': common_tip_max, 'mean': common_tip_mean, 'median': common_tip_median},
    'Smokers': {'min': smoker_tip_min, 'max': smoker_tip_max, 'mean': smoker_tip_mean, 'median': smoker_tip_median},
    'Non-smokers': {'min': non_smokers_tip_min, 'max': non_smokers_tip_max, 'mean': non_smokers_tip_mean, 'median': non_smokers_tip_median}
```

We got data in the table below for the comparision of the measures of central tendency betweens smokers and non-smokers:

![image](https://github.com/user-attachments/assets/4963e019-0098-4b49-8ff6-3d4a558cd3ca)

Let's see the comparision by histogram:

![image](https://github.com/user-attachments/assets/95e92502-dc11-4203-8369-d81bc23a3096)

#### Conclusions:

There is no signification signs to show smokers give more tips than non-smokers 


## B. 👨👩 Do males give more tips?

![image](https://github.com/user-attachments/assets/6250279c-ee29-48e9-a943-353cc590ff23)

![image](https://github.com/user-attachments/assets/644223c0-809c-4d86-a6a5-c80716232c4a)


#### Conclusions:

There is no signification signs to show male give more tips than female

## C.🕑 Do dinners bring more tips?

![image](https://github.com/user-attachments/assets/f48a7287-9446-4254-8e2b-55f93698898d)

![image](https://github.com/user-attachments/assets/c6298984-23f3-409e-bc19-fcf05a282b01)

#### Conclusions:

