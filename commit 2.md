## Research Topic

Socioeconomic status (SES) has played a significant role in sports participation rates, as youth with with a lower SES are impacted by disparities regarding injury management, opportunities to be scouted by colleges, and outside training. As sports specicialization becomes increasingly vital for skill development and recruitment, young athletes coming from lower SES families are more likely to be excluded from these opportunities due to financial limitations.  

## Problem Statement

Sports specialization involves year-round training and competition, often through club or Amateur Athletic Union (AAU) participation, in which families are typically responsible for covering expenses such as equipment, uniforms, and particpation and travel fees that can amount to thousands of dollars each year. For families that struggle making these financial committments, their children (typically Black or Hispanic) are unable to receive the same opportunities and benefits as those that are able to particpate. Outside of club sports, children who attend schools with a lower SES often have limited access to appropriate facilities, personnel, or physical education, which could influence participation rate. In which sports are these disparities most apparent, and what is the participation rate difference between white youth athletes and other minority groups?

### Potential Subtopics

- How racial identities or stereotypes can affect how welcomed an athlete feels about participating in certain sports
- Connection between SES and knowledge of sports injury education (ex. concussion education, safety protocols, etc.)

## Data Definition

<b>Nutrition, Physical Activity, and Obesity - Youth Risk Behavior Surveillance System</b>

Last Updated: August 26, 2023

https://catalog.data.gov/dataset/nutrition-physical-activity-and-obesity-youth-risk-behavior-surveillance-system

Conducted by the Centers for Disease Control and Prevention (CDC), the Youth Risk Behavior Surveillance System (YRBSS) monitors health behaviors in middle and high school students nationwide. It collects data regarding physical activity and nutrition, along with geographic and socioeconomic factors. By collecting this data, it could be used to further research on the impact socioeconomic factors have on health behaviors.

### Additional Datasets of Interest

<b>Public School Characteristics 2022-23</b>

Last Updated: October 21, 2024

https://catalog.data.gov/dataset/public-school-characteristics-2022-23-451db

The National Center for Education Statistics (NCES) gathers demographic and geographic data about U.S public schools and factors such as enrollment and Title I status. Further information consists of the percentage of students with free or reduced lunch eligibility. By researching both this dataset and the YRBSS, researchers could analyze patterns between students or schools with a lower SES and the rates of physical activity rates. 



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


```python
path = pd.read_csv('Nutrition__Physical_Activity__and_Obesity_-_Youth_Risk_Behavior_Surveillance_System.csv')
YRBSS_23 = pd.DataFrame(path)
```


```python
path = pd.read_csv('Public_School_Characteristics_2022-23.csv')
psChar_23 = pd.DataFrame(path)
```
