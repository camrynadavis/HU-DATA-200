## Research Question

How do financial barriers and public school funding disparities contribute to the underrepresentation of Black and Hispanic youth in high-cost sports by limiting access to facilities, specialized sports training, injury management and scouting opportunities?

## Problem Statement

Sports specialization involves year-round training and competition, and requires costly investments towards participation, travel, and equipment fees, which creates significant finanicial barriers for youth from lower socioeconomic backgrounds. Aside from this, public school funding disparities can limit access to appropriate facilities, personnel, or physical education, which could further hinder sports participation opportunities for youth in lower SES communities. These disparities can contribute to underrepresentation of Black or Hispanic youth in sports with high financial barriers -- hockey, gymnastics, tennis, etc., while sports such as track and field are less expensive, and therefore more accessible.

### Potential Subtopics

- Correlation between public school funding and facility quality
- How racial identities or stereotypes can affect an athlete's sense of belonging in a specific sport
- Connection between SES and knowledge of sports injury education (ex. concussion education, safety protocols, etc.)

## Data Definition

<b>Public School Characteristics 2022-23</b>

Last Updated: October 21, 2024

https://catalog.data.gov/dataset/public-school-characteristics-2022-23-451db

The National Center for Education Statistics (NCES) gathers demographic and geographic data about U.S public schools and factors such as enrollment and Title I status. Further information consists of the percentage of students with free or reduced lunch eligibility. By researching both this dataset and the YRBSS, researchers could analyze patterns between students or schools with a lower SES and the rates of physical activity rates. 



### Additional Datasets of Interest

<b>Nutrition, Physical Activity, and Obesity - Youth Risk Behavior Surveillance System</b>

Last Updated: February 4, 2025

https://catalog.data.gov/dataset/nutrition-physical-activity-and-obesity-youth-risk-behavior-surveillance-system

Conducted by the Centers for Disease Control and Prevention (CDC), the Youth Risk Behavior Surveillance System (YRBSS) monitors health behaviors in middle and high school students nationwide. It collects data regarding physical activity and nutrition, along with geographic and socioeconomic factors. By collecting this data, it could be used to further research on the impact socioeconomic factors have on health behaviors.

## Data Collection


```python
import numpy as np                
import pandas as pd              
import matplotlib.pyplot as plt   
import seaborn as sns               

pd.set_option('display.max_rows', None)
pd.set_option('display.max_columns', None)

import warnings
warnings.filterwarnings('ignore')
```

### Read the Data


```python
path = pd.read_csv('Public_School_Characteristics_2022-23.csv')
psChar_23 = pd.DataFrame(path)
```


