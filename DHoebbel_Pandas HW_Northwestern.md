

```python
#import dependencies
import pandas as pd
import numpy as np
```


```python
#read in files
schools = "Resources/schools_complete.csv"
students = "Resources/students_complete.csv"
```


```python
#Show schools_df head summary
schools_df = pd.read_csv(schools)
schools_df = schools_df.rename(columns = {'name':'school'})
schools_df.head()

```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>School ID</th>
      <th>school</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Figueroa High School</td>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Shelton High School</td>
      <td>Charter</td>
      <td>1761</td>
      <td>1056600</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Hernandez High School</td>
      <td>District</td>
      <td>4635</td>
      <td>3022020</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Griffin High School</td>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Show students_df head summary
students_df = pd.read_csv(students)
students_df["total_score"] = (students_df["reading_score"] + students_df["math_score"])/2
students_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Student ID</th>
      <th>name</th>
      <th>gender</th>
      <th>grade</th>
      <th>school</th>
      <th>reading_score</th>
      <th>math_score</th>
      <th>total_score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Paul Bradley</td>
      <td>M</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>66</td>
      <td>79</td>
      <td>72.5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Victor Smith</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>94</td>
      <td>61</td>
      <td>77.5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Kevin Rodriguez</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>90</td>
      <td>60</td>
      <td>75.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Dr. Richard Scott</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>67</td>
      <td>58</td>
      <td>62.5</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Bonnie Ray</td>
      <td>F</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>97</td>
      <td>84</td>
      <td>90.5</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Calculate total summary table values
totalSchools = schools_df["school"].count()
totalStudents = schools_df["size"].sum()
totalBudget = schools_df["budget"].sum()
totalReading = students_df["reading_score"].mean()
totalMath = students_df["math_score"].mean()
totalPassRead = students_df[students_df["reading_score"] >= 70].count()/ students_df["reading_score"].count()
totalPassMath = students_df[students_df["math_score"] >= 70].count()/ students_df["math_score"].count()
totalPass = (totalPassRead + totalPassMath)/2
```


```python
#Summary table dataframe - why are certain fields within the dataframe? ie "Student ID" and "Name"

Total_School = pd.DataFrame({"totalSchools":[totalSchools], "totalStudents":[totalSchools], "totalBudget":[totalBudget], "totalReading":[totalReading], "totalMath":[totalMath], "totalPassRead":[totalPassRead], "totalPassMath":[totalPassMath], "totalPass":[totalPass]})
Total_School.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>totalBudget</th>
      <th>totalMath</th>
      <th>totalPass</th>
      <th>totalPassMath</th>
      <th>totalPassRead</th>
      <th>totalReading</th>
      <th>totalSchools</th>
      <th>totalStudents</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>24649428</td>
      <td>78.985371</td>
      <td>Student ID       0.803932
name             0.8...</td>
      <td>Student ID       0.749809
name             0.7...</td>
      <td>Student ID       0.858055
name             0.8...</td>
      <td>81.87784</td>
      <td>15</td>
      <td>15</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Top Five Schools by Reading Score
grouped = students_df.groupby(["school"])
grouped.mean().head(5)
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Student ID</th>
      <th>reading_score</th>
      <th>math_score</th>
      <th>total_score</th>
    </tr>
    <tr>
      <th>school</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Bailey High School</th>
      <td>20358.5</td>
      <td>81.033963</td>
      <td>77.048432</td>
      <td>79.041198</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>16941.5</td>
      <td>83.975780</td>
      <td>83.061895</td>
      <td>83.518837</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>4391.0</td>
      <td>81.158020</td>
      <td>76.711767</td>
      <td>78.934893</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>36165.0</td>
      <td>80.746258</td>
      <td>77.102592</td>
      <td>78.924425</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>12995.5</td>
      <td>83.816757</td>
      <td>83.351499</td>
      <td>83.584128</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Top Five Schools by Math Score
