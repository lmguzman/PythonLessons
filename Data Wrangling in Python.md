
#Learning Objectives:

By the end of this lesson the student will:
- Merge and concatenate data frames and arrays
- Reshape and pivot data frames


    import pandas as pd
    import numpy as np

## Combining and Merging data sets


    df1 = pd.DataFrame({'key': ['b', 'b', 'a', 'c', 'a', 'a', 'b'], 'data1': range(7)})
    df1




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>data1</th>
      <th>key</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>b</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>b</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>a</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>c</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>a</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>a</td>
    </tr>
    <tr>
      <th>6</th>
      <td>6</td>
      <td>b</td>
    </tr>
  </tbody>
</table>
</div>




    df2 = pd.DataFrame({'key': ['a', 'b', 'd'], 'data2': range(3)})
    df2




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>data2</th>
      <th>key</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>a</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>b</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>d</td>
    </tr>
  </tbody>
</table>
</div>




    pd.merge(df1, df2)




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>data1</th>
      <th>key</th>
      <th>data2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>b</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>b</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>6</td>
      <td>b</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2</td>
      <td>a</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>a</td>
      <td>0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>a</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>



Note that merge works like an inner.join. Only uses keys common for both data frames by default. Otherwise need to specify how.


    pd.merge(df1, df2, how='outer')




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>data1</th>
      <th>key</th>
      <th>data2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>b</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>b</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>6</td>
      <td>b</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2</td>
      <td>a</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>a</td>
      <td>0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>a</td>
      <td>0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>3</td>
      <td>c</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>7</th>
      <td>NaN</td>
      <td>d</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>



You can also merge on multiple keys


    left = pd.DataFrame({'key1': ['foo', 'foo', 'bar'], 'key2': ['one', 'two', 'one'],
    'lval': [1, 2, 3]})
    left




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>key1</th>
      <th>key2</th>
      <th>lval</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>foo</td>
      <td>one</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>foo</td>
      <td>two</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>bar</td>
      <td>one</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>




    right = pd.DataFrame({'key1': ['foo', 'foo', 'bar', 'bar'], 'key2': ['one', 'one', 'one', 'two'],
    'rval': [4, 5, 6, 7]})
    right




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>key1</th>
      <th>key2</th>
      <th>rval</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>foo</td>
      <td>one</td>
      <td>4</td>
    </tr>
    <tr>
      <th>1</th>
      <td>foo</td>
      <td>one</td>
      <td>5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>bar</td>
      <td>one</td>
      <td>6</td>
    </tr>
    <tr>
      <th>3</th>
      <td>bar</td>
      <td>two</td>
      <td>7</td>
    </tr>
  </tbody>
</table>
</div>




    pd.merge(left, right, on=['key1', 'key2'], how='outer')




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>key1</th>
      <th>key2</th>
      <th>lval</th>
      <th>rval</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>foo</td>
      <td>one</td>
      <td>1</td>
      <td>4</td>
    </tr>
    <tr>
      <th>1</th>
      <td>foo</td>
      <td>one</td>
      <td>1</td>
      <td>5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>foo</td>
      <td>two</td>
      <td>2</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>bar</td>
      <td>one</td>
      <td>3</td>
      <td>6</td>
    </tr>
    <tr>
      <th>4</th>
      <td>bar</td>
      <td>two</td>
      <td>NaN</td>
      <td>7</td>
    </tr>
  </tbody>
</table>
</div>




    pd.merge(left, right, on='key1', suffixes=('_left', '_right'))




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>key1</th>
      <th>key2_left</th>
      <th>lval</th>
      <th>key2_right</th>
      <th>rval</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>foo</td>
      <td>one</td>
      <td>1</td>
      <td>one</td>
      <td>4</td>
    </tr>
    <tr>
      <th>1</th>
      <td>foo</td>
      <td>one</td>
      <td>1</td>
      <td>one</td>
      <td>5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>foo</td>
      <td>two</td>
      <td>2</td>
      <td>one</td>
      <td>4</td>
    </tr>
    <tr>
      <th>3</th>
      <td>foo</td>
      <td>two</td>
      <td>2</td>
      <td>one</td>
      <td>5</td>
    </tr>
    <tr>
      <th>4</th>
      <td>bar</td>
      <td>one</td>
      <td>3</td>
      <td>one</td>
      <td>6</td>
    </tr>
    <tr>
      <th>5</th>
      <td>bar</td>
      <td>one</td>
      <td>3</td>
      <td>two</td>
      <td>7</td>
    </tr>
  </tbody>
</table>
</div>