```python
psChar_23.head(7)
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
      <th>X</th>
      <th>Y</th>
      <th>OBJECTID</th>
      <th>NCESSCH</th>
      <th>SURVYEAR</th>
      <th>STABR</th>
      <th>LEAID</th>
      <th>ST_LEAID</th>
      <th>LEA_NAME</th>
      <th>SCH_NAME</th>
      <th>LSTREET1</th>
      <th>LSTREET2</th>
      <th>LCITY</th>
      <th>LSTATE</th>
      <th>LZIP</th>
      <th>LZIP4</th>
      <th>PHONE</th>
      <th>CHARTER_TEXT</th>
      <th>VIRTUAL</th>
      <th>GSLO</th>
      <th>GSHI</th>
      <th>SCHOOL_LEVEL</th>
      <th>STATUS</th>
      <th>SCHOOL_TYPE_TEXT</th>
      <th>SY_STATUS_TEXT</th>
      <th>ULOCALE</th>
      <th>NMCNTY</th>
      <th>TOTFRL</th>
      <th>FRELCH</th>
      <th>REDLCH</th>
      <th>DIRECTCERT</th>
      <th>PK</th>
      <th>KG</th>
      <th>G01</th>
      <th>G02</th>
      <th>G03</th>
      <th>G04</th>
      <th>G05</th>
      <th>G06</th>
      <th>G07</th>
      <th>G08</th>
      <th>G09</th>
      <th>G10</th>
      <th>G11</th>
      <th>G12</th>
      <th>G13</th>
      <th>UG</th>
      <th>AE</th>
      <th>TOTMENROL</th>
      <th>TOTFENROL</th>
      <th>TOTAL</th>
      <th>MEMBER</th>
      <th>FTE</th>
      <th>STUTERATIO</th>
      <th>AMALM</th>
      <th>AMALF</th>
      <th>AM</th>
      <th>ASALM</th>
      <th>ASALF</th>
      <th>AS</th>
      <th>BLALM</th>
      <th>BLALF</th>
      <th>BL</th>
      <th>HPALM</th>
      <th>HPALF</th>
      <th>HP</th>
      <th>HIALM</th>
      <th>HIALF</th>
      <th>HI</th>
      <th>TRALM</th>
      <th>TRALF</th>
      <th>TR</th>
      <th>WHALM</th>
      <th>WHALF</th>
      <th>WH</th>
      <th>LATCOD</th>
      <th>LONCOD</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-86.206200</td>
      <td>34.26020</td>
      <td>1</td>
      <td>10000500870</td>
      <td>2022-2023</td>
      <td>AL</td>
      <td>100005</td>
      <td>AL-101</td>
      <td>Albertville City</td>
      <td>Albertville Middle School</td>
      <td>600 E Alabama Ave</td>
      <td>NaN</td>
      <td>Albertville</td>
      <td>AL</td>
      <td>35950</td>
      <td></td>
      <td>(256)878-2341</td>
      <td>No</td>
      <td>Not Virtual</td>
      <td>07</td>
      <td>08</td>
      <td>Middle</td>
      <td>1</td>
      <td>Regular School</td>
      <td>Currently operational</td>
      <td>32-Town: Distant</td>
      <td>Marshall County</td>
      <td>697</td>
      <td>654</td>
      <td>43</td>
      <td>587</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>440.0</td>
      <td>450.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>459.0</td>
      <td>431.0</td>
      <td>890.0</td>
      <td>890.0</td>
      <td>45.000000</td>
      <td>19.78</td>
      <td>4.0</td>
      <td>1.0</td>
      <td>5.0</td>
      <td>4.0</td>
      <td>2.0</td>
      <td>6.0</td>
      <td>15.0</td>
      <td>14.0</td>
      <td>29.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>251.0</td>
      <td>251.0</td>
      <td>502.0</td>
      <td>17.0</td>
      <td>15.0</td>
      <td>32.0</td>
      <td>168.0</td>
      <td>147.0</td>
      <td>315.0</td>
      <td>34.26020</td>
      <td>-86.206200</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-86.204900</td>
      <td>34.26220</td>
      <td>2</td>
      <td>10000500871</td>
      <td>2022-2023</td>
      <td>AL</td>
      <td>100005</td>
      <td>AL-101</td>
      <td>Albertville City</td>
      <td>Albertville High School</td>
      <td>402 E McCord Ave</td>
      <td>NaN</td>
      <td>Albertville</td>
      <td>AL</td>
      <td>35950</td>
      <td>2322</td>
      <td>(256)894-5000</td>
      <td>No</td>
      <td>Not Virtual</td>
      <td>09</td>
      <td>12</td>
      <td>High</td>
      <td>1</td>
      <td>Regular School</td>
      <td>Currently operational</td>
      <td>32-Town: Distant</td>
      <td>Marshall County</td>
      <td>1254</td>
      <td>1178</td>
      <td>76</td>
      <td>1059</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>493.0</td>
      <td>442.0</td>
      <td>390.0</td>
      <td>387.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>868.0</td>
      <td>844.0</td>
      <td>1712.0</td>
      <td>1712.0</td>
      <td>85.199997</td>
      <td>20.09</td>
      <td>0.0</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>4.0</td>
      <td>5.0</td>
      <td>9.0</td>
      <td>23.0</td>
      <td>34.0</td>
      <td>57.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>490.0</td>
      <td>468.0</td>
      <td>958.0</td>
      <td>26.0</td>
      <td>19.0</td>
      <td>45.0</td>
      <td>325.0</td>
      <td>316.0</td>
      <td>641.0</td>
      <td>34.26220</td>
      <td>-86.204900</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-86.220100</td>
      <td>34.27330</td>
      <td>3</td>
      <td>10000500879</td>
      <td>2022-2023</td>
      <td>AL</td>
      <td>100005</td>
      <td>AL-101</td>
      <td>Albertville City</td>
      <td>Albertville Intermediate School</td>
      <td>901 W McKinney Ave</td>
      <td>NaN</td>
      <td>Albertville</td>
      <td>AL</td>
      <td>35950</td>
      <td>1300</td>
      <td>(256)878-7698</td>
      <td>No</td>
      <td>Not Virtual</td>
      <td>05</td>
      <td>06</td>
      <td>Middle</td>
      <td>1</td>
      <td>Regular School</td>
      <td>Currently operational</td>
      <td>32-Town: Distant</td>
      <td>Marshall County</td>
      <td>718</td>
      <td>665</td>
      <td>53</td>
      <td>570</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>412.0</td>
      <td>462.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>451.0</td>
      <td>423.0</td>
      <td>874.0</td>
      <td>874.0</td>
      <td>43.000000</td>
      <td>20.33</td>
      <td>1.0</td>
      <td>4.0</td>
      <td>5.0</td>
      <td>4.0</td>
      <td>0.0</td>
      <td>4.0</td>
      <td>22.0</td>
      <td>28.0</td>
      <td>50.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>263.0</td>
      <td>241.0</td>
      <td>504.0</td>
      <td>7.0</td>
      <td>6.0</td>
      <td>13.0</td>
      <td>154.0</td>
      <td>144.0</td>
      <td>298.0</td>
      <td>34.27330</td>
      <td>-86.220100</td>
    </tr>
    <tr>
      <th>3</th>
      <td>-86.221806</td>
      <td>34.25270</td>
      <td>4</td>
      <td>10000500889</td>
      <td>2022-2023</td>
      <td>AL</td>
      <td>100005</td>
      <td>AL-101</td>
      <td>Albertville City</td>
      <td>Albertville Elementary School</td>
      <td>145 West End Drive</td>
      <td>NaN</td>
      <td>Albertville</td>
      <td>AL</td>
      <td>35950</td>
      <td></td>
      <td>(256)894-4822</td>
      <td>No</td>
      <td>Not Virtual</td>
      <td>03</td>
      <td>04</td>
      <td>Elementary</td>
      <td>1</td>
      <td>Regular School</td>
      <td>Currently operational</td>
      <td>32-Town: Distant</td>
      <td>Marshall County</td>
      <td>723</td>
      <td>680</td>
      <td>43</td>
      <td>583</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>430.0</td>
      <td>444.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>463.0</td>
      <td>411.0</td>
      <td>874.0</td>
      <td>874.0</td>
      <td>43.000000</td>
      <td>20.33</td>
      <td>0.0</td>
      <td>4.0</td>
      <td>4.0</td>
      <td>1.0</td>
      <td>3.0</td>
      <td>4.0</td>
      <td>22.0</td>
      <td>16.0</td>
      <td>38.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>261.0</td>
      <td>236.0</td>
      <td>497.0</td>
      <td>11.0</td>
      <td>16.0</td>
      <td>27.0</td>
      <td>168.0</td>
      <td>136.0</td>
      <td>304.0</td>
      <td>34.25270</td>
      <td>-86.221806</td>
    </tr>
    <tr>
      <th>4</th>
      <td>-86.193300</td>
      <td>34.28980</td>
      <td>5</td>
      <td>10000501616</td>
      <td>2022-2023</td>
      <td>AL</td>
      <td>100005</td>
      <td>AL-101</td>
      <td>Albertville City</td>
      <td>Albertville Kindergarten and PreK</td>
      <td>257 Country Club Rd</td>
      <td>NaN</td>
      <td>Albertville</td>
      <td>AL</td>
      <td>35951</td>
      <td>3927</td>
      <td>(256)878-7922</td>
      <td>No</td>
      <td>Not Virtual</td>
      <td>PK</td>
      <td>KG</td>
      <td>Elementary</td>
      <td>1</td>
      <td>Regular School</td>
      <td>Currently operational</td>
      <td>32-Town: Distant</td>
      <td>Marshall County</td>
      <td>392</td>
      <td>367</td>
      <td>25</td>
      <td>240</td>
      <td>133.0</td>
      <td>473.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>304.0</td>
      <td>302.0</td>
      <td>606.0</td>
      <td>606.0</td>
      <td>26.000000</td>
      <td>23.31</td>
      <td>1.0</td>
      <td>3.0</td>
      <td>4.0</td>
      <td>2.0</td>
      <td>0.0</td>
      <td>2.0</td>
      <td>26.0</td>
      <td>23.0</td>
      <td>49.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>167.0</td>
      <td>152.0</td>
      <td>319.0</td>
      <td>4.0</td>
      <td>4.0</td>
      <td>8.0</td>
      <td>104.0</td>
      <td>120.0</td>
      <td>224.0</td>
      <td>34.28980</td>
      <td>-86.193300</td>
    </tr>
    <tr>
      <th>5</th>
      <td>-86.221800</td>
      <td>34.25330</td>
      <td>6</td>
      <td>10000502150</td>
      <td>2022-2023</td>
      <td>AL</td>
      <td>100005</td>
      <td>AL-101</td>
      <td>Albertville City</td>
      <td>Albertville Primary School</td>
      <td>1100 Horton Rd</td>
      <td>NaN</td>
      <td>Albertville</td>
      <td>AL</td>
      <td>35950</td>
      <td>2532</td>
      <td>(256)878-6611</td>
      <td>No</td>
      <td>Not Virtual</td>
      <td>01</td>
      <td>02</td>
      <td>Elementary</td>
      <td>1</td>
      <td>Regular School</td>
      <td>Currently operational</td>
      <td>32-Town: Distant</td>
      <td>Marshall County</td>
      <td>779</td>
      <td>726</td>
      <td>53</td>
      <td>617</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>427.0</td>
      <td>517.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>498.0</td>
      <td>446.0</td>
      <td>944.0</td>
      <td>944.0</td>
      <td>61.000000</td>
      <td>15.48</td>
      <td>9.0</td>
      <td>1.0</td>
      <td>10.0</td>
      <td>3.0</td>
      <td>0.0</td>
      <td>3.0</td>
      <td>24.0</td>
      <td>21.0</td>
      <td>45.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>290.0</td>
      <td>256.0</td>
      <td>546.0</td>
      <td>9.0</td>
      <td>10.0</td>
      <td>19.0</td>
      <td>163.0</td>
      <td>157.0</td>
      <td>320.0</td>
      <td>34.25330</td>
      <td>-86.221800</td>
    </tr>
    <tr>
      <th>6</th>
      <td>-86.254153</td>
      <td>34.53375</td>
      <td>7</td>
      <td>10000600193</td>
      <td>2022-2023</td>
      <td>AL</td>
      <td>100006</td>
      <td>AL-048</td>
      <td>Marshall County</td>
      <td>Kate Duncan Smith DAR Middle</td>
      <td>6077 Main St</td>
      <td>NaN</td>
      <td>Grant</td>
      <td>AL</td>
      <td>35747</td>
      <td></td>
      <td>(256)728-5950</td>
      <td>No</td>
      <td>Not Virtual</td>
      <td>05</td>
      <td>08</td>
      <td>Middle</td>
      <td>1</td>
      <td>Regular School</td>
      <td>Currently operational</td>
      <td>42-Rural: Distant</td>
      <td>Marshall County</td>
      <td>151</td>
      <td>123</td>
      <td>28</td>
      <td>194</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>95.0</td>
      <td>97.0</td>
      <td>86.0</td>
      <td>86.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>192.0</td>
      <td>172.0</td>
      <td>364.0</td>
      <td>364.0</td>
      <td>22.030001</td>
      <td>16.52</td>
      <td>1.0</td>
      <td>3.0</td>
      <td>4.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>2.0</td>
      <td>0.0</td>
      <td>2.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>6.0</td>
      <td>8.0</td>
      <td>14.0</td>
      <td>5.0</td>
      <td>9.0</td>
      <td>14.0</td>
      <td>178.0</td>
      <td>152.0</td>
      <td>330.0</td>
      <td>34.53375</td>
      <td>-86.254153</td>
    </tr>
  </tbody>
</table>
</div>




```python
psChar_23.tail(7)
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
      <th>X</th>
      <th>Y</th>
      <th>OBJECTID</th>
      <th>NCESSCH</th>
      <th>SURVYEAR</th>
      <th>STABR</th>
      <th>LEAID</th>
      <th>ST_LEAID</th>
      <th>LEA_NAME</th>
      <th>SCH_NAME</th>
      <th>LSTREET1</th>
      <th>LSTREET2</th>
      <th>LCITY</th>
      <th>LSTATE</th>
      <th>LZIP</th>
      <th>LZIP4</th>
      <th>PHONE</th>
      <th>CHARTER_TEXT</th>
      <th>VIRTUAL</th>
      <th>GSLO</th>
      <th>GSHI</th>
      <th>SCHOOL_LEVEL</th>
      <th>STATUS</th>
      <th>SCHOOL_TYPE_TEXT</th>
      <th>SY_STATUS_TEXT</th>
      <th>ULOCALE</th>
      <th>NMCNTY</th>
      <th>TOTFRL</th>
      <th>FRELCH</th>
      <th>REDLCH</th>
      <th>DIRECTCERT</th>
      <th>PK</th>
      <th>KG</th>
      <th>G01</th>
      <th>G02</th>
      <th>G03</th>
      <th>G04</th>
      <th>G05</th>
      <th>G06</th>
      <th>G07</th>
      <th>G08</th>
      <th>G09</th>
      <th>G10</th>
      <th>G11</th>
      <th>G12</th>
      <th>G13</th>
      <th>UG</th>
      <th>AE</th>
      <th>TOTMENROL</th>
      <th>TOTFENROL</th>
      <th>TOTAL</th>
      <th>MEMBER</th>
      <th>FTE</th>
      <th>STUTERATIO</th>
      <th>AMALM</th>
      <th>AMALF</th>
      <th>AM</th>
      <th>ASALM</th>
      <th>ASALF</th>
      <th>AS</th>
      <th>BLALM</th>
      <th>BLALF</th>
      <th>BL</th>
      <th>HPALM</th>
      <th>HPALF</th>
      <th>HP</th>
      <th>HIALM</th>
      <th>HIALF</th>
      <th>HI</th>
      <th>TRALM</th>
      <th>TRALF</th>
      <th>TR</th>
      <th>WHALM</th>
      <th>WHALF</th>
      <th>WH</th>
      <th>LATCOD</th>
      <th>LONCOD</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>101383</th>
      <td>-64.932456</td>
      <td>18.352146</td>
      <td>101384</td>
      <td>780003000020</td>
      <td>2022-2023</td>
      <td>VI</td>
      <td>7800030</td>
      <td>VI-001</td>
      <td>Saint Thomas - Saint John School District</td>
      <td>JOSEPH SIBILLY ELEMENTARY SCHOOL</td>
      <td>14  15  16 ESTATE ELIZABETH</td>
      <td>NaN</td>
      <td>Saint Thomas</td>
      <td>VI</td>
      <td>802</td>
      <td></td>
      <td>(340)774-7001</td>
      <td>N</td>
      <td>Not Virtual</td>
      <td>PK</td>
      <td>06</td>
      <td>Elementary</td>
      <td>1</td>
      <td>Regular School</td>
      <td>Currently operational</td>
      <td>33-Town: Remote</td>
      <td>St. Thomas Island</td>
      <td>228</td>
      <td>228</td>
      <td>0</td>
      <td>-1</td>
      <td>19.0</td>
      <td>25.0</td>
      <td>25.0</td>
      <td>25.0</td>
      <td>31.0</td>
      <td>34.0</td>
      <td>34.0</td>
      <td>38.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>121.0</td>
      <td>110.0</td>
      <td>231.0</td>
      <td>231.0</td>
      <td>16.0</td>
      <td>14.44</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>4.0</td>
      <td>99.0</td>
      <td>93.0</td>
      <td>192.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>8.0</td>
      <td>5.0</td>
      <td>13.0</td>
      <td>2.0</td>
      <td>1.0</td>
      <td>3.0</td>
      <td>10.0</td>
      <td>9.0</td>
      <td>19.0</td>
      <td>18.352146</td>
      <td>-64.932456</td>
    </tr>
    <tr>
      <th>101384</th>
      <td>-64.793916</td>
      <td>18.330464</td>
      <td>101385</td>
      <td>780003000022</td>
      <td>2022-2023</td>
      <td>VI</td>
      <td>7800030</td>
      <td>VI-001</td>
      <td>Saint Thomas - Saint John School District</td>
      <td>JULIUS E SPRAUVE</td>
      <td>14 18 ESTATE ENIGHED</td>
      <td>NaN</td>
      <td>Saint John</td>
      <td>VI</td>
      <td>831</td>
      <td></td>
      <td>(340)776-6336</td>
      <td>N</td>
      <td>Not Virtual</td>
      <td>PK</td>
      <td>08</td>
      <td>Elementary</td>
      <td>1</td>
      <td>Regular School</td>
      <td>Currently operational</td>
      <td>33-Town: Remote</td>
      <td>St. John Island</td>
      <td>199</td>
      <td>199</td>
      <td>0</td>
      <td>-1</td>
      <td>8.0</td>
      <td>21.0</td>
      <td>16.0</td>
      <td>21.0</td>
      <td>14.0</td>
      <td>24.0</td>
      <td>20.0</td>
      <td>26.0</td>
      <td>27.0</td>
      <td>25.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>103.0</td>
      <td>99.0</td>
      <td>202.0</td>
      <td>202.0</td>
      <td>20.0</td>
      <td>10.10</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>79.0</td>
      <td>68.0</td>
      <td>147.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>22.0</td>
      <td>29.0</td>
      <td>51.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>2.0</td>
      <td>3.0</td>
      <td>18.330464</td>
      <td>-64.793916</td>
    </tr>
    <tr>
      <th>101385</th>
      <td>-64.917602</td>
      <td>18.341950</td>
      <td>101386</td>
      <td>780003000024</td>
      <td>2022-2023</td>
      <td>VI</td>
      <td>7800030</td>
      <td>VI-001</td>
      <td>Saint Thomas - Saint John School District</td>
      <td>LOCKHART ELEMENTARY SCHOOL</td>
      <td>41 ESTATE THOMAS</td>
      <td>NaN</td>
      <td>Saint Thomas</td>
      <td>VI</td>
      <td>802</td>
      <td></td>
      <td>(340)775-0820</td>
      <td>N</td>
      <td>Not Virtual</td>
      <td>KG</td>
      <td>03</td>
      <td>Elementary</td>
      <td>1</td>
      <td>Regular School</td>
      <td>Currently operational</td>
      <td>33-Town: Remote</td>
      <td>St. Thomas Island</td>
      <td>295</td>
      <td>295</td>
      <td>0</td>
      <td>-1</td>
      <td>NaN</td>
      <td>77.0</td>
      <td>75.0</td>
      <td>69.0</td>
      <td>77.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>171.0</td>
      <td>127.0</td>
      <td>298.0</td>
      <td>298.0</td>
      <td>18.0</td>
      <td>16.56</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>4.0</td>
      <td>3.0</td>
      <td>7.0</td>
      <td>132.0</td>
      <td>92.0</td>
      <td>224.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>33.0</td>
      <td>30.0</td>
      <td>63.0</td>
      <td>1.0</td>
      <td>2.0</td>
      <td>3.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>18.341950</td>
      <td>-64.917602</td>
    </tr>
    <tr>
      <th>101386</th>
      <td>-64.952483</td>
      <td>18.338742</td>
      <td>101387</td>
      <td>780003000026</td>
      <td>2022-2023</td>
      <td>VI</td>
      <td>7800030</td>
      <td>VI-001</td>
      <td>Saint Thomas - Saint John School District</td>
      <td>ULLA F MULLER ELEMENTARY SCHOOL</td>
      <td>7B ESTATE CONTANT</td>
      <td>NaN</td>
      <td>Saint Thomas</td>
      <td>VI</td>
      <td>802</td>
      <td></td>
      <td>(340)774-0059</td>
      <td>N</td>
      <td>Not Virtual</td>
      <td>KG</td>
      <td>06</td>
      <td>Elementary</td>
      <td>1</td>
      <td>Regular School</td>
      <td>Currently operational</td>
      <td>33-Town: Remote</td>
      <td>St. Thomas Island</td>
      <td>417</td>
      <td>417</td>
      <td>0</td>
      <td>-1</td>
      <td>NaN</td>
      <td>52.0</td>
      <td>53.0</td>
      <td>51.0</td>
      <td>47.0</td>
      <td>70.0</td>
      <td>79.0</td>
      <td>68.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>200.0</td>
      <td>220.0</td>
      <td>420.0</td>
      <td>420.0</td>
      <td>28.0</td>
      <td>15.00</td>
      <td>0.0</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>4.0</td>
      <td>6.0</td>
      <td>167.0</td>
      <td>182.0</td>
      <td>349.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>27.0</td>
      <td>27.0</td>
      <td>54.0</td>
      <td>2.0</td>
      <td>0.0</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>5.0</td>
      <td>7.0</td>
      <td>18.338742</td>
      <td>-64.952483</td>
    </tr>
    <tr>
      <th>101387</th>
      <td>-64.899024</td>
      <td>18.354782</td>
      <td>101388</td>
      <td>780003000027</td>
      <td>2022-2023</td>
      <td>VI</td>
      <td>7800030</td>
      <td>VI-001</td>
      <td>Saint Thomas - Saint John School District</td>
      <td>YVONNE BOWSKY ELEMENTARY SCHOOL</td>
      <td>15B and 16 ESTATE MANDAHL</td>
      <td>NaN</td>
      <td>Saint Thomas</td>
      <td>VI</td>
      <td>802</td>
      <td></td>
      <td>(340)775-3220</td>
      <td>N</td>
      <td>Not Virtual</td>
      <td>PK</td>
      <td>05</td>
      <td>Elementary</td>
      <td>1</td>
      <td>Regular School</td>
      <td>Currently operational</td>
      <td>33-Town: Remote</td>
      <td>St. Thomas Island</td>
      <td>425</td>
      <td>425</td>
      <td>0</td>
      <td>-1</td>
      <td>22.0</td>
      <td>62.0</td>
      <td>67.0</td>
      <td>66.0</td>
      <td>75.0</td>
      <td>68.0</td>
      <td>68.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>252.0</td>
      <td>176.0</td>
      <td>428.0</td>
      <td>428.0</td>
      <td>34.0</td>
      <td>12.59</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>2.0</td>
      <td>5.0</td>
      <td>4.0</td>
      <td>9.0</td>
      <td>201.0</td>
      <td>144.0</td>
      <td>345.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>37.0</td>
      <td>22.0</td>
      <td>59.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>8.0</td>
      <td>4.0</td>
      <td>12.0</td>
      <td>18.354782</td>
      <td>-64.899024</td>
    </tr>
    <tr>
      <th>101388</th>
      <td>-64.945940</td>
      <td>18.336658</td>
      <td>101389</td>
      <td>780003000033</td>
      <td>2022-2023</td>
      <td>VI</td>
      <td>7800030</td>
      <td>VI-001</td>
      <td>Saint Thomas - Saint John School District</td>
      <td>CANCRYN JUNIOR HIGH SCHOOL</td>
      <td>1 CROWN BAY</td>
      <td>NaN</td>
      <td>Saint Thomas</td>
      <td>VI</td>
      <td>804</td>
      <td></td>
      <td>(340)774-4540</td>
      <td>N</td>
      <td>Not Virtual</td>
      <td>04</td>
      <td>08</td>
      <td>Middle</td>
      <td>1</td>
      <td>Regular School</td>
      <td>Currently operational</td>
      <td>33-Town: Remote</td>
      <td>St. Thomas Island</td>
      <td>683</td>
      <td>683</td>
      <td>0</td>
      <td>-1</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>77.0</td>
      <td>119.0</td>
      <td>96.0</td>
      <td>189.0</td>
      <td>205.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>361.0</td>
      <td>325.0</td>
      <td>686.0</td>
      <td>686.0</td>
      <td>62.0</td>
      <td>11.06</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>4.0</td>
      <td>279.0</td>
      <td>250.0</td>
      <td>529.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>74.0</td>
      <td>62.0</td>
      <td>136.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>6.0</td>
      <td>10.0</td>
      <td>16.0</td>
      <td>18.336658</td>
      <td>-64.945940</td>
    </tr>
    <tr>
      <th>101389</th>
      <td>-64.890311</td>
      <td>18.318230</td>
      <td>101390</td>
      <td>780003000034</td>
      <td>2022-2023</td>
      <td>VI</td>
      <td>7800030</td>
      <td>VI-001</td>
      <td>Saint Thomas - Saint John School District</td>
      <td>BERTHA BOSCHULTE JUNIOR HIGH</td>
      <td>9 1 and 12A BOVONI</td>
      <td>NaN</td>
      <td>Saint Thomas</td>
      <td>VI</td>
      <td>802</td>
      <td></td>
      <td>(340)775-4222</td>
      <td>N</td>
      <td>Not Virtual</td>
      <td>06</td>
      <td>08</td>
      <td>Middle</td>
      <td>1</td>
      <td>Regular School</td>
      <td>Currently operational</td>
      <td>33-Town: Remote</td>
      <td>St. Thomas Island</td>
      <td>504</td>
      <td>504</td>
      <td>0</td>
      <td>-1</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>145.0</td>
      <td>169.0</td>
      <td>193.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>279.0</td>
      <td>228.0</td>
      <td>507.0</td>
      <td>507.0</td>
      <td>49.0</td>
      <td>10.35</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>2.0</td>
      <td>1.0</td>
      <td>3.0</td>
      <td>250.0</td>
      <td>204.0</td>
      <td>454.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>27.0</td>
      <td>21.0</td>
      <td>48.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>18.318230</td>
      <td>-64.890311</td>
    </tr>
  </tbody>
