
### 1 MATPLOTLIB


```python
# plot
import matplotlib.pyplot as plt
year=[1950,1970,1990,2010]
pop=[2.519,3.692,5.263,6.972]
plt.plot(year,pop)
#         x    y
# plt.scatter(year,pop) 散点图

plt.xlabel('Year')
plt.ylabel('Population')
plt.title('WWW')
plt.yticks([0,2,4,6,8],['0','2B','4B','6B','8B']) # 调整y轴刻度读数

plt.show()
```


![png](output_1_0.png)



```python
# histogram
import matplotlib.pyplot as plt
# help(plt.hist)
values=[0,0.6,1.4,1.6,2.2,2.5,2.6,3.2,3.5,3.9,4.2,2.6]
plt.hist(values,bins=3)
plt.show()
```


![png](output_2_0.png)


plt.text(x,y,"text")——添加图上在（x，y）处的文字  
plt.grid(True)——显示网格
plt.scatter(x,y,s=,c=,alpha=)——size, color, opacity

### 2 DICTIONARIES & PANDAS


```python
# dictionaries
pop=[30.55, 2.77, 39.21]
countries=['afghanistan', 'albania', 'algeria']
world={'afghanistan':30.55, 'albania':2.77, 'algeria':39.21}
world['albania']

# dict_name[key]
# 查看所有"key"s，dict.keys()
# result:value
# dict内无重复的key，且list不可以作为key，key必须是immutable objects
```




    2.77




```python
world={'afghanistan':30.55, 'albania':2.77, 'algeria':39.21}
# 增加dict内容
world['sealand']=0.000027
print(world)

# 查看key是否在dict内
print('sealand' in world)

# 修改某项
world['sealand']=0.000028
print(world)

# 删除某项
del(world['sealand'])
print(world)
```

    {'afghanistan': 30.55, 'albania': 2.77, 'algeria': 39.21, 'sealand': 2.7e-05}
    True
    {'afghanistan': 30.55, 'albania': 2.77, 'algeria': 39.21, 'sealand': 2.8e-05}
    {'afghanistan': 30.55, 'albania': 2.77, 'algeria': 39.21}
    


```python
# list 与 dictionary 对比
dict={"list":['select,update and remove;[]','indexed by a range of numbers'],
     "dictionary":['select,update and remove;[]','indexed by unique keys']
     }
import pandas as pd
pd.DataFrame(dict)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>list</th>
      <th>dictionary</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>select,update and remove;[]</td>
      <td>select,update and remove;[]</td>
    </tr>
    <tr>
      <th>1</th>
      <td>indexed by a range of numbers</td>
      <td>indexed by unique keys</td>
    </tr>
  </tbody>
</table>
</div>




```python
# pandas
# row=observations, column=variable

#从dictionary建立DataFrame
dict={'country':['Brazil','Russia','India'],
     'capital':['Brasilia','Moscow','New Delhi'],
     'area':[8.516, 17.10, 3.286]
     }
import pandas as pd
brics=pd.DataFrame(dict)
print(brics)

# 调整row labels
brics.index=['BR','RU','IN']
print(brics)
```

      country    capital    area
    0  Brazil   Brasilia   8.516
    1  Russia     Moscow  17.100
    2   India  New Delhi   3.286
       country    capital    area
    BR  Brazil   Brasilia   8.516
    RU  Russia     Moscow  17.100
    IN   India  New Delhi   3.286
    


```python
# 从csv导入形成DataFrame
brics=pd.read_csv("brics.csv")
print(brics)

# 从csv导入同时修改row label
brics=pd.read_csv('brics.csv',index_col=0)
print(brics)
```

      Unnamed: 0 country    capital    area
    0         BR  Brazil   Brasilia   8.516
    1         RU  Russia     Moscow  17.100
    2         IN   India  New Delhi   3.286
       country    capital    area
    BR  Brazil   Brasilia   8.516
    RU  Russia     Moscow  17.100
    IN   India  New Delhi   3.286
    


```python
# column access
print(brics["country"])
type(brics["country"])

# 输出series
```

    BR    Brazil
    RU    Russia
    IN     India
    Name: country, dtype: object
    




    pandas.core.series.Series




```python
# column access
print(brics[["country"]])
type(brics[["country"]])

# 输出DataFrame
```

       country
    BR  Brazil
    RU  Russia
    IN   India
    




    pandas.core.frame.DataFrame




```python
# 输出多个column
brics[["country","capital"]]