You can also merge on indexes


    left1 = pd.DataFrame({'key': ['a', 'b', 'a', 'a', 'b', 'c'], 'value': range(6)})
    left1




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>key</th>
      <th>value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>a</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>b</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>a</td>
      <td>2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>a</td>
      <td>3</td>
    </tr>
    <tr>
      <th>4</th>
      <td>b</td>
      <td>4</td>
    </tr>
    <tr>
      <th>5</th>
      <td>c</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>




    right1 = pd.DataFrame({'group_val': [3.5, 7]}, index=['a', 'b'])
    right1




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>group_val</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>a</th>
      <td>3.5</td>
    </tr>
    <tr>
      <th>b</th>
      <td>7.0</td>
    </tr>
  </tbody>
</table>
</div>




    pd.merge(left1, right1, left_on='key', right_index=True)




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>key</th>
      <th>value</th>
      <th>group_val</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>a</td>
      <td>0</td>
      <td>3.5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>a</td>
      <td>2</td>
      <td>3.5</td>
    </tr>
    <tr>
      <th>3</th>
      <td>a</td>
      <td>3</td>
      <td>3.5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>b</td>
      <td>1</td>
      <td>7.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>b</td>
      <td>4</td>
      <td>7.0</td>
    </tr>
  </tbody>
</table>
</div>



## Challenge! Using the following two dataframes, do an outer merge:


    lefth = pd.DataFrame({'key1': ['Ohio', 'Ohio', 'Ohio', 'Nevada', 'Nevada'], 'key2': [2000, 2001, 2002, 2001, 2002],
    'data': np.arange(5.)})
    lefth




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>data</th>
      <th>key1</th>
      <th>key2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Ohio</td>
      <td>2000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Ohio</td>
      <td>2001</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Ohio</td>
      <td>2002</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Nevada</td>
      <td>2001</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Nevada</td>
      <td>2002</td>
    </tr>
  </tbody>
</table>
</div>




    righth = pd.DataFrame(np.arange(12).reshape((6, 2)),
    index=[['Nevada', 'Nevada', 'Ohio', 'Ohio', 'Ohio', 'Ohio'], 
           [2001, 2000, 2000, 2000, 2001, 2002]], columns=['event1', 'event2'])
    righth




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>event1</th>
      <th>event2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">Nevada</th>
      <th>2001</th>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2000</th>
      <td>2</td>
      <td>3</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">Ohio</th>
      <th>2000</th>
      <td>4</td>
      <td>5</td>
    </tr>
    <tr>
      <th>2000</th>
      <td>6</td>
      <td>7</td>
    </tr>
    <tr>
      <th>2001</th>
      <td>8</td>
      <td>9</td>
    </tr>
    <tr>
      <th>2002</th>
      <td>10</td>
      <td>11</td>
    </tr>
  </tbody>
</table>
</div>



Solution:


    pd.merge(lefth, righth, left_on=['key1', 'key2'], right_index=True, how='outer')




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>data</th>
      <th>key1</th>
      <th>key2</th>
      <th>event1</th>
      <th>event2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Ohio</td>
      <td>2000</td>
      <td>4</td>
      <td>5</td>
    </tr>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Ohio</td>
      <td>2000</td>
      <td>6</td>
      <td>7</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Ohio</td>
      <td>2001</td>
      <td>8</td>
      <td>9</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Ohio</td>
      <td>2002</td>
      <td>10</td>
      <td>11</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Nevada</td>
      <td>2001</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Nevada</td>
      <td>2002</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>NaN</td>
      <td>Nevada</td>
      <td>2000</td>
      <td>2</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>




    left2 = pd.DataFrame([[1., 2.], [3., 4.], [5., 6.]], index=['a', 'c', 'e'], columns=['Ohio', 'Nevada'])
    left2




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Ohio</th>
      <th>Nevada</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>a</th>
      <td>1</td>
      <td>2</td>
    </tr>
    <tr>
      <th>c</th>
      <td>3</td>
      <td>4</td>
    </tr>
    <tr>
      <th>e</th>
      <td>5</td>
      <td>6</td>
    </tr>
  </tbody>
</table>
</div>




    right2 = pd.DataFrame([[7., 8.], [9., 10.], [11., 12.], [13, 14]],
                          index=['b', 'c', 'd', 'e'], columns=['Missouri', 'Alabama'])
    right2




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Missouri</th>
      <th>Alabama</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>b</th>
      <td>7</td>
      <td>8</td>
    </tr>
    <tr>
      <th>c</th>
      <td>9</td>
      <td>10</td>
    </tr>
    <tr>
      <th>d</th>
      <td>11</td>
      <td>12</td>
    </tr>
    <tr>
      <th>e</th>
      <td>13</td>
      <td>14</td>
    </tr>
  </tbody>
</table>
</div>