</table>
</div>




```python
psChar_23.shape
```




    (101390, 77)



- The dataframe has 101,390 rows of data.
- The dataframe has 68 columns or features.
- There are 6,894,520 total datapoints observed in the dataset.


```python
psChar_23.info(show_counts=True, verbose=True)
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 101390 entries, 0 to 101389
    Data columns (total 77 columns):
     #   Column            Non-Null Count   Dtype  
    ---  ------            --------------   -----  
     0   X                 101390 non-null  float64
     1   Y                 101390 non-null  float64
     2   OBJECTID          101390 non-null  int64  
     3   NCESSCH           101390 non-null  int64  
     4   SURVYEAR          101390 non-null  object 
     5   STABR             101390 non-null  object 
     6   LEAID             101390 non-null  int64  
     7   ST_LEAID          101390 non-null  object 
     8   LEA_NAME          101390 non-null  object 
     9   SCH_NAME          101390 non-null  object 
     10  LSTREET1          101389 non-null  object 
     11  LSTREET2          572 non-null     object 
     12  LCITY             101390 non-null  object 
     13  LSTATE            101390 non-null  object 
     14  LZIP              101390 non-null  int64  
     15  LZIP4             101390 non-null  object 
     16  PHONE             101390 non-null  object 
     17  CHARTER_TEXT      101390 non-null  object 
     18  VIRTUAL           101390 non-null  object 
     19  GSLO              101390 non-null  object 
     20  GSHI              101390 non-null  object 
     21  SCHOOL_LEVEL      101390 non-null  object 
     22  STATUS            101390 non-null  int64  
     23  SCHOOL_TYPE_TEXT  101390 non-null  object 
     24  SY_STATUS_TEXT    101390 non-null  object 
     25  ULOCALE           101390 non-null  object 
     26  NMCNTY            101390 non-null  object 
     27  TOTFRL            101390 non-null  int64  
     28  FRELCH            101390 non-null  int64  
     29  REDLCH            101390 non-null  int64  
     30  DIRECTCERT        101390 non-null  int64  
     31  PK                32392 non-null   float64
     32  KG                54061 non-null   float64
     33  G01               54412 non-null   float64
     34  G02               54469 non-null   float64
     35  G03               54459 non-null   float64
     36  G04               54258 non-null   float64
     37  G05               53014 non-null   float64
     38  G06               38023 non-null   float64
     39  G07               33224 non-null   float64
     40  G08               33492 non-null   float64
     41  G09               28101 non-null   float64
     42  G10               27889 non-null   float64
     43  G11               27888 non-null   float64
     44  G12               27816 non-null   float64
     45  G13               133 non-null     float64
     46  UG                7889 non-null    float64
     47  AE                183 non-null     float64
     48  TOTMENROL         98910 non-null   float64
     49  TOTFENROL         98910 non-null   float64
     50  TOTAL             99719 non-null   float64
     51  MEMBER            99719 non-null   float64
     52  FTE               97537 non-null   float64
     53  STUTERATIO        99576 non-null   float64
     54  AMALM             98809 non-null   float64
     55  AMALF             98811 non-null   float64
     56  AM                98857 non-null   float64
     57  ASALM             98898 non-null   float64
     58  ASALF             98900 non-null   float64
     59  AS                98906 non-null   float64
     60  BLALM             98896 non-null   float64
     61  BLALF             98893 non-null   float64
     62  BL                98903 non-null   float64
     63  HPALM             98782 non-null   float64
     64  HPALF             98783 non-null   float64
     65  HP                98829 non-null   float64
     66  HIALM             98909 non-null   float64
     67  HIALF             98910 non-null   float64
     68  HI                98910 non-null   float64
     69  TRALM             98903 non-null   float64
     70  TRALF             98905 non-null   float64
     71  TR                98906 non-null   float64
     72  WHALM             98909 non-null   float64
     73  WHALF             98909 non-null   float64
     74  WH                98910 non-null   float64
     75  LATCOD            101390 non-null  float64
     76  LONCOD            101390 non-null  float64
    dtypes: float64(48), int64(9), object(20)
    memory usage: 59.6+ MB



```python
ps23Cols = psChar_23.columns
ps23Cols
```




    Index(['X', 'Y', 'OBJECTID', 'NCESSCH', 'SURVYEAR', 'STABR', 'LEAID',
           'ST_LEAID', 'LEA_NAME', 'SCH_NAME', 'LSTREET1', 'LSTREET2', 'LCITY',
           'LSTATE', 'LZIP', 'LZIP4', 'PHONE', 'CHARTER_TEXT', 'VIRTUAL', 'GSLO',
           'GSHI', 'SCHOOL_LEVEL', 'STATUS', 'SCHOOL_TYPE_TEXT', 'SY_STATUS_TEXT',
           'ULOCALE', 'NMCNTY', 'TOTFRL', 'FRELCH', 'REDLCH', 'DIRECTCERT', 'PK',
           'KG', 'G01', 'G02', 'G03', 'G04', 'G05', 'G06', 'G07', 'G08', 'G09',
           'G10', 'G11', 'G12', 'G13', 'UG', 'AE', 'TOTMENROL', 'TOTFENROL',
           'TOTAL', 'MEMBER', 'FTE', 'STUTERATIO', 'AMALM', 'AMALF', 'AM', 'ASALM',
           'ASALF', 'AS', 'BLALM', 'BLALF', 'BL', 'HPALM', 'HPALF', 'HP', 'HIALM',
           'HIALF', 'HI', 'TRALM', 'TRALF', 'TR', 'WHALM', 'WHALF', 'WH', 'LATCOD',
           'LONCOD'],
          dtype='object')




```python
psChar_23 = psChar_23.rename(columns = {'OBJECTID':'ObjectID','NCESSCH':'NCESID','SURVYEAR':'SurveyYear', 
                                        'STABR':'StateABR','LEA_NAME':'LEAname','SCH_NAME':'SchoolName', 
                                        'LSTREET1':'Street1','LSTREET2':'Street2','LCITY':'City',
                                        'LSTATE':'State','LZIP':'Zip','LZIP4':'Zip4', 
                                        'PHONE':'Phone', 'CHARTER_TEXT':'Charter', 'VIRTUAL':'Virtual', 
                                        'GSLO':'LowestGrade','GSHI':'HighestGrade', 
                                        'SCHOOL_LEVEL':'SchoolLevel', 
                                        'STATUS':'Status', 'SCHOOL_TYPE_TEXT':'SchoolType', 
                                        'SY_STATUS_TEXT':'Status_Text',
                                        'ULOCALE':'Locale', 'NMCNTY':'County', 
                                        'TOTFRL':'TotalFreeLunch', 
                                        'FRELCH':'FreeLunch', 'REDLCH':'ReducedLunch', 
                                        'DIRECTCERT':'MealProgramCertified', 'PK':'PreK',
                                        'KG':'Kindergarten', 'G01':'Grade1', 'G02':'Grade2', 
                                        'G03':'Grade3', 'G04':'Grade4', 'G05':'Grade5', 
                                        'G06':'Grade6', 'G07':'Grade7', 'G08':'Grade8', 
                                        'G09':'Grade9','G10':'Grade10', 'G11':'Grade11', 
                                        'G12':'Grade12','G13':'Grade13', 'UG':'Ungraded', 
                                        'AE':'AdultEd', 'TOTMENROL':'TotMaleEnrollment', 
                                        'TOTFENROL':'TotFemaleEnrollment','TOTAL':'TotalEnrollment', 
                                        'MEMBER':'Member', 'FTE':'StaffFTE', 'STUTERATIO':'StudentTeacherRatio', 
                                        'AMALM':'AIANMale','AMALF':'AIANFem', 'AM':'AIANTotal', 
                                        'ASALM':'AsianMale', 'ASALF':'AsianFemale', 'AS':'AsianTotal', 
                                        'BLALM':'BlackMale','BLALF':'BlackFemale', 'BL':'BlackTotal', 
                                        'HPALM':'HPIMale', 'HPALF':'HPIFemale', 'HP':'HPITotal', 
                                        'HIALM':'HispanicMale','HIALF':'HispanicFemale', 'HI':'HispanicTotal', 
                                        'TRALM':'TRMale', 'TRALF':'TRFemale', 'TR':'TRTotal', 
                                        'WHALM':'WhiteMale','WHALF':'WhiteFemale', 'WH':'WhiteTotal', 
                                        'LATCOD':'Latitude','LONCOD':'Longitude'})

