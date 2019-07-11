
## WRITING YOUR OWN FUNCTIONS
#### user-defined functions


```python
# built-in functions
# str()
x=str(5)
print(x)
print(type(x))
```

    5
    <class 'str'>
    


```python
# defining a function
def square():  # <-- function header
    new_value=4**2  # <-- function body
    print(new_value)
square()
```

    16
    


```python
# function parameters
def square(value):
    new_value=value**2
    print(new_value)
square(4)
```

    16
    


```python
# return values from functions, assign it to a variable
def square(value):
    new_value=value**2
    return new_value

num=square(4)

print(num)
```

    16
    


```python
# docstrings, placed in the immediate line after the function header, in between triple double quotes"""
def square(value):
    """Return the square of a value."""
    new_value=value**2
    return new_value
```

Assigning a variable y to a function that prints a value but does not return a value will result in that variable y being of type NoneType!


```python
# multiple function parameters
def raise_to_power(value1,value2):
    """Raise value1 to the power of value2."""
    new_value=value1 ** value2
    return new_value

result=raise_to_power(2,3)
print(result)
```

    8
    

#### return multiple values: tuples
tuples:  
like a list - can contain multiple values  
immutable - can't modify values!  
constructed using parentheses()


```python
even_nums=(2,4,6)
print(type(even_nums))
```

    <class 'tuple'>
    


```python
# unpack tubles
a,b,c=even_nums
print(a)
print(b)
print(c)
```

    2
    4
    6
    


```python
# accessing tuple elements like you do with lists
# using zero-indexing
even_nums=(2,4,6)

print(even_nums[1])

second_num=even_nums[1]
print(second_num)
```

    4
    4
    


```python
# returning multiple values
def raise_both(value1, value2):
    """Raise value1 to the power of value2 and vice versa"""
    
    new_value1=value1**value2
    new_value2=value2**value1
    
    new_tuple=(new_value1,new_value2)
    
    return new_tuple
result=raise_both(2,3)
print(result)

# the return statement return x, y has the same result as return (x, y)
```

    (8, 9)
    

## Default arguments, variable-length arguments and scope

scope  
global scope:defined in the main body of a script  
local scope:defined inside a function  
built-in scope:names in the pre-defined built-in module


```python
# 例子，说明global和local不同
new_val=10
def square(value):
    """Returns the square of a number"""
    new_val=value**2
    return new_val

print(square(3))

print(new_val)
```

    9
    10
    


```python
# 若实在找不到local，才会去找global，最后找built-in
new_val=10
def square(value):
    """Returns the square of a number"""
    new_value2=new_val**2
    return new_value2

print(square(3))
print(new_val)

new_val=20
print(square(3))
```

    100
    10
    400
    


```python
# 如何在function里改变一个具有global name的variable
new_val=10
def square(value):
    """Returns the square of a number"""
    global new_val # 一个global加上想要access并改名字的global variable
    new_val=new_val**2 #把new_val平方
    return new_val

print(new_val)
print(square(3))
print(new_val)
```

    10
    100
    100
    


```python
# 查看哪些在built-in里
import builtins
dir(builtins)
```




    ['ArithmeticError',
     'AssertionError',
     'AttributeError',
     'BaseException',
     'BlockingIOError',
     'BrokenPipeError',
     'BufferError',
     'BytesWarning',
     'ChildProcessError',
     'ConnectionAbortedError',
     'ConnectionError',
     'ConnectionRefusedError',
     'ConnectionResetError',
     'DeprecationWarning',
     'EOFError',
     'Ellipsis',
     'EnvironmentError',
     'Exception',
     'False',
     'FileExistsError',
     'FileNotFoundError',
     'FloatingPointError',
     'FutureWarning',
     'GeneratorExit',
     'IOError',
     'ImportError',
     'ImportWarning',
     'IndentationError',
     'IndexError',
     'InterruptedError',
     'IsADirectoryError',
     'KeyError',
     'KeyboardInterrupt',
     'LookupError',
     'MemoryError',
     'ModuleNotFoundError',
     'NameError',
     'None',
     'NotADirectoryError',
     'NotImplemented',
     'NotImplementedError',
     'OSError',
     'OverflowError',
     'PendingDeprecationWarning',
     'PermissionError',
     'ProcessLookupError',
     'RecursionError',
     'ReferenceError',
     'ResourceWarning',
     'RuntimeError',
     'RuntimeWarning',
     'StopAsyncIteration',
     'StopIteration',
     'SyntaxError',
     'SyntaxWarning',
     'SystemError',
     'SystemExit',
     'TabError',
     'TimeoutError',
     'True',
     'TypeError',
     'UnboundLocalError',
     'UnicodeDecodeError',
     'UnicodeEncodeError',
     'UnicodeError',
     'UnicodeTranslateError',
     'UnicodeWarning',
     'UserWarning',
     'ValueError',
     'Warning',
     'WindowsError',
     'ZeroDivisionError',
     '__IPYTHON__',
     '__build_class__',
     '__debug__',
     '__doc__',
     '__import__',
     '__loader__',
     '__name__',
     '__package__',
     '__spec__',
     'abs',
     'all',
     'any',
     'ascii',
     'bin',
     'bool',
     'breakpoint',
     'bytearray',
     'bytes',
     'callable',
     'chr',
     'classmethod',
     'compile',
     'complex',
     'copyright',
     'credits',
     'delattr',
     'dict',
     'dir',
     'display',
     'divmod',
     'enumerate',
     'eval',
     'exec',
     'filter',
     'float',
     'format',
     'frozenset',
     'get_ipython',
     'getattr',
     'globals',
     'hasattr',
     'hash',
     'help',
     'hex',
     'id',
     'input',
     'int',
     'isinstance',
     'issubclass',
     'iter',
     'len',
     'license',
     'list',
     'locals',
     'map',
     'max',
     'memoryview',
     'min',
     'next',
     'object',
     'oct',
     'open',
     'ord',
     'pow',
     'print',
     'property',
     'range',
     'repr',
     'reversed',
     'round',
     'set',
     'setattr',
     'slice',
     'sorted',
     'staticmethod',
     'str',
     'sum',
     'super',
     'tuple',
     'type',
     'vars',
     'zip']