grouped.mean().head(5)
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Student ID</th>
      <th>reading_score</th>
      <th>math_score</th>
      <th>total_score</th>
    </tr>
    <tr>
      <th>school</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Bailey High School</th>
      <td>20358.5</td>
      <td>81.033963</td>
      <td>77.048432</td>
      <td>79.041198</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>16941.5</td>
      <td>83.975780</td>
      <td>83.061895</td>
      <td>83.518837</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>4391.0</td>
      <td>81.158020</td>
      <td>76.711767</td>
      <td>78.934893</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>36165.0</td>
      <td>80.746258</td>
      <td>77.102592</td>
      <td>78.924425</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>12995.5</td>
      <td>83.816757</td>
      <td>83.351499</td>
      <td>83.584128</td>
    </tr>
  </tbody>
</table>
</div>




```python
#reading and math scores by grades
grouped = students_df.groupby(["school","grade"])
grouped.mean()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Student ID</th>
      <th>reading_score</th>
      <th>math_score</th>
      <th>total_score</th>
    </tr>
    <tr>
      <th>school</th>
      <th>grade</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="4" valign="top">Bailey High School</th>
      <th>10th</th>
      <td>20365.058918</td>
      <td>80.907183</td>
      <td>76.996772</td>
      <td>78.951977</td>
    </tr>
    <tr>
      <th>11th</th>
      <td>20345.148681</td>
      <td>80.945643</td>
      <td>77.515588</td>
      <td>79.230616</td>
    </tr>
    <tr>
      <th>12th</th>
      <td>20386.724708</td>
      <td>80.912451</td>
      <td>76.492218</td>
      <td>78.702335</td>
    </tr>
    <tr>
      <th>9th</th>
      <td>20344.481481</td>
      <td>81.303155</td>
      <td>77.083676</td>
      <td>79.193416</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">Cabrera High School</th>
      <th>10th</th>
      <td>16909.487124</td>
      <td>84.253219</td>
      <td>83.154506</td>
      <td>83.703863</td>
    </tr>
    <tr>
      <th>11th</th>
      <td>16955.047718</td>
      <td>83.788382</td>
      <td>82.765560</td>
      <td>83.276971</td>
    </tr>
    <tr>
      <th>12th</th>
      <td>16924.570681</td>
      <td>84.287958</td>
      <td>83.277487</td>
      <td>83.782723</td>
    </tr>
    <tr>
      <th>9th</th>
      <td>16969.634470</td>
      <td>83.676136</td>
      <td>83.094697</td>
      <td>83.385417</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">Figueroa High School</th>
      <th>10th</th>
      <td>4332.703801</td>
      <td>81.408912</td>
      <td>76.539974</td>
      <td>78.974443</td>
    </tr>
    <tr>
      <th>11th</th>
      <td>4424.478138</td>
      <td>80.640339</td>
      <td>76.884344</td>
      <td>78.762341</td>
    </tr>
    <tr>
      <th>12th</th>
      <td>4414.922705</td>
      <td>81.384863</td>
      <td>77.151369</td>
      <td>79.268116</td>
    </tr>
    <tr>
      <th>9th</th>
      <td>4397.878505</td>
      <td>81.198598</td>
      <td>76.403037</td>
      <td>78.800818</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">Ford High School</th>
      <th>10th</th>
      <td>36122.879944</td>
      <td>81.262712</td>
      <td>77.672316</td>
      <td>79.467514</td>
    </tr>
    <tr>
      <th>11th</th>
      <td>36212.534143</td>
      <td>80.403642</td>
      <td>76.918058</td>
      <td>78.660850</td>
    </tr>
    <tr>
      <th>12th</th>
      <td>36153.562152</td>
      <td>80.662338</td>
      <td>76.179963</td>
      <td>78.421150</td>
    </tr>
    <tr>
      <th>9th</th>
      <td>36170.595438</td>
      <td>80.632653</td>
      <td>77.361345</td>
      <td>78.996999</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">Griffin High School</th>
      <th>10th</th>
      <td>12983.711823</td>
      <td>83.706897</td>
      <td>84.229064</td>
      <td>83.967980</td>
    </tr>
    <tr>
      <th>11th</th>
      <td>12983.038781</td>
      <td>84.288089</td>
      <td>83.842105</td>
      <td>84.065097</td>
    </tr>
    <tr>
      <th>12th</th>
      <td>12977.143836</td>
      <td>84.013699</td>
      <td>83.356164</td>
      <td>83.684932</td>
    </tr>
    <tr>
      <th>9th</th>
      <td>13031.305623</td>
      <td>83.369193</td>
      <td>82.044010</td>
      <td>82.706601</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">Hernandez High School</th>
      <th>10th</th>
      <td>9930.783211</td>
      <td>80.660147</td>
      <td>77.337408</td>
      <td>78.998778</td>
    </tr>
    <tr>
      <th>11th</th>
      <td>9948.641544</td>
      <td>81.396140</td>
      <td>77.136029</td>
      <td>79.266085</td>
    </tr>
    <tr>
      <th>12th</th>
      <td>9978.563966</td>
      <td>80.857143</td>
      <td>77.186567</td>
      <td>79.021855</td>
    </tr>
    <tr>
      <th>9th</th>
      <td>9928.620839</td>
      <td>80.866860</td>
      <td>77.438495</td>
      <td>79.152677</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">Holden High School</th>
      <th>10th</th>
      <td>23076.342105</td>
      <td>83.324561</td>
      <td>83.429825</td>
      <td>83.377193</td>
    </tr>
    <tr>
      <th>11th</th>
      <td>23046.883495</td>
      <td>83.815534</td>
      <td>85.000000</td>
      <td>84.407767</td>
    </tr>
    <tr>
      <th>12th</th>
      <td>23041.108434</td>
      <td>84.698795</td>
      <td>82.855422</td>
      <td>83.777108</td>
    </tr>
    <tr>
      <th>9th</th>
      <td>23068.314961</td>
      <td>83.677165</td>
      <td>83.787402</td>
      <td>83.732283</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">Huang High School</th>
      <th>10th</th>
      <td>1450.796610</td>
      <td>81.512386</td>
      <td>75.908735</td>
      <td>78.710561</td>
    </tr>
    <tr>
      <th>11th</th>
      <td>1458.094313</td>
      <td>81.417476</td>
      <td>76.446602</td>
      <td>78.932039</td>
    </tr>
    <tr>
      <th>12th</th>
      <td>1485.035897</td>
      <td>80.305983</td>
      <td>77.225641</td>
      <td>78.765812</td>
    </tr>
    <tr>
      <th>9th</th>
      <td>1445.726303</td>
      <td>81.290284</td>
      <td>77.027251</td>
      <td>79.158768</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">Johnson High School</th>
      <th>10th</th>
      <td>32467.993480</td>
      <td>80.773431</td>
      <td>76.691117</td>
      <td>78.732274</td>
    </tr>
    <tr>
      <th>11th</th>
      <td>32378.549249</td>
      <td>80.616027</td>
      <td>77.491653</td>
      <td>79.053840</td>
    </tr>
    <tr>
      <th>12th</th>
      <td>32414.657051</td>
      <td>81.227564</td>
      <td>76.863248</td>
      <td>79.045406</td>
    </tr>
    <tr>
      <th>9th</th>
      <td>32399.975714</td>
      <td>81.260714</td>
      <td>77.187857</td>
      <td>79.224286</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">Pena High School</th>
      <th>10th</th>
      <td>23769.208000</td>
      <td>83.612000</td>
      <td>83.372000</td>
      <td>83.492000</td>
    </tr>
    <tr>
      <th>11th</th>
      <td>23742.605469</td>
      <td>84.335938</td>
      <td>84.328125</td>
      <td>84.332031</td>
    </tr>
    <tr>
      <th>12th</th>
      <td>23733.342541</td>
      <td>84.591160</td>
      <td>84.121547</td>
      <td>84.356354</td>
    </tr>
    <tr>
      <th>9th</th>
      <td>23766.127273</td>
      <td>83.807273</td>
      <td>83.625455</td>
      <td>83.716364</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">Rodriguez High School</th>
      <th>10th</th>
      <td>28050.171154</td>
      <td>80.629808</td>
      <td>76.612500</td>
      <td>78.621154</td>
    </tr>
    <tr>
      <th>11th</th>
      <td>28048.515905</td>
      <td>80.864811</td>
      <td>76.395626</td>
      <td>78.630219</td>
    </tr>
    <tr>
      <th>12th</th>
      <td>28023.722433</td>
      <td>80.376426</td>
      <td>77.690748</td>
      <td>79.033587</td>
    </tr>
    <tr>
      <th>9th</th>
      <td>28017.408076</td>
      <td>80.993127</td>
      <td>76.859966</td>
      <td>78.926546</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">Shelton High School</th>
      <th>10th</th>
      <td>6748.301339</td>
      <td>83.441964</td>
      <td>82.917411</td>
      <td>83.179688</td>
    </tr>
    <tr>
      <th>11th</th>
      <td>6742.453883</td>
      <td>84.373786</td>
      <td>83.383495</td>
      <td>83.878641</td>
    </tr>
    <tr>
      <th>12th</th>
      <td>6740.566038</td>
      <td>82.781671</td>
      <td>83.778976</td>
      <td>83.280323</td>
    </tr>
    <tr>
      <th>9th</th>
      <td>6750.615094</td>
      <td>84.122642</td>
      <td>83.420755</td>
      <td>83.771698</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">Thomas High School</th>
      <th>10th</th>
      <td>38346.368171</td>
      <td>84.254157</td>
      <td>83.087886</td>
      <td>83.671021</td>
    </tr>
    <tr>
      <th>11th</th>
      <td>38345.636145</td>
      <td>83.585542</td>
      <td>83.498795</td>
      <td>83.542169</td>
    </tr>
    <tr>
      <th>12th</th>
      <td>38360.289941</td>
      <td>83.831361</td>
      <td>83.497041</td>
      <td>83.664201</td>
    </tr>
    <tr>
      <th>9th</th>
      <td>38356.793926</td>
      <td>83.728850</td>
      <td>83.590022</td>
      <td>83.659436</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">Wilson High School</th>
      <th>10th</th>
      <td>14884.930693</td>
      <td>84.021452</td>
      <td>83.724422</td>
      <td>83.872937</td>
    </tr>
    <tr>
      <th>11th</th>
      <td>14855.539232</td>
      <td>83.764608</td>
      <td>83.195326</td>
      <td>83.479967</td>
    </tr>
    <tr>
      <th>12th</th>
      <td>14860.597315</td>
      <td>84.317673</td>
      <td>83.035794</td>
      <td>83.676734</td>
    </tr>
    <tr>
      <th>9th</th>
      <td>14879.667195</td>
      <td>83.939778</td>
      <td>83.085578</td>
      <td>83.512678</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">Wright High School</th>
      <th>10th</th>
      <td>25122.296296</td>
      <td>83.812757</td>
      <td>84.010288</td>
      <td>83.911523</td>
    </tr>
    <tr>
      <th>11th</th>
      <td>25147.331034</td>
      <td>84.156322</td>
      <td>83.836782</td>
      <td>83.996552</td>
    </tr>
    <tr>
      <th>12th</th>
      <td>25115.626016</td>
      <td>84.073171</td>
      <td>83.644986</td>
      <td>83.859079</td>
    </tr>
    <tr>
      <th>9th</th>
      <td>25152.370588</td>
      <td>83.833333</td>
      <td>83.264706</td>
      <td>83.549020</td>
    </tr>
  </tbody>
</table>
</div>




```python
#sort schools by highest passing rate
groupedv2 = students_df.groupby('school').mean().reset_index()
groupedv2.sort_values('total_score', ascending=False)