ps23Cols = psChar_23.columns
psChar_23.head()
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
      <th>X</th>
      <th>Y</th>
      <th>ObjectID</th>
      <th>NCESID</th>
      <th>SurveyYear</th>
      <th>StateABR</th>
      <th>LEAID</th>
      <th>ST_LEAID</th>
      <th>LEAname</th>
      <th>SchoolName</th>
      <th>Street1</th>
      <th>Street2</th>
      <th>City</th>
      <th>State</th>
      <th>Zip</th>
      <th>Zip4</th>
      <th>Phone</th>
      <th>Charter</th>
      <th>Virtual</th>
      <th>LowestGrade</th>
      <th>HighestGrade</th>
      <th>SchoolLevel</th>
      <th>Status</th>
      <th>SchoolType</th>
      <th>Status_Text</th>
      <th>Locale</th>
      <th>County</th>
      <th>TotalFreeLunch</th>
      <th>FreeLunch</th>
      <th>ReducedLunch</th>
      <th>MealProgramCertified</th>
      <th>PreK</th>
      <th>Kindergarten</th>
      <th>Grade1</th>
      <th>Grade2</th>
      <th>Grade3</th>
      <th>Grade4</th>
      <th>Grade5</th>
      <th>Grade6</th>
      <th>Grade7</th>
      <th>Grade8</th>
      <th>Grade9</th>
      <th>Grade10</th>
      <th>Grade11</th>
      <th>Grade12</th>
      <th>Grade13</th>
      <th>Ungraded</th>
      <th>AdultEd</th>
      <th>TotMaleEnrollment</th>
      <th>TotFemaleEnrollment</th>
      <th>TotalEnrollment</th>
      <th>Member</th>
      <th>StaffFTE</th>
      <th>StudentTeacherRatio</th>
      <th>AIANMale</th>
      <th>AIANFem</th>
      <th>AIANTotal</th>
      <th>AsianMale</th>
      <th>AsianFemale</th>
      <th>AsianTotal</th>
      <th>BlackMale</th>
      <th>BlackFemale</th>
      <th>BlackTotal</th>
      <th>HPIMale</th>
      <th>HPIFemale</th>
      <th>HPITotal</th>
      <th>HispanicMale</th>
      <th>HispanicFemale</th>
      <th>HispanicTotal</th>
      <th>TRMale</th>
      <th>TRFemale</th>
      <th>TRTotal</th>
      <th>WhiteMale</th>
      <th>WhiteFemale</th>
      <th>WhiteTotal</th>
      <th>Latitude</th>
      <th>Longitude</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-86.206200</td>
      <td>34.2602</td>
      <td>1</td>
      <td>10000500870</td>
      <td>2022-2023</td>
      <td>AL</td>
      <td>100005</td>
      <td>AL-101</td>
      <td>Albertville City</td>
      <td>Albertville Middle School</td>
      <td>600 E Alabama Ave</td>
      <td>NaN</td>
      <td>Albertville</td>
      <td>AL</td>
      <td>35950</td>
      <td></td>
      <td>(256)878-2341</td>
      <td>No</td>
      <td>Not Virtual</td>
      <td>07</td>
      <td>08</td>
      <td>Middle</td>
      <td>1</td>
      <td>Regular School</td>
      <td>Currently operational</td>
      <td>32-Town: Distant</td>
      <td>Marshall County</td>
      <td>697</td>
      <td>654</td>
      <td>43</td>
      <td>587</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>440.0</td>
      <td>450.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>459.0</td>
      <td>431.0</td>
      <td>890.0</td>
      <td>890.0</td>
      <td>45.000000</td>
      <td>19.78</td>
      <td>4.0</td>
      <td>1.0</td>
      <td>5.0</td>
      <td>4.0</td>
      <td>2.0</td>
      <td>6.0</td>
      <td>15.0</td>
      <td>14.0</td>
      <td>29.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>251.0</td>
      <td>251.0</td>
      <td>502.0</td>
      <td>17.0</td>
      <td>15.0</td>
      <td>32.0</td>
      <td>168.0</td>
      <td>147.0</td>
      <td>315.0</td>
      <td>34.2602</td>
      <td>-86.206200</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-86.204900</td>
      <td>34.2622</td>
      <td>2</td>
      <td>10000500871</td>
      <td>2022-2023</td>
      <td>AL</td>
      <td>100005</td>
      <td>AL-101</td>
      <td>Albertville City</td>
      <td>Albertville High School</td>
      <td>402 E McCord Ave</td>
      <td>NaN</td>
      <td>Albertville</td>
      <td>AL</td>
      <td>35950</td>
      <td>2322</td>
      <td>(256)894-5000</td>
      <td>No</td>
      <td>Not Virtual</td>
      <td>09</td>
      <td>12</td>
      <td>High</td>
      <td>1</td>
      <td>Regular School</td>
      <td>Currently operational</td>
      <td>32-Town: Distant</td>
      <td>Marshall County</td>
      <td>1254</td>
      <td>1178</td>
      <td>76</td>
      <td>1059</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>493.0</td>
      <td>442.0</td>
      <td>390.0</td>
      <td>387.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>868.0</td>
      <td>844.0</td>
      <td>1712.0</td>
      <td>1712.0</td>
      <td>85.199997</td>
      <td>20.09</td>
      <td>0.0</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>4.0</td>
      <td>5.0</td>
      <td>9.0</td>
      <td>23.0</td>
      <td>34.0</td>
      <td>57.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>490.0</td>
      <td>468.0</td>
      <td>958.0</td>
      <td>26.0</td>
      <td>19.0</td>
      <td>45.0</td>
      <td>325.0</td>
      <td>316.0</td>
      <td>641.0</td>
      <td>34.2622</td>
      <td>-86.204900</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-86.220100</td>
      <td>34.2733</td>
      <td>3</td>
      <td>10000500879</td>
      <td>2022-2023</td>
      <td>AL</td>
      <td>100005</td>
      <td>AL-101</td>
      <td>Albertville City</td>
      <td>Albertville Intermediate School</td>
      <td>901 W McKinney Ave</td>
      <td>NaN</td>
      <td>Albertville</td>
      <td>AL</td>
      <td>35950</td>
      <td>1300</td>
      <td>(256)878-7698</td>
      <td>No</td>
      <td>Not Virtual</td>
      <td>05</td>
      <td>06</td>
      <td>Middle</td>
      <td>1</td>
      <td>Regular School</td>
      <td>Currently operational</td>
      <td>32-Town: Distant</td>
      <td>Marshall County</td>
      <td>718</td>
      <td>665</td>
      <td>53</td>
      <td>570</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>412.0</td>
      <td>462.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>451.0</td>
      <td>423.0</td>
      <td>874.0</td>
      <td>874.0</td>
      <td>43.000000</td>
      <td>20.33</td>
      <td>1.0</td>
      <td>4.0</td>
      <td>5.0</td>
      <td>4.0</td>
      <td>0.0</td>
      <td>4.0</td>
      <td>22.0</td>
      <td>28.0</td>
      <td>50.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>263.0</td>
      <td>241.0</td>
      <td>504.0</td>
      <td>7.0</td>
      <td>6.0</td>
      <td>13.0</td>
      <td>154.0</td>
      <td>144.0</td>
      <td>298.0</td>
      <td>34.2733</td>
      <td>-86.220100</td>
    </tr>
    <tr>
      <th>3</th>
      <td>-86.221806</td>
      <td>34.2527</td>
      <td>4</td>
      <td>10000500889</td>
      <td>2022-2023</td>
      <td>AL</td>
      <td>100005</td>
      <td>AL-101</td>
      <td>Albertville City</td>
      <td>Albertville Elementary School</td>
      <td>145 West End Drive</td>
      <td>NaN</td>
      <td>Albertville</td>
      <td>AL</td>
      <td>35950</td>
      <td></td>
      <td>(256)894-4822</td>
      <td>No</td>
      <td>Not Virtual</td>
      <td>03</td>
      <td>04</td>
      <td>Elementary</td>
      <td>1</td>
      <td>Regular School</td>
      <td>Currently operational</td>
      <td>32-Town: Distant</td>
      <td>Marshall County</td>
      <td>723</td>
      <td>680</td>
      <td>43</td>
      <td>583</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>430.0</td>
      <td>444.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>463.0</td>
      <td>411.0</td>
      <td>874.0</td>
      <td>874.0</td>
      <td>43.000000</td>
      <td>20.33</td>
      <td>0.0</td>
      <td>4.0</td>
      <td>4.0</td>
      <td>1.0</td>
      <td>3.0</td>
      <td>4.0</td>
      <td>22.0</td>
      <td>16.0</td>
      <td>38.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>261.0</td>
      <td>236.0</td>
      <td>497.0</td>
      <td>11.0</td>
      <td>16.0</td>
      <td>27.0</td>
      <td>168.0</td>
      <td>136.0</td>
      <td>304.0</td>
      <td>34.2527</td>
      <td>-86.221806</td>
    </tr>
    <tr>
      <th>4</th>
      <td>-86.193300</td>
      <td>34.2898</td>
      <td>5</td>
      <td>10000501616</td>
      <td>2022-2023</td>
      <td>AL</td>
      <td>100005</td>
      <td>AL-101</td>
      <td>Albertville City</td>
      <td>Albertville Kindergarten and PreK</td>
      <td>257 Country Club Rd</td>
      <td>NaN</td>
      <td>Albertville</td>
      <td>AL</td>
      <td>35951</td>
      <td>3927</td>
      <td>(256)878-7922</td>
      <td>No</td>
      <td>Not Virtual</td>
      <td>PK</td>
      <td>KG</td>
      <td>Elementary</td>
      <td>1</td>
      <td>Regular School</td>
      <td>Currently operational</td>
      <td>32-Town: Distant</td>
      <td>Marshall County</td>
      <td>392</td>
      <td>367</td>
      <td>25</td>
      <td>240</td>
      <td>133.0</td>
      <td>473.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>304.0</td>
      <td>302.0</td>
      <td>606.0</td>
      <td>606.0</td>
      <td>26.000000</td>
      <td>23.31</td>
      <td>1.0</td>
      <td>3.0</td>
      <td>4.0</td>
      <td>2.0</td>
      <td>0.0</td>
      <td>2.0</td>
      <td>26.0</td>
      <td>23.0</td>
      <td>49.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>167.0</td>
      <td>152.0</td>
      <td>319.0</td>
      <td>4.0</td>
      <td>4.0</td>
      <td>8.0</td>
      <td>104.0</td>
      <td>120.0</td>
      <td>224.0</td>
      <td>34.2898</td>
      <td>-86.193300</td>
    </tr>
  </tbody>
