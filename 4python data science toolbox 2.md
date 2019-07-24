
## iterables, iterators,list comprehension and generators

### iterators in pythonland
iterables:  
lists, tuples, strings, range object, dictionaries, file connections  
an object with an associated iter() method  
applying iter() to an iterable creates an iterator
iterator:
produce consecutive values with next()  
next()可用于查看iterator/iterable里的各项


```python
# create iterator from iterable
word='Da'
it=iter(word) # 在一个iterable上用iter()
next(it)
```




    'D'




```python
next(it)
```




    'a'




```python
next(it)
```


    ---------------------------------------------------------------------------

    StopIteration                             Traceback (most recent call last)

    <ipython-input-3-bc1ab118995a> in <module>
    ----> 1 next(it)
    

    StopIteration: 



```python
word='Data'
it=iter(word)
print(*it) # * unpacks all elements of the iterator or iterable
```

    D a t a
    


```python
print(*it) # 第二遍没有可以iterate的东西了
```

    
    


```python
# iter dict, applying items()
pythonistas={'hugo':'bowne-anderson','francis':'castro'}
for key,value in pythonistas.items():
    print(key,value)
```

    hugo bowne-anderson
    francis castro
    


```python
# iter file connections 
file=open('file.txt')
it=iter(file)
print(next(it))
```

    this is the first line
    
    


```python
print(next(it))
```

    this is the second line
    

an iterable is an object that can return an iterator, while an iterator is an object that keeps state and produces the next value when you call next() on it. 


```python
# iter range()
for i in range(5):
    print(i)
```

    0
    1
    2
    3
    4
    

range() doesn't actually create the list; instead, it creates a range object with an iterator that produces the values until it reaches the limit 

There are also functions that take iterators and iterables as arguments. For example, the list() and sum() functions return a list and the sum of elements, respectively.


```python
# Create a range object: values
values = range(10,21)

# Print the range object
print(values)

# Create a list of integers: values_list
values_list = list(values)

# Print values_list
print(values_list)

# Get the sum of values: values_sum
values_sum = sum(values) # sum的是range()

# Print values_sum
print(values_sum)

```

    range(10, 21)
    [10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20]
    165
    

### playing with iterators  
enumerate():  
takes any iterable as argument, e.g.list


```python
avengers=['hawkeye','iron man','thor','quicksilver']
e=enumerate(avengers)
print(type(e))
print(e)

e_list=list(e) # 转化为list of tuples
print(e_list)
```

    <class 'enumerate'>
    <enumerate object at 0x0000029A04633090>
    [(0, 'hawkeye'), (1, 'iron man'), (2, 'thor'), (3, 'quicksilver')]
    

enumerate object本身也是一个iterable，可以被unpack/loop over


```python
avengers=['hawkeye','iron man','thor','quicksilver']

for index,value in enumerate(avengers):
    print(index,value)
```

    0 hawkeye
    1 iron man
    2 thor
    3 quicksilver
    


```python
# 默认index从0开始，可用start argument 调整
for index,value in enumerate(avengers,start=10):
    print(index,value)
```

    10 hawkeye
    11 iron man
    12 thor
    13 quicksilver
    

zip()接收任意个iterables，输出iterator of tuples


```python
avengers=['hawkeye','iron man','thor','quicksilver']
names=['barton','stark','odinson','maximoff']

z=zip(avengers,names)
print(type(z))
# zip object是iterator of tuples
```

    <class 'zip'>
    


```python
# 转化为list来print
z_list=list(z)
print(z_list)
```

    [('hawkeye', 'barton'), ('iron man', 'stark'), ('thor', 'odinson'), ('quicksilver', 'maximoff')]
    

每一个element都是一个tuple，每个tuple里包含各个list中的对应第n项


```python
# for loop
avengers=['hawkeye','iron man','thor','quicksilver']
names=['barton','stark','odinson','maximoff']

for z1,z2 in zip(avengers,names):
    print(z1,z2)
```

    hawkeye barton
    iron man stark
    thor odinson
    quicksilver maximoff
    


```python
# 使用*
avengers=['hawkeye','iron man','thor','quicksilver']
names=['barton','stark','odinson','maximoff']

z=zip(avengers,names)
print(*z)
```

    ('hawkeye', 'barton') ('iron man', 'stark') ('thor', 'odinson') ('quicksilver', 'maximoff')
    


```python
mutants = ('charles xavier', 
            'bobby drake', 
            'kurt wagner', 
            'max eisenhardt', 
            'kitty pryde')
powers=('telepathy',
       'thermokinesis',
       'teleportation',
       'magnetokinesis',
       'intangibility')

# Create a zip object from mutants and powers: z1
z1 = zip(mutants,powers)

# Print the tuples in z1 by unpacking with *
print(*z1)

# Re-create a zip object from mutants and powers: z1
z1 = zip(mutants,powers)

# 'Unzip' the tuples in z1 by unpacking with * and zip(): result1, result2
result1, result2 = zip(*z1)

# Check if unpacked tuples are equivalent to original tuples
print(result1 == mutants)
print(result2 == powers)

```

    ('charles xavier', 'telepathy') ('bobby drake', 'thermokinesis') ('kurt wagner', 'teleportation') ('max eisenhardt', 'magnetokinesis') ('kitty pryde', 'intangibility')
    True
    True
    

### using iterators to load large files into memory

too much data! -solution:  
load data in chunks  
每一个chunk里单独处理，切断后再加载下一个chunk  
specify the chunk: chunksize  


```python
# 假设例子(不要运行)
import pandas as pd
result=[]
for chunk in pd.read_csv('data.csv',chunksize=1000):
    result.append(sum(chunk['x'])) # sum of column of interest
total=sum(result)
print(total)
```


