### Group Assignment 2: Exploring Walkscore Data to Add to our Park Access and Affordable Housing
# This part of the project aims to visualize and assess variables relevant to walkability across different LA cities
# By Adriana Valencia Wences



```python
# import pandas
import pandas as pd
```


```python
# read the Walk Score LA data
df = pd.read_csv('Walk_Score__2019_.csv')
```


```python
# look at data size
df.shape
```




    (71, 2)




```python
# look at data size
df.head()
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
      <th>City</th>
      <th>Walk Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Agoura Hills</td>
      <td>36</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Alhambra</td>
      <td>69</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Arcadia</td>
      <td>53</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Artesia</td>
      <td>75</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Azusa</td>
      <td>55</td>
    </tr>
  </tbody>
</table>
</div>




```python
# look at all of the data
pd.set_option('display.max_columns', None)
pd.set_option('display.max_rows', None)
```


```python
# look at sample
df.sample()
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
      <th>City</th>
      <th>Walk Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Alhambra</td>
      <td>69</td>
    </tr>
  </tbody>
</table>
</div>




```python
# import relevant libraries before plotting and visualizing
# read and visualize spatial data
import geopandas as gpd

# add basemaps
import contextily as ctx

#add plots
import matplotlib.pyplot as plt

```


```python
# look at data types
df.info
```




    <bound method DataFrame.info of                     City  Walk Score
    0           Agoura Hills          36
    1               Alhambra          69
    2                Arcadia          53
    3                Artesia          75
    4                  Azusa          55
    5           Baldwin Park          50
    6                   Bell          74
    7           Bell Gardens          68
    8             Bellflower          62
    9          Beverly Hills          78
    10               Burbank          69
    11             Calabasas          20
    12                Carson          53
    13              Cerritos          54
    14             Claremont          46
    15               Compton          63
    16                Covina          56
    17                Cudahy          63
    18           Culver City          73
    19           Diamond Bar          28
    20                Downey          59
    21                Duarte          47
    22              El Monte          60
    23            El Segundo          69
    24               Gardena          74
    25              Glendale          69
    26              Glendora          44
    27             Hawthorne          69
    28         Hermosa Beach          84
    29       Huntington Park          80
    30             Inglewood          69
    31  La Cañada Flintridge          31
    32              La Habra          61
    33             La Mirada          47
    34             La Puente          54
    35              La Verne          39
    36              Lakewood          53
    37             Lancaster          28
    38              Lawndale          76
    39                Lomita          69
    40            Long Beach          70
    41           Los Angeles          67
    42               Lynwood          65
    43       Manhattan Beach          70
    44               Maywood          77
    45              Monrovia          60
    46            Montebello          64
    47         Monterey Park          61
    48               Norwalk          58
    49              Palmdale          25
    50             Paramount          63
    51              Pasadena          66
    52           Pico Rivera          56
    53                Pomona          52
    54   Rancho Palos Verdes          26
    55         Redondo Beach          74
    56              Rosemead          61
    57             San Dimas          36
    58          San Fernando          73
    59           San Gabriel          69
    60         Santa Clarita          34
    61          Santa Monica          83
    62        South El Monte          64
    63            South Gate          69
    64        South Pasadena          65
    65           Temple City          55
    66              Torrance          64
    67                Walnut          32
    68           West Covina          45
    69        West Hollywood          91
    70              Whittier          61>




```python
# plot data
df.plot(figsize=(10,10))
```




    <AxesSubplot:>




    
![png](output_9_1.png)
    



```python
# need to decide if we are doing incorporated cities, may need to filter out unicorporated cities later
# need to add geospatial data, so that I can map it based on city
# need to look up how to add city names instead of numbers assigned to cities and arranged the axes accordingly, small to large
# for now, I will add LA City Boundary data in order to add city geodata into this notebook
```


```python
# read LA County City Boundary Data
gdf = gpd.read_file('LA_County_City_Boundaries.geojson')
```


```python
# look at City Boundary Data
gdf.shape
```




    (318, 20)