</table>
</div>




```python
psChar_23.isnull().sum()
```




    X                            0
    Y                            0
    ObjectID                     0
    NCESID                       0
    SurveyYear                   0
    StateABR                     0
    LEAID                        0
    ST_LEAID                     0
    LEAname                      0
    SchoolName                   0
    Street1                      1
    Street2                 100818
    City                         0
    State                        0
    Zip                          0
    Zip4                         0
    Phone                        0
    Charter                      0
    Virtual                      0
    LowestGrade                  0
    HighestGrade                 0
    SchoolLevel                  0
    Status                       0
    SchoolType                   0
    Status_Text                  0
    Locale                       0
    County                       0
    TotalFreeLunch               0
    FreeLunch                    0
    ReducedLunch                 0
    MealProgramCertified         0
    PreK                     68998
    Kindergarten             47329
    Grade1                   46978
    Grade2                   46921
    Grade3                   46931
    Grade4                   47132
    Grade5                   48376
    Grade6                   63367
    Grade7                   68166
    Grade8                   67898
    Grade9                   73289
    Grade10                  73501
    Grade11                  73502
    Grade12                  73574
    Grade13                 101257
    Ungraded                 93501
    AdultEd                 101207
    TotMaleEnrollment         2480
    TotFemaleEnrollment       2480
    TotalEnrollment           1671
    Member                    1671
    StaffFTE                  3853
    StudentTeacherRatio       1814
    AIANMale                  2581
    AIANFem                   2579
    AIANTotal                 2533
    AsianMale                 2492
    AsianFemale               2490
    AsianTotal                2484
    BlackMale                 2494
    BlackFemale               2497
    BlackTotal                2487
    HPIMale                   2608
    HPIFemale                 2607
    HPITotal                  2561
    HispanicMale              2481
    HispanicFemale            2480
    HispanicTotal             2480
    TRMale                    2487
    TRFemale                  2485
    TRTotal                   2484
    WhiteMale                 2481
    WhiteFemale               2481
    WhiteTotal                2480
    Latitude                     0
    Longitude                    0
    dtype: int64




```python
def missing(DataFrame):
    print('Percentage of missing values in the dataset:\n',
          round((DataFrame.isnull().sum() *100/len(DataFrame)), 2).sort_values(ascending=False))

missing(psChar_23)
```

    Percentage of missing values in the dataset:
     Grade13                 99.87
    AdultEd                 99.82
    Street2                 99.44
    Ungraded                92.22
    Grade12                 72.57
    Grade10                 72.49
    Grade11                 72.49
    Grade9                  72.28
    PreK                    68.05
    Grade7                  67.23
    Grade8                  66.97
    Grade6                  62.50
    Grade5                  47.71
    Kindergarten            46.68
    Grade4                  46.49
    Grade1                  46.33
    Grade3                  46.29
    Grade2                  46.28
    StaffFTE                 3.80
    HPIFemale                2.57
    HPIMale                  2.57
    AIANMale                 2.55
    AIANFem                  2.54
    HPITotal                 2.53
    AIANTotal                2.50
    AsianMale                2.46
    BlackMale                2.46
    AsianFemale              2.46
    BlackFemale              2.46
    WhiteFemale              2.45
    WhiteTotal               2.45
    TRTotal                  2.45
    AsianTotal               2.45
    BlackTotal               2.45
    HispanicMale             2.45
    HispanicFemale           2.45
    HispanicTotal            2.45
    WhiteMale                2.45
    TotFemaleEnrollment      2.45
    TRFemale                 2.45
    TRMale                   2.45
    TotMaleEnrollment        2.45
    StudentTeacherRatio      1.79
    TotalEnrollment          1.65
    Member                   1.65
    City                     0.00
    Street1                  0.00
    SchoolName               0.00
    LEAname                  0.00
    LEAID                    0.00
    ST_LEAID                 0.00
    StateABR                 0.00
    SurveyYear               0.00
    X                        0.00
    NCESID                   0.00
    ObjectID                 0.00
    Y                        0.00
    ReducedLunch             0.00
    MealProgramCertified     0.00
    TotalFreeLunch           0.00
    FreeLunch                0.00
    Zip                      0.00
    State                    0.00
    Zip4                     0.00
    Phone                    0.00
    Charter                  0.00
    Virtual                  0.00
    LowestGrade              0.00
    HighestGrade             0.00
    SchoolLevel              0.00
    Status                   0.00
    SchoolType               0.00
    Status_Text              0.00
    Locale                   0.00
    County                   0.00
    Latitude                 0.00
    Longitude                0.00
    dtype: float64


