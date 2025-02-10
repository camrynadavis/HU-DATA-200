## Research Question

How do financial barriers and public school funding disparities contribute to the underrepresentation of Black and Hispanic youth in high-cost sports by limiting access to facilities, specialized sports training, injury management and scouting opportunities?

## Problem Statement

Sports specialization involves year-round training and competition, and requires costly investments towards participation, travel, and equipment fees, which creates significant finanicial barriers for youth from lower socioeconomic backgrounds. Aside from this, public school funding disparities can limit access to appropriate facilities, personnel, or physical education, which could further hinder sports participation opportunities for youth in lower SES communities. These disparities can contribute to underrepresentation of Black or Hispanic youth in sports with high financial barriers -- hockey, gymnastics, tennis, etc., while sports such as track and field are less expensive, and therefore more accessible.

### Potential Subtopics

- Public school funding and facility quality
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
psChar_23 = psChar_23.rename(columns = {'OBJECTID':'ObjectID', 'NCESSCH':'NCESID', 'SURVYEAR':'SurveyYear', 'STABR':'StateABR',  
       'LEA_NAME':'LEAName', 'SCH_NAME':'SchoolName', 'LSTREET1':'Street1', 'LSTREET2':'Street2', 'LCITY':'City',
       'LSTATE':'State', 'LZIP':'Zip', 'LZIP4':'Zip4', 'PHONE':'Phone', 'CHARTER_TEXT':'Charter', 'VIRTUAL':'Virtual', 'GSLO':'LowestGrade',
       'GSHI':'HighestGrade', 'SCHOOL_LEVEL':'SchoolLevel', 'STATUS':'Status', 'SCHOOL_TYPE_TEXT':'SchoolType', 'SY_STATUS_TEXT':'Status',
       'ULOCALE':'Locale', 'NMCNTY':'County', 'TOTFRL':'TotalFreeLunch', 'FRELCH':'FreeLunch', 'REDLCH':'ReducedLunch', 
       'DIRECTCERT':'MealProgramCertified', 'PK':'PreK','KG':'Kindergarten', 'G01':'Grade1', 'G02':'Grade2', 'G03':'Grade3', 'G04':'Grade4', 
       'G05':'Grade5', 'G06':'Grade6', 'G07':'Grade7', 'G08':'Grade8', 'G09':'Grade9','G10':'Grade10', 'G11':'Grade11', 'G12':'Grade12', 
       'G13':'Grade13', 'UG':'Ungraded', 'AE':'AdultEd', 'TOTMENROL':'TotMaleEnrollment', 'TOTFENROL':'TotFemaleEnrollment',
       'TOTAL':'TotalEnrollment', 'MEMBER':'Member', 'FTE':'StaffFTE', 'STUTERATIO':'StudentTeacherRatio', 'AMALM':'AIANMale', 
       'AMALF':'AIANFem', 'AM':'AIANTotal', 'ASALM':'AsianMale', 'ASALF':'AsianFemale', 'AS':'AsianTotal', 'BLALM':'BlackMale', 
       'BLALF':'BlackFemale', 'BL':'BlackTotal', 'HPALM':'HPIMale', 'HPALF':'HPIFemale', 'HP':'HPITotal', 'HIALM':'HispanicMale',
       'HIALF':'HispanicFemale', 'HI':'HispanicTotal', 'TRALM':'TRMale', 'TRALF':'TRFemale', 'TR':'TRTotal', 'WHALM':'WhiteMale', 
       'WHALF':'WhiteFemale', 'WH':'WhiteTotal', 'LATCOD':'Latitude','LONCOD':'Longitude'})
```


```python
ps23Cols = psChar_23.columns
ps23Cols
```




    Index(['X', 'Y', 'ObjectID', 'NCESID', 'SurveyYear', 'StateABR', 'LEAID',
           'ST_LEAID', 'LEAName', 'SchoolName', 'Street1', 'Street2', 'City',
           'State', 'Zip', 'Zip4', 'Phone', 'Charter', 'Virtual', 'LowestGrade',
           'HighestGrade', 'SchoolLevel', 'Status', 'SchoolType', 'Status',
           'Locale', 'County', 'TotalFreeLunch', 'FreeLunch', 'ReducedLunch',
           'MealProgramCertified', 'PreK', 'Kindergarten', 'Grade1', 'Grade2',
           'Grade3', 'Grade4', 'Grade5', 'Grade6', 'Grade7', 'Grade8', 'Grade9',
           'Grade10', 'Grade11', 'Grade12', 'Grade13', 'Ungraded', 'AdultEd',
           'TotMaleEnrollment', 'TotFemaleEnrollment', 'TotalEnrollment', 'Member',
           'StaffFTE', 'StudentTeacherRatio', 'AIANMale', 'AIANFem', 'AIANTotal',
           'AsianMale', 'AsianFemale', 'AsianTotal', 'BlackMale', 'BlackFemale',
           'BlackTotal', 'HPIMale', 'HPIFemale', 'HPITotal', 'HispanicMale',
           'HispanicFemale', 'HispanicTotal', 'TRMale', 'TRFemale', 'TRTotal',
           'WhiteMale', 'WhiteFemale', 'WhiteTotal', 'Latitude', 'Longitude'],
          dtype='object')




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
      <th>ObjectID</th>
      <th>NCESID</th>
      <th>SurveyYear</th>
      <th>StateABR</th>
      <th>LEAID</th>
      <th>ST_LEAID</th>
      <th>LEAName</th>
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
      <th>Status</th>
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
      <th>ObjectID</th>
      <th>NCESID</th>
      <th>SurveyYear</th>
      <th>StateABR</th>
      <th>LEAID</th>
      <th>ST_LEAID</th>
      <th>LEAName</th>
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
      <th>Status</th>
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
    LEAName                      0
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
    Status                       0
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
psChar_23.shape
```




    (101390, 77)




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
    LEAName                  0.00
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
    Status                   0.00
    Locale                   0.00
    County                   0.00
    Latitude                 0.00
    Longitude                0.00
    dtype: float64


### Observations

A total of eighteen columns have missing value percentages above forty-five percent. For the 'Grade' columns, this could be explained because this dataset includes schools at various education levels, meaning some schools might not offer certain grade levels. Given this, I would drop the AdultEd column, as this research is focused only on youth sports participation. I would also drop columns 'Phone', 'LEAName', 'LEADID', 'ST_LEAID', 'SurveyYear', 'StaffFTE', 'Member', and 'NCESID', as they are not necessary for analysis. Removing these columns would help declutter the dataset without impacting the research. 