####Here we use a similar index and non overlapping columns


    left2.join(right2, how='outer')




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Ohio</th>
      <th>Nevada</th>
      <th>Missouri</th>
      <th>Alabama</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>a</th>
      <td>1</td>
      <td>2</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>b</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>7</td>
      <td>8</td>
    </tr>
    <tr>
      <th>c</th>
      <td>3</td>
      <td>4</td>
      <td>9</td>
      <td>10</td>
    </tr>
    <tr>
      <th>d</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>11</td>
      <td>12</td>
    </tr>
    <tr>
      <th>e</th>
      <td>5</td>
      <td>6</td>
      <td>13</td>
      <td>14</td>
    </tr>
  </tbody>
</table>
</div>



##Concatenating along axis


    arr = np.arange(12).reshape((3, 4))
    arr




    array([[ 0,  1,  2,  3],
           [ 4,  5,  6,  7],
           [ 8,  9, 10, 11]])




    np.concatenate([arr, arr], axis=1)




    array([[ 0,  1,  2,  3,  0,  1,  2,  3],
           [ 4,  5,  6,  7,  4,  5,  6,  7],
           [ 8,  9, 10, 11,  8,  9, 10, 11]])




    s1 = pd.Series([0, 1], index=['a', 'b'])
    s2 = pd.Series([2, 3, 4], index=['c', 'd', 'e'])
    s3 = pd.Series([5, 6], index=['f', 'g'])
    print(s1)
    print(s2)
    print(s3)

    a    0
    b    1
    dtype: int64
    c    2
    d    3
    e    4
    dtype: int64
    f    5
    g    6
    dtype: int64



    pd.concat([s1,s2,s3])




    a    0
    b    1
    c    2
    d    3
    e    4
    f    5
    g    6
    dtype: int64



By default concat works along axis=0, producing another Series. If you pass axis=1, the result will instead be a DataFrame (axis=1 is the columns):


    pd.concat([s1, s2, s3], axis=1)




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>a</th>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>b</th>
      <td>1</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>c</th>
      <td>NaN</td>
      <td>2</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>d</th>
      <td>NaN</td>
      <td>3</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>e</th>
      <td>NaN</td>
      <td>4</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>f</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>5</td>
    </tr>
    <tr>
      <th>g</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>6</td>
    </tr>
  </tbody>
</table>
</div>




    s4 = pd.concat([s1 * 5, s3])
    s4




    a    0
    b    5
    f    5
    g    6
    dtype: int64



###Challenge!
What would be the difference between: 

pd.concat([s1, s4], axis=1)
and

pd.concat([s1, s4], axis=1, join='inner')


    result = pd.concat([s1, s1, s3], keys=['one', 'two', 'three'])
    result




    one    a    0
           b    1
    two    a    0
           b    1
    three  f    5
           g    6
    dtype: int64



Notice the keys used for each series


    result.unstack()




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>a</th>
      <th>b</th>
      <th>f</th>
      <th>g</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>one</th>
      <td>0</td>
      <td>1</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>two</th>
      <td>0</td>
      <td>1</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>three</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>5</td>
      <td>6</td>
    </tr>
  </tbody>
</table>
</div>



###Challenge!

Try concatenating two data frame objects setting a key for each data frame


If you need to ignore the row names


    df1 = pd.DataFrame(np.random.randn(3, 4), columns=['a', 'b', 'c', 'd'])
    df1




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>a</th>
      <th>b</th>
      <th>c</th>
      <th>d</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.406209</td>
      <td>0.134499</td>
      <td>-0.736462</td>
      <td>1.048186</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-1.057252</td>
      <td>0.250065</td>
      <td>-0.238468</td>
      <td>0.091275</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-0.317977</td>
      <td>0.986328</td>
      <td>-0.392398</td>
      <td>0.260411</td>
    </tr>
  </tbody>
</table>
</div>




    df2 = pd.DataFrame(np.random.randn(2, 3), columns=['b', 'd', 'a'])
    df2




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>b</th>
      <th>d</th>
      <th>a</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.811604</td>
      <td>-2.037728</td>
      <td>-1.684153</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-0.544392</td>
      <td>-0.561306</td>
      <td>-0.452706</td>
    </tr>
  </tbody>
</table>
</div>




    pd.concat([df1, df2], ignore_index=True)




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>a</th>
      <th>b</th>
      <th>c</th>
      <th>d</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.406209</td>
      <td>0.134499</td>
      <td>-0.736462</td>
      <td>1.048186</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-1.057252</td>
      <td>0.250065</td>
      <td>-0.238468</td>
      <td>0.091275</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-0.317977</td>
      <td>0.986328</td>
      <td>-0.392398</td>
      <td>0.260411</td>
    </tr>
    <tr>
      <th>3</th>
      <td>-1.684153</td>
      <td>0.811604</td>
      <td>NaN</td>
      <td>-2.037728</td>
    </tr>
    <tr>
      <th>4</th>
      <td>-0.452706</td>
      <td>-0.544392</td>
      <td>NaN</td>
      <td>-0.561306</td>
    </tr>
  </tbody>