### Observations

A total of eighteen columns have missing value percentages above forty-five percent. For the 'Grade' columns, this could be explained because this dataset includes schools at various education levels, meaning some schools might not offer certain grade levels. Given this, I would drop the AdultEd column, as this research is focused only on youth sports participation. I would also drop columns 'Phone', 'LEAName', 'LEADID', 'ST_LEAID', 'SurveyYear', 'StaffFTE', 'Member', and 'NCESID', as they are not necessary for analysis. Removing these columns would help declutter the dataset without impacting the research. 


```python
dropCols = ['AdultEd','Phone','LEAname','LEAID','ST_LEAID','SurveyYear','StaffFTE','Member','NCESID']

psChar_23 = psChar_23.drop(columns=dropCols)
psChar_23 

psChar_23.isnull().sum()
```




    X                            0
    Y                            0
    ObjectID                     0
    StateABR                     0
    SchoolName                   0
    Street1                      1
    Street2                 100818
    City                         0
    State                        0
    Zip                          0
    Zip4                         0
    Charter                      0
    Virtual                      0
    LowestGrade                  0
    HighestGrade                 0
    SchoolLevel                  0
    Status                       0
    SchoolType                   0
    Status_Text                  0
    Locale                       0
    County                       0
    TotalFreeLunch               0
    FreeLunch                    0
    ReducedLunch                 0
    MealProgramCertified         0
    PreK                     68998
    Kindergarten             47329
    Grade1                   46978
    Grade2                   46921
    Grade3                   46931
    Grade4                   47132
    Grade5                   48376
    Grade6                   63367
    Grade7                   68166
    Grade8                   67898
    Grade9                   73289
    Grade10                  73501
    Grade11                  73502
    Grade12                  73574
    Grade13                 101257
    Ungraded                 93501
    TotMaleEnrollment         2480
    TotFemaleEnrollment       2480
    TotalEnrollment           1671
    StudentTeacherRatio       1814
    AIANMale                  2581
    AIANFem                   2579
    AIANTotal                 2533
    AsianMale                 2492
    AsianFemale               2490
    AsianTotal                2484
    BlackMale                 2494
    BlackFemale               2497
    BlackTotal                2487
    HPIMale                   2608
    HPIFemale                 2607
    HPITotal                  2561
    HispanicMale              2481
    HispanicFemale            2480
    HispanicTotal             2480
    TRMale                    2487
    TRFemale                  2485
    TRTotal                   2484
    WhiteMale                 2481
    WhiteFemale               2481
    WhiteTotal                2480
    Latitude                     0
    Longitude                    0
    dtype: int64




```python
psChar_23['Locale'].unique()
```




    array(['32-Town: Distant', '42-Rural: Distant', '41-Rural: Fringe',
           '13-City: Small', '21-Suburb: Large', '12-City: Mid-size',
           '33-Town: Remote', '31-Town: Fringe', '23-Suburb: Small',
           '43-Rural: Remote', '22-Suburb: Mid-size', '11-City: Large'],
          dtype=object)




```python
Locale = {'42-Rural: Distant':'Rural',
            '41-Rural: Fringe':'Rural',
            '43-Rural: Remote':'Rural',
            '32-Town: Distant':'Town',
            '33-Town: Remote':'Town',
            '31-Town: Fringe':'Town',
            '13-City: Small':'City',
            '12-City: Mid-size':'City',
            '11-City: Large':'City',
            '21-Suburb: Large':'Suburb',
            '23-Suburb: Small':'Suburb',
            '22-Suburb: Mid-size':'Suburb'}

Locale
```




    {'42-Rural: Distant': 'Rural',
     '41-Rural: Fringe': 'Rural',
     '43-Rural: Remote': 'Rural',
     '32-Town: Distant': 'Town',
     '33-Town: Remote': 'Town',
     '31-Town: Fringe': 'Town',
     '13-City: Small': 'City',
     '12-City: Mid-size': 'City',
     '11-City: Large': 'City',
     '21-Suburb: Large': 'Suburb',
     '23-Suburb: Small': 'Suburb',
     '22-Suburb: Mid-size': 'Suburb'}




```python
psChar_23['Locale'] = psChar_23['Locale'].map(Locale)

psChar_23['Locale'].unique()
```




    array(['Town', 'Rural', 'City', 'Suburb'], dtype=object)




