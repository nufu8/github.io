---
layout: page
title: "Lab 00"
description: "MetData's very first lab: Python Basics"
img: assets/img/lab00.png
importance: 1
category: work
related_publications: true
---

**WK 1**

---

For the first week of Metropolitan Data 1 we took a look at the first steps in Python.

### Exercise 1
**Write a properly documented function with the following behaviour:**

- It has a meaningful name (i.e. it is related to its behaviour).
- It takes an integer that represents the length of a sequence that will be created.
- It creates a dictionary that is empty.
- It loops over the sequence and stores each number as the key of an entry in the dictionary, assigning either "odd" or "even" to the value, depending on the type of number.
- Returns the dictionary.

{% raw %}

```
def define_even_or_odd(sequence_length):
    """
    Generates a dictionary where each key is a number in a sequence from 0 to sequence_length.
    The corresponding value is either 'odd' or 'even', depending on whether the key is odd or even.

    Parameters:
    sequence_length (int): The length of the sequence to generate (non-negative integer).

    Returns:
    even_odd_dict: A dictionary with numbers as keys and 'odd' or 'even' as values.
    """
    if sequence_length < 0:
        raise ValueError("sequence_length must be a non-negative integer.")
    
    even_odd_dict = {} 

    for i in range(0, sequence_length + 1):
        if i % 2 == 0:
            even_odd_dict[i] = "even"
        else:
            even_odd_dict[i] = "odd"

    return even_odd_dict

print("list of odd and even", define_even_or_odd(100))
  ```
  
{% endraw %}
___

### Exercise 2
**Create a tuple called `tup` with the following seven objects:**

- The first element is an integer of your choice
- The second element is a float of your choice  
- The third element is the sum of the first two elements
- The fourth element is the difference of the first two elements
- The fifth element is the first element divided by the second element
- Display the output of `tup`.  What is the type of the variable `tup`? What happens if you try and chage an item in the tuple?
 
{% raw %}

```
# Step 1: define the elements
first_element = 64
second_element = 5.0
third_element = first_element + second_element
fourth_element = first_element - second_element
fifth_element = first_element / second_element

# Step 2: create the tuple 'tup' with all five elements
tup = (first_element, second_element, third_element, fourth_element, fifth_element)

# Step 3: display the tuple
print("Tuple:", tup)
# output: (64, 5.0, 69.0, 59.0, 12.8)

# Step 4: display the type of the variable 'tup'
print("Type of tup:", type(tup))

# Step 5: trying to change an item in the tuple 
try:
    tup[0] = 20  
except TypeError as e:
    print("Error when trying to modify tuple:", e)

# Tuples are immutable, meaning you cannot change their contents once they are created.
# Hence, attempting to modify an item raises a TypeError.
``` 
{% endraw %}

___

### Exercise 3
**Build a list that contains every prime number between 1 and 100, in two different ways:**
    
1. Using for loops and conditional if statements.
2. **(Stretch Goal)** Using a list comprehension.  You should be able to do this in one line of code. **Hint:** it might help to look up the function `all()` in the documentation.

**Way 1: Using for loops and conditional if statements.**

{% raw %}
```
def list_primes_one(len_seq):

    prime_numbers = []
    list_numbers = range(2, len_seq + 1)

    for i in list_numbers:
        for j in range(2, i):
            if i % j == 0:
                break
        else:
            prime_numbers.append(i)
        
    return prime_numbers
``` 
{% endraw %}

**Display the prime numbers list**

{% raw %}
```
print("Prime numbers (using for loop):", list_primes_one(100))
``` 
{% endraw %}

**Way 2: Using a list comprehension.**

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


