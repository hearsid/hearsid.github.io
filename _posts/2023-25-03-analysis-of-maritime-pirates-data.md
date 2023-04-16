---
layout: post
title: "Data Analysis: Maritime Pirates data"
date: 2023-24-03 19:33:58 +0530
category: python
---

EDA

Columns:
- Year: The year in which the attack occurred.
- Date: The date on which the attack occurred.
- Time: The time at which the attack occurred.
- Zone: The general region of the world in which the attack occurred.
- Area: The more specific location within the zone where the attack occurred.
- Country: The country in which the attack occurred.
- Location Detail: A more detailed description of the location of the attack.
- Vessel Type: The type of vessel that was attacked (e.g. cargo, tanker, fishing vessel).
- Vessel Name: The name of the vessel that was attacked.
- Vessel Nationality: The nationality of the vessel that was attacked.
- Vessel Gross Tonnage: The gross tonnage of the vessel that was attacked.
- Cargo Type: The type of cargo that the attacked vessel was carrying.
- Incident Type: The type of incident (e.g. hijacking, boarding, kidnapping) that occurred during the attack.
- Weapon Used: The type of weapon used during the attack.
- Latitude: The latitude coordinates of the location of the attack.
- Longitude: The longitude coordinates of the location of the attack.
- Description: A detailed description of the attack.

Link:
- https://colab.research.google.com/drive/1v6iqiB775e6YhFbg3S-LpJc8cmRqkCs3#scrollTo=AEzlz-aIH7JS

Bar chart of location wise attacks:
![pirates location](/assets/img/pirates-country-graph.png)

```python
# Import necessary libraries
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Load the dataset into a pandas dataframe
df = pd.read_csv('global_maritime_pirate_attacks.csv')

# Check the first few rows of the dataframe
print(df.head())

# Check the number of rows and columns in the dataframe
print(df.shape)

# Check for missing values
print(df.isnull().sum())

# Visualize the number of attacks per year
sns.countplot(x='Year', data=df)
plt.show()

# Visualize the types of incidents that occurred
sns.countplot(x='Incident Type', data=df)
plt.show()

# Create a new feature for the number of days since the last attack
df['Days Since Last Attack'] = (df['Date'] - df['Date'].shift()).fillna(pd.Timedelta(seconds=0))
df['Days Since Last Attack'] = df['Days Since Last Attack'].apply(lambda x: x.days)

# Train a logistic regression model to predict the outcome of an attack
from sklearn.linear_model import LogisticRegression
from sklearn.model_selection import train_test_split
from sklearn.metrics import accuracy_score, confusion_matrix

X = df[['Year', 'Latitude', 'Longitude', 'Vessel Gross Tonnage', 'Days Since Last Attack']]
y = df['Outcome']

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

model = LogisticRegression()
model.fit(X_train, y_train)

y_pred = model.predict(X_test)

print('Accuracy:', accuracy_score(y_test, y_pred))
print('Confusion Matrix:', confusion_matrix(y_test, y_pred))
```