</table>
</div>



## Reshaping

- stack: this “rotates” or pivots from the columns in the data to the rows 
- unstack: this pivots from the rows into the columns


    data = pd.DataFrame(np.arange(6).reshape((2, 3)), 
                        index=pd.Index(['Ohio', 'Colorado'], name='state'), 
                        columns=pd.Index(['one', 'two', 'three'], name='number'))
    data




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>number</th>
      <th>one</th>
      <th>two</th>
      <th>three</th>
    </tr>
    <tr>
      <th>state</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Ohio</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
    </tr>
    <tr>
      <th>Colorado</th>
      <td>3</td>
      <td>4</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>




    result = data.stack()
    result




    state     number
    Ohio      one       0
              two       1
              three     2
    Colorado  one       3
              two       4
              three     5
    dtype: int64




    result.unstack()




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>number</th>
      <th>one</th>
      <th>two</th>
      <th>three</th>
    </tr>
    <tr>
      <th>state</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Ohio</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
    </tr>
    <tr>
      <th>Colorado</th>
      <td>3</td>
      <td>4</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>



## Pivoting - Long to wide 


    long_gap = pd.read_csv('long_gap.csv')


    long_gap[:10]




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>country</th>
      <th>Description</th>
      <th>country_val</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Afghanistan</td>
      <td>life</td>
      <td>37.478833</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Albania</td>
      <td>life</td>
      <td>68.432917</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Algeria</td>
      <td>life</td>
      <td>59.030167</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Angola</td>
      <td>life</td>
      <td>37.883500</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Argentina</td>
      <td>life</td>
      <td>69.060417</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Australia</td>
      <td>life</td>
      <td>74.662917</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Austria</td>
      <td>life</td>
      <td>73.103250</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Bahrain</td>
      <td>life</td>
      <td>65.605667</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Bangladesh</td>
      <td>life</td>
      <td>49.834083</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Belgium</td>
      <td>life</td>
      <td>73.641750</td>
    </tr>
  </tbody>
</table>
</div>




    pivoted = long_gap.pivot('country','Description', 'country_val')


    pivoted.head()




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>Description</th>
      <th>gdp</th>
      <th>life</th>
      <th>pop</th>
    </tr>
    <tr>
      <th>country</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Afghanistan</th>
      <td>802.674598</td>
      <td>37.478833</td>
      <td>15823715.416667</td>
    </tr>
    <tr>
      <th>Albania</th>
      <td>3255.366633</td>
      <td>68.432917</td>
      <td>2580249.166667</td>
    </tr>
    <tr>
      <th>Algeria</th>
      <td>4426.025973</td>
      <td>59.030167</td>
      <td>19875406.166667</td>
    </tr>
    <tr>
      <th>Angola</th>
      <td>3607.100529</td>
      <td>37.883500</td>
      <td>7309390.083333</td>
    </tr>
    <tr>
      <th>Argentina</th>
      <td>8955.553783</td>
      <td>69.060417</td>
      <td>28602239.916667</td>
    </tr>
  </tbody>
</table>
</div>



### Challenge!

Can you pivot using unstack and set_index?




    unstacked = long_gap.set_index(['country', 'Description']).unstack('Description')


    unstacked.head()




<div>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th colspan="3" halign="left">country_val</th>
    </tr>
    <tr>
      <th>Description</th>
      <th>gdp</th>
      <th>life</th>
      <th>pop</th>
    </tr>
    <tr>
      <th>country</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Afghanistan</th>
      <td>802.674598</td>
      <td>37.478833</td>
      <td>15823715.416667</td>
    </tr>
    <tr>
      <th>Albania</th>
      <td>3255.366633</td>
      <td>68.432917</td>
      <td>2580249.166667</td>
    </tr>
    <tr>
      <th>Algeria</th>
      <td>4426.025973</td>
      <td>59.030167</td>
      <td>19875406.166667</td>
    </tr>
    <tr>
      <th>Angola</th>
      <td>3607.100529</td>
      <td>37.883500</td>
      <td>7309390.083333</td>
    </tr>
    <tr>
      <th>Argentina</th>
      <td>8955.553783</td>
      <td>69.060417</td>
      <td>28602239.916667</td>
    </tr>
  </tbody>
</table>
</div>




    