# DataFrame
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>country</th>
      <th>capital</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>BR</th>
      <td>Brazil</td>
      <td>Brasilia</td>
    </tr>
    <tr>
      <th>RU</th>
      <td>Russia</td>
      <td>Moscow</td>
    </tr>
    <tr>
      <th>IN</th>
      <td>India</td>
      <td>New Delhi</td>
    </tr>
  </tbody>
</table>
</div>




```python
# row access
brics[1:3]
# DataFrame
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>country</th>
      <th>capital</th>
      <th>area</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>RU</th>
      <td>Russia</td>
      <td>Moscow</td>
      <td>17.100</td>
    </tr>
    <tr>
      <th>IN</th>
      <td>India</td>
      <td>New Delhi</td>
      <td>3.286</td>
    </tr>
  </tbody>
</table>
</div>




```python
# row access: loc(label-based),iloc(integer position-based)
brics.loc["RU"]
# row as pandas series

brics.loc[["RU"]]
# DataFrame
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>country</th>
      <th>capital</th>
      <th>area</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>RU</th>
      <td>Russia</td>
      <td>Moscow</td>
      <td>17.1</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 选取其中某些row，可以不连续
brics.loc[["RU","IN"]]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>country</th>
      <th>capital</th>
      <th>area</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>RU</th>
      <td>Russia</td>
      <td>Moscow</td>
      <td>17.100</td>
    </tr>
    <tr>
      <th>IN</th>
      <td>India</td>
      <td>New Delhi</td>
      <td>3.286</td>
    </tr>
  </tbody>
</table>
</div>




```python
# row & column loc
brics.loc[["RU","IN"],["country","capital"]]

# 需要指定某些行/列的时候才需要内部多一个[]
brics.loc[:, ["country","capital"]]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>country</th>
      <th>capital</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>BR</th>
      <td>Brazil</td>
      <td>Brasilia</td>
    </tr>
    <tr>
      <th>RU</th>
      <td>Russia</td>
      <td>Moscow</td>
    </tr>
    <tr>
      <th>IN</th>
      <td>India</td>
      <td>New Delhi</td>
    </tr>
  </tbody>
</table>
</div>




```python
# row access iloc
brics.iloc[[1]]
brics.iloc[[1,2]]

# row & column access
brics.iloc[[1,2],[0,1]]
brics.iloc[:,[0,1]]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>country</th>
      <th>capital</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>BR</th>
      <td>Brazil</td>
      <td>Brasilia</td>
    </tr>
    <tr>
      <th>RU</th>
      <td>Russia</td>
      <td>Moscow</td>
    </tr>
    <tr>
      <th>IN</th>
      <td>India</td>
      <td>New Delhi</td>
    </tr>
  </tbody>
</table>
</div>



### 3 LOGIC,CONTROL FLOW AND FILTERING

<, <=, >, >=, ==, !=  
str可与str比较大小，考虑其在字母表中顺序靠前，则小  
True=1，False=0


```python
# np.array 比较大小
import numpy as np
np_height=np.array([1.73,1.68,1.71,1.89,1.79])
np_weight=np.array([65.4,59.2,63.6,88.4,68.7])
bmi=np_height/np_weight**2
bmi>23
```




    array([False, False, False, False, False])



boolean operators  
and or not
对于numpy
np.logical_and
np.logical_or
np.logical_not


```python
# for numpy
bmi>21
bmi<22
np.logical_and(bmi>21,bmi<22)
```




    array([False, False, False, False, False])



#### conditional statements  
if condition:  
    expression  
elif condition:  
    expression  
else:  
    expression  
expression # not part of it


```python
import pandas as pd
brics=pd.read_csv("brics.csv", index_col=0)
brics
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>country</th>
      <th>capital</th>
      <th>area</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>BR</th>
      <td>Brazil</td>
      <td>Brasilia</td>
      <td>8.516</td>
    </tr>
    <tr>
      <th>RU</th>
      <td>Russia</td>
      <td>Moscow</td>
      <td>17.100</td>
    </tr>
    <tr>
      <th>IN</th>
      <td>India</td>
      <td>New Delhi</td>
      <td>3.286</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 筛选pandas DataFrame
# 某个column哪些项符合要求
brics['area']>8
```




    BR     True
    RU     True
    IN    False
    Name: area, dtype: bool




