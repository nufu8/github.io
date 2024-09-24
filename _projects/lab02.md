---
layout: page
title: "Lab 02"
description: "Lab 3: Handling Data"
img: assets/img/data.jpg
importance: 2
category: work
related_publications: true
---

**WK 3**

---

For the third week of Metropolitan Data 1 we learned how to process datasets.

### Question 1

**## Exercise 1: Loading the data:**

- **Load the `goodreads.csv` file into Python**
- **Explore it by looking at first and last 5 rows**
- **Change the column names to `["rating", 'review_count', 'isbn', 'booktype','author_url', 'year', 'genre_urls', 'dir','rating_count', 'name']`**

{% raw %}

```
import pandas as pd

df = pd.read_csv('goodreads.csv')

print(df.head())
print(df.tail())

df.columns = ["rating", "review_count", "isbn", "booktype", "author_url", "year", "genre_urls", "dir", "rating_count", "name"]
  ```
  
{% endraw %}
___

### Question 2: Subsetting the data

- **Subset the data by creating new dataframe only with `["rating", 'isbn', 'author_url', 'year', 'genre_urls', 'name']`**

{% raw %}

```
import pandas as pd

df = pd.read_csv('goodreads.csv')

print(df.head())
print(df.tail())

df.columns = ["rating", "review_count", "isbn", "booktype", "author_url", "year", "genre_urls", "dir", "rating_count", "name"]

# Subsetting data with a new dataframe
subset_df = df[["rating", "isbn", "author_url", "year", "genre_urls", "name"]]

``` 
{% endraw %}

___

### Question 3:  Manage Missing Data
**We’ve got a number of ways in general of dealing with missing data. These involve**

**1. Dropping off cases (or rows) in the data with any missing variables**
**2. Excluding variables in the data with any missing data**
**3. Selectively choosing indicators with only a limited amount of missing data**
**4. Replacing missing variables with averages, or other representative values**
**5. Creating a separate model to predict missing data**

**- Count the missing values in each column**
**- Manage the missing values (delete or replace values or leave them as they are) and briefly explain your choice for each column**


{% raw %}
```
import pandas as pd
import os

df = pd.read_csv('goodreads.csv')

df.columns = ["rating", "review_count", "isbn", "booktype", "author_url", "year", "genre_urls", "dir", "rating_count", "name"]

# Retrieve missing values with .isnull function, and count them
missingValues = df.isnull().sum()

# Copy cleaned data to new dataframe
clean_df = df.copy()

# Column 1: Rating. Drop because important
if missingValues['rating'] > 0:
    clean_df = clean_df.dropna(subset=['rating'])

# Column 2. ISBN. Drop because important
if missingValues['isbn'] > 0:
    clean_df = clean_df.dropna(subset=['isbn'])

# Column 3. Author URL. Leave because not essential

# Column 4. Year. Replace with mean
if missingValues['year'] > 0:
    median_year = clean_df['year'].mean()
    clean_df['year'].fillna(median_year, inplace=True)

# Column 5. Genre URLs. Leave because not important

# Column 6. Name. Drop because important
if missingValues['name'] > 0:
    clean_df = clean_df.dropna(subset=['name'])

# Print cleaned up dataframe
print(clean_df.head())
```
{% endraw %}


### Question 4:  Shape the data
**- Parse the `author_url` to create new column named `author`**
**- Sort the data by putting higher rates go first. If there are overlapping rates, try to put earlier years go first.**
**(Stretch Goal) Examine how many books were published at each year and find lowest, highest rate of each year.**


{% raw %}
```
import pandas as pd
goodreads = pd.read_csv(r"C:\Users\Gebruiker\Documents\MADE MD1\data\goodreads.csv") 
goodreads.columns = 'rating', 'review_count', 'isbn', 'booktype', 'author_url', 'year', 'genre_urls', 'dir', 'rating_count', 'name'
goodreads = goodreads.dropna(subset=['author_url'])
# This line filters out the null-values in the column author_url from the dataframe in preperation of redefining the new column author with the parsing.
def get_author(author_url):
    name = author_url.split('/')[-1].split('.')[1:][0]
    return name
# This line writes a function which splits the needed author name from the url-values, to ultimately put into the new column author
goodreads['author'] = goodreads.author_url.map(get_author)
# This line puts the name from the splitted value from author_url into the new column author
goodreads.author[:]
# This line is used to check if the new column has the right values
goodreads.sort_values(by=['rating','year'], ascending=[False, True], inplace=True)
# This line sorts the rows first by rating descending and then by year ascending, inplace commands creates acutal change in the dataframe
goodreads[['rating', 'author', 'year']]
# This line prints the new dataframe, proving to us that the sorting was correctly executed
```
{% endraw %}


