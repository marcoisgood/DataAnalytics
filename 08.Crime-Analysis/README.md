# =============You safe I happy ===============
#### Analyzed by Marco Lin

![](http://52.41.251.138/sites/default/files/2017-11/crime%20rate_0.jpg)

#### Our company is Decrime. We dedicate to police enforcement optimization. This project we focus on the analysis of crimes to explore the information of crimes for our customers. 
#### At first, we will explore in four aspects of dataset. In this part, we can understand the tendency of crimes in 40 years (from 1975 to 2015). We will show what kind of crimes take up most all of crimes. In addition, we will find out which city has most crimes in 40 years. In addition, the correlation between population and crimes is our focus as well. 
#### Furthermore, we will concentrate on California. This is because our customers are from California. They may be interested in the fact in this state. Also, we will compare with different Periods of time to see the changing. 
#### Then, we will choose one city in California to see what kind of crimes happen most. Second, we will see what the city is safest recently. And showing the percentage of different crimes type. At the end, the report will finish with summery and recommendations. 

## =======preparation==========


```python
import pandas as pd
import numpy as np
import geopandas as gp
import matplotlib.pyplot as plt
from pandas import DataFrame, Series
crimes = pd.read_csv("../week8crime/report.csv")
%matplotlib inline
```


```python
crimes.describe()
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
      <th>report_year</th>
      <th>population</th>
      <th>violent_crimes</th>
      <th>homicides</th>
      <th>rapes</th>
      <th>assaults</th>
      <th>robberies</th>
      <th>months_reported</th>
      <th>crimes_percapita</th>
      <th>homicides_percapita</th>
      <th>rapes_percapita</th>
      <th>assaults_percapita</th>
      <th>robberies_percapita</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>2829.000000</td>
      <td>2.760000e+03</td>
      <td>2.794000e+03</td>
      <td>2795.000000</td>
      <td>2754.000000</td>
      <td>2753.000000</td>
      <td>2754.000000</td>
      <td>2692.000000</td>
      <td>2794.000000</td>
      <td>2795.000000</td>
      <td>2754.000000</td>
      <td>2753.000000</td>
      <td>2754.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>1995.000000</td>
      <td>7.956981e+05</td>
      <td>2.963255e+04</td>
      <td>398.385331</td>
      <td>416.278867</td>
      <td>4405.146023</td>
      <td>4000.245098</td>
      <td>11.868871</td>
      <td>1093.049810</td>
      <td>15.372812</td>
      <td>59.305167</td>
      <td>566.595434</td>
      <td>459.968112</td>
    </tr>
    <tr>
      <th>std</th>
      <td>11.834251</td>
      <td>1.012451e+06</td>
      <td>1.728630e+05</td>
      <td>2281.276402</td>
      <td>479.811934</td>
      <td>6977.293769</td>
      <td>8653.902965</td>
      <td>1.118194</td>
      <td>676.884678</td>
      <td>12.350640</td>
      <td>31.971570</td>
      <td>369.436996</td>
      <td>340.903534</td>
    </tr>
    <tr>
      <th>min</th>
      <td>1975.000000</td>
      <td>1.007630e+05</td>
      <td>1.540000e+02</td>
      <td>1.000000</td>
      <td>15.000000</td>
      <td>15.000000</td>
      <td>83.000000</td>
      <td>0.000000</td>
      <td>16.490000</td>
      <td>0.210000</td>
      <td>1.640000</td>
      <td>1.610000</td>
      <td>11.460000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>1985.000000</td>
      <td>3.779310e+05</td>
      <td>3.014750e+03</td>
      <td>32.000000</td>
      <td>176.250000</td>
      <td>1467.000000</td>
      <td>1032.000000</td>
      <td>12.000000</td>
      <td>625.082500</td>
      <td>6.955000</td>
      <td>35.775000</td>
      <td>319.090000</td>
      <td>210.242500</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>1995.000000</td>
      <td>5.366145e+05</td>
      <td>5.135500e+03</td>
      <td>64.000000</td>
      <td>291.000000</td>
      <td>2597.000000</td>
      <td>1940.000000</td>
      <td>12.000000</td>
      <td>949.680000</td>
      <td>11.980000</td>
      <td>55.900000</td>
      <td>487.480000</td>
      <td>374.400000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>2005.000000</td>
      <td>8.168558e+05</td>
      <td>9.058500e+03</td>
      <td>131.000000</td>
      <td>465.000000</td>
      <td>4556.000000</td>
      <td>3609.750000</td>
      <td>12.000000</td>
      <td>1409.507500</td>
      <td>20.230000</td>
      <td>77.797500</td>
      <td>728.240000</td>
      <td>612.005000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>2015.000000</td>
      <td>8.550861e+06</td>
      <td>1.932274e+06</td>
      <td>24703.000000</td>
      <td>3899.000000</td>
      <td>71030.000000</td>
      <td>107475.000000</td>
      <td>12.000000</td>
      <td>4352.830000</td>
      <td>94.740000</td>
      <td>199.300000</td>
      <td>2368.220000</td>
      <td>2337.520000</td>
    </tr>
  </tbody>
</table>
</div>




```python
crimes.columns
```




    Index(['report_year', 'agency_code', 'agency_jurisdiction', 'population',
           'violent_crimes', 'homicides', 'rapes', 'assaults', 'robberies',
           'months_reported', 'crimes_percapita', 'homicides_percapita',
           'rapes_percapita', 'assaults_percapita', 'robberies_percapita'],
          dtype='object')




```python
crimes.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 2829 entries, 0 to 2828
    Data columns (total 15 columns):
    report_year            2829 non-null int64
    agency_code            2788 non-null object
    agency_jurisdiction    2829 non-null object
    population             2760 non-null float64
    violent_crimes         2794 non-null float64
    homicides              2795 non-null float64
    rapes                  2754 non-null float64
    assaults               2753 non-null float64
    robberies              2754 non-null float64
    months_reported        2692 non-null float64
    crimes_percapita       2794 non-null float64
    homicides_percapita    2795 non-null float64
    rapes_percapita        2754 non-null float64
    assaults_percapita     2753 non-null float64
    robberies_percapita    2754 non-null float64
    dtypes: float64(12), int64(1), object(2)
    memory usage: 331.6+ KB


## ===========Data Exploration=============

### A. Total violent Crimes Tendency from 1975 to 2015 in USA


```python
crime_rate = crimes.groupby(by = "report_year").sum()
crime_rate1 = crime_rate["violent_crimes"]
crime_rate2 = crime_rate[["homicides","rapes","assaults","robberies"]]
```


```python
crime_rate1.plot() 
```




    <matplotlib.axes._subplots.AxesSubplot at 0x11b591198>




![png](output_10_1.png)


### Explanation:
The events of crimes from 1975 to 1990 was going up from 1600000 to 2800000. Then, after 1995, the number decreased.


```python
crime_rate2.plot() 
```




    <matplotlib.axes._subplots.AxesSubplot at 0x11b622b38>




![png](output_12_1.png)


### Explanation:
It appears that number of assaults has dramaticly increased from 1985 to 1992. Also, the number of robberies has noticeably increased from 1987 to 1992 as well. Then, they both have decreased from 1995. The number of homicides and rapes are steady.

### B. In 40 years, the cities which has high violentest crimes


```python
rank_crime = crimes.groupby(by = "agency_jurisdiction").sum()
```


```python
rank_crime1 = rank_crime.sort_values(by= "violent_crimes", ascending=[False]).head(10)
rank_crime1[["violent_crimes","population"]]
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
      <th>violent_crimes</th>
      <th>population</th>
    </tr>
    <tr>
      <th>agency_jurisdiction</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>United States</th>
      <td>58163955.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>New York City, NY</th>
      <td>4263284.0</td>
      <td>313777539.0</td>
    </tr>
    <tr>
      <th>Los Angeles, CA</th>
      <td>1979166.0</td>
      <td>142984519.0</td>
    </tr>
    <tr>
      <th>Chicago, IL</th>
      <td>1960886.0</td>
      <td>118467098.0</td>
    </tr>
    <tr>
      <th>Detroit, MI</th>
      <td>918003.0</td>
      <td>41436021.0</td>
    </tr>
    <tr>
      <th>Houston, TX</th>
      <td>819539.0</td>
      <td>76033056.0</td>
    </tr>
    <tr>
      <th>Philadelphia, PA</th>
      <td>763201.0</td>
      <td>65551379.0</td>
    </tr>
    <tr>
      <th>Baltimore, MD</th>
      <td>600630.0</td>
      <td>29297653.0</td>
    </tr>
    <tr>
      <th>Dallas, TX</th>
      <td>590468.0</td>
      <td>44640012.0</td>
    </tr>
    <tr>
      <th>Miami-Dade County, FL</th>
      <td>500061.0</td>
      <td>41612313.0</td>
    </tr>
  </tbody>
</table>
</div>



### Explanation:
In this 40 years, New York City has over 4200000 violent crimes happens. 


```python
crimes_NewYork = crimes[(crimes['agency_jurisdiction'] == "New York City, NY")]
crimes_NewYork1 = crimes_NewYork[['report_year','violent_crimes', 'population']]
```


```python
crimes_NewYork2 = crimes_NewYork1.groupby(by = "report_year").sum()
```


```python
crimes_NewYork2.plot(y='violent_crimes')
```




    <matplotlib.axes._subplots.AxesSubplot at 0x11b5e26a0>




![png](output_20_1.png)



```python
crimes_NewYork2.plot(y='population')
```




    <matplotlib.axes._subplots.AxesSubplot at 0x11b817828>




![png](output_21_1.png)


### Explanation:
In this two figures, we can understand the population of New York City are increasing from 1995. And, the number of crimes are decreasing from 1990. It seems that the New York City has a bunch number of crimes becasue of it's populaton. Comparing with the its past, the city are getting safe. 

### C. The crimes in California


```python
crimes_in_CA = crimes[(crimes['agency_jurisdiction'] == "Oakland, CA") |
       (crimes['agency_jurisdiction'] == "Long Beach, CA" ) |
      (crimes['agency_jurisdiction'] == "Los Angeles County, CA" ) |
      (crimes['agency_jurisdiction'] == "Los Angeles, CA" ) |
      (crimes['agency_jurisdiction'] == "Sacramento, CA" ) |
      (crimes['agency_jurisdiction'] == "San Francisco, CA" ) |
      (crimes['agency_jurisdiction'] == "San Jose, CA" ) |
      (crimes['agency_jurisdiction'] == "Fresno, CA" ) |
      (crimes['agency_jurisdiction'] == "San Diego, CA" )]
```


```python
crimes_in_CA1 = crimes_in_CA.groupby(by = "agency_jurisdiction").sum()
crimes_in_CA1.sort_values(by= "crimes_percapita", ascending=[False]).head(10)
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
      <th>report_year</th>
      <th>population</th>
      <th>violent_crimes</th>
      <th>homicides</th>
      <th>rapes</th>
      <th>assaults</th>
      <th>robberies</th>
      <th>months_reported</th>
      <th>crimes_percapita</th>
      <th>homicides_percapita</th>
      <th>rapes_percapita</th>
      <th>assaults_percapita</th>
      <th>robberies_percapita</th>
    </tr>
    <tr>
      <th>agency_jurisdiction</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Oakland, CA</th>
      <td>81795</td>
      <td>15490811.0</td>
      <td>280043.0</td>
      <td>4475.0</td>
      <td>14574.0</td>
      <td>126237.0</td>
      <td>134757.0</td>
      <td>468.0</td>
      <td>74332.67</td>
      <td>1190.96</td>
      <td>3906.72</td>
      <td>33377.60</td>
      <td>35857.39</td>
    </tr>
    <tr>
      <th>Los Angeles, CA</th>
      <td>81795</td>
      <td>142984519.0</td>
      <td>1979166.0</td>
      <td>25999.0</td>
      <td>69748.0</td>
      <td>1027731.0</td>
      <td>855688.0</td>
      <td>480.0</td>
      <td>57819.00</td>
      <td>769.39</td>
      <td>2089.38</td>
      <td>29763.86</td>
      <td>25196.38</td>
    </tr>
    <tr>
      <th>San Francisco, CA</th>
      <td>81795</td>
      <td>30759868.0</td>
      <td>360218.0</td>
      <td>3588.0</td>
      <td>14555.0</td>
      <td>136130.0</td>
      <td>205945.0</td>
      <td>480.0</td>
      <td>48815.45</td>
      <td>488.45</td>
      <td>1999.53</td>
      <td>18353.16</td>
      <td>27974.34</td>
    </tr>
    <tr>
      <th>Los Angeles County, CA</th>
      <td>81795</td>
      <td>42083296.0</td>
      <td>426589.0</td>
      <td>6270.0</td>
      <td>14827.0</td>
      <td>287532.0</td>
      <td>117960.0</td>
      <td>480.0</td>
      <td>42042.71</td>
      <td>617.05</td>
      <td>1449.17</td>
      <td>28367.84</td>
      <td>11608.67</td>
    </tr>
    <tr>
      <th>Long Beach, CA</th>
      <td>81795</td>
      <td>17562745.0</td>
      <td>175503.0</td>
      <td>2456.0</td>
      <td>7505.0</td>
      <td>76344.0</td>
      <td>89198.0</td>
      <td>480.0</td>
      <td>41604.22</td>
      <td>588.62</td>
      <td>1823.30</td>
      <td>17771.23</td>
      <td>21421.07</td>
    </tr>
    <tr>
      <th>Sacramento, CA</th>
      <td>81795</td>
      <td>15570963.0</td>
      <td>154466.0</td>
      <td>1963.0</td>
      <td>7432.0</td>
      <td>75781.0</td>
      <td>69290.0</td>
      <td>480.0</td>
      <td>41535.93</td>
      <td>546.17</td>
      <td>2096.25</td>
      <td>19920.05</td>
      <td>18973.45</td>
    </tr>
    <tr>
      <th>Fresno, CA</th>
      <td>81795</td>
      <td>14976953.0</td>
      <td>137711.0</td>
      <td>1904.0</td>
      <td>6328.0</td>
      <td>73621.0</td>
      <td>55858.0</td>
      <td>480.0</td>
      <td>38975.92</td>
      <td>565.87</td>
      <td>1931.64</td>
      <td>20011.64</td>
      <td>16466.80</td>
    </tr>
    <tr>
      <th>San Diego, CA</th>
      <td>81795</td>
      <td>46189196.0</td>
      <td>308976.0</td>
      <td>3149.0</td>
      <td>15165.0</td>
      <td>182919.0</td>
      <td>107743.0</td>
      <td>480.0</td>
      <td>27736.65</td>
      <td>294.11</td>
      <td>1377.98</td>
      <td>16006.34</td>
      <td>10058.31</td>
    </tr>
    <tr>
      <th>San Jose, CA</th>
      <td>81795</td>
      <td>33186359.0</td>
      <td>167548.0</td>
      <td>1513.0</td>
      <td>14290.0</td>
      <td>106707.0</td>
      <td>45038.0</td>
      <td>480.0</td>
      <td>21029.55</td>
      <td>198.50</td>
      <td>1852.62</td>
      <td>13134.74</td>
      <td>5843.69</td>
    </tr>
  </tbody>
</table>
</div>



### Explanation:
In California, the data in this 40 years, according to the crimes per capita, Okland is the most dangerous city.

### C.2) The Crimes in California in 2015


```python
crimes_in_CA_2000 = crimes_in_CA[(crimes_in_CA['report_year'] == 2015)]
```


```python
crimes_in_CA_2000_1 = crimes_in_CA_2000.groupby(by = "agency_jurisdiction").sum()
crimes_in_CA_2000_1.sort_values(by= "crimes_percapita", ascending=[False]).head(10)
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
      <th>report_year</th>
      <th>population</th>
      <th>violent_crimes</th>
      <th>homicides</th>
      <th>rapes</th>
      <th>assaults</th>
      <th>robberies</th>
      <th>months_reported</th>
      <th>crimes_percapita</th>
      <th>homicides_percapita</th>
      <th>rapes_percapita</th>
      <th>assaults_percapita</th>
      <th>robberies_percapita</th>
    </tr>
    <tr>
      <th>agency_jurisdiction</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Oakland, CA</th>
      <td>2015</td>
      <td>419481.0</td>
      <td>6051.0</td>
      <td>85.0</td>
      <td>285.0</td>
      <td>2391.0</td>
      <td>3290.0</td>
      <td>0.0</td>
      <td>1442.50</td>
      <td>20.26</td>
      <td>67.94</td>
      <td>569.99</td>
      <td>784.30</td>
    </tr>
    <tr>
      <th>San Francisco, CA</th>
      <td>2015</td>
      <td>863782.0</td>
      <td>6710.0</td>
      <td>53.0</td>
      <td>344.0</td>
      <td>2703.0</td>
      <td>3610.0</td>
      <td>0.0</td>
      <td>776.82</td>
      <td>6.14</td>
      <td>39.82</td>
      <td>312.93</td>
      <td>417.93</td>
    </tr>
    <tr>
      <th>Sacramento, CA</th>
      <td>2015</td>
      <td>489717.0</td>
      <td>3611.0</td>
      <td>43.0</td>
      <td>105.0</td>
      <td>2289.0</td>
      <td>1174.0</td>
      <td>0.0</td>
      <td>737.36</td>
      <td>8.78</td>
      <td>21.44</td>
      <td>467.41</td>
      <td>239.73</td>
    </tr>
    <tr>
      <th>Los Angeles, CA</th>
      <td>2015</td>
      <td>3962726.0</td>
      <td>25156.0</td>
      <td>282.0</td>
      <td>2209.0</td>
      <td>13713.0</td>
      <td>8952.0</td>
      <td>0.0</td>
      <td>634.82</td>
      <td>7.12</td>
      <td>55.74</td>
      <td>346.05</td>
      <td>225.91</td>
    </tr>
    <tr>
      <th>Long Beach, CA</th>
      <td>2015</td>
      <td>476318.0</td>
      <td>2766.0</td>
      <td>36.0</td>
      <td>177.0</td>
      <td>1499.0</td>
      <td>1054.0</td>
      <td>0.0</td>
      <td>580.70</td>
      <td>7.56</td>
      <td>37.16</td>
      <td>314.71</td>
      <td>221.28</td>
    </tr>
    <tr>
      <th>Fresno, CA</th>
      <td>2015</td>
      <td>520837.0</td>
      <td>2871.0</td>
      <td>39.0</td>
      <td>167.0</td>
      <td>1653.0</td>
      <td>1012.0</td>
      <td>0.0</td>
      <td>551.23</td>
      <td>7.49</td>
      <td>32.06</td>
      <td>317.37</td>
      <td>194.30</td>
    </tr>
    <tr>
      <th>Los Angeles County, CA</th>
      <td>2015</td>
      <td>1111939.0</td>
      <td>5173.0</td>
      <td>98.0</td>
      <td>304.0</td>
      <td>3559.0</td>
      <td>1212.0</td>
      <td>0.0</td>
      <td>465.22</td>
      <td>8.81</td>
      <td>27.34</td>
      <td>320.07</td>
      <td>109.00</td>
    </tr>
    <tr>
      <th>San Diego, CA</th>
      <td>2015</td>
      <td>1400467.0</td>
      <td>5582.0</td>
      <td>37.0</td>
      <td>566.0</td>
      <td>3601.0</td>
      <td>1378.0</td>
      <td>0.0</td>
      <td>398.58</td>
      <td>2.64</td>
      <td>40.42</td>
      <td>257.13</td>
      <td>98.40</td>
    </tr>
    <tr>
      <th>San Jose, CA</th>
      <td>2015</td>
      <td>1031458.0</td>
      <td>3400.0</td>
      <td>30.0</td>
      <td>375.0</td>
      <td>1855.0</td>
      <td>1140.0</td>
      <td>0.0</td>
      <td>329.63</td>
      <td>2.91</td>
      <td>36.36</td>
      <td>179.84</td>
      <td>110.52</td>
    </tr>
  </tbody>
</table>
</div>



### Explanation:
We concentated on 2015 the recent data, most dangerous city is still Oakland. Others are San franciso, Saramento

### D. Oakland Crimes Analysis


```python
crimes_in_CA_OKA = crimes_in_CA_2000[(crimes_in_CA_2000['agency_jurisdiction'] == 'Oakland, CA')]
crimes_in_CA_OKA
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
      <th>report_year</th>
      <th>agency_code</th>
      <th>agency_jurisdiction</th>
      <th>population</th>
      <th>violent_crimes</th>
      <th>homicides</th>
      <th>rapes</th>
      <th>assaults</th>
      <th>robberies</th>
      <th>months_reported</th>
      <th>crimes_percapita</th>
      <th>homicides_percapita</th>
      <th>rapes_percapita</th>
      <th>assaults_percapita</th>
      <th>robberies_percapita</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2803</th>
      <td>2015</td>
      <td>CA00109</td>
      <td>Oakland, CA</td>
      <td>419481.0</td>
      <td>6051.0</td>
      <td>85.0</td>
      <td>285.0</td>
      <td>2391.0</td>
      <td>3290.0</td>
      <td>NaN</td>
      <td>1442.5</td>
      <td>20.26</td>
      <td>67.94</td>
      <td>569.99</td>
      <td>784.3</td>
    </tr>
  </tbody>
</table>
</div>




```python
plt.figure(figsize=(10,8)) #调节图形大小
labels = [u'Homicides',u'Rapes',u'Assaults',u'Robberies'] #定义标签
sizes = [85.0,285.0,2391.0,3290.0] #每块值
colors = ['red','yellowgreen','lightskyblue','yellow'] #每块颜色定义
explode = (0.6,0,0,0) #将某一块分割出来，值越大分割出的间隙越大
patches,text1,text2 = plt.pie(sizes,
                      explode=explode,
                      labels=labels,
                      colors=colors,
                      autopct = '%3.2f%%', #数值保留固定小数位
                      shadow = True, #无阴影设置
                      startangle =90, #逆时针起始角度设置
                      pctdistance = 0.6) #数值距圆心半径倍数距离
#patches饼图的返回值，texts1饼图外label的文本，texts2饼图内部的文本
# x，y轴刻度设置一致，保证饼图为圆形
plt.axis('equal')
```




    (-1.1109203616822707,
     1.1111485148335918,
     -1.140576631347584,
     1.7298916687925672)




![png](output_33_1.png)


### Explanation:
We analyzed the percentage of crimes in Oakland. Robberies take up 54.3% and Assaults is 39%

## ===========One column selection=============


```python
crimes1 = pd.read_csv("../week8crime/report.csv", index_col=2)
crimes1_in2015 = crimes1[(crimes1['report_year'] == 2015)]
crimes1_in2015_1 = crimes1_in2015.sort_values(by= "crimes_percapita", ascending=[True]).head(10)
crimes1_in2015_1['crimes_percapita']
```




    agency_jurisdiction
    Fairfax County, VA        88.41
    Nassau County, NY        124.20
    Suffolk County, NY       124.86
    Virginia Beach, VA       138.25
    Montgomery County, MD    194.61
    Honolulu, HI             243.87
    San Jose, CA             329.63
    El Paso, TX              366.58
    Austin, TX               372.53
    United States            372.60
    Name: crimes_percapita, dtype: float64



### Explanation:
It appears that the safest city in USA is Fairfax County, VA with only 88.41 crimes per capita.

![](http://pics2.city-data.com/city/maps/fr1789.png)

## ================Sort=================


```python
data_sort = crimes[['report_year','homicides','rapes','assaults','robberies']]
data_sort.columns
```




    Index(['report_year', 'homicides', 'rapes', 'assaults', 'robberies'], dtype='object')



### Explanation:
By those columns, we could understand what the consist of crimes in each year.

## ===============Series=================


```python
data_series = data_sort.groupby(by = "report_year").sum()
data_series.tail(10)
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
      <th>homicides</th>
      <th>rapes</th>
      <th>assaults</th>
      <th>robberies</th>
    </tr>
    <tr>
      <th>report_year</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2006</th>
      <td>24693.0</td>
      <td>22190.0</td>
      <td>278598.0</td>
      <td>214051.0</td>
    </tr>
    <tr>
      <th>2007</th>
      <td>24179.0</td>
      <td>21141.0</td>
      <td>272239.0</td>
      <td>210704.0</td>
    </tr>
    <tr>
      <th>2008</th>
      <td>23180.0</td>
      <td>20160.0</td>
      <td>264209.0</td>
      <td>206677.0</td>
    </tr>
    <tr>
      <th>2009</th>
      <td>21384.0</td>
      <td>19895.0</td>
      <td>249491.0</td>
      <td>188615.0</td>
    </tr>
    <tr>
      <th>2010</th>
      <td>20589.0</td>
      <td>19660.0</td>
      <td>241700.0</td>
      <td>171034.0</td>
    </tr>
    <tr>
      <th>2011</th>
      <td>20363.0</td>
      <td>19573.0</td>
      <td>232878.0</td>
      <td>165825.0</td>
    </tr>
    <tr>
      <th>2012</th>
      <td>20675.0</td>
      <td>19709.0</td>
      <td>239243.0</td>
      <td>166938.0</td>
    </tr>
    <tr>
      <th>2013</th>
      <td>19663.0</td>
      <td>22739.0</td>
      <td>230952.0</td>
      <td>163472.0</td>
    </tr>
    <tr>
      <th>2014</th>
      <td>19513.0</td>
      <td>27107.0</td>
      <td>237519.0</td>
      <td>151336.0</td>
    </tr>
    <tr>
      <th>2015</th>
      <td>21738.0</td>
      <td>29423.0</td>
      <td>239964.0</td>
      <td>149998.0</td>
    </tr>
  </tbody>
</table>
</div>



### Explanation:
It seems that the numbers of each type are almost same, but the assaults in average has higher chances to happend. The order of crimes frequency is assaults, robberies, homicides, rapes.

## ==============Summary================

According our analysis, the number of crimes is decreasing in general. The highest number of crimes was in 1990 to 1995. And in this 40 years, New York City has most highest crimes happens. But the reason is the increasing of population. Fortunately, along with increasing of population in New York, the rate of crimes is decreasing. In addition, in California, according to crimes per capita, Oakland not just was the most dangerous city but also is the most dangerous city in 2015. Comparing with crime per capita in 2015, in the rank of dangerous city, Oakland is first, San Francisco is second, Sacramento is third. By analyzing the consist of crimes in Oakland, 54 percent is Robberies and 39 percent is Assaults. We also find the safest city on USA is Fairfax, VA. It only has 88 crimes per capita. So, by exploring the data, from 2006 to 2015, assaults are most happens. And, second is Robberies.

## ===========Recommendations=============

The crime in Oakland City is the problem now. But also Oakland city may be a good research objectives to find how to effectively decrease the crimes. In general, the rate of assaults and robberies are still super higher than homicides and rapes. We can focus on how to prevent this two and also enhance the police enforcement effectiveness on this two to decrease it and build a safer country. 