```python
# 一步完成
brics[brics['area']>8]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>country</th>
      <th>capital</th>
      <th>area</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>BR</th>
      <td>Brazil</td>
      <td>Brasilia</td>
      <td>8.516</td>
    </tr>
    <tr>
      <th>RU</th>
      <td>Russia</td>
      <td>Moscow</td>
      <td>17.100</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 包含Boolean operators，筛选DataFrame
np.logical_and(brics['area']>8,brics['area']<10)
```




    BR     True
    RU    False
    IN    False
    Name: area, dtype: bool




```python
# 一步完成
brics[np.logical_and(brics['area']>8,brics['area']<10)]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>country</th>
      <th>capital</th>
      <th>area</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>BR</th>
      <td>Brazil</td>
      <td>Brasilia</td>
      <td>8.516</td>
    </tr>
  </tbody>
</table>
</div>



### 4 LOOPS


```python
# for loop
# for var in seq:
#    expression
fam = [1.73, 1.68, 1.71, 1.89]
for height in fam:
    print(height)
```


```python
# 添加index显示的输出一个list
fam = [1.73, 1.68, 1.71, 1.89]
for index, height in enumerate(fam):
    print('index'+str(index)+":"+str(height))
```


```python
# for loop 可用于list以外
for c in 'family':
    print(c.capitalize())
```


```python
# FOR DICTIONARY
world = {'afghanistan':30.55,
        'albania':2.77,
        'algeria':39.21}
for key, value in world.items():
    print(key + "---" + str(value))
# print dictionary 是随机的
```

    afghanistan---30.55
    albania---2.77
    algeria---39.21
    


```python
# for np array：1D可直接用，2D如下：
import numpy as np
np_height=np.array([1.73,1.68,1.71,1.89,1.79])
np_weight=np.array([65.4,59.2,63.6,88.4,68.7])
meas=np.array([np_height,np_weight])

for val in np.nditer(meas):
    print(val)
```

    1.73
    1.68
    1.71
    1.89
    1.79
    65.4
    59.2
    63.6
    88.4
    68.7
    


```python
# for pandas dataframe
import pandas as pd
# brics=pd.read_csv('brics.csv',index_col=0)
# 创建一个brics
dict={'country':['Brazil','Russia','India'],
     'capital':['Brasilia','Moscow','New Delhi'],
     'area':[8.516, 17.10, 3.286]
     }
brics=pd.DataFrame(dict)
brics.index=['BR','RU','IN']

for lab, row in brics.iterrows():
    #print(lab) # 输出label
    #print(row) # 输出一个row里的全部内容(附带有column title)
    print(lab + ":" + row["capital"])
    
# 可以用for loop为DataFrame增加一个column
for lab, row in brics.iterrows():
    brics.loc[lab,'name_length']=len(row['country'])
#print(brics)

# 更高效的方法，使用apply，不需要for loop
brics['name_length']=brics['country'].apply(len)
#print(brics)
```

    BR:Brasilia
    RU:Moscow
    IN:New Delhi
    

### CASE STUDY: HACKER STATISTICS

解决一个问题时使用模拟的方式：hacker statistics


```python
# random generators
import numpy as np
np.random.rand()
# random from 0 to 1

np.random.seed(123)
# 随机数的本质：从seed计算出一个数，因此，同一个seed生成的一组随机数一一对应相同
```




    0.033291671369947484




```python
# 生成整数随机数
import numpy as np
np.random.seed(123)# 设置seed参数这个操作本身无结果，无输出
coin=np.random.randint(0,2) # randomly generate 0 or 1,不包含2
print(coin)
if coin==0:
    print('heads')
else:
    print('tails')
```

    0
    heads
    

用dice决定下一步——random step  
用dice 100次决定下一步——random walk  


```python
import numpy as np
np.random.seed(123)
outcomes=[] # initialize an empty list 
for x in range(10): 
# range(): 生成一个list of numbers(一组从头到尾的整数），用于迭代
    coin=np.random.randint(0,2)
    if coin==0:
        outcomes.append("heads") # append(),增加
    else:
        outcomes.append("tails")
print(outcomes)

# 这个不是一个random walk
# 而是一组random steps
# 因为items of the list 不是基于前面的部分的
```

    ['heads', 'tails', 'heads', 'heads', 'heads', 'heads', 'heads', 'tails', 'tails', 'heads']
    


```python
import numpy as np
np.random.seed(123)

tails=[0]
for x in range(10):
    coin=np.random.randint(0,2)
    tails.append(tails[x]+coin)
    
    # add coin to the previous number of tails: tails[x]+coin

