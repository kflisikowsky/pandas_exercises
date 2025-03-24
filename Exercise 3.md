# Exercise 3. - GroupBy

### Introduction:

GroupBy can be summarized as Split-Apply-Combine.

Special thanks to: https://github.com/justmarkham for sharing the dataset and materials.

Check out this [Diagram](http://i.imgur.com/yjNkiwL.png)  

Check out [Alcohol Consumption Exercises Video Tutorial](https://youtu.be/az67CMdmS6s) to watch a data scientist go through the exercises


### Step 1. Import the necessary libraries


```python
import pandas as pd
```

### Step 2. Import the dataset from this [address](https://raw.githubusercontent.com/justmarkham/DAT8/master/data/drinks.csv). 


```python
df = pd.read_csv('https://raw.githubusercontent.com/justmarkham/DAT8/master/data/drinks.csv')
```

### Step 3. Assign it to a variable called drinks.


```python
drinks = df
```

             country  beer_servings  spirit_servings  wine_servings  \
    0    Afghanistan              0                0              0   
    1        Albania             89              132             54   
    2        Algeria             25                0             14   
    3        Andorra            245              138            312   
    4         Angola            217               57             45   
    ..           ...            ...              ...            ...   
    188    Venezuela            333              100              3   
    189      Vietnam            111                2              1   
    190        Yemen              6                0              0   
    191       Zambia             32               19              4   
    192     Zimbabwe             64               18              4   
    
         total_litres_of_pure_alcohol continent  
    0                             0.0        AS  
    1                             4.9        EU  
    2                             0.7        AF  
    3                            12.4        EU  
    4                             5.9        AF  
    ..                            ...       ...  
    188                           7.7        SA  
    189                           2.0        AS  
    190                           0.1        AS  
    191                           2.5        AF  
    192                           4.7        AF  
    
    [193 rows x 6 columns]
    

### Step 4. Which continent drinks more beer on average?


```python
beer_by_continent = drinks.groupby('continent').agg({'beer_servings' : 'mean'})
most_beer = beer_by_continent.sort_values('beer_servings')
print(most_beer)
```

    <bound method NDFrame.last of            beer_servings
    continent               
    AS             37.045455
    AF             61.471698
    OC             89.687500
    SA            175.083333
    EU            193.777778>
    

### Step 5. For each continent print the statistics for wine consumption.


```python
wine = drinks.groupby('continent').agg({'wine_servings' : 'describe'})
print(wine)
```

              wine_servings                                                   \
                      count        mean        std  min   25%    50%     75%   
    continent                                                                  
    AF                 53.0   16.264151  38.846419  0.0   1.0    2.0   13.00   
    AS                 44.0    9.068182  21.667034  0.0   0.0    1.0    8.00   
    EU                 45.0  142.222222  97.421738  0.0  59.0  128.0  195.00   
    OC                 16.0   35.625000  64.555790  0.0   1.0    8.5   23.25   
    SA                 12.0   62.416667  88.620189  1.0   3.0   12.0   98.50   
    
                      
                 max  
    continent         
    AF         233.0  
    AS         123.0  
    EU         370.0  
    OC         212.0  
    SA         221.0  
    

### Step 6. Print the mean alcohol consumption per continent for every column


```python
alcohol = drinks.groupby('continent').mean(numeric_only=True)
print(alcohol)
```

               beer_servings  spirit_servings  wine_servings  \
    continent                                                  
    AF             61.471698        16.339623      16.264151   
    AS             37.045455        60.840909       9.068182   
    EU            193.777778       132.555556     142.222222   
    OC             89.687500        58.437500      35.625000   
    SA            175.083333       114.750000      62.416667   
    
               total_litres_of_pure_alcohol  
    continent                                
    AF                             3.007547  
    AS                             2.170455  
    EU                             8.617778  
    OC                             3.381250  
    SA                             6.308333  
    

### Step 7. Print the median alcohol consumption per continent for every column


```python
alcohol_median = drinks.groupby('continent').median(numeric_only=True)
print(alcohol_median)
```

               beer_servings  spirit_servings  wine_servings  \
    continent                                                  
    AF                  32.0              3.0            2.0   
    AS                  17.5             16.0            1.0   
    EU                 219.0            122.0          128.0   
    OC                  52.5             37.0            8.5   
    SA                 162.5            108.5           12.0   
    
               total_litres_of_pure_alcohol  
    continent                                
    AF                                 2.30  
    AS                                 1.20  
    EU                                10.00  
    OC                                 1.75  
    SA                                 6.85  
    

### Step 8. Print the mean, min and max values for spirit consumption.
#### This time output a DataFrame


```python
drinks.spirit_servings.describe()
```




    count    193.000000
    mean      80.994819
    std       88.284312
    min        0.000000
    25%        4.000000
    50%       56.000000
    75%      128.000000
    max      438.000000
    Name: spirit_servings, dtype: float64