```python
psChar_23.head()
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
      <th>X</th>
      <th>Y</th>
      <th>ObjectID</th>
      <th>StateABR</th>
      <th>SchoolName</th>
      <th>Street1</th>
      <th>Street2</th>
      <th>City</th>
      <th>State</th>
      <th>Zip</th>
      <th>Zip4</th>
      <th>Charter</th>
      <th>Virtual</th>
      <th>LowestGrade</th>
      <th>HighestGrade</th>
      <th>SchoolLevel</th>
      <th>Status</th>
      <th>SchoolType</th>
      <th>Status_Text</th>
      <th>Locale</th>
      <th>County</th>
      <th>TotalFreeLunch</th>
      <th>FreeLunch</th>
      <th>ReducedLunch</th>
      <th>MealProgramCertified</th>
      <th>PreK</th>
      <th>Kindergarten</th>
      <th>Grade1</th>
      <th>Grade2</th>
      <th>Grade3</th>
      <th>Grade4</th>
      <th>Grade5</th>
      <th>Grade6</th>
      <th>Grade7</th>
      <th>Grade8</th>
      <th>Grade9</th>
      <th>Grade10</th>
      <th>Grade11</th>
      <th>Grade12</th>
      <th>Grade13</th>
      <th>Ungraded</th>
      <th>TotMaleEnrollment</th>
      <th>TotFemaleEnrollment</th>
      <th>TotalEnrollment</th>
      <th>StudentTeacherRatio</th>
      <th>AIANMale</th>
      <th>AIANFem</th>
      <th>AIANTotal</th>
      <th>AsianMale</th>
      <th>AsianFemale</th>
      <th>AsianTotal</th>
      <th>BlackMale</th>
      <th>BlackFemale</th>
      <th>BlackTotal</th>
      <th>HPIMale</th>
      <th>HPIFemale</th>
      <th>HPITotal</th>
      <th>HispanicMale</th>
      <th>HispanicFemale</th>
      <th>HispanicTotal</th>
      <th>TRMale</th>
      <th>TRFemale</th>
      <th>TRTotal</th>
      <th>WhiteMale</th>
      <th>WhiteFemale</th>
      <th>WhiteTotal</th>
      <th>Latitude</th>
      <th>Longitude</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-86.206200</td>
      <td>34.2602</td>
      <td>1</td>
      <td>AL</td>
      <td>Albertville Middle School</td>
      <td>600 E Alabama Ave</td>
      <td>NaN</td>
      <td>Albertville</td>
      <td>AL</td>
      <td>35950</td>
      <td></td>
      <td>No</td>
      <td>Not Virtual</td>
      <td>07</td>
      <td>08</td>
      <td>Middle</td>
      <td>1</td>
      <td>Regular School</td>
      <td>Currently operational</td>
      <td>Town</td>
      <td>Marshall County</td>
      <td>697</td>
      <td>654</td>
      <td>43</td>
      <td>587</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>440.0</td>
      <td>450.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>459.0</td>
      <td>431.0</td>
      <td>890.0</td>
      <td>19.78</td>
      <td>4.0</td>
      <td>1.0</td>
      <td>5.0</td>
      <td>4.0</td>
      <td>2.0</td>
      <td>6.0</td>
      <td>15.0</td>
      <td>14.0</td>
      <td>29.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>251.0</td>
      <td>251.0</td>
      <td>502.0</td>
      <td>17.0</td>
      <td>15.0</td>
      <td>32.0</td>
      <td>168.0</td>
      <td>147.0</td>
      <td>315.0</td>
      <td>34.2602</td>
      <td>-86.206200</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-86.204900</td>
      <td>34.2622</td>
      <td>2</td>
      <td>AL</td>
      <td>Albertville High School</td>
      <td>402 E McCord Ave</td>
      <td>NaN</td>
      <td>Albertville</td>
      <td>AL</td>
      <td>35950</td>
      <td>2322</td>
      <td>No</td>
      <td>Not Virtual</td>
      <td>09</td>
      <td>12</td>
      <td>High</td>
      <td>1</td>
      <td>Regular School</td>
      <td>Currently operational</td>
      <td>Town</td>
      <td>Marshall County</td>
      <td>1254</td>
      <td>1178</td>
      <td>76</td>
      <td>1059</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>493.0</td>
      <td>442.0</td>
      <td>390.0</td>
      <td>387.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>868.0</td>
      <td>844.0</td>
      <td>1712.0</td>
      <td>20.09</td>
      <td>0.0</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>4.0</td>
      <td>5.0</td>
      <td>9.0</td>
      <td>23.0</td>
      <td>34.0</td>
      <td>57.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>490.0</td>
      <td>468.0</td>
      <td>958.0</td>
      <td>26.0</td>
      <td>19.0</td>
      <td>45.0</td>
      <td>325.0</td>
      <td>316.0</td>
      <td>641.0</td>
      <td>34.2622</td>
      <td>-86.204900</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-86.220100</td>
      <td>34.2733</td>
      <td>3</td>
      <td>AL</td>
      <td>Albertville Intermediate School</td>
      <td>901 W McKinney Ave</td>
      <td>NaN</td>
      <td>Albertville</td>
      <td>AL</td>
      <td>35950</td>
      <td>1300</td>
      <td>No</td>
      <td>Not Virtual</td>
      <td>05</td>
      <td>06</td>
      <td>Middle</td>
      <td>1</td>
      <td>Regular School</td>
      <td>Currently operational</td>
      <td>Town</td>
      <td>Marshall County</td>
      <td>718</td>
      <td>665</td>
      <td>53</td>
      <td>570</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>412.0</td>
      <td>462.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>451.0</td>
      <td>423.0</td>
      <td>874.0</td>
      <td>20.33</td>
      <td>1.0</td>
      <td>4.0</td>
      <td>5.0</td>
      <td>4.0</td>
      <td>0.0</td>
      <td>4.0</td>
      <td>22.0</td>
      <td>28.0</td>
      <td>50.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>263.0</td>
      <td>241.0</td>
      <td>504.0</td>
      <td>7.0</td>
      <td>6.0</td>
      <td>13.0</td>
      <td>154.0</td>
      <td>144.0</td>
      <td>298.0</td>
      <td>34.2733</td>
      <td>-86.220100</td>
    </tr>
    <tr>
      <th>3</th>
      <td>-86.221806</td>
      <td>34.2527</td>
      <td>4</td>
      <td>AL</td>
      <td>Albertville Elementary School</td>
      <td>145 West End Drive</td>
      <td>NaN</td>
      <td>Albertville</td>
      <td>AL</td>
      <td>35950</td>
      <td></td>
      <td>No</td>
      <td>Not Virtual</td>
      <td>03</td>
      <td>04</td>
      <td>Elementary</td>
      <td>1</td>
      <td>Regular School</td>
      <td>Currently operational</td>
      <td>Town</td>
      <td>Marshall County</td>
      <td>723</td>
      <td>680</td>
      <td>43</td>
      <td>583</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>430.0</td>
      <td>444.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>463.0</td>
      <td>411.0</td>
      <td>874.0</td>
      <td>20.33</td>
      <td>0.0</td>
      <td>4.0</td>
      <td>4.0</td>
      <td>1.0</td>
      <td>3.0</td>
      <td>4.0</td>
      <td>22.0</td>
      <td>16.0</td>
      <td>38.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>261.0</td>
      <td>236.0</td>
      <td>497.0</td>
      <td>11.0</td>
      <td>16.0</td>
      <td>27.0</td>
      <td>168.0</td>
      <td>136.0</td>
      <td>304.0</td>
      <td>34.2527</td>
      <td>-86.221806</td>
    </tr>
    <tr>
      <th>4</th>
      <td>-86.193300</td>
      <td>34.2898</td>
      <td>5</td>
      <td>AL</td>
      <td>Albertville Kindergarten and PreK</td>
      <td>257 Country Club Rd</td>
      <td>NaN</td>
      <td>Albertville</td>
      <td>AL</td>
      <td>35951</td>
      <td>3927</td>
      <td>No</td>
      <td>Not Virtual</td>
      <td>PK</td>
      <td>KG</td>
      <td>Elementary</td>
      <td>1</td>
      <td>Regular School</td>
      <td>Currently operational</td>
      <td>Town</td>
      <td>Marshall County</td>
      <td>392</td>
      <td>367</td>
      <td>25</td>
      <td>240</td>
      <td>133.0</td>
      <td>473.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>304.0</td>
      <td>302.0</td>
      <td>606.0</td>
      <td>23.31</td>
      <td>1.0</td>
      <td>3.0</td>
      <td>4.0</td>
      <td>2.0</td>
      <td>0.0</td>
      <td>2.0</td>
      <td>26.0</td>
      <td>23.0</td>
      <td>49.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>167.0</td>
      <td>152.0</td>
      <td>319.0</td>
      <td>4.0</td>
      <td>4.0</td>
      <td>8.0</td>
      <td>104.0</td>
      <td>120.0</td>
      <td>224.0</td>
      <td>34.2898</td>
      <td>-86.193300</td>
    </tr>
  </tbody>
</table>
</div>




```python
psChar_23OG = psChar_23
```


```python
psChar_23.describe()
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
      <th>X</th>
      <th>Y</th>
      <th>ObjectID</th>
      <th>Zip</th>
      <th>Status</th>
      <th>TotalFreeLunch</th>
      <th>FreeLunch</th>
      <th>ReducedLunch</th>
      <th>MealProgramCertified</th>
      <th>PreK</th>
      <th>Kindergarten</th>
      <th>Grade1</th>
      <th>Grade2</th>
      <th>Grade3</th>
      <th>Grade4</th>
      <th>Grade5</th>
      <th>Grade6</th>
      <th>Grade7</th>
      <th>Grade8</th>
      <th>Grade9</th>
      <th>Grade10</th>
      <th>Grade11</th>
      <th>Grade12</th>
      <th>Grade13</th>
      <th>Ungraded</th>
      <th>TotMaleEnrollment</th>
      <th>TotFemaleEnrollment</th>
      <th>TotalEnrollment</th>
      <th>StudentTeacherRatio</th>
      <th>AIANMale</th>
      <th>AIANFem</th>
      <th>AIANTotal</th>
      <th>AsianMale</th>
      <th>AsianFemale</th>
      <th>AsianTotal</th>
      <th>BlackMale</th>
      <th>BlackFemale</th>
      <th>BlackTotal</th>
      <th>HPIMale</th>
      <th>HPIFemale</th>
      <th>HPITotal</th>
      <th>HispanicMale</th>
      <th>HispanicFemale</th>
      <th>HispanicTotal</th>
      <th>TRMale</th>
      <th>TRFemale</th>
      <th>TRTotal</th>
      <th>WhiteMale</th>
      <th>WhiteFemale</th>
      <th>WhiteTotal</th>
      <th>Latitude</th>
      <th>Longitude</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>101390.000000</td>
      <td>101390.000000</td>
      <td>101390.000000</td>
      <td>101390.000000</td>
      <td>101390.000000</td>
      <td>101390.000000</td>
      <td>101390.000000</td>
      <td>101390.000000</td>
      <td>101390.000000</td>
      <td>32392.000000</td>
      <td>54061.000000</td>
      <td>54412.000000</td>
      <td>54469.000000</td>
      <td>54459.000000</td>
      <td>54258.000000</td>
      <td>53014.000000</td>
      <td>38023.000000</td>
      <td>33224.000000</td>
      <td>33492.000000</td>
      <td>28101.000000</td>
      <td>27889.000000</td>
      <td>27888.000000</td>
      <td>27816.000000</td>
      <td>133.000000</td>
      <td>7889.000000</td>
      <td>98910.000000</td>
      <td>98910.000000</td>
      <td>99719.000000</td>
      <td>99576.000000</td>
      <td>98809.000000</td>
      <td>98811.000000</td>
      <td>98857.000000</td>
      <td>98898.000000</td>
      <td>98900.000000</td>
      <td>98906.000000</td>
      <td>98896.000000</td>
      <td>98893.000000</td>
      <td>98903.000000</td>
      <td>98782.000000</td>
      <td>98783.000000</td>
      <td>98829.000000</td>
      <td>98909.000000</td>
      <td>98910.000000</td>
      <td>98910.000000</td>
      <td>98903.000000</td>
      <td>98905.000000</td>
      <td>98906.000000</td>
      <td>98909.000000</td>
      <td>98909.000000</td>
      <td>98910.000000</td>
      <td>101390.000000</td>
      <td>101390.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>-93.018793</td>
      <td>37.829053</td>
      <td>50695.500000</td>
      <td>54142.143486</td>
      <td>1.067245</td>
      <td>245.605227</td>
      <td>210.221412</td>
      <td>22.268074</td>
      <td>93.988352</td>
      <td>40.983823</td>
      <td>65.520135</td>
      <td>66.317651</td>
      <td>64.595954</td>
      <td>65.936484</td>
      <td>65.968705</td>
      <td>68.097201</td>
      <td>96.287852</td>
      <td>111.467343</td>
      <td>113.483877</td>
      <td>147.977866</td>
      <td>143.631181</td>
      <td>133.416416</td>
      <td>131.700065</td>
      <td>13.533835</td>
      <td>15.537330</td>
      <td>255.192529</td>
      <td>241.898807</td>
      <td>497.605060</td>
      <td>15.003147</td>
      <td>2.494176</td>
      <td>2.392922</td>
      <td>4.884773</td>
      <td>13.926621</td>
      <td>13.116977</td>
      <td>27.041676</td>
      <td>37.747705</td>
      <td>36.331024</td>
      <td>74.072384</td>
      <td>0.966664</td>
      <td>0.912080</td>
      <td>1.877860</td>
      <td>73.314794</td>
      <td>70.106005</td>
      <td>143.420059</td>
      <td>12.459117</td>
      <td>12.046732</td>
      <td>24.505349</td>
      <td>114.297061</td>
      <td>107.005894</td>
      <td>221.300718</td>
      <td>37.829053</td>
      <td>-93.018793</td>
    </tr>
    <tr>
      <th>std</th>
      <td>17.529915</td>
      <td>5.742854</td>
      <td>29268.916234</td>
      <td>29019.175805</td>
      <td>0.543609</td>
      <td>286.333793</td>
      <td>261.173677</td>
      <td>42.551195</td>
      <td>171.652331</td>
      <td>51.355382</td>
      <td>44.667621</td>
      <td>43.747748</td>
      <td>42.866839</td>
      <td>43.947306</td>
      <td>45.175769</td>
      <td>52.967014</td>
      <td>104.053353</td>
      <td>121.719374</td>
      <td>126.030072</td>
      <td>201.096251</td>
      <td>190.541635</td>
      <td>175.934093</td>
      <td>171.683639</td>
      <td>14.912649</td>
      <td>39.720262</td>
      <td>238.610843</td>
      <td>232.190904</td>
      <td>469.146689</td>
      <td>22.046021</td>
      <td>12.806250</td>
      <td>12.382737</td>
      <td>25.071642</td>
      <td>42.931145</td>
      <td>40.522241</td>
      <td>83.179729</td>
      <td>73.318161</td>
      <td>72.320949</td>
      <td>144.791997</td>
      <td>6.645046</td>
      <td>6.241464</td>
      <td>12.801317</td>
      <td>122.223271</td>
      <td>117.565596</td>
      <td>239.029766</td>
      <td>17.699249</td>
      <td>17.599337</td>
      <td>34.872361</td>
      <td>134.294673</td>
      <td>129.277185</td>
      <td>262.807276</td>
      <td>5.742854</td>
      <td>17.529915</td>
    </tr>
    <tr>
      <th>min</th>
      <td>-176.640331</td>
      <td>-14.348924</td>
      <td>1.000000</td>
      <td>601.000000</td>
      <td>1.000000</td>
      <td>-9.000000</td>
      <td>-9.000000</td>
      <td>-9.000000</td>
      <td>-9.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>-2.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>-14.348924</td>
      <td>-176.640331</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>-101.852437</td>
      <td>33.950597</td>
      <td>25348.250000</td>
      <td>30228.000000</td>
      <td>1.000000</td>
      <td>51.000000</td>
      <td>22.000000</td>
      <td>0.000000</td>
      <td>-1.000000</td>
      <td>15.000000</td>
      <td>37.000000</td>
      <td>38.000000</td>
      <td>37.000000</td>
      <td>37.000000</td>
      <td>37.000000</td>
      <td>36.000000</td>
      <td>23.000000</td>
      <td>20.000000</td>
      <td>19.000000</td>
      <td>9.000000</td>
      <td>12.000000</td>
      <td>14.000000</td>
      <td>15.000000</td>
      <td>2.000000</td>
      <td>1.000000</td>
      <td>117.000000</td>
      <td>110.000000</td>
      <td>230.000000</td>
      <td>11.590000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>2.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>7.000000</td>
      <td>6.000000</td>
      <td>13.000000</td>
      <td>2.000000</td>
      <td>2.000000</td>
      <td>4.000000</td>
      <td>18.000000</td>
      <td>15.000000</td>
      <td>33.000000</td>
      <td>33.950597</td>
      <td>-101.852437</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>-89.603343</td>
      <td>38.744732</td>
      <td>50695.500000</td>
      <td>55336.000000</td>
      <td>1.000000</td>
      <td>175.500000</td>
      <td>139.000000</td>
      <td>10.000000</td>
      <td>-1.000000</td>
      <td>30.000000</td>
      <td>61.000000</td>
      <td>63.000000</td>
      <td>61.000000</td>
      <td>62.000000</td>
      <td>62.000000</td>
      <td>61.000000</td>
      <td>62.000000</td>
      <td>66.000000</td>
      <td>66.000000</td>
      <td>64.000000</td>
      <td>63.000000</td>
      <td>60.000000</td>
      <td>62.000000</td>
      <td>8.000000</td>
      <td>5.000000</td>
      <td>209.000000</td>
      <td>198.000000</td>
      <td>407.000000</td>
      <td>14.400000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>2.000000</td>
      <td>2.000000</td>
      <td>4.000000</td>
      <td>8.000000</td>
      <td>7.000000</td>
      <td>15.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>28.000000</td>
      <td>26.000000</td>
      <td>54.000000</td>
      <td>7.000000</td>
      <td>7.000000</td>
      <td>15.000000</td>
      <td>80.000000</td>
      <td>74.000000</td>
      <td>154.000000</td>
      <td>38.744732</td>
      <td>-89.603342</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>-81.262800</td>
      <td>41.670558</td>
      <td>76042.750000</td>
      <td>78610.000000</td>
      <td>1.000000</td>
      <td>347.000000</td>
      <td>305.000000</td>
      <td>29.000000</td>
      <td>137.000000</td>
      <td>52.000000</td>
      <td>88.000000</td>
      <td>89.000000</td>
      <td>86.000000</td>
      <td>88.000000</td>
      <td>88.000000</td>
      <td>89.000000</td>
      <td>130.000000</td>
      <td>172.000000</td>
      <td>175.000000</td>
      <td>209.000000</td>
      <td>200.000000</td>
      <td>182.000000</td>
      <td>180.000000</td>
      <td>21.000000</td>
      <td>16.000000</td>
      <td>320.000000</td>
      <td>303.000000</td>
      <td>622.000000</td>
      <td>17.460000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>3.000000</td>
      <td>9.000000</td>
      <td>9.000000</td>
      <td>18.000000</td>
      <td>42.000000</td>
      <td>40.000000</td>
      <td>82.000000</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>91.000000</td>
      <td>86.000000</td>
      <td>177.000000</td>
      <td>17.000000</td>
      <td>17.000000</td>
      <td>34.000000</td>
      <td>165.000000</td>
      <td>154.000000</td>
      <td>318.000000</td>
      <td>41.670558</td>
      <td>-81.262800</td>
    </tr>
    <tr>
      <th>max</th>
      <td>145.784430</td>
      <td>71.300337</td>
      <td>101390.000000</td>
      <td>99950.000000</td>
      <td>8.000000</td>
      <td>10074.000000</td>
      <td>5563.000000</td>
      <td>1400.000000</td>
      <td>6230.000000</td>
      <td>1618.000000</td>
      <td>1205.000000</td>
      <td>1398.000000</td>
      <td>1534.000000</td>
      <td>1433.000000</td>
      <td>1469.000000</td>
      <td>1474.000000</td>
      <td>1686.000000</td>
      <td>1908.000000</td>
      <td>2240.000000</td>
      <td>6251.000000</td>
      <td>3368.000000</td>
      <td>3454.000000</td>
      <td>3071.000000</td>
      <td>66.000000</td>
      <td>1178.000000</td>
      <td>9978.000000</td>
      <td>10377.000000</td>
      <td>20355.000000</td>
      <td>3600.000000</td>
      <td>619.000000</td>
      <td>666.000000</td>
      <td>1285.000000</td>
      <td>1947.000000</td>
      <td>1529.000000</td>
      <td>3476.000000</td>
      <td>2546.000000</td>
      <td>2589.000000</td>
      <td>5135.000000</td>
      <td>556.000000</td>
      <td>440.000000</td>
      <td>996.000000</td>
      <td>3011.000000</td>
      <td>3883.000000</td>
      <td>6894.000000</td>
      <td>1714.000000</td>
      <td>1548.000000</td>
      <td>3262.000000</td>
      <td>5736.000000</td>
      <td>5942.000000</td>
      <td>11678.000000</td>
      <td>71.300337</td>
      <td>145.784430</td>
    </tr>
  </tbody>