```python
# 上述等价于 假设例子(不要运行)
import pandas as pd
total=0
for chunk in pd.read_csv('data.csv',chunksize=1000):
    total += sum(chunk['x'])
print(total)
```


```python
# 转化为函数

# Define count_entries()
def count_entries(csv_file,c_size,colname):
    """Return a dictionary with counts of
    occurrences as value for each key."""
    
    # Initialize an empty dictionary: counts_dict
    counts_dict = {}

    # Iterate over the file chunk by chunk
    for chunk in pd.read_csv(csv_file,chunksize=c_size):

        # Iterate over the column in DataFrame
        for entry in chunk[colname]:
            if entry in counts_dict.keys():
                counts_dict[entry] += 1
            else:
                counts_dict[entry] = 1

    # Return counts_dict
    return counts_dict

# Call count_entries(): result_counts
# e.g.result_counts = count_entries('tweets.csv',10,'lang')

# Print result_counts
# e.g.print(result_counts)

```

list comprehensions:  
create lists from other lists, DataFrame columns, etc.  
more efficient than using a for loop  

### list comprehension  
[values wanted/output expression + for referring to the original list]  
list comprehension 可用于any iterable


```python
# 等价于 for loop
nums=[12,8,21,3,16]
new_nums=[]
for num in nums:
    new_nums.append(num + 1)
print(new_nums)
```

    [13, 9, 22, 4, 17]
    


```python
# list comprehension等价于 for loop
nums=[12,8,21,3,16]
new_nums=[num+1 for num in nums]
print(new_nums)
```

    [13, 9, 22, 4, 17]
    


```python
# 用于range()
result=[num for num in range(11)]
print(result)
```

    [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
    

list comprehension:  
components:  
iterable  
iterator variable(represent members of iterable)  
output expression


```python
# for nested loops
pairs_1=[]
for num1 in range(0,2):
    for num2 in range(6,8):
        pairs_1.append((num1,num2))
        
print(pairs_1)
```

    [(0, 6), (0, 7), (1, 6), (1, 7)]
    


```python
# 如何用list comprehension 实现
pairs_2=[(num1,num2) for num1 in range(0,2) for num2 in range(6,8)]
print(pairs_2)
```

    [(0, 6), (0, 7), (1, 6), (1, 7)]
    

To create the list of lists, you simply have to supply the list comprehension as the output expression of the overall list comprehension:  
[[output expression] for iterator variable in iterable]  
Note that here, the output expression is itself a list comprehension.

### conditionals in comprehension

[ output expression for iterator variable in iterable if predicate expression ].


```python
# conditionals on the iterable
[num**2 for num in range(10) if num % 2 ==0]
```




    [0, 4, 16, 36, 64]



% operator:  
the % (modulo) operator yields the remainder from the division of the first argument by the second


```python
# conditional on the output expression
[num**2 if num%2==0 else 0 for num in range(10)]
```




    [0, 0, 4, 0, 16, 0, 36, 0, 64, 0]




```python
# dict comprehensions to create dictionaries
# use curly braces instead of brackets
# key and value are seperated by :

pos_neg={num:-num for num in range(9)}
print(pos_neg)
print(type(pos_neg))
```

    {0: 0, 1: -1, 2: -2, 3: -3, 4: -4, 5: -5, 6: -6, 7: -7, 8: -8}
    <class 'dict'>
    

### generator expressions


```python
# use () instead of [] in list comprehension creating generator
(2*num for num in range(10))
```




    <generator object <genexpr> at 0x0000025EA4A4F570>



list comprehension - returns a list  
generators - returns a generator object  
both can be iterated over


```python
# printing values from generator
result = (num for num in range(6))

for num in result:
    print(num)
```

    0
    1
    2
    3
    4
    5
    


```python
# 或使用list()
result=(num for num in range(6))
print(list(result))
```

    [0, 1, 2, 3, 4, 5]
    


```python
# 也可被next()
result=(num for num in range(6))
print(next(result))
```

    0
    


```python
print(next(result))
```

    1
    

由于generator不直接创建list，因此可以generator很大的信息量，而comprehension由于要创建list，所以不能存储过大的信息量


```python
# conditionals 等comprehension里用的，generator一样可以使用
even_nums=(num for num in range(10) if num % 2 ==0)
print(list(even_nums))
```

    [0, 2, 4, 6, 8]
    

generator functions:  
produces generator objects when called  
defined like a regular function - def  
yields a sequence of values instead of returning a single value  
generates a value with yield keyword


```python
def num_sequence(n):
    """Generate values from 0 to n."""
    i=0
    while i<n:
        yield i
        i+=1
        
result=num_sequence(5)
print(type(result))
```

    <class 'generator'>
    


```python
for item in result:
    print(item)
```

    0
    1
    2
    3
    4
    


```python
# Create a list of strings
lannister = ['cersei', 'jaime', 'tywin', 'tyrion', 'joffrey']

# Define generator function get_lengths
def get_lengths(input_list):
    """Generator function that yields the
    length of the strings in input_list."""

    # Yield the length of a string
    for person in input_list:
        yield len(person)

# Print the values generated by get_lengths()
for value in get_lengths(lannister):
    print(value)
```

    6
    5
    5
    6
    7
    

To begin, you need to open a connection to this file using what is known as a context manager.   
For example, the command with open('datacamp.csv') as datacamp binds the csv file 'datacamp.csv' as datacamp in the context manager.  
Here, the with statement is the context manager, and its purpose is to ensure that resources are efficiently allocated when opening a connection to a file.


```python

```
