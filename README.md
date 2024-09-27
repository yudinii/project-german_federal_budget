# (project)german_federal_budget_visualization

![header](https://capsule-render.vercel.app/api?type=venom&color=0:418FDE,100:0033A0&height=200&text=project%20migration&stroke=0033A0)


## Goal
The main purpose of this project is basically to see how much German Federal allocates their budget to supporting migrants and refugees. For this, I analyze the German Federal budget public data from official [bundeshaushalt website](https://www.bundeshaushalt.de/DE/Download-Portal/download-portal.html). I downloaded the data from 2020 to 2024 to see the serial trend of usage of the budget and compare between the years, also uncover important trends and insights into how funding for migrants and refugees has changed over time. Finally, I made it as interactive visulaization using Tableau.

&nbsp; 

Through this project, I wanted to answer these questions.

*- How much of the budget does the German federal allocate each year to supporting refugees and migrants?*

*- What proportion of the total budget does this allocated amount represent?*

*- Is there a significant increase or decrease in the allocated budget? If so, to what extent?*

*- Are there any observable trends in the allocated budget over time?*

&nbsp; 
&nbsp; 
&nbsp; 

----
### 1. Data Explanation

First, from the official [bundeshaushalt website](https://www.bundeshaushalt.de/DE/Download-Portal/download-portal.html), I downloaded `bundeshaushalt` data from 2020 to 2024 as CSV files.

The data has total 14 columns : `'einzelplan'`, `'einzelplan-text'`, `'einahmen-ausgaben'`, `'einahmen-ausgaben-text'`, `'kapitel'`, `'kapitel-text'`, `'titel'`, `'funktion'`, `'titel-text'`, `'flex'`, `'seite'`, `'soll '`, `'titelgruppe'`, `'tgr-text'`

### 2. Data preparation


For the preparation,
* I _translated all the column names and values into English_ for better understanding
* I _removed 2 null columns_ which have no values inside (`title group`, `title group text`)
* I _filtered the dataset only with the expenditure_ to focus specifically on the expenditure data for analyzing how much the German federal allocates to the migrant sector
* Also, make all text entries into broader categories so that we can see 
* (for python viz) I made filtered data which only includes data related with 'migration', 'refugee'. 

I used Jupyter Notebook to create quick visualizations in Python and prepare the data for visualization in Tableau.<br />
Here's the code I used below. 

**1) Import the libaries and read the dataset**
```.py
import pandas as pd
import numpy as np

import matplotlib.pyplot as plt
import seaborn as sns
```
```.py
haushalt_2024 = pd.read_csv("/Users/yujin/Desktop/projects/project-german_federal_budget_viz/dataset/HH_2024.csv", delimiter=';', on_bad_lines='skip')
```

**2) Change the column names to English**
```.py
column_mapping = {
    'einzelplan': 'individual plan',
    'einzelplan-text': 'individual plan text',
    'einahmen-ausgaben': 'income expenditure',
    'einahmen-ausgaben-text': 'income expenditure text',
    'kapitel': 'chapter',
    'kapitel-text': 'chapter text',
    'titel': 'title',
    'funktion': 'function',
    'titel-text': 'title text',
    'flex': 'flex',
    'seite': 'page',
    'soll ': 'target',
    'titelgruppe': 'title group',
    'tgr-text': 'title group text'
}

haushalt_2024.rename(columns=column_mapping, inplace=True)
```
**3) Filter the dataset only with expeniture**
```.py
haushalt_2024_expenditure = haushalt_2024[haushalt_2024['income expenditure'] == 'E']
```
**4) Remove 2 columns which only have null values**
```.py
haushalt_2024_expenditure = haushalt_2024_expenditure.drop(['title group', 'title group text'], axis=1)
```
**5) Check the dataset**
```.py
haushalt_2024_expenditure.isnull().sum()
```
```.py
haushalt_2024_expenditure.info()
```
```.py
unique_values_per_column = haushalt_2024_expenditure.nunique()
print(unique_values_per_column)
```
```.py
for column in haushalt_2024_expenditure.columns:
    unique_values = haushalt_2024_expenditure[column].unique()
    print(f"Unique values in '{column}':")
    print(unique_values)
    print("\n")
```
**6) Translate text values into English**
```.py

```

(for python viz) Filter the dataset**
