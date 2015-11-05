
##Welcome to Pandas! - Introductory lesson to Pandas


First, we need to import the package. In Python, you need to import the packages or the functions before using them. When using a function from that package, you need to call the package. In order to have an abreviated version you can import the package as another shorter name. 


    import pandas


    import pandas as pd

First, lets create a list 


    d = [0,1,2,3,4,5]


    print(d)

    [0, 1, 2, 3, 4, 5]


Now, we can create a data frame using the function from Pandas. Since we imported pandas as pd, we can call the data frame function using pd.DataFrame


    myDf = pd.DataFrame(d)


    print(myDf)

       0
    0  0
    1  1
    2  2
    3  3
    4  4
    5  5


We can rename the columns using the name of your dataframe followed by the function columns


    myDf.columns = ['Col1']


    myDf




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Col1</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>



You can insert a new column into the data frame by indexing into a new name


    myDf['NewCol'] = 5


    myDf




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Col1</th>
      <th>NewCol</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>5</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>5</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>5</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>



You can modify your column by selecting it from the data frame and replacing it 


    myDf['NewCol'] = myDf['NewCol'] + 1


    myDf




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Col1</th>
      <th>NewCol</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>6</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>6</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>6</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>6</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>6</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>6</td>
    </tr>
  </tbody>
</table>
</div>



You can delete columns from the data frame using the del function 


    del myDf['NewCol']


    myDf




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Col1</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>




    myDf['test'] = [5,4,3,2,1,0]


    myDf




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Col1</th>
      <th>test</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>4</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>3</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>1</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>



We can create new columns using existing columns 


    myDf['ExtraCol'] = myDf['Col1'] + myDf['test']


    myDf




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Col1</th>
      <th>test</th>
      <th>ExtraCol</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>5</td>
      <td>5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>4</td>
      <td>5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>3</td>
      <td>5</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>2</td>
      <td>5</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>1</td>
      <td>5</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>0</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>



The index of a data frame provides the names per row. It can be used similarly to joints in SQL databases


    myDf.index




    Int64Index([0, 1, 2, 3, 4, 5], dtype='int64')




    i = ['a', 'b','c', 'd','e','f']


    myDf.index = i


    myDf




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Col1</th>
      <th>test</th>
      <th>ExtraCol</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>a</th>
      <td>0</td>
      <td>5</td>
      <td>5</td>
    </tr>
    <tr>
      <th>b</th>
      <td>1</td>
      <td>4</td>
      <td>5</td>
    </tr>
    <tr>
      <th>c</th>
      <td>2</td>
      <td>3</td>
      <td>5</td>
    </tr>
    <tr>
      <th>d</th>
      <td>3</td>
      <td>2</td>
      <td>5</td>
    </tr>
    <tr>
      <th>e</th>
      <td>4</td>
      <td>1</td>
      <td>5</td>
    </tr>
    <tr>
      <th>f</th>
      <td>5</td>
      <td>0</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>



We can select different rows using the location function


    myDf.loc['a']




    Col1        0
    test        5
    ExtraCol    5
    Name: a, dtype: int64




    myDf.loc['a':'d']




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Col1</th>
      <th>test</th>
      <th>ExtraCol</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>a</th>
      <td>0</td>
      <td>5</td>
      <td>5</td>
    </tr>
    <tr>
      <th>b</th>
      <td>1</td>
      <td>4</td>
      <td>5</td>
    </tr>
    <tr>
      <th>c</th>
      <td>2</td>
      <td>3</td>
      <td>5</td>
    </tr>
    <tr>
      <th>d</th>
      <td>3</td>
      <td>2</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>




See how the double brackets are used in this case because we need to first create a list with elements `'a'` and `'d'`


    myDf.loc[['a','d']]




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Col1</th>
      <th>test</th>
      <th>ExtraCol</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>a</th>
      <td>0</td>
      <td>5</td>
      <td>5</td>
    </tr>
    <tr>
      <th>d</th>
      <td>3</td>
      <td>2</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>



To use row numbers you need to use the `.iloc` function instead 


    myDf.iloc[0:3]




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Col1</th>
      <th>test</th>
      <th>ExtraCol</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>a</th>
      <td>0</td>
      <td>5</td>
      <td>5</td>
    </tr>
    <tr>
      <th>b</th>
      <td>1</td>
      <td>4</td>
      <td>5</td>
    </tr>
    <tr>
      <th>c</th>
      <td>2</td>
      <td>3</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>



We can also select columns by subsetting with the name of the column, like in any list


    myDf['Col1']




    a    0
    b    1
    c    2
    d    3
    e    4
    f    5
    Name: Col1, dtype: int64




    myDf[['Col1','test']]




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Col1</th>
      <th>test</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>a</th>
      <td>0</td>
      <td>5</td>
    </tr>
    <tr>
      <th>b</th>
      <td>1</td>
      <td>4</td>
    </tr>
    <tr>
      <th>c</th>
      <td>2</td>
      <td>3</td>
    </tr>
    <tr>
      <th>d</th>
      <td>3</td>
      <td>2</td>
    </tr>
    <tr>
      <th>e</th>
      <td>4</td>
      <td>1</td>
    </tr>
    <tr>
      <th>f</th>
      <td>5</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>



