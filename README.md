# 🍽️ Restaurant Tips Analysis

![](https://estrategia.vepormas.com/wp-content/uploads/2018/04/21DIC_1630_BLOG_RETAIL_2.png)

This project aims to use the restaurant tips dataset to practice creating composition plots and visualizations.

We will examine the relationship between different variables and the tips given.

The dataset consists of information from 244 restaurant bills, collected in the US in 1987.

It includes details about the tips given to restaurant staff, such as the total bill, tip amount, gender of the person paying, smoking status, day of the week, time of day, and party size.

# 1. Access data
You can get the analysis in the attachment "Restaurant_tips_analysis.ipynbin" this  repository

If you can not load the analysis in this repository, you can get the analysis on your notebook in https://colab.research.google.com by following these steps:
 
 ### 📥 Data import

 First, Open the Colab and let’s import the needed libraries: Pandas & Matplotlib, then import data from (https://raw.githubusercontent.com/RusAbk/sca_datasets/main/tips.csv)

```
import pandas as pd
import matplotlib.pyplot as plt
data = pd.read_csv('https://raw.githubusercontent.com/RusAbk/sca_datasets/main/tips.csv')
```

### 🔍 Data exploration

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

As we know, measures of central tendency is one of the basic tools, that allow us to compare different datasets as it shows the most typical values.

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

|        |       0 |
|:-------|--------:|
| min    |  1      |
| max    | 10      |
| mean   |  2.9983 |
| median |  2.9    |


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

|        |   Common |   Smokers |   Non-smokers |
|:-------|---------:|----------:|--------------:|
| min    |  1       |   1       |       1       |
| max    | 10       |  10       |       9       |
| mean   |  2.99828 |   3.00871 |       2.99185 |
| median |  2.9     |   3       |       2.74    |

Let's see the comparision by histogram:

```
fig, axis = plt.subplots(1,3,figsize=(15,5))
axis[0].hist(data.tip,bins=5,color='#74b9ff')
axis[0].set_xlabel('Tip value')
axis[0].set_ylabel('Frequency')
axis[0].set_title('Whole dataset tip values')
axis[0].grid(True)

axis[1].hist(smoker_df.tip,bins=5,color='#ff7675')
axis[1].set_xlabel('Tip value')
axis[1].set_ylabel('Frequency')
axis[1].set_title('Smokers tip values')
axis[1].grid(True)

axis[2].hist(non_smoker_df.tip,bins=5,color='#55efc4')
axis[2].set_xlabel('Tip value')
axis[2].set_ylabel('Frequency')
axis[2].set_title('Non-smokers tip values')
axis[2].grid(True)
```

![image](https://github.com/user-attachments/assets/95e92502-dc11-4203-8369-d81bc23a3096)

#### Conclusions:

There is no signification signs to show smokers give more tips than non-smokers 


## B. 👨👩 Do males give more tips?

I do the same above steps to analyse whether Males give more tips than Females

```
##### Create data for male and female

male_df=data[data['sex']=='Male']
female_df=data[data['sex']=='Female']

##### Calculate measurements for male and female:

male_tip_min=male_df['tip'].min()
male_tip_max=male_df['tip'].max()
male_tip_mean=male_df['tip'].mean()
male_tip_median=male_df['tip'].median()

female_tip_min=female_df['tip'].min()
female_tip_max=female_df['tip'].max()
female_tip_mean=female_df['tip'].mean()
female_tip_median=female_df['tip'].median()

all_vals_dict = {
    'Common': {'min': common_tip_min, 'max': common_tip_max, 'mean': common_tip_mean, 'median': common_tip_median},
    'Male': {'min': male_tip_min, 'max': male_tip_max, 'mean': male_tip_mean, 'median': male_tip_median},
    'Female': {'min': female_tip_min, 'max': female_tip_max, 'mean': female_tip_mean, 'median': female_tip_median}
}

# Make a dataframe
all_mct = pd.DataFrame(all_vals_dict)
# Output the dataframe
all_mct.to_markdown()
```

|        |   Common |     Male |   Female |
|:-------|---------:|---------:|---------:|
| min    |  1       |  1       |  1       |
| max    | 10       | 10       |  6.5     |
| mean   |  2.99828 |  3.08962 |  2.83345 |
| median |  2.9     |  3       |  2.75    |

Let's see the comparision by histogram:

```
fig, axis = plt.subplots(1,3,figsize=(15,5))
axis[0].hist(data.tip,bins=5,color='#74b9ff')
axis[0].set_xlabel('Tip value')
axis[0].set_ylabel('Frequency')
axis[0].set_title('Whole dataset tip values')
axis[0].grid(True)

axis[1].hist(male_df.tip,bins=5,color='#ff7675')
axis[1].set_xlabel('Tip value')
axis[1].set_ylabel('Frequency')
axis[1].set_title('Male tip values')
axis[1].grid(True)

axis[2].hist(female_df.tip,bins=5,color='#55efc4')
axis[2].set_xlabel('Tip value')
axis[2].set_ylabel('Frequency')
axis[2].set_title('Female tip values')
axis[2].grid(True)
```

![image](https://github.com/user-attachments/assets/644223c0-809c-4d86-a6a5-c80716232c4a)


#### Conclusions:

There is no signification signs to show male give more tips than female

## C. 🕑 Do dinners bring more tips?

I do the same above steps to analyse whether Males give more tips than Females

```
##### Create data for male and female

dinner_df=data[data['time']=='Dinner']
lunch_df=data[data['time']=='Lunch']

##### Calculate measurements for male and female:

dinner_tip_min=dinner_df['tip'].min()
dinner_tip_max=dinner_df['tip'].max()
dinner_tip_mean=dinner_df['tip'].mean()
dinner_tip_median=dinner_df['tip'].median()

lunch_tip_min=lunch_df['tip'].min()
lunch_tip_max=lunch_df['tip'].max()
lunch_tip_mean=lunch_df['tip'].mean()
lunch_tip_median=lunch_df['tip'].median()

all_vals_dict = {
    'Common': {'min': common_tip_min, 'max': common_tip_max, 'mean': common_tip_mean, 'median': common_tip_median},
    'Male': {'min': male_tip_min, 'max': male_tip_max, 'mean': male_tip_mean, 'median': male_tip_median},
    'Female': {'min': female_tip_min, 'max': female_tip_max, 'mean': female_tip_mean, 'median': female_tip_median}
}

all_vals_dict = {
    'Common': {'min': common_tip_min, 'max': common_tip_max, 'mean': common_tip_mean, 'median': common_tip_median},
    'Dinner': {'min': dinner_tip_min, 'max': dinner_tip_max, 'mean': dinner_tip_mean, 'median': dinner_tip_median},
    'Lunch': {'min': lunch_tip_min, 'max': lunch_tip_max, 'mean': lunch_tip_mean, 'median': lunch_tip_median}
}

# Make a dataframe
all_mct = pd.DataFrame(all_vals_dict)
# Output the dataframe
all_mct
```

|        |   Common |   Dinner |   Lunch |
|:-------|---------:|---------:|--------:|
| min    |  1       |  1       | 1.25    |
| max    | 10       | 10       | 6.7     |
| mean   |  2.99828 |  3.10267 | 2.72809 |
| median |  2.9     |  3       | 2.25    |

Let's see the comparision by histogram:

```
ig, axis = plt.subplots(1,3,figsize=(15,5))
axis[0].hist(data.tip,bins=5,color='#74b9ff')
axis[0].set_xlabel('Tip value')
axis[0].set_ylabel('Frequency')
axis[0].set_title('Whole dataset tip values')
axis[0].grid(True)

axis[1].hist(dinner_df.tip,bins=5,color='#ff7675')
axis[1].set_xlabel('Tip value')
axis[1].set_ylabel('Frequency')
axis[1].set_title('Dinner tip values')
axis[1].grid(True)

axis[2].hist(lunch_df.tip,bins=5,color='#55efc4')
axis[2].set_xlabel('Tip value')
axis[2].set_ylabel('Frequency')
axis[2].set_title('Lunch tip values')
axis[2].grid(True)
```

![image](https://github.com/user-attachments/assets/c6298984-23f3-409e-bc19-fcf05a282b01)

#### Conclusions:

There is no signification signs to show smokers give more tips than non-smokers 