```python
# nested functions

# 重复运算
def mod2plus5(x1,x2,x3):
    """Returns the remainder plus 5 of three values"""
    new_x1=x1 % 2+5
    new_x2=x2 % 2+5
    new_x3=x3 % 2+5
    return new_x1,new_x2,new_x3
mod2plus5(1,2,3)
```




    (6, 5, 6)




```python
# nest函数节约运算
def mod2plus5(x1,x2,x3): # 这个是enclosing函数
    """Returns the remainder plus 5 of three values"""
    
    def inner(x):
        """Returns the remainder plus 5 of a value"""
        return x % 2 +5
    return inner(x1),inner(x2),inner(x3) # 这个是enclosing函数
mod2plus5(1,2,3)
```




    (6, 5, 6)




```python
# nest函数输出复合函数
def raise_val(n):
    """Return the inner function"""
    def inner(x):
        """Raise x to the power of n"""
        raised=x**n
        return raised
    return inner #输出的是一个需要输入x，输出x的n次方的函数

square=raise_val(2) # raise_val(2)是一个将所有输入平方的函数
cube=raise_val(3) # raise_val(3)是一个将所有输入立方的函数
print(square(2),cube(4))
```

    4 64
    


```python
# 在inner函数里改变在enclosing函数里的值，用nonlocal

def outer():
    """Prints the value of n."""
    n=1
    
    def inner():
        nonlocal n
        n=2
        print(n)
    inner()
    print(n)
```


```python
outer()
```

    2
    2
    

#### default and flexible arguments  



```python
# 如何设置default argument
def power(number, pow=1): # 用'='加一个值代表default
    """Raise number to the power of pow"""
    new_value=number**pow
    return new_value
print(power(9,2))
print(power(9))
```

    81
    9
    


```python
# 如何设置flexible arguments，不确定有多少个argument，用*args，这是一个tuple
def add_all(*args):
    """Sum all values in *args together"""
    # initialize sum
    sum_all=0
    # accumulate the sum
    for num in args:
        sum_all += num # +=意思是相加，然后返回值给前一个变量
    return sum_all

add_all(1,3,6,7)
```




    17




```python
# **kwargs，输出dict里的key-value pair

def print_all(**kwargs):
    """Print out key-value pairs in **kwargs"""
    
    # Print out the key-value pairs
    for key, value in kwargs.items(): # kwargs是一个dict
        print(key + ":" + value)
              
print_all(name='dumbledore',job='headmaster')
```

    name:dumbledore
    job:headmaster
    

items() method is used to return the list with all dictionary keys with values.

## LAMBDA FUNCTIONS AND ERROR-HANDLING


```python
raise_to_power= lambda x,y : x**y
raise_to_power(2,3)
```




    8




```python
# map是一个anonymous function
# map(func,seq), map() applies the function to ALL elements in the sequence
nums=[48,6,9,21,1]

square_all=map(lambda num:num**2, nums)

print(square_all)
# 输出一个map object
```

    <map object at 0x0000020E92B83748>
    


```python
# 转换为list
print(list(square_all))
```

    [2304, 36, 81, 441, 1]
    

error and exceptions


```python
float('2.3')
float('hello')
```


    ---------------------------------------------------------------------------

    ValueError                                Traceback (most recent call last)

    <ipython-input-26-0554ecf9c7e0> in <module>
          1 float('2.3')
    ----> 2 float('hello')
    

    ValueError: could not convert string to float: 'hello'



```python
# try-exception 方法指示错误
def sqrt(x):
    """Return the square root of a number"""
    try:
        return x ** (0.5)
    except:
        print('x must be an int or float')
        
sqrt('hi')
```


```python
# 可以指出error类型，如TypeError
def sqrt(x):
    """Return the square root of a number"""
    try:
        return x ** (0.5)
    except TypeError:
        print('x must be an int or float')
        
sqrt('hi')
```

    x must be an int or float
    

TypeError: raised when an operation or function is applied to an object of inappropriate type. The associated value is a string giving details about the type mismatch.


```python
# raise 方法指示使用错误
def sqrt(x):
    """Return the square root of a number"""
    if x<0:
        raise ValueError('x must be non-negative')
        # python本身可以运算负数开方，但为该函数排除此定义域
    try:
        return x ** 0.5
    except TypeError:
        print('x must be an int or float')
        
sqrt(-2)
```


    ---------------------------------------------------------------------------

    ValueError                                Traceback (most recent call last)

    <ipython-input-28-695563127d42> in <module>
         10         print('x must be an int or float')
         11 
    ---> 12 sqrt(-2)
    

    <ipython-input-28-695563127d42> in sqrt(x)
          3     """Return the square root of a number"""
          4     if x<0:
    ----> 5         raise ValueError('x must be non-negative')
          6         # python本身可以运算负数开方，但为该函数排除此定义域
          7     try:
    

    ValueError: x must be non-negative

