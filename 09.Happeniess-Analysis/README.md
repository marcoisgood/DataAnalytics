<h1 style="color:white; background-color:steelblue;"><center style="font-size:50px">HAPPINESS </center><br><center style="font-size:20px">Author: Marco Lin</center></h1>


![](https://ichef.bbci.co.uk/news/660/cpsprodpb/1655A/production/_92928419_thinkstockphotos-508347326.jpg)

<h2><center style="font-size:25px">Contents</center></h2>

<p style="font-size:22px"><u><a href = "#1"> Part 1 - Introduction </a></u></p>
<p style="font-size:18px"><a href = "#11"> Chapter 1 - Objectives</a></p>
<p style="font-size:18px"><a href = "#12"> Chapter 2 - Happiness Facts 2017</a></p>
<p style="font-size:20px"><u><a href = "#2"> Part 2 - Correlation and Changing in 2015 2016 2017</a></u></p>
<p style="font-size:18px"><a href = "#23"> Chapter 3 - Rank of Happiness Changing</a></p>
<p style="font-size:18px"><a href = "#24"> Chapter 4 - Year-by-year Comparison in each factor</a></p>
<p style="font-size:20px"><u><a href = "#3"> Part 3 - Clustering</a></u></p>
<p style="font-size:18px"><a href = "#35"> Chapter 5 - Step-by-step clustering</a></p>
<p style="font-size:20px"><u><a href = "#4"> Part 4 - Final</a></u></p>
<p style="font-size:18px"><a href = "#46"> Chapter 6 - Recommandation and Summary</a></p>



<h2><center style="font-size:30px"><u><a id= 1>Part 1: Introduction</a></u></center></h2>

<p style="font-size:18px"><u><a id= 11>Chapter 1 - Objectives</a></u></p>

In this book, we will explore the dataset of happiness from 2015 to 2017. This is not a psychology book, but a data science book that is based on facts. So, in there we just talk about the facts based on our data. then we will try to figure out what make people feel happier.
We have three dataset, so at the first we will focus on the data in 2017. By showing our reaaders some facts at the beginning to led them to explore deeper information behine the data. 
We have three part in this book, part 1 is our introduction that just like I said that some interesting facts. Top 5 happy countries in the world, freest country in the world, and longest life expectancy country in the world. 
Then in part two we will analyze the correlation between serveral factors and happiness score and also the changing in rank of happiness. In addition, we comare with the changing in each factors like GDP, life expectancy, and Family over the years (2015 ~ 2017).
In part three, we will use the agglomeration method to analyze our cluster then show our reader a Dendrogram to understand the clustering.
At the final part, end with summary and recommandation for our reader.

<p style="font-size:18px"><u><a id= 12>Chapter 2 - Happiness Facts in 2017</a></u></p>


```python
import pandas as pd
import numpy as np
import geopandas as gp
import matplotlib.pyplot as plt
import seaborn as sns
import plotly.graph_objs as go
#import plotly.plotly as py
#from plotly.graph_objs import Figure
import plotly as py
from pandas import DataFrame, Series
from mpl_toolkits.mplot3d import Axes3D
from scipy.cluster.hierarchy import dendrogram, linkage, leaves_list
%matplotlib inline
```


```python
data15 = pd.read_csv("world-happiness-report/2015.csv")
data16 = pd.read_csv("world-happiness-report/2016.csv")
data17 = pd.read_csv("world-happiness-report/2017.csv")
```

<p style="font-size:18px"><u>2.1 Top 5 Happy Countries in 2017</u></p>


```python
data17.columns
```




    Index(['Country', 'Happiness.Rank', 'Happiness.Score', 'Whisker.high',
           'Whisker.low', 'Economy..GDP.per.Capita.', 'Family',
           'Health.Life.Expectancy', 'Freedom', 'Generosity',
           'Trust..Government.Corruption.', 'Dystopia.Residual'],
          dtype='object')




```python
data17[['Country','Happiness.Rank']].head()
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
      <th>Country</th>
      <th>Happiness.Rank</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Norway</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Denmark</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Iceland</td>
      <td>3</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Switzerland</td>
      <td>4</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Finland</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>



#### Explanation: 
The recent data we have is in 2017. In this table, it shows that the top 5 in happiness rank are Norway, Denmark, Iceland, Switerland, Finland. We will explore the changing of rank in 2015 to 2017 in chapter 3.

![](http://www.traveller.com.au/content/dam/images/1/0/7/9/q/g/image.related.articleLeadwide.620x349.gv2li5.png/1490074477177.jpg)

<p style="font-size:18px"><u>2.2 Freest Country in 2017</u></p>


```python
data17[['Country','Freedom','Happiness.Rank']].sort_values(by= "Freedom", ascending=[False]).head(10)
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
      <th>Country</th>
      <th>Freedom</th>
      <th>Happiness.Rank</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>46</th>
      <td>Uzbekistan</td>
      <td>0.658249</td>
      <td>47</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Norway</td>
      <td>0.635423</td>
      <td>1</td>
    </tr>
    <tr>
      <th>128</th>
      <td>Cambodia</td>
      <td>0.633376</td>
      <td>129</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Iceland</td>
      <td>0.627163</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Denmark</td>
      <td>0.626007</td>
      <td>2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Switzerland</td>
      <td>0.620071</td>
      <td>4</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Finland</td>
      <td>0.617951</td>
      <td>5</td>
    </tr>
    <tr>
      <th>7</th>
      <td>New Zealand</td>
      <td>0.614062</td>
      <td>8</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Sweden</td>
      <td>0.612924</td>
      <td>9</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Canada</td>
      <td>0.611101</td>
      <td>7</td>
    </tr>
  </tbody>
</table>
</div>



#### Explanation: 
It appears that the highest freedom score country is Uzbekistan. And the interesting thing is excepting Uzbekistan and Cambodia, higher freedom score has higher happiness socre.

![](https://www.kfw-entwicklungsbank.de/Bilder/Bilderordner/Maps/Uzbekistan-Map_Responsive_1080x608.jpg)

<p style="font-size:18px"><u>2.3 Longest Lift Expectancy Countries in 2017 </u></p>


```python
data17[['Country','Health.Life.Expectancy','Happiness.Rank']].sort_values(by= 'Health.Life.Expectancy', ascending=[False]).head(10)

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
      <th>Country</th>
      <th>Health.Life.Expectancy</th>
      <th>Happiness.Rank</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>25</th>
      <td>Singapore</td>
      <td>0.949492</td>
      <td>26</td>
    </tr>
    <tr>
      <th>70</th>
      <td>Hong Kong S.A.R., China</td>
      <td>0.943062</td>
      <td>71</td>
    </tr>
    <tr>
      <th>50</th>
      <td>Japan</td>
      <td>0.913476</td>
      <td>51</td>
    </tr>
    <tr>
      <th>54</th>
      <td>South Korea</td>
      <td>0.900214</td>
      <td>55</td>
    </tr>
    <tr>
      <th>33</th>
      <td>Spain</td>
      <td>0.888961</td>
      <td>34</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Switzerland</td>
      <td>0.858131</td>
      <td>4</td>
    </tr>
    <tr>
      <th>47</th>
      <td>Italy</td>
      <td>0.853144</td>
      <td>48</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Luxembourg</td>
      <td>0.845089</td>
      <td>18</td>
    </tr>
    <tr>
      <th>64</th>
      <td>Cyprus</td>
      <td>0.844715</td>
      <td>65</td>
    </tr>
    <tr>
      <th>30</th>
      <td>France</td>
      <td>0.844466</td>
      <td>31</td>
    </tr>
  </tbody>
</table>
</div>



#### Explanation: 

The highest Health.Life.Expectancy score country goes to Singapore. As we see, top 4 countries which has higher life expectancy are all Asian countries. According the data, it seems that there is no correlation between it and happiness rank.

![](http://static.asiawebdirect.com/m/phuket/portals/www-singapore-com/homepage/pagePropertiesImage/singapore.jpg.jpg)

<h2><center style="font-size:30px"><u><a id= 2>Part 2: Correlation and Changing in 2015 2016 2017</a></u></center></h2>

<p style="font-size:18px"><u><a id = 23>Chapter 3 - TOP 10 Countries in Happiness Rank Changing</a></u></p>

![](https://geology.com/world/cia-world-map.gif)

### Rank in 2017:


```python
data17['Country'].head(10)
```




    0         Norway
    1        Denmark
    2        Iceland
    3    Switzerland
    4        Finland
    5    Netherlands
    6         Canada
    7    New Zealand
    8         Sweden
    9      Australia
    Name: Country, dtype: object



### Rank in 2016:


```python
data16['Country'].head(10)
```




    0        Denmark
    1    Switzerland
    2        Iceland
    3         Norway
    4        Finland
    5         Canada
    6    Netherlands
    7    New Zealand
    8      Australia
    9         Sweden
    Name: Country, dtype: object



### Rank in 2015:


```python
data15['Country'].head(10)
```




    0    Switzerland
    1        Iceland
    2        Denmark
    3         Norway
    4         Canada
    5        Finland
    6    Netherlands
    7         Sweden
    8    New Zealand
    9      Australia
    Name: Country, dtype: object




```python
top5 = np.array([1,2,4,2,3,3,3,1,2,4,4,1,5,6,7,
                 6,5,5,7,7,6,8,10,9,9,8,8,10,9,10])
top5 = top5.reshape(10,-1)
top5_df = DataFrame(top5, index = ["Switzerland", "Iceland", "Denmark", "Norway", "Canada",
                                   "Finland","Netherlands","Sweden","New Zealand","Australia"])
top5_df.columns = [["2015", "2016", "2017"]]
top5_df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th>2015</th>
      <th>2016</th>
      <th>2017</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Switzerland</th>
      <td>1</td>
      <td>2</td>
      <td>4</td>
    </tr>
    <tr>
      <th>Iceland</th>
      <td>2</td>
      <td>3</td>
      <td>3</td>
    </tr>
    <tr>
      <th>Denmark</th>
      <td>3</td>
      <td>1</td>
      <td>2</td>
    </tr>
    <tr>
      <th>Norway</th>
      <td>4</td>
      <td>4</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Canada</th>
      <td>5</td>
      <td>6</td>
      <td>7</td>
    </tr>
    <tr>
      <th>Finland</th>
      <td>6</td>
      <td>5</td>
      <td>5</td>
    </tr>
    <tr>
      <th>Netherlands</th>
      <td>7</td>
      <td>7</td>
      <td>6</td>
    </tr>
    <tr>
      <th>Sweden</th>
      <td>8</td>
      <td>10</td>
      <td>9</td>
    </tr>
    <tr>
      <th>New Zealand</th>
      <td>9</td>
      <td>8</td>
      <td>8</td>
    </tr>
    <tr>
      <th>Australia</th>
      <td>10</td>
      <td>9</td>
      <td>10</td>
    </tr>
  </tbody>
</table>
</div>



#### Explanation: 
I organized the data I got. it shows that from 2015 to 2017, rank of happiness has a small change. But in general, the rank of happiness is very stable.

<p style="font-size:18px"><u>2.3 Correlation Changing </u></p>

Below, let's analyze the correlation in 2015 to 2017

<p style="font-size:16px"><u> a. Correlation in 2017</u></p>


```python
data17.corr()
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
      <th>Happiness.Rank</th>
      <th>Happiness.Score</th>
      <th>Whisker.high</th>
      <th>Whisker.low</th>
      <th>Economy..GDP.per.Capita.</th>
      <th>Family</th>
      <th>Health.Life.Expectancy</th>
      <th>Freedom</th>
      <th>Generosity</th>
      <th>Trust..Government.Corruption.</th>
      <th>Dystopia.Residual</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Happiness.Rank</th>
      <td>1.000000</td>
      <td>-0.992774</td>
      <td>-0.993058</td>
      <td>-0.991533</td>
      <td>-0.813244</td>
      <td>-0.736753</td>
      <td>-0.780716</td>
      <td>-0.551608</td>
      <td>-0.132620</td>
      <td>-0.405842</td>
      <td>-0.484506</td>
    </tr>
    <tr>
      <th>Happiness.Score</th>
      <td>-0.992774</td>
      <td>1.000000</td>
      <td>0.999497</td>
      <td>0.999520</td>
      <td>0.812469</td>
      <td>0.752737</td>
      <td>0.781951</td>
      <td>0.570137</td>
      <td>0.155256</td>
      <td>0.429080</td>
      <td>0.475355</td>
    </tr>
    <tr>
      <th>Whisker.high</th>
      <td>-0.993058</td>
      <td>0.999497</td>
      <td>1.000000</td>
      <td>0.998036</td>
      <td>0.811868</td>
      <td>0.750934</td>
      <td>0.776634</td>
      <td>0.569907</td>
      <td>0.155462</td>
      <td>0.426459</td>
      <td>0.478824</td>
    </tr>
    <tr>
      <th>Whisker.low</th>
      <td>-0.991533</td>
      <td>0.999520</td>
      <td>0.998036</td>
      <td>1.000000</td>
      <td>0.812267</td>
      <td>0.753767</td>
      <td>0.786385</td>
      <td>0.569808</td>
      <td>0.154904</td>
      <td>0.431223</td>
      <td>0.471505</td>
    </tr>
    <tr>
      <th>Economy..GDP.per.Capita.</th>
      <td>-0.813244</td>
      <td>0.812469</td>
      <td>0.811868</td>
      <td>0.812267</td>
      <td>1.000000</td>
      <td>0.688296</td>
      <td>0.843077</td>
      <td>0.369873</td>
      <td>-0.019011</td>
      <td>0.350944</td>
      <td>0.024226</td>
    </tr>
    <tr>
      <th>Family</th>
      <td>-0.736753</td>
      <td>0.752737</td>
      <td>0.750934</td>
      <td>0.753767</td>
      <td>0.688296</td>
      <td>1.000000</td>
      <td>0.612080</td>
      <td>0.424966</td>
      <td>0.051693</td>
      <td>0.231841</td>
      <td>0.070506</td>
    </tr>
    <tr>
      <th>Health.Life.Expectancy</th>
      <td>-0.780716</td>
      <td>0.781951</td>
      <td>0.776634</td>
      <td>0.786385</td>
      <td>0.843077</td>
      <td>0.612080</td>
      <td>1.000000</td>
      <td>0.349827</td>
      <td>0.063191</td>
      <td>0.279752</td>
      <td>0.054963</td>
    </tr>
    <tr>
      <th>Freedom</th>
      <td>-0.551608</td>
      <td>0.570137</td>
      <td>0.569907</td>
      <td>0.569808</td>
      <td>0.369873</td>
      <td>0.424966</td>
      <td>0.349827</td>
      <td>1.000000</td>
      <td>0.316083</td>
      <td>0.499183</td>
      <td>0.081926</td>
    </tr>
    <tr>
      <th>Generosity</th>
      <td>-0.132620</td>
      <td>0.155256</td>
      <td>0.155462</td>
      <td>0.154904</td>
      <td>-0.019011</td>
      <td>0.051693</td>
      <td>0.063191</td>
      <td>0.316083</td>
      <td>1.000000</td>
      <td>0.294159</td>
      <td>-0.116627</td>
    </tr>
    <tr>
      <th>Trust..Government.Corruption.</th>
      <td>-0.405842</td>
      <td>0.429080</td>
      <td>0.426459</td>
      <td>0.431223</td>
      <td>0.350944</td>
      <td>0.231841</td>
      <td>0.279752</td>
      <td>0.499183</td>
      <td>0.294159</td>
      <td>1.000000</td>
      <td>-0.022755</td>
    </tr>
    <tr>
      <th>Dystopia.Residual</th>
      <td>-0.484506</td>
      <td>0.475355</td>
      <td>0.478824</td>
      <td>0.471505</td>
      <td>0.024226</td>
      <td>0.070506</td>
      <td>0.054963</td>
      <td>0.081926</td>
      <td>-0.116627</td>
      <td>-0.022755</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
plt.figure(figsize=(16,11))
sns.heatmap(data17.corr(),annot=True,cmap="Greens",linewidths=.5,fmt=".2f");
plt.show()
```


![png](output_38_0.png)


#### Explanation: 
In this heatmap, it shows how factors are correlated with happiness score. As we see, economy GDP per capita affects the happiness score most. The rate is up to 0.81. It's pretty good. And, sencond and third are family and health life expectancy. We can say the countries which has hight GDP, life expectancy, and family make citizen happier.

<p style="font-size:16px"><u> b. Correlation in 2016</u></p>


```python
plt.figure(figsize=(16,11))
sns.heatmap(data16.corr(),annot=True,cmap="Greens",linewidths=.5,fmt=".2f");
plt.show()
```


![png](output_41_0.png)


#### Explanation: 
It seems that the number of correlation between happiness score and GDP, Family, and Life Expectancy are less than the data in 2017. But, they are still main factors contributing to happiness score.

<p style="font-size:16px"><u> c. Correlation in 2015</u></p>


```python
plt.figure(figsize=(16,11))
sns.heatmap(data15.corr(),annot=True,cmap="Greens",linewidths=.5,fmt=".2f");
plt.show()
```


![png](output_44_0.png)


#### Explanation: 
Above this three heatmap show that from 2015 to 2017, three columns contributing to happiness score are barely changing. So, we can say in general, people care more about economy, their family and their life expectancy that makes them feel happy.

<p style="font-size:18px"><u><a id = 24>Chapter 4 - Year-by-year Comparison</a></u></p>

<p style="font-size:18px"><u>4.1 Comparison Changing </u></p>

<p style="font-size:16px"><u> a. Happiness score</u></p>

![](https://thumbs.dreamstime.com/t/happiness-word-happiness-word-d-rendered-red-gray-metallic-color-isolated-white-background-114636778.jpg)


```python
sns.kdeplot(data15['Happiness Score'], label='2015')
sns.kdeplot(data16['Happiness Score'], label='2016')
sns.kdeplot(data17['Happiness.Score'], label='2017')
plt.xlabel('Happiness Score')
```

    /Users/MrM/anaconda3/lib/python3.7/site-packages/scipy/stats/stats.py:1713: FutureWarning: Using a non-tuple sequence for multidimensional indexing is deprecated; use `arr[tuple(seq)]` instead of `arr[seq]`. In the future this will be interpreted as an array index, `arr[np.array(seq)]`, which will result either in an error or a different result.
      return np.add.reduce(sorted[indexer] * weights, axis=axis) / sumval





    Text(0.5, 0, 'Happiness Score')




![png](output_50_2.png)


#### Explanation: 
From 2015 to 2017, in average, the line of 2016 moved to right a little be, and line of 2017 almost touched 0.3. It seems that in the world, most countries are improving themself. 

<p style="font-size:16px"><u> b. Freedom</u></p>

![](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTa1j-Y-ZvHUwXf9MNEF9zQ99doWRtoi6lkYtZ-TQ54OpkN0UrRWg)


```python
sns.kdeplot(data15['Freedom'], label='2015')
sns.kdeplot(data16['Freedom'], label='2016')
sns.kdeplot(data17['Freedom'], label='2017')
plt.xlabel('Freedom Score')
```




    Text(0.5, 0, 'Freedom Score')




![png](output_54_1.png)


#### Explanation: 
In 2017, look at highest point, freedom score was higher than in 2015 and 2016. It seems that the freedom socres in general are increasing.

<p style="font-size:16px"><u> c. GDP</u></p>

![](https://moneycrashers-sparkchargemedia.netdna-ssl.com/wp-content/uploads/2012/07/gdp-data-report-1068x600.jpg)


```python
sns.kdeplot(data15['Economy..GDP.per.Capita.'], label='2015')
sns.kdeplot(data16['Economy..GDP.per.Capita.'], label='2016')
sns.kdeplot(data17['Economy..GDP.per.Capita.'], label='2017')
plt.xlabel('GDP Score')
```




    Text(0.5, 0, 'GDP Score')




![png](output_58_1.png)


#### Explanation: 
The polt shows that the number of countries which has greater than 1.5 is increaing. That is the reason why the line of 2017 moved to right a little.

<p style="font-size:16px"><u> d. Life Expectancy</u></p>

![](http://www.consumerhealthfdn.org/wp-content/uploads/2018/02/life-expectancy-1024x1024.png)


```python
sns.kdeplot(data15['Health.Life.Expectancy'], label='2015')
sns.kdeplot(data17['Health.Life.Expectancy'], label='2017')
plt.xlabel('Life Expectancy Score')
```




    Text(0.5, 0, 'Life Expectancy Score')




![png](output_62_1.png)


#### Explanation: 
From 2015 to 2017, interesting thing is in general, the life expectancy score less than in 2015. 

<h2><center style="font-size:30px"><u><a id = 3>Part 3: Clustering<a/></u></center></h2>

<p style="font-size:20px"><u><a id = 35>Chapter 5 - Step-by-step clustering and Dendrogram</a></u></p>

<p style="font-size:18px"><u>5.1 - Choose variables and calculate the distance  </u></p>


```python
data16S = data16[(data16['Region'] == 'Eastern Asia') | (data16['Region'] == 'North America')]
```


```python
data_clustering = data16S[['Country','Freedom','Economy..GDP.per.Capita.','Health.Life.Expectancy']]
```


```python
data_clustering.set_index(['Country'], inplace = True)
```


```python
data_clustering
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
      <th>Freedom</th>
      <th>Economy..GDP.per.Capita.</th>
      <th>Health.Life.Expectancy</th>
    </tr>
    <tr>
      <th>Country</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Canada</th>
      <td>0.57370</td>
      <td>1.44015</td>
      <td>0.82760</td>
    </tr>
    <tr>
      <th>United States</th>
      <td>0.48163</td>
      <td>1.50796</td>
      <td>0.77900</td>
    </tr>
    <tr>
      <th>Taiwan</th>
      <td>0.32377</td>
      <td>1.39729</td>
      <td>0.79565</td>
    </tr>
    <tr>
      <th>Japan</th>
      <td>0.46761</td>
      <td>1.38007</td>
      <td>0.91491</td>
    </tr>
    <tr>
      <th>South Korea</th>
      <td>0.25168</td>
      <td>1.35948</td>
      <td>0.88645</td>
    </tr>
    <tr>
      <th>Hong Kong</th>
      <td>0.48079</td>
      <td>1.51070</td>
      <td>0.95277</td>
    </tr>
    <tr>
      <th>China</th>
      <td>0.44012</td>
      <td>1.02780</td>
      <td>0.73561</td>
    </tr>
    <tr>
      <th>Mongolia</th>
      <td>0.35972</td>
      <td>0.98853</td>
      <td>0.55469</td>
    </tr>
  </tbody>
</table>
</div>



#### Explanation:

I chose this three columns for clutering.


```python
from sklearn.metrics.pairwise import euclidean_distances
data_clustering_D = DataFrame(euclidean_distances(data_clustering))
data_clustering_D.astype(float)
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
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
      <th>5</th>
      <th>6</th>
      <th>7</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.000000</td>
      <td>0.124246</td>
      <td>0.255583</td>
      <td>0.149959</td>
      <td>0.337147</td>
      <td>0.171106</td>
      <td>0.443101</td>
      <td>0.569410</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.124246</td>
      <td>0.000000</td>
      <td>0.193507</td>
      <td>0.187147</td>
      <td>0.294056</td>
      <td>0.173794</td>
      <td>0.483900</td>
      <td>0.578778</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.255583</td>
      <td>0.193507</td>
      <td>0.000000</td>
      <td>0.187642</td>
      <td>0.121948</td>
      <td>0.249407</td>
      <td>0.392001</td>
      <td>0.475856</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0.149959</td>
      <td>0.187147</td>
      <td>0.187642</td>
      <td>0.000000</td>
      <td>0.218769</td>
      <td>0.136643</td>
      <td>0.396230</td>
      <td>0.542865</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0.337147</td>
      <td>0.294056</td>
      <td>0.121948</td>
      <td>0.218769</td>
      <td>0.000000</td>
      <td>0.282413</td>
      <td>0.410212</td>
      <td>0.509256</td>
    </tr>
    <tr>
      <th>5</th>
      <td>0.171106</td>
      <td>0.173794</td>
      <td>0.249407</td>
      <td>0.136643</td>
      <td>0.282413</td>
      <td>0.000000</td>
      <td>0.531041</td>
      <td>0.667673</td>
    </tr>
    <tr>
      <th>6</th>
      <td>0.443101</td>
      <td>0.483900</td>
      <td>0.392001</td>
      <td>0.396230</td>
      <td>0.410212</td>
      <td>0.531041</td>
      <td>0.000000</td>
      <td>0.201837</td>
    </tr>
    <tr>
      <th>7</th>
      <td>0.569410</td>
      <td>0.578778</td>
      <td>0.475856</td>
      <td>0.542865</td>
      <td>0.509256</td>
      <td>0.667673</td>
      <td>0.201837</td>
      <td>0.000000</td>
    </tr>
  </tbody>
</table>
</div>



#### Explanation:
We calculated the distance of each variables. The table we have is for next step to find the clustering. We will find several clustering by analyze the closest variables.

<p style="font-size:18px"><u>5.2 - Clustering by distance  </u></p>


```python
import random

clusterOne = 0
clusterTwo = 0

while clusterTwo == clusterOne:
    clusterOne = random.randint(0,7)
    clusterTwo = random.randint(0,7)

groupOne = []
groupTwo = []


for j in range(0,8):
    if clusterOne == j:
        pass
    else:
        if data_clustering_D.iloc[clusterOne][j] > data_clustering_D.iloc[clusterTwo][j]:
            groupTwo.append(clusterTwo*10+j)
        else:
            groupOne.append(clusterOne*10+j)
```

#### Explanation: 
By this for loop, we can find two clusters. The output like below.


```python
groupTwo
```




    [76, 77]



#### Explanation: 
In this group, index 7 is Mongolia, and we have China, Mongolia in the same group.


```python
groupOne
```




    [50, 51, 52, 53, 54]



#### Explanation: 
In this group, index 5 is Hong Kong, and we have Canada, United States, Taiwan, Japan, South Korea in the same group.

<p style="font-size:18px"><u>5.2 - Dendrogram </u></p>

I focus on the region Eastern asia and North America.


```python
data16a = data16[(data16['Region'] == 'Eastern Asia') | (data16['Region'] == 'North America')]
```


```python
data_dendrogram = data16a[['Country','Freedom','Economy..GDP.per.Capita.','Health.Life.Expectancy']]
```


```python
data_dendrogram.set_index(['Country'], inplace = True)
```


```python
Z = linkage(data_dendrogram, 'average')
```


```python
plt.figure(figsize=(40, 40))
D = dendrogram(Z=Z, orientation="right", leaf_font_size=40, 
               labels = data_dendrogram.index)
```


![png](output_87_0.png)


#### Explanation
Dendgram can show us which data are most close and it is easy for us to identify different clusters. In here, it appears that Hongkong and Japan are belong to same cluster. USA and Canada, South Korea and Taiwan, Monglia and China are other three clusters. In this dendgram, we have 7 clusters. 

<h2><center style="font-size:30px"><u><a id =4>Part 4: Final</a></u></center></h2>

<p style="font-size:18px"><u><a id= 46>Chapter 6 - Recommandation and Summary</a></u></p>

<p style="font-size:18px"><u> 6.1 - Summary</u></p>

As we see in this analysis, the top 5 happy countries were Norway, Denmark, Iceland, Switzerland, and Finland in 2017. The freest country was Uzbekistan. Longest life expectancy country were Singapore. By comparing with each dataset in each year, we found from 2015 to 2017, top 10 happy countries in the world were almost same. So, we analyzed the correlation between happiness score and factors. We also found the factors which were contributed to happiness score didn’t change. GDP per capita, Family, and life expectancy were three main factors which affected happiness score most. But according to comparison of changing of factors like freedom, GDP, and life expectancy in each year, it appears that in each countries had a small improvement every year. The number of countries which has higher score in each have enhanced. So, it shows that people felt happier in general. For clustering, we chose the countries which is located at Eastern Asian and North America. By calculating the distance of scores, we can get a dendgram at the end. This plot shows that which countries have similar attributes. For example, Hong Kong and Japan were together. USA and Canada were in same cluster. We have 7 clusters over here. 

<p style="font-size:18px"><u> 6.2 - Recommandation</u></p>

For recommendation, as we know GDP, family score, and life expectancy will affect happiness score most. So, we recommend governments that if they want to enhance the happiness score from citizen, they should start from this three factors. But the higher priority factor is GDP. So, we can say people in general will feel better if their country has higher GDP meaning people may feel more comfortable with money. So, I will recommend government money can’t buy everything but can buy happiness. 
