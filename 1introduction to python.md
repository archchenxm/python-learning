
## PYTHON BASICS

float()  
str()  
int()  
bool()



```python
2+3
```




    5




```python
'ab'+'cd'
```




    'abcd'



## PYTHON LISTS
name a collection of values  
contain any type  
contain different types  
[a, b, c]  
list里可以包含list


```python
# subsetting lists
fam=["liz",1.73,"emma",1.68,"mom",1.71,"dad",1.89]
fam[3]
```




    1.68




```python
fam[3:5]
# [start : end]
# inclusive : exclusive
```




    [1.68, 'mom']




```python
# change list elements
fam=["liz",1.73,"emma",1.68,"mom",1.71,"dad",1.89]
print(fam)

fam[7]=1.86

print(fam)
```

    ['liz', 1.73, 'emma', 1.68, 'mom', 1.71, 'dad', 1.89]
    ['liz', 1.73, 'emma', 1.68, 'mom', 1.71, 'dad', 1.86]
    


```python
# adding and removing elements
fam+["me",1.79]
print(fam)

del(fam[2])
print(fam)
```

    ['liz', 1.73, 'emma', 1.68, 'mom', 1.71, 'dad', 1.86]
    ['liz', 1.73, 1.68, 'mom', 1.71, 'dad', 1.86]
    


```python
# x与y完全等价，修改y即修改x
x=['a','b','c']
y=x
y[1]='z'
print(y)
print(x)
```

    ['a', 'z', 'c']
    ['a', 'z', 'c']
    


```python
# y是另一个list，改变y不改变x
x=['a','b','c']
y=list(x) # 或y=x[:]
y[1]='z'
print(x)
```

    ['a', 'b', 'c']
    

## FUNCTIONS AND PACKAGES


```python
fam=[1.73,1.68,1.71,1.89]
print(max(fam))
```

    1.89
    


```python
round(1.68,1)
# 保留几位小数，不写则保留到整数
```




    1.7




```python
help(round)
# 查询function的documents
```

    Help on built-in function round in module builtins:
    
    round(number, ndigits=None)
        Round a number to a given precision in decimal digits.
        
        The return value is an integer if ndigits is omitted or None.  Otherwise
        the return value has the same type as the number.  ndigits may be negative.
    
    

#### METHODS: Functions that belong to objects



```python
# list methods
print(fam)
print(fam.index(1.73))
print(fam.count(1.68))

fam.append('me') # 增加"me"
print(fam)
```

    [1.73, 1.68, 1.71, 1.89]
    0
    1
    [1.73, 1.68, 1.71, 1.89, 'me']
    


```python
# str methods
sister='liz'
print(sister.capitalize()) # 首字母大写
print(sister.replace('z','sa')) # 替换字段
print(sister.index('z')) # 显示第几个字母是什么
```

    Liz
    lisa
    2
    

## NUMPY

list不能list间一一对应运算，list+list会合并list  
numpy array 只能包含一种type，array之间的运算是一一对应运算


```python
height=[1.73,1.68,1.71]
weight=[65.4,59.2,63.6]
# weight/height**2 会错误
import numpy as np
np_height=np.array(height)
np_weight=np.array(weight)
bmi=np_weight/np_height**2
print(bmi)
```

    [21.85171573 20.97505669 21.75028214]
    


```python
# numpy subsetting
print(bmi[1])
print(bmi>21)
print(bmi[bmi>21])
```

    20.97505668934241
    [ True False  True]
    [21.85171573 21.75028214]
    

2D numpy arrays


```python
np_2d=np.array([[1.73,1.68,1.71],[65.4,59.2,63.6]]) # 内部是一个list of list
np_2d.shape # 看2d array的形状（行，列）
```




    (2, 3)




```python
# 2d numpy array 也只能包含一种type
import numpy as np
np_2d=np.array([[1.73,1.68,1.71],[65.4,59.2,"63.6"]]) 
print(np_2d)
```

    [['1.73' '1.68' '1.71']
     ['65.4' '59.2' '63.6']]
    


```python
# subsetting
import numpy as np
np_2d=np.array([[1.73,1.68,1.71],[65.4,59.2,63.6]]) 

print(np_2d[0])

print(np_2d[0][2])

print(np_2d[0,2])

print(np_2d[:,1:3])

print(np_2d[1,:])
```

np.mean(array)  
np.median()  
np.corrcoef()  # 两个参数
np.std()  
sum()  
sort()  
np.column_stack() # 两个参数，两个nparray，作为两个column合成一个



```python
import numpy as pd
# round，保留小数位数
# 随机，distribution mean,distribution standard dev.,numbers of samples
height=np.round(np.random.normal(1.75,0.20,5000),2)
weight=np.round(np.random.normal(60.32,15,5000),2)
np_city=np.column_stack((height,weight))
print(np_city)
```
