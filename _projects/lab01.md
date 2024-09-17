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

![histogram](C:\Users\Stan Huynh\Personal Files\School\Master\MSc MADE\Data I\github.io\assets\img\2a.png)
<img src="assets\img\2a.png" alt="Alt text">


**B)**

{% raw %}
```
def list_primes_two(len_seq):

    prime_numbers = [i for i in range(2, len_seq + 1) if all(i % j != 0 for j in range(2, i))]

    return prime_numbers

# Display the prime numbers list
print("Prime numbers (using list comprehension):", list_primes_two(100))
```
{% endraw %}

___

### Exercise 4
**Write a function to test the "prime-ness" of a number.**
    
In Exercise 4, above, you wrote code that generated a list of the prime numbers between 1 and 100. Now, write a function called `isprime()` that takes in a positive integer $N$, and determines whether or not it is prime.  Return `True` if it's prime and return `False` if it isn't. Then, using a list comprehension and `isprime()`, create a list `myprimes` that contains all the prime numbers less than 100.  

{% raw %}
```
# Function to check if a number is prime
def isprime(N):
    """
    Determines if a given positive integer N is a prime number.

    Parameters:
    N (int): The number to be checked for primality.

    Returns:
    bool: True if N is prime, False otherwise.
    """

    for i in range(2, N):
        if N % i == 0:
            return False     
        
    return True
```
{% endraw %}

**Function to generate a list of prime numbers**

{% raw %}
```
def list_primes_two(len_seq):

    myprimes = [i for i in range(2, len_seq) if isprime(i)]

    return myprimes
```
{% endraw %}

**Display the prime numbers less than 100**

{% raw %}
```
print("Prime numbers less than 100:", list_primes_two(100))
```
{% endraw %}


