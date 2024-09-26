# (project)german_federal_budget_visualization

![header](https://capsule-render.vercel.app/api?type=venom&color=0:418FDE,100:0033A0&height=200&text=project%20migration&stroke=0033A0)


## Goal
The main purpose of this project is basically to see how much German Federal allocates their budget to supporting migrants and refugees. For this, I analyze the German Federal budget public data from official [bundeshaushalt website](https://www.bundeshaushalt.de/DE/Download-Portal/download-portal.html). I downloaded the data from 2020 to 2024 to see the serial trend of usage of the budget and compare between the years, also uncover important trends and insights into how funding for migrants and refugees has changed over time. Finally, I made it as interactive visulaization using Tableau.

&nbsp; 
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
### 1. Data preparation

First, from the official [bundeshaushalt website](https://www.bundeshaushalt.de/DE/Download-Portal/download-portal.html), I downloaded `bundeshaushalt` data from 2020 to 2024 as CSV files.

For the preparation,
* I changed the column names into English for better understanding
* I removed 2 null columns which have no value inside (`title group`, `title group text`)
* I filtered the dataset only with the expenditure to focus specifically on the expenditure data for analyzing how much the German federal allocates to the migrant sector
* (for python viz) I made filtered data which only includes data related with 'migration', 'refugee'. 

I used Jupyter Notebook to create quick visualizations in Python and prepare the data for visualization in Tableau.
Here's the code I used below. 

**1) Import the libaries and read the dataset**
```
import pandas as pd
import numpy as np

import matplotlib.pyplot as plt
import seaborn as sns
```
```
haushalt_2024 = pd.read_csv("/Users/yujin/Desktop/projects/project-german_federal_budget_viz/dataset/HH_2024.csv", delimiter=';', on_bad_lines='skip')
```

**2) Change the column names to English**
```
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
**3) Check the dataset**
```
haushalt_2024.isnull().sum()
```
```
haushalt_2024.info()
```
```
unique_values_per_column = haushalt_2024.nunique()
print(unique_values_per_column)
```
```
for column in haushalt_2024.columns:
    unique_values = haushalt_2024[column].unique()
    print(f"Unique values in '{column}':")
    print(unique_values)
    print("\n")
```
**4) (for python viz) Filter the dataset**