</table>
</div>



### Observations of Descriptive Statistics

(Min, Max):
- TotalFreeLunch (-9, 10074); FreeLunch (-9, 5563); ReducedLunch (-9, 1400); MealProgramCertified (-9, 6230)
- PreK (0, 1618)
- Kindergarten (0, 1205)
- Grade1 (0, 1398)
- Grade2 (0, 1534)
- Grade3 (0, 1433)
- Grade4 (0, 1469)
- Grade5 (0, 1474)
- Grade6 (0, 1686)
- Grade7 (0, 1908)
- Grade8 (0, 2240)
- Grade9 (0, 6251)
- Grade10 (0, 3368)
- Grade11 (0, 3454)
- Grade12 (0, 3071)
- Grade13 (0, 66)
- Ungraded (0, 1178)
- Total Male Enrollment (0, 9978); Total Female Enrollment (0, 10377); Total Enrollment (0, 20355)
- Student Teacher Ratio (-2, 3600)
- American Indian/Alaskan Native Male (0, 619); American Indian/Alaskan Native Female (0, 666); American Indian/Alaskan Native Total (0, 1285)
- Asian Male (0, 1947); Asian Female (0, 1529); Asian Total (0, 3476)
- Black Male (0, 2546); Black Female (0, 2589); Black Total (0, 5135)
- Native Hawaiian/Pacific Islander(HPI) Male (0, 556); Native Hawaiian/Pacific Islander(HPI) Female (0, 440); Native Hawaiian/Pacific Islander(HPI) Total (0, 996)
- Hispanic Male (0, 3011); Hispanic Female (0, 3883); Hispanic Total (0, 6894)
- Two or More Races Male (0, 1714); Two or More Races Female (0, 1548); Two or More Races Total (0, 3262)
- White Male (0, 5736); White Female (0, 5942); White Total (0, 11678)

Mean:
- TotalFreeLunch 245.6; FreeLunch 210.2; ReducedLunch 22.2; MealProgramCertified 93.99
- PreK 40.99
- Kindergarten 65.5
- Grade1 66.3
- Grade2 64.6
- Grade3 65.99
- Grade4 65.9
- Grade5 68.1
- Grade6 96.2
- Grade7 111.5
- Grade8 113.5
- Grade9 148
- Grade10 143.6
- Grade11 133.4
- Grade12 131.7
- Grade13 13.5
- Ungraded 15.5
- Total Male Enrollment 255.2; Total Female Enrollment 241.9; Total Enrollment 497.6
- Student Teacher Ratio 15.0
- American Indian/Alaskan Native Male 2.5; American Indian/Alaskan Native Female 2.4; American Indian/Alaskan Native Total 4.9
- Asian Male 13.9; Asian Female 13.1; Asian Total 27.0
- Black Male 37.7; Black Female 36.3; Black Total 74.1
- Native Hawaiian/Pacific Islander(HPI) Male 0.97; Native Hawaiian/Pacific Islander(HPI) Female 0.91; Native Hawaiian/Pacific Islander(HPI) Total 1.9
- Hispanic Male 73.3; Hispanic Female 70.1; Hispanic Total 143.4
- Two or More Races Male 12.5; Two or More Races Female 12.0; Two or More Races Total 24.5
- White Male 114.3; White Female 107.0; White Total 221.3

Mean/Median Closeness:

The medians for the free/reduced lunch status of the schools are lower than the means (skewed left).

For the columns covering the elementary school grades and the student/teacher ratio, the mean and median are close. For the other grades, the values are skewed left. They are also close for Grade13 and Ungraded students, and American Indian/Alaskan Native and Native Hawaiian/Pacific Islander demographics, because of the smaller sampling size. 

The median for the student-teacher ratio is close to the mean. 

The medians for enrollment rates are lower than the means. 

The medians for Asian student & students belonging to Two or More Races (TR) demographics are lower than the means. 

The medians for Black and Hispanic student demographics are significantly lower than the means. 

The medians for White student demographics are lower than the means. 

Quartile Ranges (25%, 75%):

- TotalFreeLunch (51, 347); FreeLunch (22, 305); ReducedLunch (0, 29); MealProgramCertified (-1, 137)
- PreK (15, 52)
- Kindergarten (37, 88)
- Grade1 (38, 89)
- Grade2 (37, 86)
- Grade3 (37, 88)
- Grade4 (37, 88)
- Grade5 (36, 89)
- Grade6 (23, 130)
- Grade7 (20, 172)
- Grade8 (19, 175)
- Grade9 (9, 209)
- Grade10 (12, 200)
- Grade11 (14, 182)
- Grade12 (15, 180)
- Grade13 (2, 21)
- Ungraded (1, 16)
- Total Male Enrollment (117, 320); Total Female Enrollment (110, 303); Total Enrollment (203, 622)
- Student Teacher Ratio (11.6, 17.5)
- American Indian/Alaskan Native Male (0, 1); American Indian/Alaskan Native Female (0, 1); American Indian/Alaskan Native Total (0, 3)
- Asian Male (0, 9); Asian Female (0, 9); Asian Total (0, 18)
- Black Male (1, 42); Black Female (1, 40); Black Total (2, 82)
- Native Hawaiian/Pacific Islander(HPI) Male (0, 1); Native Hawaiian/Pacific Islander(HPI) Female (0, 0); Native Hawaiian/Pacific Islander(HPI) Total (0, 1)
- Hispanic Male (7, 91); Hispanic Female (6, 86); Hispanic Total (13, 177)
- Two or More Races Male (2, 17); Two or More Races Female (2, 17); Two or More Races Total (4, 34)
- White Male (18, 165); White Female (15, 154); White Total (33, 318)

Standard Deviation:

Higher - Lunch, PreK,Grade6 and above (including ungraded), Student/Teacher ratio, AIAN, Asian, Black, HPI, Hispanic demographics, White is also higher but not as significant as the other disparities. 
Lower- Kinder thru Grade5, 
Same- Enrollment, TR

The standard deviation for the total free lunch and free lunch statuses are close, while the standard deviations for reduced lunch and meal program certified schools are moderately lower than the means. 

The standard deviation for PreK students is higher than the mean, while the standard deviations for Kindergarten through Grade 5 are all lower. The standard deviations for ungraded students and from Grade 6 and above are higher than the means. 

The standard deviations for enrollment rates are mostly similar to the means. 

The standard deviation for the student to teacher ratio is a bit higher than the mean. 

The standard deviations for White student demographics are moderately higher than their means, yet the disparity is not as significant as it is in all other races.  