And even subset rows of already selected columns


    myDf[['Col1', 'test']][1:2]




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Col1</th>
      <th>test</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>b</th>
      <td>1</td>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div>




    myDf[['Col1', 'test']][1:3]




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Col1</th>
      <th>test</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>b</th>
      <td>1</td>
      <td>4</td>
    </tr>
    <tr>
      <th>c</th>
      <td>2</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>




    myDf[['Col1','test']][3:]




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Col1</th>
      <th>test</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>d</th>
      <td>3</td>
      <td>2</td>
    </tr>
    <tr>
      <th>e</th>
      <td>4</td>
      <td>1</td>
    </tr>
    <tr>
      <th>f</th>
      <td>5</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




    myDf[['Col1','test']][:3]




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Col1</th>
      <th>test</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>a</th>
      <td>0</td>
      <td>5</td>
    </tr>
    <tr>
      <th>b</th>
      <td>1</td>
      <td>4</td>
    </tr>
    <tr>
      <th>c</th>
      <td>2</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>



A way we can visualize parts of a data frame is with the functions `head()` and `tail()` that shows the first and last 5 rows


    myDf.head()




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Col1</th>
      <th>test</th>
      <th>ExtraCol</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>a</th>
      <td>0</td>
      <td>5</td>
      <td>5</td>
    </tr>
    <tr>
      <th>b</th>
      <td>1</td>
      <td>4</td>
      <td>5</td>
    </tr>
    <tr>
      <th>c</th>
      <td>2</td>
      <td>3</td>
      <td>5</td>
    </tr>
    <tr>
      <th>d</th>
      <td>3</td>
      <td>2</td>
      <td>5</td>
    </tr>
    <tr>
      <th>e</th>
      <td>4</td>
      <td>1</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>



Use the `?` to double check what a function does and how it works. What does `zip` do?


    zip?

You can also import functions of a package without importing the whole package. In this case we need the random function from numpy


    from numpy import random

We will set the seed of the random number generator in order to obtain the same numbers


    random.seed(500)

Let's create a list with five names


    names = ['Bob', 'Jessica', 'Mary', 'John', 'Ana']

Now lets make a list that randomly takes any of the names in our name list. This new list contains 1000 elements. The following two cells do the same thing.


    random_names = [names[random.randint(low = 0, high = len(names))] for i in range(1000)]


    random_names2 = []
    for i in range(1000):
        random_names2.append(names[random.randint(0, 5)])  


    len(names)




    5




    random.randint?


    random_names[:10]




    ['Bob',
     'John',
     'Mary',
     'Ana',
     'John',
     'John',
     'Jessica',
     'Bob',
     'John',
     'Jessica']



Now lets create another list with some random numbers from 0 to 1000


    births = [random.randint(low = 0, high = 1000) for i in range(1000)]

Now lets zip the baby names and the number of births. If you are using Python 3, make sure you list it after you zip it. 


    BabySet = zip(random_names, births)


    BabySet




    <zip at 0x10702d088>




    BabySet = list(zip(random_names, births))


    BabySet[:10]




    [('Bob', 697),
     ('John', 770),
     ('Mary', 537),
     ('Ana', 714),
     ('John', 43),
     ('John', 288),
     ('Jessica', 909),
     ('Bob', 16),
     ('John', 289),
     ('Jessica', 585)]



Now that we have this list, we can transform it into a data frame 


    Babydf = pd.DataFrame(data = BabySet, columns = ['Names', 'Births'])


    Babydf.head()




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Names</th>
      <th>Births</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Bob</td>
      <td>697</td>
    </tr>
    <tr>
      <th>1</th>
      <td>John</td>
      <td>770</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Mary</td>
      <td>537</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Ana</td>
      <td>714</td>
    </tr>
    <tr>
      <th>4</th>
      <td>John</td>
      <td>43</td>
    </tr>
  </tbody>
</table>
</div>



Now lets save this data frame into a csv


    Babydf.to_csv?


    Babydf.to_csv('births1880.csv', index = False, header = False)

Now let's import this csv. We are going to save in location the path for the file. 
Notice the r before the string. Prefixing with r makes escapes the whole thing. 


    Location = r'/Users/.../.../births1880.csv'

You can import the csv using `pd.read_csv`


    otherdf = pd.read_csv(Location, header =  None)


    otherdf.head()




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Bob</td>
      <td>697</td>
    </tr>
    <tr>
      <th>1</th>
      <td>John</td>
      <td>770</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Mary</td>
      <td>537</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Ana</td>
      <td>714</td>
    </tr>
    <tr>
      <th>4</th>
      <td>John</td>
      <td>43</td>
    </tr>
  </tbody>
</table>
</div>




    df = otherdf.head()


    df




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Bob</td>
      <td>697</td>
    </tr>
    <tr>
      <th>1</th>
      <td>John</td>
      <td>770</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Mary</td>
      <td>537</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Ana</td>
      <td>714</td>
    </tr>
    <tr>
      <th>4</th>
      <td>John</td>
      <td>43</td>
    </tr>
  </tbody>
</table>
</div>



These lessons are developed for the RStudyGroup in Vancouver, BC. Based on lessons from iPython.org



    
