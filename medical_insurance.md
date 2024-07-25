```python
import pandas as pd
from statistics import mean
import matplotlib.pyplot as plt
```


```python
data = pd.read_csv("insurance.csv")
```


```python
data.head()
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
      <th>age</th>
      <th>sex</th>
      <th>bmi</th>
      <th>children</th>
      <th>smoker</th>
      <th>region</th>
      <th>charges</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>19</td>
      <td>female</td>
      <td>27.900</td>
      <td>0</td>
      <td>yes</td>
      <td>southwest</td>
      <td>16884.92400</td>
    </tr>
    <tr>
      <th>1</th>
      <td>18</td>
      <td>male</td>
      <td>33.770</td>
      <td>1</td>
      <td>no</td>
      <td>southeast</td>
      <td>1725.55230</td>
    </tr>
    <tr>
      <th>2</th>
      <td>28</td>
      <td>male</td>
      <td>33.000</td>
      <td>3</td>
      <td>no</td>
      <td>southeast</td>
      <td>4449.46200</td>
    </tr>
    <tr>
      <th>3</th>
      <td>33</td>
      <td>male</td>
      <td>22.705</td>
      <td>0</td>
      <td>no</td>
      <td>northwest</td>
      <td>21984.47061</td>
    </tr>
    <tr>
      <th>4</th>
      <td>32</td>
      <td>male</td>
      <td>28.880</td>
      <td>0</td>
      <td>no</td>
      <td>northwest</td>
      <td>3866.85520</td>
    </tr>
  </tbody>
</table>
</div>




```python
data.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 1338 entries, 0 to 1337
    Data columns (total 7 columns):
     #   Column    Non-Null Count  Dtype  
    ---  ------    --------------  -----  
     0   age       1338 non-null   int64  
     1   sex       1338 non-null   object 
     2   bmi       1338 non-null   float64
     3   children  1338 non-null   int64  
     4   smoker    1338 non-null   object 
     5   region    1338 non-null   object 
     6   charges   1338 non-null   float64
    dtypes: float64(2), int64(2), object(3)
    memory usage: 73.3+ KB



```python
## compare sex and charges
sex_charges = data[['sex','charges']]
sex_charges.head()
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
      <th>sex</th>
      <th>charges</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>female</td>
      <td>16884.92400</td>
    </tr>
    <tr>
      <th>1</th>
      <td>male</td>
      <td>1725.55230</td>
    </tr>
    <tr>
      <th>2</th>
      <td>male</td>
      <td>4449.46200</td>
    </tr>
    <tr>
      <th>3</th>
      <td>male</td>
      <td>21984.47061</td>
    </tr>
    <tr>
      <th>4</th>
      <td>male</td>
      <td>3866.85520</td>
    </tr>
  </tbody>
</table>
</div>




```python
## found the average cost of females vs male
averagecost_of_sex = data[["sex", "charges"]].groupby("sex").mean()
print(averagecost_of_sex)
```

                 charges
    sex                 
    female  12569.578844
    male    13956.751178



```python
sex = ["female", "male"]
charges =  [12569.58, 13956.75]

plt.bar(range(len(sex)), charges)

ax = plt.subplot()
ax.set_xticks(range(2))
ax.set_xticklabels(sex)
plt.title('average charge bases on sex')
plt.show()
```


    
![png](output_6_0.png)
    



```python
## compare smoking habits and charges
smoking_charges = data[['smoker','charges']]
smoking_charges.head()
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
      <th>smoker</th>
      <th>charges</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>yes</td>
      <td>16884.92400</td>
    </tr>
    <tr>
      <th>1</th>
      <td>no</td>
      <td>1725.55230</td>
    </tr>
    <tr>
      <th>2</th>
      <td>no</td>
      <td>4449.46200</td>
    </tr>
    <tr>
      <th>3</th>
      <td>no</td>
      <td>21984.47061</td>
    </tr>
    <tr>
      <th>4</th>
      <td>no</td>
      <td>3866.85520</td>
    </tr>
  </tbody>
</table>
</div>




```python
## found the average cost based on smoking habits
data[["smoker", "charges"]].groupby("smoker").mean()
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
      <th>charges</th>
    </tr>
    <tr>
      <th>smoker</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>no</th>
      <td>8434.268298</td>
    </tr>
    <tr>
      <th>yes</th>
      <td>32050.231832</td>
    </tr>
  </tbody>
</table>
</div>




```python
smoker = ["no", "yes"]
charges =  [8434.27, 32050.23]

plt.bar(range(len(smoker)), charges)

ax = plt.subplot()
ax.set_xticks(range(2))
ax.set_xticklabels(smoker)
plt.title('average cost based on smoking habits')
plt.show()
```


    
![png](output_9_0.png)
    



```python
## in conclusion, in general males compared to females have to pay more and smokers to nonsomkers have to pay more

```