```python
gdf.head()
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
      <th>OBJECTID</th>
      <th>CITY</th>
      <th>CITY_ID</th>
      <th>CITY_TYPE</th>
      <th>CITY_NAME</th>
      <th>CITY_LABEL</th>
      <th>COLOR_CODE</th>
      <th>ABBR</th>
      <th>CITY_NO</th>
      <th>DESCRIPTN</th>
      <th>URL</th>
      <th>PHONE</th>
      <th>OF_AREA_SM</th>
      <th>FEAT_TYPE</th>
      <th>COMMENT</th>
      <th>COLOR_EGIS</th>
      <th>POPULATION</th>
      <th>ShapeSTArea</th>
      <th>ShapeSTLength</th>
      <th>geometry</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>47054</td>
      <td>None</td>
      <td>None</td>
      <td>Unincorporated</td>
      <td>Unincorporated</td>
      <td>CO</td>
      <td>1</td>
      <td>None</td>
      <td>0</td>
      <td>UNINC</td>
      <td>www.lacounty.gov</td>
      <td>2139744321</td>
      <td>0.000</td>
      <td>Land</td>
      <td>None</td>
      <td>Yellow - RGB 255,255,115</td>
      <td>None</td>
      <td>9.772983e+07</td>
      <td>87319.861585</td>
      <td>POLYGON ((-118.29604 34.71834, -118.29713 34.7...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>47055</td>
      <td>None</td>
      <td>None</td>
      <td>City</td>
      <td>Los Angeles</td>
      <td>Los Angeles</td>
      <td>9</td>
      <td>None</td>
      <td>49</td>
      <td>LA</td>
      <td>http://www.lacity.org</td>
      <td>2134733231</td>
      <td>468.852</td>
      <td>Breakwater</td>
      <td>None</td>
      <td>Gray - RGB 178,178,178</td>
      <td>None</td>
      <td>2.211628e+04</td>
      <td>979.782645</td>
      <td>POLYGON ((-118.45620 33.96123, -118.45636 33.9...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>47056</td>
      <td>None</td>
      <td>None</td>
      <td>City</td>
      <td>Los Angeles</td>
      <td>Los Angeles</td>
      <td>9</td>
      <td>None</td>
      <td>49</td>
      <td>LA</td>
      <td>http://www.lacity.org</td>
      <td>2134733231</td>
      <td>468.852</td>
      <td>Breakwater</td>
      <td>None</td>
      <td>Gray - RGB 178,178,178</td>
      <td>None</td>
      <td>5.329338e+04</td>
      <td>2226.794124</td>
      <td>POLYGON ((-118.45722 33.96182, -118.45737 33.9...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>47057</td>
      <td>None</td>
      <td>None</td>
      <td>City</td>
      <td>Los Angeles</td>
      <td>Los Angeles</td>
      <td>9</td>
      <td>None</td>
      <td>49</td>
      <td>LA</td>
      <td>http://www.lacity.org</td>
      <td>2134733231</td>
      <td>468.852</td>
      <td>Breakwater</td>
      <td>None</td>
      <td>Gray - RGB 178,178,178</td>
      <td>None</td>
      <td>1.179389e+05</td>
      <td>4796.088398</td>
      <td>POLYGON ((-118.46433 33.96365, -118.46433 33.9...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>47058</td>
      <td>None</td>
      <td>None</td>
      <td>Unincorporated</td>
      <td>Unincorporated</td>
      <td>CO</td>
      <td>1</td>
      <td>None</td>
      <td>0</td>
      <td>UNINC</td>
      <td>www.lacounty.gov</td>
      <td>2139744321</td>
      <td>0.000</td>
      <td>Land</td>
      <td>None</td>
      <td>Yellow - RGB 255,255,115</td>
      <td>None</td>
      <td>3.330984e+05</td>
      <td>2883.436433</td>
      <td>POLYGON ((-118.01564 33.97709, -118.01564 33.9...</td>
    </tr>
  </tbody>
</table>
</div>




```python
# plot it
gdf.plot(figsize=(10,10))
```




    <AxesSubplot:>




    
![png](output_14_1.png)
    



```python
# yay it worked
# look at data types
gdf.info()
```

    <class 'geopandas.geodataframe.GeoDataFrame'>
    RangeIndex: 318 entries, 0 to 317
    Data columns (total 20 columns):
     #   Column         Non-Null Count  Dtype   
    ---  ------         --------------  -----   
     0   OBJECTID       318 non-null    int64   
     1   CITY           0 non-null      object  
     2   CITY_ID        0 non-null      object  
     3   CITY_TYPE      318 non-null    object  
     4   CITY_NAME      318 non-null    object  
     5   CITY_LABEL     318 non-null    object  
     6   COLOR_CODE     318 non-null    int64   
     7   ABBR           0 non-null      object  
     8   CITY_NO        318 non-null    int64   
     9   DESCRIPTN      318 non-null    object  
     10  URL            318 non-null    object  
     11  PHONE          318 non-null    object  
     12  OF_AREA_SM     318 non-null    float64 
     13  FEAT_TYPE      318 non-null    object  
     14  COMMENT        0 non-null      object  
     15  COLOR_EGIS     318 non-null    object  
     16  POPULATION     0 non-null      object  
     17  ShapeSTArea    318 non-null    float64 
     18  ShapeSTLength  318 non-null    float64 
     19  geometry       318 non-null    geometry
    dtypes: float64(3), geometry(1), int64(3), object(13)
    memory usage: 49.8+ KB



```python
# now to get cities, instead of geoid, it doesn't come with geoid info
gdf.CITY_NAME.head()
```




    0    Unincorporated
    1       Los Angeles
    2       Los Angeles
    3       Los Angeles
    4    Unincorporated
    Name: CITY_NAME, dtype: object




```python

```
