
# Numpy and more pandas!

While pandas provides the functionality of data frames, numpy provides the functionality of: arrays, standard mathematical functions, linear algebra and toold for integrating code written in C, C++ and Fortran

As you saw last time, we need to import the packages in order to use them


```python
import numpy as np
```

One of the most important functions of numpy is the array function. The most simple array has one dimension and can be created from a list


```python
data = [4, 6, 89, 29]
```


```python
arr1 = np.array(data)
print(arr1)
```

    [ 4  6 89 29]


Nested lists can then provide the other dimensions to the array


```python
nested = [[1, 7, 8, 9], [5, 10, 4, 3]]
```


```python
arr2 = np.array(nested)
print(arr2)
```

    [[ 1  7  8  9]
     [ 5 10  4  3]]


## Indexing arrays:


```python
arr3 = np.arange(10)
print(arr3)
```

    [0 1 2 3 4 5 6 7 8 9]



```python
arr3[5]
```




    5




```python
arr3[5:8] = 12
print(arr3)
```

    [ 0  1  2  3  4 12 12 12  8  9]



```python
arr_slice = arr3[5:8]
```


```python
arr_slice[1] = 12345
```

What do you think happens now to our original arr3 array?


```python
print(arr3)
```

    [    0     1     2     3     4    12 12345    12     8     9]


The values are propagated, therefore array slices are *views* on the original array, not copies

What about indexing higher dimensional arrays?


```python
print(arr2)
```

    [[ 1  7  8  9]
     [ 5 10  4  3]]



```python
arr2[1]
```




    array([ 5, 10,  4,  3])




```python
arr2[1][2]
```




    4




```python
arr2[1,2]
```




    4



Rows go first, then columns, then any extra dimension


You can also index using logical operators, or you can pass lists of indexes in the order desired

If I use a negative index, what do you think it will do?


```python
arr2[1,-2]
```




    4




```python
arr4 = np.arange(32).reshape((8,4))
print(arr4)
```

    [[ 0  1  2  3]
     [ 4  5  6  7]
     [ 8  9 10 11]
     [12 13 14 15]
     [16 17 18 19]
     [20 21 22 23]
     [24 25 26 27]
     [28 29 30 31]]



```python
arr4[[1,5,7,2],[0,3,1,2]]
```




    array([ 4, 23, 29, 10])



Having two lists as index, pairs up both of them, returning the elements (1,0), (5,3), (7,1), (2,2)

If you want the rectangular region formed by selecting a subset of the matrix's rows and columns


```python
arr4[[1, 5, 7, 2]][:,[0, 3, 1, 2]]
```




    array([[ 4,  7,  5,  6],
           [20, 23, 21, 22],
           [28, 31, 29, 30],
           [ 8, 11,  9, 10]])


Or use the np.ix_ function

```python
arr4[np.ix_([1,5,7,2],[0,3,1,2])]
```




    array([[ 4,  7,  5,  6],
           [20, 23, 21, 22],
           [28, 31, 29, 30],
           [ 8, 11,  9, 10]])



## Transposing 

Transposing also presents a view of the underlying data and not a copy of it


```python
print(arr4) 
```

    [[ 0  1  2  3]
     [ 4  5  6  7]
     [ 8  9 10 11]
     [12 13 14 15]
     [16 17 18 19]
     [20 21 22 23]
     [24 25 26 27]
     [28 29 30 31]]



```python
print(arr4.T)
```

    [[ 0  4  8 12 16 20 24 28]
     [ 1  5  9 13 17 21 25 29]
     [ 2  6 10 14 18 22 26 30]
     [ 3  7 11 15 19 23 27 31]]


.transpose will accept a tuple of axis numbers to permute the axes

## Element-wise array functions


```python
np.sqrt(arr4)
```




    array([[ 0.        ,  1.        ,  1.41421356,  1.73205081],
           [ 2.        ,  2.23606798,  2.44948974,  2.64575131],
           [ 2.82842712,  3.        ,  3.16227766,  3.31662479],
           [ 3.46410162,  3.60555128,  3.74165739,  3.87298335],
           [ 4.        ,  4.12310563,  4.24264069,  4.35889894],
           [ 4.47213595,  4.58257569,  4.69041576,  4.79583152],
           [ 4.89897949,  5.        ,  5.09901951,  5.19615242],
           [ 5.29150262,  5.38516481,  5.47722558,  5.56776436]])



## Mathematical and Statistical methods


```python
arr4.mean()
```




    15.5




```python
arr4.mean(axis = 1)
```




    array([  1.5,   5.5,   9.5,  13.5,  17.5,  21.5,  25.5,  29.5])




```python
arr4.sum(axis = 0)
```




    array([112, 120, 128, 136])



Boolean values are coerced into 1 (True) and 0 for (False)


```python
arr5 = np.random.randn(8)
```


```python
arr5.sort()
```


```python
print(arr5)
```

    [-0.95152919 -0.80220033 -0.11915317 -0.06137181 -0.05436698  0.820126
      1.34513854  1.88949846]


## Broadcasting


```python
arr6 = np.random.randn(4,3)
```


```python
arr6
```




    array([[ 0.56801206, -1.45446944,  0.34754167],
           [-0.60611374,  0.25154329, -0.27219432],
           [ 2.16397494,  2.084998  , -1.25341479],
           [-1.38168469, -0.16785704, -1.58701196]])




```python
arr6.mean(0)
```




    array([ 0.18604714,  0.1785537 , -0.69126985])




```python
demeaned = arr6 - arr6.mean(0)
```


```python
demeaned
```




    array([[ 0.38196492, -1.63302315,  1.03881152],
           [-0.79216088,  0.07298959,  0.41907553],
           [ 1.97792779,  1.9064443 , -0.56214495],
           [-1.56773183, -0.34641075, -0.89574211]])



## Challenge

1. Calculate the dot product between two matrices
2. Create an three dimensional array with random numbers. Calculate the sum across the third dimension and then substract from the original array.
