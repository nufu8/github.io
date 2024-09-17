---
layout: page
title: "Lab 01"
description: "Lab 2: Fiddling with Pandas. No pandas were harmed during the making of this lab."
img: assets/img/sad_panda.png
importance: 2
category: work
related_publications: true
---

**WK 2**

---

For the second week of Metropolitan Data 1 we explored various Python libraries such as Pandas.

### Question 1
**Write a Python code snippet using IPython.display to embed this Google Sheet directly into a Jupyter notebook for easy reference and interaction.**

{% raw %}

```
from IPython.display import IFrame

IFrame("https://docs.google.com/spreadsheets/d/1EAx8_ksSCmoWW_SlhFyq2QrRn0FNNhcg1TtDFJzZRgc/edit?hl=en&gid=1#gid=1", width=1000, height=500)
  ```
  
{% endraw %}
___

### Question 2

**a) Save the csv file to your compluter and Load the data in Tab "TOTAL Casualties".**
**b) Display the first 5 rows of the dataset using .head().**
**c) Extract the column names and create a dictionary where each column name is the key, and the first value in that column is the value.**

{% raw %}

```
import pandas as pd

f = "Wikileaks Afghanistan war logs analysis - TOTAL CASUALTIES, ALL CAUSES.csv"

# Importing the csv file into a dataframe and resetting the header to row number 2
df = pd.read_csv(f, header=1)

# Print first 5 rows
print(df.head())

# Extract  column names
column_names = df.columns

# Create dictionary
dict ={}

# Populate dictionary
for column in column_names:
    firstValue = df[column].iloc[0]
    dict[column] = firstValue

# Print output
print(dict)
``` 
{% endraw %}

___

### Question 3
**a) Plot a histogram of any numeric column from the dataset.**
**b) Use a kernel density plot (KDE) to visualize the distribution of another numeric column.**
**c) Create a bar chart of a categorical variable and discuss how the plot changes if you switch to a horizontal bar plot.**

**A)**
{% raw %}
```
# a) make a histogram from the info from columb "Taliban"
sns.histplot(y="Taliban", data=db_a)
``` 
{% endraw %}


{% include figure.liquid loading="eager" path="assets/img/2a.png" title="example image" class="img-fluid rounded z-depth-1" %}

**B)**

{% raw %}
```
# b) make a KDE plot
sns.kdeplot(db_a["Nato - official figures"])
```
{% endraw %}

{% include figure.liquid loading="eager" path="assets/img/2b.png" title="example image" class="img-fluid rounded z-depth-1" %}

___

**C)**

{% raw %}
```
# c)
sns.displot(db_a, x="Month")
```
{% endraw %}

{% include figure.liquid loading="eager" path="assets/img/2c.png" title="example image" class="img-fluid rounded z-depth-1" %}

### Question 4
**a) Write a loop that iterates through each row of a DataFrame and prints the value of one specific column.**
**b) Modify the loop so that it extracts rows where a numeric column value is greater than a threshold and stores these rows in a new DataFrame.**

**A)**
{% raw %}
```
for index, row in db_a.iterrows():
    print(row['Civilians'])
```
{% endraw %}

**B)**
{% raw %}
```
filtered_rows = []
for index, row in db_a.iterrows():
   if int(row['Civilians']) > 100:
      filtered_rows.append(row)

filtered_db_a = pd.DataFrame(filtered_rows)
filtered_db_a
```
{% endraw %}

### Question 5
## Question 5
**a) Create a list containing the names "Civilians" and "Afghan forces"**
**b) From the imported data keep the the values from these two columns only. Keep in mind that "Year" and "Month" identify each column and sould remain in the dataset.**
**c) Obtain a monthly total count of casualties for these two groups and create a line and a bar plot of them.**

**A)**
{% raw %}
```
list_of_headers = list(db_a)
new_list = [list_of_headers[1], list_of_headers[2]]
new_list
```
{% endraw %}

**B)**
{% raw %}
```
db_new = db_a.drop(columns=["Taliban", "Nato (detailed in spreadsheet)", "Nato - official figures"])
db_new["Total_Civilians_Afghan"] = db_a[new_list[0]] + db_a[new_list[1]]
db_new
```
{% endraw %}

**C)**
{% raw %}
```
sns.displot( x="Total_Civilians_Afghan", data=db_new, hue="Year", multiple="stack")
```
{% endraw %}