groupedv2.head(5)
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>school</th>
      <th>Student ID</th>
      <th>reading_score</th>
      <th>math_score</th>
      <th>total_score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Bailey High School</td>
      <td>20358.5</td>
      <td>81.033963</td>
      <td>77.048432</td>
      <td>79.041198</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Cabrera High School</td>
      <td>16941.5</td>
      <td>83.975780</td>
      <td>83.061895</td>
      <td>83.518837</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Figueroa High School</td>
      <td>4391.0</td>
      <td>81.158020</td>
      <td>76.711767</td>
      <td>78.934893</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Ford High School</td>
      <td>36165.0</td>
      <td>80.746258</td>
      <td>77.102592</td>
      <td>78.924425</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Griffin High School</td>
      <td>12995.5</td>
      <td>83.816757</td>
      <td>83.351499</td>
      <td>83.584128</td>
    </tr>
  </tbody>
</table>
</div>




```python
#sort schools by highest passing rate
groupedv2 = students_df.groupby('school').mean().reset_index()
groupedv2.sort_values('total_score', ascending=True)

groupedv2.head(5)
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>school</th>
      <th>Student ID</th>
      <th>reading_score</th>
      <th>math_score</th>
      <th>total_score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Bailey High School</td>
      <td>20358.5</td>
      <td>81.033963</td>
      <td>77.048432</td>
      <td>79.041198</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Cabrera High School</td>
      <td>16941.5</td>
      <td>83.975780</td>
      <td>83.061895</td>
      <td>83.518837</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Figueroa High School</td>
      <td>4391.0</td>
      <td>81.158020</td>
      <td>76.711767</td>
      <td>78.934893</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Ford High School</td>
      <td>36165.0</td>
      <td>80.746258</td>
      <td>77.102592</td>
      <td>78.924425</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Griffin High School</td>
      <td>12995.5</td>
      <td>83.816757</td>
      <td>83.351499</td>
      <td>83.584128</td>
    </tr>
  </tbody>
</table>
</div>




```python
schools_df["budget"].value_counts()
```




    1049400    1
    917500     1
    1884411    1
    3094650    1
    1056600    1
    248087     1
    1319574    1
    1763916    1
    1081356    1
    1910635    1
    3022020    1
    2547363    1
    585858     1
    1043130    1
    3124928    1
    Name: budget, dtype: int64




```python
#School Budget Bins
bins = [0, 1000000, 2000000, 3000000, 10000000]

