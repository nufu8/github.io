---
layout: page
title: Lab 00
description: MetData's very first lab: Python Basics
img: assets/img/lab00.png
importance: 3
category: work
related_publications: true
---

For the first week of Metropolitan Data 1 we took a look at the first steps in Python.

### Exercise 1
**Write a properly documented function with the following behaviour:**

- It has a meaningful name (i.e. it is related to its behaviour).
- It takes an integer that represents the length of a sequence that will be created.
- It creates a dictionary that is empty.
- It loops over the sequence and stores each number as the key of an entry in the dictionary, assigning either "odd" or "even" to the value, depending on the type of number.

- Returns the dictionary.

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

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/1.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/3.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/5.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Caption photos easily. On the left, a road goes through a tunnel. Middle, leaves artistically fall in a hipster photoshoot. Right, in another hipster photoshoot, a lumberjack grasps a handful of pine needles.
</div>
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/5.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    This image can also have a caption. It's like magic.
</div>

You can also put regular text between your rows of images.
Say you wanted to write a little bit about your project before you posted the rest of the images.
You describe how you toiled, sweated, _bled_ for your project, and then... you reveal its glory in the next row of images.

<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/6.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/11.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    You can also have artistically styled 2/3 + 1/3 images, like these.
</div>

The code is simple.
Just wrap your images with `<div class="col-sm">` and place them inside `<div class="row">` (read more about the <a href="https://getbootstrap.com/docs/4.4/layout/grid/">Bootstrap Grid</a> system).
To make images responsive, add `img-fluid` class to each; for rounded corners and shadows use `rounded` and `z-depth-1` classes.
Here's the code for the last row of images above:

{% raw %}

```html
<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/6.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
  </div>
  <div class="col-sm-4 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/11.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
```

{% endraw %}