### Question 5: Saving the results
**- Save the cleaned dataframe as 'hw-03-cleaned.csv' in data folder**
**The code added below is not up to date, please refer to the file handed in on Brightspace**

{% raw %}
```
import pandas as pd
import os

df = pd.read_csv('goodreads.csv')

df.columns = ["rating", "review_count", "isbn", "booktype", "author_url", "year", "genre_urls", "dir", "rating_count", "name"]

# Retrieve missing values with .isnull function, and count them
missingValues = df.isnull().sum()

# Copy cleaned data to new dataframe
clean_df = df.copy()

# Column 1: Rating. Drop because important
if missingValues['rating'] > 0:
    clean_df = clean_df.dropna(subset=['rating'])

# 2. Review count. replace with mean value
if missingValues['review_count'] > 0:
    mean_review_count = clean_df['review_count'].mean()
    clean_df['review_count'].fillna(mean_review_count, inplace=True)

# 3. ISBN. Drop because important
if missingValues['isbn'] > 0:
    clean_df = clean_df.dropna(subset=['isbn'])

# 4. Author URL. Leave because not essential

# 5. Year. Replace with mean
if missingValues['year'] > 0:
    median_year = clean_df['year'].mean()
    clean_df['year'].fillna(median_year, inplace=True)

# 6. Genre URLs. Leave because not important

# 7. Name. Drop because important
if missingValues['name'] > 0:
    clean_df = clean_df.dropna(subset=['name'])

# Print cleaned up dataframe
print(clean_df.head())

# Parse author_url
# clean_df['author'] = clean_df['author_url']. 

# Sort by descending rating. Higher ratings come first
clean_df.sort_values(by=['rating', 'year'], ascending=[False, True], inplace=True)

# Save cleaned dataframe
output_folder = 'data'
clean_df_path= os.path.join(output_folder, 'cleaned_df.csv')
clean_df.to_csv(clean_df_path)
```
{% endraw %}

### Question 6: Investigate the relationship between the number of reviews and the average rating for books in the dataset cleaned-goodreads.csv procided.

- **Calculate the correlation coefficient. Give me a short definition of this coefficient**
- **Create a scatter plot showing the relationship between these two features.**
- **Based on the plot and the correlation, provide a brief interpretation of the relationship.**

**Python Tools: Use pandas and numpy for correlation, and matplotlib or seaborn for the scatter plot.**

{% raw %}
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sb
goodreads = pd.read_csv(r"C:\Users\Gebruiker\Documents\MADE MD1\data\cleaned-goodreads.csv") 
# Imports the required toolboxes and cleaned file for the database of goodreads
goodreads['review_count'].corr(goodreads['rating'])
# This line gives us the correlation between the columns of review_count and rating, the result is a coefficient of -0,037. This means a very slight negative correlation between a higher number of reviews and a higher average rating.
sb.scatterplot(x='review_count', y='rating', data=goodreads)
plt.xlim(0, 5000)
plt.title('Scatter Plot of rating vs number of reviews')
plt.show()
# C. scatterplot is linear so the correlation is weak. this means that the rating is not strongly related to the amount of reviews. 
```
{% endraw %}

### Question 7: Calculate the following descriptive statistics for the numerical features (e.g., number of reviews, average rating, etc.):
- **Mean**
- **Median**
- **Standard Deviation**
- **Range**
- **Create a histogram or box plot for at least one of the numerical features, highlighting any skewness or outliers.**
    
**Python Tools: Use pandas for data manipulation and matplotlib or seaborn for visualization.**

{% raw %}
```
import pandas as pd
import seaborn as sb
import matplotlib.pyplot as plt
goodreads = pd.read_csv(r"C:\Users\Gebruiker\Documents\MADE MD1\data\cleaned-goodreads.csv") 
stats = goodreads.describe()
# This line gives to command to get all the descriptive statistics from the goodreads-database
range = stats.loc['max'] - stats.loc['min']
# This calculates thhe range by subtracting the minimum from the maximum following its lack of this descriptive statistic in the default ones.
filtered_stats = pd.DataFrame({
    'Mean': stats.loc['mean'],
    'Median': stats.loc['50%'],
    'Standard Deviation': stats.loc['std'],
    'Range': range
})
# This creates a new dataframe displaying only the required descriptive statistics
print(filtered_stats)
sb.histplot(goodreads['rating'], bins=5, kde=True)
# This creates a histogram with 5 bars (one for each whole rating-number), the kde-curve shows the skewness even more than just the bars of the histogram
plt.title("Histogram ratings goodreads")
plt.show
# this histogram shows no outliers, because the variable of ratings already has a limited range. This skewness shows to be slightly to the left, meaning outliers towardfs lower ratings are slight;y more common (negatively skewed).

```
{% endraw %}