# Create the names for the four bins
group_names = ['Low Budget', 'Moderate Less Budget', 'Moderate More Budget', 'High Spend']

# Cut budget and place the into bins
budget = pd.cut(schools_df["budget"], bins, labels=group_names)
budget
#join bin dataframe and schools_df
#schools_df.join(budget, how="outer")
```




    0     Moderate Less Budget
    1     Moderate Less Budget
    2     Moderate Less Budget
    3               High Spend
    4               Low Budget
    5     Moderate Less Budget
    6     Moderate Less Budget
    7               High Spend
    8               Low Budget
    9               Low Budget
    10    Moderate Less Budget
    11    Moderate More Budget
    12              High Spend
    13    Moderate Less Budget
    14    Moderate Less Budget
    Name: budget, dtype: category
    Categories (4, object): [Low Budget < Moderate Less Budget < Moderate More Budget < High Spend]




```python
#School Size Bins
bins = [0, 1000, 2500, 4000, 5000]

# Create the names for the four bins
group_names = ['Small', 'Small-ish', 'Medium', 'Large']

# Cut size and place the into bins
size = pd.cut(schools_df["size"], bins, labels=group_names)
size
#join bin dataframe and schools_df
#schools_df.join(size, how="outer")
```




    0        Medium
    1        Medium
    2     Small-ish
    3         Large
    4     Small-ish
    5     Small-ish
    6     Small-ish
    7         Large
    8         Small
    9         Small
    10    Small-ish
    11       Medium
    12        Large
    13       Medium
    14    Small-ish
    Name: size, dtype: category
    Categories (4, object): [Small < Small-ish < Medium < Large]




```python
#School Type Bins
bins = [0, 1000, 2500, 4000, 5000]

# Create the names for the four bins
group_names = ['Small', 'Small-ish', 'Medium', 'Large']

# Cut size and place the into bins
size = pd.cut(schools_df["size"], bins, labels=group_names)
size
#join bin dataframe and schools_df
#schools_df.join(size, how="outer")
```




    0        Medium
    1        Medium
    2     Small-ish
    3         Large
    4     Small-ish
    5     Small-ish
    6     Small-ish
    7         Large
    8         Small
    9         Small
    10    Small-ish
    11       Medium
    12        Large
    13       Medium
    14    Small-ish
    Name: size, dtype: category
    Categories (4, object): [Small < Small-ish < Medium < Large]




```python
#breakout scores by school type
```


```python
#Three sentences about trends
```
