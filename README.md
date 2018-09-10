
# List and String Review
Below we review a few list methods and programming patterns. This will be a foundational skill that you will use nearly everywhere in your coding practice.

## The Pickle Module

To see a more detailed list to work with, we're going to import the pickle module. This module lets you save pretty much any python object whether its a function, class, or piece of data. (We've previously seen how to import spreadsheet data with Pandas.)


```python
import pickle
```


```python
#Open the file where stuff is stored (this is similar to python's built in method)
pkl_file = open('names.pkl', 'rb')
#Use pickles load method
names = pickle.load(pkl_file)
#Close the file you are done working with.
pkl_file.close()
```

## Previewing Data
Remember we can print the length of many objects, and we can use slices to preview the first few items:


```python
print(len(names))
print(names[:10])
```

    100
    ['Joseph Owens ', 'Lamar Webster  ', ' Lester Garner ', ' Yvonne Perkins   ', 'Theodore Byrd', 'Billy Wallace   ', 'Jeremiah Burns   ', 'Heather Bridges', 'Shannon Ramirez', ' Jermaine Gibson']


## Slicing and Iterating through Lists
Recall that we can also iterate through a list if we want to check some condition or perform some operation.


```python
#Iterate through the first 5 elements (indexed 0 through 4) of the list
for name in names[:5]:
    print(name)
```

    Joseph Owens 
    Lamar Webster  
     Lester Garner 
     Yvonne Perkins   
    Theodore Byrd



```python
#A more complicated example with a conditional and a string slice

#Iterate throught the entire list
for name in names:
    #Slice the current string and perform  a conditional on the 0th indexed character
    if name[0] == 'M':
        print('This name starts with M!')
        print(name)
        print('\n')
```

    This name starts with M!
    Mabel Fleming 
    
    
    This name starts with M!
    Marcia Griffin
    
    
    This name starts with M!
    Meredith Bowen
    
    
    This name starts with M!
    Mona Estrada
    
    
    This name starts with M!
    Maryann Armstrong
    
    


## List Comprehensions
We've briefly seen some examples of list comprehensions such as:  
` df.columns = [col.strip() for col in df.columns]`. 
This can often be a handy way to quickly encapsulate an idea that requires a for loop. In the example above, we iterate through df.columns and strip any leading/trailing whitespace from the column name. We then reassign this new list (with whitespace removed) back to df.columns.


```python
#Similar to the second example above
[name for name in names if name[0]=='M']
```




    ['Mabel Fleming ',
     'Marcia Griffin',
     'Meredith Bowen',
     'Mona Estrada',
     'Maryann Armstrong']



## Cleaning and Transforming Data
You might notice that some of our names are poorly formated. Specifically, many of the names have some extra whitespace.


```python
names[:5]
```




    ['Joseph Owens ',
     'Lamar Webster  ',
     ' Lester Garner ',
     ' Yvonne Perkins   ',
     'Theodore Byrd']



# List and String Practice
Below look at the original style 1 example. Your first goal is to figure out what transformation to apply to each name in names in order to remove all that extra whitespace. Once you've done that, rewrite the code in the more pythonic list comprehension. To summarize:  
* Clean up each name in the for loop
* Rewrite the for loop as a list comprehension


```python
#Style 1
names2 = []
for name in names:
    new_name = #You code here; do something to name to clean it up 
    names2.append(new_name)
```


```python
#Style 2: More Pythonic!
names = [] #Your code here; rewrite the above code block as a List comprehension!
```

# Extension
Below, look at the code I used to add random whitespace to some entries in the list. The new code references a python math package called **numpy**. Traditionally, this is imported under the alias np; `import numpy as np`. The `np.random.rand()` method produces a random floating number between 0 and 1. Thus the conditional should apply to roughly 25% of cases. Similarly, the amount of whitespace added is a random integer between 1 and 4.  

The **enumearte()** method is also demonstrated below. It is a very useful built in function that returns the index of the iterable. Thus the line `for n, name in enumerate(names)` will return 0, name[0] followed by 1, name[1] followed by 2, name[2], etc. As you can see, this is useful for getting surrounding elements later, where we can create a window view before or after the current element (Here `names[n-2:n+3]`).
Review the code below and add additional comments describing what the various lines of code do. Be sure to review the *pop* and *insert* methods in particular.


```python
#Here's how I made the data a messier!
#Warning: rerunning this will continue to muck up the data
import numpy as np

print(len(names))
print_count = 0
for n, name in enumerate(names):
    if np.random.rand() < .25:
        if print_count < 3:
            print('Originally:')
            print(names[n-2:n+3])
        old = names.pop(n)
        new = old + ' '*np.random.randint(1,4)
        names.insert(n, new)
        if print_count < 3:
            print('Now:')
            print(names[n-2:n+3])
            print('Item updated: {} to {}'.format(old,new))
            print('\n')
            print_count += 1
print(len(names))
```

    100
    Originally:
    ['Billy Wallace   ', 'Jeremiah Burns   ', 'Heather Bridges', 'Shannon Ramirez', ' Jermaine Gibson']
    Now:
    ['Billy Wallace   ', 'Jeremiah Burns   ', 'Heather Bridges ', 'Shannon Ramirez', ' Jermaine Gibson']
    Item updated: Heather Bridges to Heather Bridges 
    
    
    Originally:
    ['Heather Bridges ', 'Shannon Ramirez', ' Jermaine Gibson', 'Lance Thompson', 'Frankie Clarke']
    Now:
    ['Heather Bridges ', 'Shannon Ramirez', ' Jermaine Gibson  ', 'Lance Thompson', 'Frankie Clarke']
    Item updated:  Jermaine Gibson to  Jermaine Gibson  
    
    
    Originally:
    [' Kimberly Weave ', 'Gabriel Murphy', 'Mabel Fleming ', 'Ignacio Thornton  ', 'Lauren Fields  ']
    Now:
    [' Kimberly Weave ', 'Gabriel Murphy', 'Mabel Fleming   ', 'Ignacio Thornton  ', 'Lauren Fields  ']
    Item updated: Mabel Fleming  to Mabel Fleming   
    
    
    100


## DIY
Create your own loop similar above to make a messy (but reversible) data *noiser*. Then write and apply a function that would remove that noise and clean the data.