print(tails)

# 这是一个random walk
```

    [0, 0, 1, 1, 1, 1, 1, 1, 2, 3, 3]
    


```python
import numpy as np
np.random.seed(123)

# Initialize random_walk
random_walk=[0]

for x in range(100) :
    # Set step: last element in random_walk
    step=random_walk[x]

    # Roll the dice
    dice = np.random.randint(1,7)

    # Determine next step
    if dice <= 2:
        step = step - 1
        # Replace below: use max to make sure step can't go below 0
        # step =max(0,step-1)
        # x = max(10, x - 1),保证x在减小的时候永远不小于10
        
    elif dice <= 5:
        step = step + 1
    else:
        step = step + np.random.randint(1,7)

    # append next_step to random_walk
    random_walk.append(step)

# Print random_walk
print(random_walk)
```

    [0, 3, 4, 5, 4, 5, 6, 7, 6, 5, 4, 3, 2, 1, 0, -1, 0, 5, 4, 3, 4, 3, 4, 5, 6, 7, 8, 7, 8, 7, 8, 9, 10, 11, 10, 14, 15, 14, 15, 14, 15, 16, 17, 18, 19, 20, 21, 24, 25, 26, 27, 32, 33, 37, 38, 37, 38, 39, 38, 39, 40, 42, 43, 44, 43, 42, 43, 44, 43, 42, 43, 44, 46, 45, 44, 45, 44, 45, 46, 47, 49, 48, 49, 50, 51, 52, 53, 52, 51, 52, 51, 52, 53, 52, 55, 56, 57, 58, 57, 58, 59]
    


```python
# Import matplotlib.pyplot as plt
import matplotlib.pyplot as plt

# Plot random_walk
plt.plot(random_walk)
# 如果plot只填写一个参数
# the index of the list——the x axis
# the values in the list——the y axis.

# Show the plot
plt.show()

```


![png](output_44_0.png)



```python
# distribution

import numpy as py
np.random.seed(123)

# 增加visualization
import matplotlib.pyplot as plt

# 1000次模拟“扔10次硬币向下的次数为多少”
final_tails=[]
for x in range(1000):
    
    # 10次模拟扔硬币，统计向下的次数
    tails=[0]
    for x in range(10):
        coin=np.random.randint(0,2)
        # 每个tails list 是扔硬币向下次数逐渐累加的一组数字，共计11个
        tails.append(tails[x]+coin)
        
    # 每一个tails list的最后一项代表“扔10次硬币有多少次向下”
    # 汇集形成final_tails这个list
    final_tails.append(tails[-1])
    
# 生成直方图，代表distribution
plt.hist(final_tails,bins=10)
plt.show()

# print(final_tails)，显示1000次模拟的结果
```


![png](output_45_0.png)



```python
# 爬帝国大厦问题
# 一个人根据掷色子结果爬楼，能不能爬到60级（有一定概率掉下来）
import numpy as np
import matplotlib.pyplot as plt
np.random.seed(123)

# initialize and populate all_walks
all_walks = []
for i in range(10) :
    random_walk = [0]
    for x in range(100) :
        step = random_walk[-1]
        dice = np.random.randint(1,7)
        if dice <= 2:
            step = max(0, step - 1)
        elif dice <= 5:
            step = step + 1
        else:
            step = step + np.random.randint(1,7)
            
        
        # Implement clumsiness，次数多了可能会有骤跌（归零）的曲线
        if np.random.rand()<=0.001:
            step = 0

        random_walk.append(step)
    all_walks.append(random_walk)

# Convert all_walks to Numpy array: np_aw
np_aw=np.array(all_walks)

# Plot np_aw and show
plt.plot(np_aw)
plt.show()

# Clear the figure
plt.clf()

# Transpose np_aw: np_aw_t
np_aw_t=np.transpose(np_aw)
# 第一行颠倒为第一列，第二行变为第二列

# Plot np_aw_t and show
plt.plot(np_aw_t)
plt.show()
```


![png](output_46_0.png)



![png](output_46_1.png)



```python
# 显示最后一步到哪里的distribution
# Select last row from np_aw_t: ends
ends= np_aw_t[-1,:]

# Plot histogram of ends, display plot
plt.hist(ends)
plt.show()
```


![png](output_47_0.png)



```python
# 计算上到60级的概率
np.mean(ends>=60)
# np.mean(ends > 30) gives you the fraction of simulations that ended higher than step 30.
```




    0.9


