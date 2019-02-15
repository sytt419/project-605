
# title: "Global Terrorism Attacks Project 605"
author: "Jois Xie"


```python
import pathlib
from setuptools import setup

# The directory containing this file
HERE = pathlib.Path(project605).parent

# The text of the README file
README = (HERE / "README.md").read_text()

# This call to setup() does all the work
setup(
    name="realpython-reader",
    version="1.0.0",
    description="Read the latest Real Python tutorials",
    long_description=README,
    long_description_content_type="text/markdown",
    url="https://github.com/realpython/reader",
    author="Real Python",
    author_email="office@realpython.com",
    license="MIT",
    classifiers=[
        "License :: OSI Approved :: MIT License",
        "Programming Language :: Python :: 3",
        "Programming Language :: Python :: 3.7",
    ],
    packages=["reader"],
    include_package_data=True,
    install_requires=["feedparser", "html2text"],
    entry_points={
        "console_scripts": [
            "realpython=reader.__main__:main",
        ]
    },
)

```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-207-e66765f9ee17> in <module>()
          3 
          4 # The directory containing this file
    ----> 5 HERE = pathlib.Path(project605).parent
          6 
          7 # The text of the README file


    NameError: name 'project605' is not defined



```python
## Get the imports out of the way
import pandas as pd
import numpy as np
import datetime as dt
import seaborn as sns

import plotly
import plotly.plotly as py
plotly.tools.set_credentials_file(username='srveale', api_key='GajxMbxLyoAc3R0I6K6e')
import plotly.graph_objs as go
from plotly import tools
# import plotly.offline as py

import matplotlib as mpl
import matplotlib.pyplot as plt
mpl.style.use('ggplot')
import matplotlib.dates as mdates
from matplotlib import dates
from matplotlib.lines import Line2D
from datetime import datetime
import seaborn as sns
```


```python
import os
os.getcwd()
```




    '/Users/siyuxie/Desktop'




```python
os.chdir('/Users/siyuxie/desktop')
```


```python
## Read in the raw data
#raw = pd.read_csv('605project.csv', 'r', encoding='mac_roman')
raw = pd.read_csv("605project.csv", encoding='latin-1')
```

# Q1. What is the trend of total number of terrorists happen each year from 1970 to 2017? Which year has the highest attack?

The total number of terrorists increase from 1970 to 2017, 2014 has the highest number of attacks among those years.


```python
plt.subplots(figsize=(15,6))
sns.countplot('iyear',data=raw,palette='RdYlGn_r',edgecolor=sns.color_palette('dark',7))
plt.xticks(rotation=90)
plt.title('Number Of Terrorist Activities Each Year')
plt.show()
```


![png](output_7_0.png)



```python
terror_region=pd.crosstab(raw.iyear,raw.region_txt)
terror_region.plot(color=sns.color_palette('Set2',12))
fig=plt.gcf()
fig.set_size_inches(18,6)
plt.show()
```


![png](output_8_0.png)



```python
terror_region=pd.crosstab(raw.iyear,raw.weaptype1_txt)
terror_region.plot(color=sns.color_palette('Set2',12))
fig=plt.gcf()
fig.set_size_inches(18,6)
plt.show()
```


![png](output_9_0.png)


# Q1. What amount of total attacks for each country from 1970 to 2017? Which country has the highest number and which country has the lowest?


```python
column_list = raw.columns.values.tolist()
column_list
```




    ['eventid',
     'iyear',
     'imonth',
     'iday',
     'country',
     'country_txt',
     'region',
     'region_txt',
     'provstate',
     'city',
     'latitude',
     'longitude',
     'location',
     'summary',
     'attacktype1_txt',
     'targtype1',
     'targtype1_txt',
     'natlty1',
     'natlty1_txt',
     'gname',
     'motive',
     'weaptype1_txt',
     'weapdetail',
     'propextent_txt',
     'propvalue',
     'propcomment',
     'addnotes',
     'dbsource']




```python
raw['country_txt'].unique()
```




    array(['Dominican Republic', 'Mexico', 'Philippines', 'Greece', 'Japan',
           'United States', 'Uruguay', 'Italy', 'East Germany (GDR)',
           'Ethiopia', 'Guatemala', 'Venezuela', 'West Germany (FRG)',
           'Switzerland', 'Jordan', 'Spain', 'Brazil', 'Egypt', 'Argentina',
           'Lebanon', 'Ireland', 'Turkey', 'Paraguay', 'Iran',
           'United Kingdom', 'Colombia', 'Bolivia', 'Nicaragua',
           'Netherlands', 'Belgium', 'Canada', 'Australia', 'Pakistan',
           'Zambia', 'Sweden', 'Costa Rica', 'South Yemen', 'Cambodia',
           'Israel', 'Poland', 'Taiwan', 'Panama', 'Kuwait',
           'West Bank and Gaza Strip', 'Austria', 'Czechoslovakia', 'India',
           'France', 'South Vietnam', 'Brunei', 'Zaire',
           "People's Republic of the Congo", 'Portugal', 'Algeria',
           'El Salvador', 'Thailand', 'Haiti', 'Sudan', 'Morocco', 'Cyprus',
           'Myanmar', 'Afghanistan', 'Peru', 'Chile', 'Honduras',
           'Yugoslavia', 'Ecuador', 'New Zealand', 'Malaysia', 'Singapore',
           'Botswana', 'Jamaica', 'Chad', 'North Yemen', 'Andorra', 'Syria',
           'South Korea', 'United Arab Emirates', 'South Africa', 'Kenya',
           'Iraq', 'Somalia', 'Tanzania', 'Sri Lanka', 'Namibia', 'Bahamas',
           'Nigeria', 'Barbados', 'Trinidad and Tobago', 'Bangladesh',
           'Angola', 'Mauritania', 'Saudi Arabia', 'Djibouti', 'Indonesia',
           'Malta', 'Rhodesia', 'Soviet Union', 'Denmark', 'Western Sahara',
           'Guyana', 'Mozambique', 'Tunisia', 'Uganda', 'Norway', 'Lesotho',
           'Gabon', 'Libya', 'Bahrain', 'Hong Kong', 'Senegal', 'Zimbabwe',
           'Guinea', 'Grenada', 'New Hebrides', 'Belize', 'Guadeloupe',
           'Martinique', 'Vatican City', 'Albania',
           'Central African Republic', 'Seychelles', 'Dominica', 'Qatar',
           'Bulgaria', 'Suriname', 'Swaziland', 'Luxembourg', 'Iceland',
           'French Guiana', 'Falkland Islands', 'Burkina Faso',
           'New Caledonia', 'Romania', 'Niger', 'Nepal', 'Togo', 'Finland',
           'Fiji', 'Ghana', 'Maldives', 'Mauritius', 'Hungary', 'Laos',
           'Papua New Guinea', 'China', 'Liberia', 'Republic of the Congo',
           'Mali', 'Germany', 'Yemen', 'Rwanda', 'Sierra Leone', 'Cameroon',
           'Cuba', 'Croatia', 'Georgia', 'Azerbaijan', 'Madagascar',
           'Lithuania', 'Burundi', 'Ukraine', 'Moldova', 'Armenia', 'Russia',
           'Ivory Coast', 'Kazakhstan', 'Antigua and Barbuda',
           'Bosnia-Herzegovina', 'Equatorial Guinea', 'Tajikistan', 'Malawi',
           'Uzbekistan', 'Latvia', 'Estonia', 'Vietnam', 'Comoros', 'Benin',
           'Slovak Republic', 'Macedonia', 'Wallis and Futuna', 'Belarus',
           'Czech Republic', 'Slovenia', 'Gambia', 'North Korea', 'Eritrea',
           'St. Kitts and Nevis', 'French Polynesia', 'Macau', 'Kyrgyzstan',
           'Vanuatu', 'Democratic Republic of the Congo', 'Kosovo',
           'Solomon Islands', 'East Timor', 'St. Lucia', 'Guinea-Bissau',
           'Montenegro', 'International', 'Turkmenistan', 'Serbia-Montenegro',
           'Bhutan', 'Serbia', 'South Sudan'], dtype=object)




```python
# for american countries
america = raw[raw.country_txt == 'United States']
america
#america <- subset(raw, Product = p.id & Month < mn & Year == yr, select = c(Time, Product))
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
      <th>eventid</th>
      <th>iyear</th>
      <th>imonth</th>
      <th>iday</th>
      <th>country</th>
      <th>country_txt</th>
      <th>region</th>
      <th>region_txt</th>
      <th>provstate</th>
      <th>city</th>
      <th>...</th>
      <th>natlty1_txt</th>
      <th>gname</th>
      <th>motive</th>
      <th>weaptype1_txt</th>
      <th>weapdetail</th>
      <th>propextent_txt</th>
      <th>propvalue</th>
      <th>propcomment</th>
      <th>addnotes</th>
      <th>dbsource</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>5</th>
      <td>1.970010e+11</td>
      <td>1970</td>
      <td>1</td>
      <td>1</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>Illinois</td>
      <td>Cairo</td>
      <td>...</td>
      <td>United States</td>
      <td>Black Nationalists</td>
      <td>To protest the Cairo Illinois Police Deparment</td>
      <td>Firearms</td>
      <td>Several gunshots were fired.</td>
      <td>Minor (likely &lt; $1 million)</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>The Cairo Chief of Police, William Petersen, r...</td>
      <td>Hewitt Project</td>
    </tr>
    <tr>
      <th>7</th>
      <td>1.970010e+11</td>
      <td>1970</td>
      <td>1</td>
      <td>2</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>California</td>
      <td>Oakland</td>
      <td>...</td>
      <td>United States</td>
      <td>Unknown</td>
      <td>NaN</td>
      <td>Explosives</td>
      <td>NaN</td>
      <td>Minor (likely &lt; $1 million)</td>
      <td>22500.0</td>
      <td>Three transformers were damaged.</td>
      <td>Damages were estimated to be between $20,000-$...</td>
      <td>Hewitt Project</td>
    </tr>
    <tr>
      <th>8</th>
      <td>1.970010e+11</td>
      <td>1970</td>
      <td>1</td>
      <td>2</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>Wisconsin</td>
      <td>Madison</td>
      <td>...</td>
      <td>United States</td>
      <td>New Year's Gang</td>
      <td>To protest the War in Vietnam and the draft</td>
      <td>Incendiary</td>
      <td>Firebomb consisting of gasoline</td>
      <td>Minor (likely &lt; $1 million)</td>
      <td>60000.0</td>
      <td>Basketball courts, weight room, swimming pool,...</td>
      <td>The New Years Gang issue a communiqu to a loc...</td>
      <td>Hewitt Project</td>
    </tr>
    <tr>
      <th>9</th>
      <td>1.970010e+11</td>
      <td>1970</td>
      <td>1</td>
      <td>3</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>Wisconsin</td>
      <td>Madison</td>
      <td>...</td>
      <td>United States</td>
      <td>New Year's Gang</td>
      <td>To protest the War in Vietnam and the draft</td>
      <td>Incendiary</td>
      <td>Poured gasoline on the floor and lit it with a...</td>
      <td>Minor (likely &lt; $1 million)</td>
      <td>NaN</td>
      <td>Slight damage</td>
      <td>Karl Armstrong's girlfriend, Lynn Schultz, dro...</td>
      <td>Hewitt Project</td>
    </tr>
    <tr>
      <th>10</th>
      <td>1.970010e+11</td>
      <td>1970</td>
      <td>1</td>
      <td>1</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>Wisconsin</td>
      <td>Baraboo</td>
      <td>...</td>
      <td>United States</td>
      <td>Weather Underground, Weathermen</td>
      <td>NaN</td>
      <td>Explosives</td>
      <td>Explosive</td>
      <td>Minor (likely &lt; $1 million)</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PGIS</td>
    </tr>
    <tr>
      <th>11</th>
      <td>1.970010e+11</td>
      <td>1970</td>
      <td>1</td>
      <td>6</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>Colorado</td>
      <td>Denver</td>
      <td>...</td>
      <td>United States</td>
      <td>Left-Wing Militants</td>
      <td>Protest the draft and Vietnam War</td>
      <td>Incendiary</td>
      <td>Molotov cocktail</td>
      <td>Minor (likely &lt; $1 million)</td>
      <td>305.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Hewitt Project</td>
    </tr>
    <tr>
      <th>13</th>
      <td>1.970010e+11</td>
      <td>1970</td>
      <td>1</td>
      <td>9</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>Michigan</td>
      <td>Detroit</td>
      <td>...</td>
      <td>United States</td>
      <td>Left-Wing Militants</td>
      <td>NaN</td>
      <td>Incendiary</td>
      <td>Firebomb</td>
      <td>Minor (likely &lt; $1 million)</td>
      <td>NaN</td>
      <td>Building was damaged</td>
      <td>NaN</td>
      <td>Hewitt Project</td>
    </tr>
    <tr>
      <th>14</th>
      <td>1.970010e+11</td>
      <td>1970</td>
      <td>1</td>
      <td>9</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>Puerto Rico</td>
      <td>Rio Piedras</td>
      <td>...</td>
      <td>United States</td>
      <td>Armed Commandos of Liberation</td>
      <td>To protest United States owned businesses in P...</td>
      <td>Incendiary</td>
      <td>Fire set in back of store</td>
      <td>Major (likely &gt;= $1 million but &lt; $1 billion)</td>
      <td>2000000.0</td>
      <td>Store destroyed</td>
      <td>The fire began at 8:30 PM. The Armed Commandos...</td>
      <td>Hewitt Project</td>
    </tr>
    <tr>
      <th>17</th>
      <td>1.970010e+11</td>
      <td>1970</td>
      <td>1</td>
      <td>12</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>New York</td>
      <td>New York City</td>
      <td>...</td>
      <td>United States</td>
      <td>Black Nationalists</td>
      <td>Suspected motives were to protest the Vietnam ...</td>
      <td>Explosives</td>
      <td>Crudely made pipe bomb.  Five inches long and ...</td>
      <td>Minor (likely &lt; $1 million)</td>
      <td>NaN</td>
      <td>Damaged a blackboard and shattered a pane of g...</td>
      <td>One half hour after the bomb explosion, an ano...</td>
      <td>Hewitt Project</td>
    </tr>
    <tr>
      <th>18</th>
      <td>1.970010e+11</td>
      <td>1970</td>
      <td>1</td>
      <td>12</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>Puerto Rico</td>
      <td>Rio Grande</td>
      <td>...</td>
      <td>United States</td>
      <td>Strikers</td>
      <td>NaN</td>
      <td>Explosives</td>
      <td>Bomb</td>
      <td>Unknown</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Hewitt Project</td>
    </tr>
    <tr>
      <th>19</th>
      <td>1.970010e+11</td>
      <td>1970</td>
      <td>1</td>
      <td>13</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>Washington</td>
      <td>Seattle</td>
      <td>...</td>
      <td>United States</td>
      <td>Black Nationalists</td>
      <td>Retaliation for the store owner who shot and k...</td>
      <td>Incendiary</td>
      <td>Firebomb</td>
      <td>Minor (likely &lt; $1 million)</td>
      <td>17000.0</td>
      <td>NaN</td>
      <td>The store was a White owned business operating...</td>
      <td>Hewitt Project</td>
    </tr>
    <tr>
      <th>20</th>
      <td>1.970010e+11</td>
      <td>1970</td>
      <td>1</td>
      <td>14</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>Illinois</td>
      <td>Champaign</td>
      <td>...</td>
      <td>United States</td>
      <td>Black Nationalists</td>
      <td>NaN</td>
      <td>Incendiary</td>
      <td>Firebomb thrown through window</td>
      <td>Minor (likely &lt; $1 million)</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Hewitt Project</td>
    </tr>
    <tr>
      <th>22</th>
      <td>1.970010e+11</td>
      <td>1970</td>
      <td>1</td>
      <td>19</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>Washington</td>
      <td>Seattle</td>
      <td>...</td>
      <td>United States</td>
      <td>Black Nationalists</td>
      <td>The incident took place during disturbances be...</td>
      <td>Explosives</td>
      <td>NaN</td>
      <td>Minor (likely &lt; $1 million)</td>
      <td>2200.0</td>
      <td>Windows were shattered at the Liberal Arts and...</td>
      <td>Witnesses observed three African American male...</td>
      <td>Hewitt Project</td>
    </tr>
    <tr>
      <th>23</th>
      <td>1.970010e+11</td>
      <td>1970</td>
      <td>1</td>
      <td>19</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>Washington</td>
      <td>Seattle</td>
      <td>...</td>
      <td>United States</td>
      <td>Student Radicals</td>
      <td>The incident took place during heightened anti...</td>
      <td>Explosives</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Judith and Silas Bissell were both members of ...</td>
      <td>Hewitt Project</td>
    </tr>
    <tr>
      <th>24</th>
      <td>1.970010e+11</td>
      <td>1970</td>
      <td>1</td>
      <td>19</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>New Jersey</td>
      <td>Jersey City</td>
      <td>...</td>
      <td>United States</td>
      <td>White extremists</td>
      <td>Intimidate the Black Panther Party.</td>
      <td>Incendiary</td>
      <td>Gasoline was placed on the steps of the buildi...</td>
      <td>Minor (likely &lt; $1 million)</td>
      <td>NaN</td>
      <td>The fire caused minor damages to the door and ...</td>
      <td>The building might have been shot at a second ...</td>
      <td>Hewitt Project</td>
    </tr>
    <tr>
      <th>28</th>
      <td>1.970010e+11</td>
      <td>1970</td>
      <td>1</td>
      <td>22</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>Nebraska</td>
      <td>South Sioux City</td>
      <td>...</td>
      <td>United States</td>
      <td>Strikers</td>
      <td>The attack occurred during the violent Iowa Be...</td>
      <td>Explosives</td>
      <td>Dynamite thrown at foundation of home</td>
      <td>Minor (likely &lt; $1 million)</td>
      <td>NaN</td>
      <td>Sizable hole in the house and broken windows</td>
      <td>This attack might be linked with other episode...</td>
      <td>Hewitt Project</td>
    </tr>
    <tr>
      <th>29</th>
      <td>1.970010e+11</td>
      <td>1970</td>
      <td>1</td>
      <td>25</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>Mississippi</td>
      <td>West Point</td>
      <td>...</td>
      <td>United States</td>
      <td>White extremists</td>
      <td>The motive of the attack was to prevent the Af...</td>
      <td>Incendiary</td>
      <td>NaN</td>
      <td>Minor (likely &lt; $1 million)</td>
      <td>NaN</td>
      <td>Building burnt down</td>
      <td>Police, at the time suspected, that this attac...</td>
      <td>Hewitt Project</td>
    </tr>
    <tr>
      <th>30</th>
      <td>1.970010e+11</td>
      <td>1970</td>
      <td>1</td>
      <td>25</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>New York</td>
      <td>New York City</td>
      <td>...</td>
      <td>United States</td>
      <td>Black Nationalists</td>
      <td>To kill police</td>
      <td>Firearms</td>
      <td>Nine thirty-caliber cartridges from a carbine ...</td>
      <td>Minor (likely &lt; $1 million)</td>
      <td>NaN</td>
      <td>One window in a building shattered</td>
      <td>Police do not believe that this attack was rel...</td>
      <td>Hewitt Project</td>
    </tr>
    <tr>
      <th>31</th>
      <td>1.970010e+11</td>
      <td>1970</td>
      <td>1</td>
      <td>26</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>Mississippi</td>
      <td>West Point</td>
      <td>...</td>
      <td>United States</td>
      <td>Black Nationalists</td>
      <td>African American opposition to the school inte...</td>
      <td>Explosives</td>
      <td>Several sticks of dynamite were thrown, from a...</td>
      <td>Minor (likely &lt; $1 million)</td>
      <td>NaN</td>
      <td>Windows shattered</td>
      <td>Police, at the time, suspected that this attac...</td>
      <td>Hewitt Project</td>
    </tr>
    <tr>
      <th>32</th>
      <td>1.970010e+11</td>
      <td>1970</td>
      <td>1</td>
      <td>26</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>New York</td>
      <td>New York City</td>
      <td>...</td>
      <td>United States</td>
      <td>Black Nationalists</td>
      <td>To kill police</td>
      <td>Firearms</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Police do not believe that this attack was rel...</td>
      <td>Hewitt Project</td>
    </tr>
    <tr>
      <th>33</th>
      <td>1.970010e+11</td>
      <td>1970</td>
      <td>1</td>
      <td>27</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>Ohio</td>
      <td>Norwalk</td>
      <td>...</td>
      <td>United States</td>
      <td>Left-Wing Militants</td>
      <td>Protest and sabotage the draft</td>
      <td>Incendiary</td>
      <td>NaN</td>
      <td>Minor (likely &lt; $1 million)</td>
      <td>8800.0</td>
      <td>Smoke damage</td>
      <td>The perpetrators broke through the door of the...</td>
      <td>Hewitt Project</td>
    </tr>
    <tr>
      <th>35</th>
      <td>1.970010e+11</td>
      <td>1970</td>
      <td>1</td>
      <td>28</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>Washington</td>
      <td>Seattle</td>
      <td>...</td>
      <td>United States</td>
      <td>White extremists</td>
      <td>NaN</td>
      <td>Explosives</td>
      <td>NaN</td>
      <td>Minor (likely &lt; $1 million)</td>
      <td>3000.0</td>
      <td>Small hole in the door</td>
      <td>NaN</td>
      <td>Hewitt Project</td>
    </tr>
    <tr>
      <th>36</th>
      <td>1.970010e+11</td>
      <td>1970</td>
      <td>1</td>
      <td>30</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>Nebraska</td>
      <td>South Sioux City</td>
      <td>...</td>
      <td>United States</td>
      <td>Strikers</td>
      <td>The attack occurred during the violent Iowa Be...</td>
      <td>Explosives</td>
      <td>Dynamite</td>
      <td>Minor (likely &lt; $1 million)</td>
      <td>NaN</td>
      <td>Damaged foundation of building</td>
      <td>This incident might be part of a multiple atta...</td>
      <td>Hewitt Project</td>
    </tr>
    <tr>
      <th>37</th>
      <td>1.970010e+11</td>
      <td>1970</td>
      <td>1</td>
      <td>30</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>Nebraska</td>
      <td>South Sioux City</td>
      <td>...</td>
      <td>United States</td>
      <td>Strikers</td>
      <td>The attack occurred during the violent Iowa Be...</td>
      <td>Explosives</td>
      <td>Dynamite</td>
      <td>Minor (likely &lt; $1 million)</td>
      <td>2500.0</td>
      <td>NaN</td>
      <td>This incident might be part of a multiple atta...</td>
      <td>Hewitt Project</td>
    </tr>
    <tr>
      <th>38</th>
      <td>1.970010e+11</td>
      <td>1970</td>
      <td>1</td>
      <td>30</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>Florida</td>
      <td>Coral Gables</td>
      <td>...</td>
      <td>United States</td>
      <td>Student Radicals</td>
      <td>To protest the R.O.T.C. program and the War in...</td>
      <td>Incendiary</td>
      <td>Two firebombs ignited, at least one of them wa...</td>
      <td>Minor (likely &lt; $1 million)</td>
      <td>NaN</td>
      <td>Army personnel carrier was damaged</td>
      <td>NaN</td>
      <td>Hewitt Project</td>
    </tr>
    <tr>
      <th>40</th>
      <td>1.970010e+11</td>
      <td>1970</td>
      <td>1</td>
      <td>31</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>Colorado</td>
      <td>Denver</td>
      <td>...</td>
      <td>United States</td>
      <td>Unknown</td>
      <td>NaN</td>
      <td>Explosives</td>
      <td>Suspected use of dynamite</td>
      <td>Minor (likely &lt; $1 million)</td>
      <td>NaN</td>
      <td>Restroom damaged</td>
      <td>NaN</td>
      <td>Hewitt Project</td>
    </tr>
    <tr>
      <th>41</th>
      <td>1.970020e+11</td>
      <td>1970</td>
      <td>2</td>
      <td>1</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>Oregon</td>
      <td>Portland</td>
      <td>...</td>
      <td>United States</td>
      <td>Left-Wing Militants</td>
      <td>Protest and sabotage the draft</td>
      <td>Incendiary</td>
      <td>Fire started with gasoline</td>
      <td>Minor (likely &lt; $1 million)</td>
      <td>4189.0</td>
      <td>Approximately two hundred and fifty draft reco...</td>
      <td>It is suspected that the perpetrator was attem...</td>
      <td>Hewitt Project</td>
    </tr>
    <tr>
      <th>42</th>
      <td>1.970020e+11</td>
      <td>1970</td>
      <td>2</td>
      <td>1</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>Illinois</td>
      <td>Cairo</td>
      <td>...</td>
      <td>United States</td>
      <td>Black Nationalists</td>
      <td>To protest police presence in Pyramid Courts</td>
      <td>Firearms</td>
      <td>High-powered rifle or carbine</td>
      <td>Minor (likely &lt; $1 million)</td>
      <td>NaN</td>
      <td>Windshield of police car shattered</td>
      <td>This attack took place during heightened racia...</td>
      <td>Hewitt Project</td>
    </tr>
    <tr>
      <th>43</th>
      <td>1.970020e+11</td>
      <td>1970</td>
      <td>2</td>
      <td>2</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>New York</td>
      <td>New York City</td>
      <td>...</td>
      <td>United States</td>
      <td>Unknown</td>
      <td>NaN</td>
      <td>Incendiary</td>
      <td>Incendiary device</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Hewitt Project</td>
    </tr>
    <tr>
      <th>44</th>
      <td>1.970020e+11</td>
      <td>1970</td>
      <td>2</td>
      <td>3</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>New York</td>
      <td>New York City</td>
      <td>...</td>
      <td>United States</td>
      <td>Unknown</td>
      <td>NaN</td>
      <td>Incendiary</td>
      <td>Incendiary device packed in a cigarette box th...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Part of a multiple attack with 197002030002.  ...</td>
      <td>Hewitt Project</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>175737</th>
      <td>2.017060e+11</td>
      <td>2017</td>
      <td>6</td>
      <td>9</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>New York</td>
      <td>New York City</td>
      <td>...</td>
      <td>United States</td>
      <td>Anti-Muslim extremists</td>
      <td>NaN</td>
      <td>Firearms</td>
      <td>A pellet gun was used in the attack.</td>
      <td>Minor (likely &lt; $1 million)</td>
      <td>-99.0</td>
      <td>A window was damaged in this attack.</td>
      <td>The victims included Mahamadou Gumaneh.</td>
      <td>START Primary Collection</td>
    </tr>
    <tr>
      <th>175914</th>
      <td>2.017060e+11</td>
      <td>2017</td>
      <td>6</td>
      <td>14</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>Virginia</td>
      <td>Alexandria</td>
      <td>...</td>
      <td>United States</td>
      <td>Anti-Republican extremists</td>
      <td>The specific motive is unknown; however, sourc...</td>
      <td>Firearms</td>
      <td>A 7.62-mm SKS semiautomatic rifle and a 9-mm h...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>The victims included David Bailey, Crystal Gri...</td>
      <td>START Primary Collection</td>
    </tr>
    <tr>
      <th>176194</th>
      <td>2.017060e+11</td>
      <td>2017</td>
      <td>6</td>
      <td>21</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>Michigan</td>
      <td>Flint</td>
      <td>...</td>
      <td>United States</td>
      <td>Anti-Government extremists</td>
      <td>An unaffiliated individual, identified as Amor...</td>
      <td>Melee</td>
      <td>A 12-inch knife was used in the attack.</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>START Primary Collection</td>
    </tr>
    <tr>
      <th>176364</th>
      <td>2.017060e+11</td>
      <td>2017</td>
      <td>6</td>
      <td>26</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>New York</td>
      <td>New York City</td>
      <td>...</td>
      <td>United States</td>
      <td>Anti-Semitic extremists</td>
      <td>The specific motive is unknown; however, sourc...</td>
      <td>Incendiary</td>
      <td>NaN</td>
      <td>Minor (likely &lt; $1 million)</td>
      <td>-99.0</td>
      <td>A bus was damaged in this attack.</td>
      <td>NaN</td>
      <td>START Primary Collection</td>
    </tr>
    <tr>
      <th>176685</th>
      <td>2.017070e+11</td>
      <td>2017</td>
      <td>7</td>
      <td>5</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>New York</td>
      <td>Bronx</td>
      <td>...</td>
      <td>United States</td>
      <td>Anti-Police extremists</td>
      <td>The specific motive is unknown; however, sourc...</td>
      <td>Firearms</td>
      <td>A Ruger .38 revolver was used in the attack.</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>There is doubt that this incident meets terror...</td>
      <td>START Primary Collection</td>
    </tr>
    <tr>
      <th>176735</th>
      <td>2.017070e+11</td>
      <td>2017</td>
      <td>7</td>
      <td>7</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>Texas</td>
      <td>Dallas</td>
      <td>...</td>
      <td>United States</td>
      <td>Anti-LGBT extremists</td>
      <td>NaN</td>
      <td>Incendiary</td>
      <td>NaN</td>
      <td>Minor (likely &lt; $1 million)</td>
      <td>-99.0</td>
      <td>An LGBT community resource center was damaged ...</td>
      <td>NaN</td>
      <td>START Primary Collection</td>
    </tr>
    <tr>
      <th>176758</th>
      <td>2.017070e+11</td>
      <td>2017</td>
      <td>7</td>
      <td>8</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>Indiana</td>
      <td>Columbus</td>
      <td>...</td>
      <td>United States</td>
      <td>Unknown</td>
      <td>NaN</td>
      <td>Incendiary</td>
      <td>NaN</td>
      <td>Minor (likely &lt; $1 million)</td>
      <td>-99.0</td>
      <td>A church was damaged in this attack.</td>
      <td>NaN</td>
      <td>START Primary Collection</td>
    </tr>
    <tr>
      <th>176804</th>
      <td>2.017070e+11</td>
      <td>2017</td>
      <td>7</td>
      <td>9</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>Pennsylvania</td>
      <td>Campbelltown</td>
      <td>...</td>
      <td>United States</td>
      <td>Environmentalists</td>
      <td>NaN</td>
      <td>Incendiary</td>
      <td>NaN</td>
      <td>Minor (likely &lt; $1 million)</td>
      <td>-99.0</td>
      <td>A portable toilet was damaged in this attack.</td>
      <td>NaN</td>
      <td>START Primary Collection</td>
    </tr>
    <tr>
      <th>176949</th>
      <td>2.017070e+11</td>
      <td>2017</td>
      <td>7</td>
      <td>13</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>Pennsylvania</td>
      <td>Campbelltown</td>
      <td>...</td>
      <td>United States</td>
      <td>Environmentalists</td>
      <td>NaN</td>
      <td>Incendiary</td>
      <td>NaN</td>
      <td>Minor (likely &lt; $1 million)</td>
      <td>-99.0</td>
      <td>A portable toilet was damaged in this attack.</td>
      <td>NaN</td>
      <td>START Primary Collection</td>
    </tr>
    <tr>
      <th>177647</th>
      <td>2.017080e+11</td>
      <td>2017</td>
      <td>8</td>
      <td>4</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>Missouri</td>
      <td>Kansas City</td>
      <td>...</td>
      <td>United States</td>
      <td>Unknown</td>
      <td>NaN</td>
      <td>Chemical</td>
      <td>An unidentified toxic substance, which smelled...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>START Primary Collection</td>
    </tr>
    <tr>
      <th>177655</th>
      <td>2.017080e+11</td>
      <td>2017</td>
      <td>8</td>
      <td>5</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>Minnesota</td>
      <td>Bloomington</td>
      <td>...</td>
      <td>United States</td>
      <td>White Rabbit Three Percent Illinois Patriot Fr...</td>
      <td>NaN</td>
      <td>Explosives</td>
      <td>A PVC pipe bomb containing black powder and di...</td>
      <td>Minor (likely &lt; $1 million)</td>
      <td>-99.0</td>
      <td>An Islamic center was damaged in this attack.</td>
      <td>NaN</td>
      <td>START Primary Collection</td>
    </tr>
    <tr>
      <th>177863</th>
      <td>2.017080e+11</td>
      <td>2017</td>
      <td>8</td>
      <td>12</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>Virginia</td>
      <td>Charlottesville</td>
      <td>...</td>
      <td>United States</td>
      <td>Neo-Nazi extremists</td>
      <td>NaN</td>
      <td>Vehicle (not to include vehicle-borne explosiv...</td>
      <td>A silver Dodge Challenger was used in the attack.</td>
      <td>Minor (likely &lt; $1 million)</td>
      <td>-99.0</td>
      <td>A vehicle was damaged in this attack.</td>
      <td>NaN</td>
      <td>START Primary Collection</td>
    </tr>
    <tr>
      <th>178079</th>
      <td>2.017080e+11</td>
      <td>2017</td>
      <td>8</td>
      <td>19</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>Texas</td>
      <td>Houston</td>
      <td>...</td>
      <td>United States</td>
      <td>Unknown</td>
      <td>The specific motive is unknown; however, sourc...</td>
      <td>Explosives</td>
      <td>A homemade explosive device was used in the at...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>START Primary Collection</td>
    </tr>
    <tr>
      <th>178776</th>
      <td>2.017090e+11</td>
      <td>2017</td>
      <td>9</td>
      <td>11</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>Louisiana</td>
      <td>Baton Rouge</td>
      <td>...</td>
      <td>United States</td>
      <td>White extremists</td>
      <td>The specific motive is unknown; however, sourc...</td>
      <td>Firearms</td>
      <td>NaN</td>
      <td>Minor (likely &lt; $1 million)</td>
      <td>-99.0</td>
      <td>A door and a window were damaged in this attack.</td>
      <td>Gleeson was charged with two similar incidents...</td>
      <td>START Primary Collection</td>
    </tr>
    <tr>
      <th>178798</th>
      <td>2.017090e+11</td>
      <td>2017</td>
      <td>9</td>
      <td>12</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>Louisiana</td>
      <td>Baton Rouge</td>
      <td>...</td>
      <td>United States</td>
      <td>White extremists</td>
      <td>The specific motive is unknown; however, sourc...</td>
      <td>Firearms</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Gleeson was charged with two similar incidents...</td>
      <td>START Primary Collection</td>
    </tr>
    <tr>
      <th>178858</th>
      <td>2.017090e+11</td>
      <td>2017</td>
      <td>9</td>
      <td>14</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>Louisiana</td>
      <td>Baton Rouge</td>
      <td>...</td>
      <td>United States</td>
      <td>White extremists</td>
      <td>The specific motive is unknown; however, sourc...</td>
      <td>Firearms</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Gleeson was charged with two similar incidents...</td>
      <td>START Primary Collection</td>
    </tr>
    <tr>
      <th>179098</th>
      <td>2.017090e+11</td>
      <td>2017</td>
      <td>9</td>
      <td>24</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>Tennessee</td>
      <td>Antioch</td>
      <td>...</td>
      <td>United States</td>
      <td>Unknown</td>
      <td>An unaffiliated individual, identified as Eman...</td>
      <td>Firearms</td>
      <td>A pistol was used in the attack.</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>The victims included Melanie Smith, Robert Eng...</td>
      <td>START Primary Collection</td>
    </tr>
    <tr>
      <th>179344</th>
      <td>2.017100e+11</td>
      <td>2017</td>
      <td>10</td>
      <td>1</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>Nevada</td>
      <td>Las Vegas</td>
      <td>...</td>
      <td>United States</td>
      <td>Anti-Government extremists</td>
      <td>NaN</td>
      <td>Firearms</td>
      <td>AR-15 semiautomatic rifles equipped with bump ...</td>
      <td>Unknown</td>
      <td>-99.0</td>
      <td>A hotel window and other unspecified property ...</td>
      <td>Amaq News Agency, the Islamic State of Iraq an...</td>
      <td>START Primary Collection</td>
    </tr>
    <tr>
      <th>179474</th>
      <td>2.017100e+11</td>
      <td>2017</td>
      <td>10</td>
      <td>6</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>North Carolina</td>
      <td>Fletcher</td>
      <td>...</td>
      <td>United States</td>
      <td>Unknown</td>
      <td>An unaffiliated individual, identified as Mich...</td>
      <td>Explosives</td>
      <td>A timed homemade explosive device containing a...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>START Primary Collection</td>
    </tr>
    <tr>
      <th>179522</th>
      <td>2.017100e+11</td>
      <td>2017</td>
      <td>10</td>
      <td>8</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>Washington</td>
      <td>Spokane</td>
      <td>...</td>
      <td>United States</td>
      <td>White extremists</td>
      <td>Two unaffiliated individuals, identified as Ja...</td>
      <td>Firearms</td>
      <td>A pistol was used in the attack.</td>
      <td>Minor (likely &lt; $1 million)</td>
      <td>-99.0</td>
      <td>A house was damaged in this attack.</td>
      <td>NaN</td>
      <td>START Primary Collection</td>
    </tr>
    <tr>
      <th>179912</th>
      <td>2.017100e+11</td>
      <td>2017</td>
      <td>10</td>
      <td>22</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>Nebraska</td>
      <td>Oxford</td>
      <td>...</td>
      <td>United States</td>
      <td>White extremists</td>
      <td>The specific motive is unknown; however, sourc...</td>
      <td>Firearms</td>
      <td>A .38-caliber handgun and a knife were used in...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>START Primary Collection</td>
    </tr>
    <tr>
      <th>180052</th>
      <td>2.017100e+11</td>
      <td>2017</td>
      <td>10</td>
      <td>28</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>Puerto Rico</td>
      <td>San Juan</td>
      <td>...</td>
      <td>United States</td>
      <td>Anti-LGBT extremists</td>
      <td>NaN</td>
      <td>Incendiary</td>
      <td>Petrol bombs were used in the attack.</td>
      <td>Minor (likely &lt; $1 million)</td>
      <td>-99.0</td>
      <td>A bar was damaged in this attack.</td>
      <td>There is doubt that this incident meets terror...</td>
      <td>START Primary Collection</td>
    </tr>
    <tr>
      <th>180118</th>
      <td>2.017100e+11</td>
      <td>2017</td>
      <td>10</td>
      <td>31</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>New York</td>
      <td>New York City</td>
      <td>...</td>
      <td>Argentina</td>
      <td>Jihadi-inspired extremists</td>
      <td>An unaffiliated individual, identified as Sayf...</td>
      <td>Vehicle (not to include vehicle-borne explosiv...</td>
      <td>A rental pickup truck and replica firearms wer...</td>
      <td>Minor (likely &lt; $1 million)</td>
      <td>-99.0</td>
      <td>A school bus was damaged in this attack.</td>
      <td>The victims included tourists from Argentina a...</td>
      <td>START Primary Collection</td>
    </tr>
    <tr>
      <th>180135</th>
      <td>2.017100e+11</td>
      <td>2017</td>
      <td>10</td>
      <td>31</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>Louisiana</td>
      <td>Richland Parish</td>
      <td>...</td>
      <td>United States</td>
      <td>White extremists</td>
      <td>NaN</td>
      <td>Incendiary</td>
      <td>Gasoline was used in the attack.</td>
      <td>Minor (likely &lt; $1 million)</td>
      <td>-99.0</td>
      <td>A church was damaged in this attack.</td>
      <td>NaN</td>
      <td>START Primary Collection</td>
    </tr>
    <tr>
      <th>180304</th>
      <td>2.017110e+11</td>
      <td>2017</td>
      <td>11</td>
      <td>7</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>Illinois</td>
      <td>Champaign</td>
      <td>...</td>
      <td>United States</td>
      <td>White Rabbit Three Percent Illinois Patriot Fr...</td>
      <td>NaN</td>
      <td>Explosives</td>
      <td>A PVC pipe bomb containing thermite and a magn...</td>
      <td>Minor (likely &lt; $1 million)</td>
      <td>-99.0</td>
      <td>A window was damaged in this attack.</td>
      <td>NaN</td>
      <td>START Primary Collection</td>
    </tr>
    <tr>
      <th>180461</th>
      <td>2.017110e+11</td>
      <td>2017</td>
      <td>11</td>
      <td>13</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>North Carolina</td>
      <td>Vale</td>
      <td>...</td>
      <td>United States</td>
      <td>Pro-LGBT Rights extremists</td>
      <td>Pro-LGBT Rights extremists claimed responsibil...</td>
      <td>Incendiary</td>
      <td>NaN</td>
      <td>Minor (likely &lt; $1 million)</td>
      <td>-99.0</td>
      <td>A church was damaged in this attack.</td>
      <td>NaN</td>
      <td>START Primary Collection</td>
    </tr>
    <tr>
      <th>181141</th>
      <td>2.017120e+11</td>
      <td>2017</td>
      <td>12</td>
      <td>7</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>New Mexico</td>
      <td>Aztec</td>
      <td>...</td>
      <td>United States</td>
      <td>White extremists</td>
      <td>An unaffiliated individual, identified as Will...</td>
      <td>Firearms</td>
      <td>A 9-mm Glock handgun was used in the attack.</td>
      <td>Minor (likely &lt; $1 million)</td>
      <td>-99.0</td>
      <td>A classroom wall was damaged in this attack.</td>
      <td>The victims included students Casey Jordan Mar...</td>
      <td>START Primary Collection</td>
    </tr>
    <tr>
      <th>181219</th>
      <td>2.017120e+11</td>
      <td>2017</td>
      <td>12</td>
      <td>11</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>New York</td>
      <td>New York City</td>
      <td>...</td>
      <td>United States</td>
      <td>Jihadi-inspired extremists</td>
      <td>An unaffiliated individual, identified as Akay...</td>
      <td>Explosives</td>
      <td>A crude pipe bomb consisting of screws,  Chris...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>START Primary Collection</td>
    </tr>
    <tr>
      <th>181478</th>
      <td>2.017120e+11</td>
      <td>2017</td>
      <td>12</td>
      <td>22</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>Pennsylvania</td>
      <td>Harrisburg</td>
      <td>...</td>
      <td>United States</td>
      <td>Unknown</td>
      <td>NaN</td>
      <td>Firearms</td>
      <td>Two 9-mm handguns were used in the attack.</td>
      <td>Minor (likely &lt; $1 million)</td>
      <td>-99.0</td>
      <td>A vehicle was damaged in this attack.</td>
      <td>There is doubt that this incident meets terror...</td>
      <td>START Primary Collection</td>
    </tr>
    <tr>
      <th>181479</th>
      <td>2.017120e+11</td>
      <td>2017</td>
      <td>12</td>
      <td>22</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>Pennsylvania</td>
      <td>Harrisburg</td>
      <td>...</td>
      <td>United States</td>
      <td>Unknown</td>
      <td>NaN</td>
      <td>Firearms</td>
      <td>Two 9-mm handguns were used in the attack.</td>
      <td>Minor (likely &lt; $1 million)</td>
      <td>-99.0</td>
      <td>A vehicle was damaged in this attack.</td>
      <td>There is doubt that this incident meets terror...</td>
      <td>START Primary Collection</td>
    </tr>
  </tbody>
</table>
<p>2836 rows × 28 columns</p>
</div>




```python
plt.subplots(figsize=(15,6))
sns.countplot('iyear',data=america,palette='RdYlGn_r',edgecolor=sns.color_palette('dark',7))
plt.xticks(rotation=90)
plt.title('Number Of Terrorist Activities Each Year in United States')
plt.show()
```


![png](output_14_0.png)



```python
raw['weaptype1_txt'].unique()
```




    array(['Unknown', 'Explosives', 'Incendiary', 'Firearms', 'Chemical',
           'Melee', 'Sabotage Equipment',
           'Vehicle (not to include vehicle-borne explosives, i.e., car or truck bombs)',
           'Fake Weapons', 'Radiological', 'Other', 'Biological'],
          dtype=object)




```python
america.head()
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
      <th>eventid</th>
      <th>iyear</th>
      <th>imonth</th>
      <th>iday</th>
      <th>country</th>
      <th>country_txt</th>
      <th>region</th>
      <th>region_txt</th>
      <th>provstate</th>
      <th>city</th>
      <th>...</th>
      <th>natlty1_txt</th>
      <th>gname</th>
      <th>motive</th>
      <th>weaptype1_txt</th>
      <th>weapdetail</th>
      <th>propextent_txt</th>
      <th>propvalue</th>
      <th>propcomment</th>
      <th>addnotes</th>
      <th>dbsource</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>5</th>
      <td>1.970010e+11</td>
      <td>1970</td>
      <td>1</td>
      <td>1</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>Illinois</td>
      <td>Cairo</td>
      <td>...</td>
      <td>United States</td>
      <td>Black Nationalists</td>
      <td>To protest the Cairo Illinois Police Deparment</td>
      <td>Firearms</td>
      <td>Several gunshots were fired.</td>
      <td>Minor (likely &lt; $1 million)</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>The Cairo Chief of Police, William Petersen, r...</td>
      <td>Hewitt Project</td>
    </tr>
    <tr>
      <th>7</th>
      <td>1.970010e+11</td>
      <td>1970</td>
      <td>1</td>
      <td>2</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>California</td>
      <td>Oakland</td>
      <td>...</td>
      <td>United States</td>
      <td>Unknown</td>
      <td>NaN</td>
      <td>Explosives</td>
      <td>NaN</td>
      <td>Minor (likely &lt; $1 million)</td>
      <td>22500.0</td>
      <td>Three transformers were damaged.</td>
      <td>Damages were estimated to be between $20,000-$...</td>
      <td>Hewitt Project</td>
    </tr>
    <tr>
      <th>8</th>
      <td>1.970010e+11</td>
      <td>1970</td>
      <td>1</td>
      <td>2</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>Wisconsin</td>
      <td>Madison</td>
      <td>...</td>
      <td>United States</td>
      <td>New Year's Gang</td>
      <td>To protest the War in Vietnam and the draft</td>
      <td>Incendiary</td>
      <td>Firebomb consisting of gasoline</td>
      <td>Minor (likely &lt; $1 million)</td>
      <td>60000.0</td>
      <td>Basketball courts, weight room, swimming pool,...</td>
      <td>The New Years Gang issue a communiqu to a loc...</td>
      <td>Hewitt Project</td>
    </tr>
    <tr>
      <th>9</th>
      <td>1.970010e+11</td>
      <td>1970</td>
      <td>1</td>
      <td>3</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>Wisconsin</td>
      <td>Madison</td>
      <td>...</td>
      <td>United States</td>
      <td>New Year's Gang</td>
      <td>To protest the War in Vietnam and the draft</td>
      <td>Incendiary</td>
      <td>Poured gasoline on the floor and lit it with a...</td>
      <td>Minor (likely &lt; $1 million)</td>
      <td>NaN</td>
      <td>Slight damage</td>
      <td>Karl Armstrong's girlfriend, Lynn Schultz, dro...</td>
      <td>Hewitt Project</td>
    </tr>
    <tr>
      <th>10</th>
      <td>1.970010e+11</td>
      <td>1970</td>
      <td>1</td>
      <td>1</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>Wisconsin</td>
      <td>Baraboo</td>
      <td>...</td>
      <td>United States</td>
      <td>Weather Underground, Weathermen</td>
      <td>NaN</td>
      <td>Explosives</td>
      <td>Explosive</td>
      <td>Minor (likely &lt; $1 million)</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PGIS</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 28 columns</p>
</div>




```python
america2017 = america[america.iyear == 2017]
america2017['weapon_count'] = america2017.groupby('weaptype1_txt')["weaptype1_txt"].transform('count')
america2017.head()
```

    /Users/siyuxie/anaconda3/lib/python3.7/site-packages/ipykernel_launcher.py:2: SettingWithCopyWarning:
    
    
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
    





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
      <th>eventid</th>
      <th>iyear</th>
      <th>imonth</th>
      <th>iday</th>
      <th>country</th>
      <th>country_txt</th>
      <th>region</th>
      <th>region_txt</th>
      <th>provstate</th>
      <th>city</th>
      <th>...</th>
      <th>gname</th>
      <th>motive</th>
      <th>weaptype1_txt</th>
      <th>weapdetail</th>
      <th>propextent_txt</th>
      <th>propvalue</th>
      <th>propcomment</th>
      <th>addnotes</th>
      <th>dbsource</th>
      <th>weapon_count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>170846</th>
      <td>2.017010e+11</td>
      <td>2017</td>
      <td>1</td>
      <td>2</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>Illinois</td>
      <td>Chicago</td>
      <td>...</td>
      <td>Anti-White extremists</td>
      <td>The specific motive is unknown; however, sourc...</td>
      <td>Melee</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>START Primary Collection</td>
      <td>7</td>
    </tr>
    <tr>
      <th>170951</th>
      <td>2.017010e+11</td>
      <td>2017</td>
      <td>1</td>
      <td>6</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>Florida</td>
      <td>Fort Lauderdale</td>
      <td>...</td>
      <td>Jihadi-inspired extremists</td>
      <td>An unaffiliated individual, identified as Este...</td>
      <td>Firearms</td>
      <td>A 9-mm pistol was used in the attack.</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Casualty numbers conflict across sources. Foll...</td>
      <td>START Primary Collection</td>
      <td>25</td>
    </tr>
    <tr>
      <th>170978</th>
      <td>2.017010e+11</td>
      <td>2017</td>
      <td>1</td>
      <td>7</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>NaN</td>
      <td>Hudson Bend</td>
      <td>...</td>
      <td>Anti-Muslim extremists</td>
      <td>NaN</td>
      <td>Incendiary</td>
      <td>NaN</td>
      <td>Minor (likely &lt; $1 million)</td>
      <td>-99.0</td>
      <td>A mosque was damaged in this attack.</td>
      <td>There is doubt that this incident meets terror...</td>
      <td>START Primary Collection</td>
      <td>25</td>
    </tr>
    <tr>
      <th>170984</th>
      <td>2.017010e+11</td>
      <td>2017</td>
      <td>1</td>
      <td>7</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>Texas</td>
      <td>Fort Worth</td>
      <td>...</td>
      <td>Unknown</td>
      <td>NaN</td>
      <td>Incendiary</td>
      <td>NaN</td>
      <td>Minor (likely &lt; $1 million)</td>
      <td>-99.0</td>
      <td>A church was damaged in this attack.</td>
      <td>NaN</td>
      <td>START Primary Collection</td>
      <td>25</td>
    </tr>
    <tr>
      <th>171158</th>
      <td>2.017010e+11</td>
      <td>2017</td>
      <td>1</td>
      <td>14</td>
      <td>217</td>
      <td>United States</td>
      <td>1</td>
      <td>North America</td>
      <td>Washington</td>
      <td>Bellevue</td>
      <td>...</td>
      <td>Anti-Muslim extremists</td>
      <td>The specific motive is unknown; however, sourc...</td>
      <td>Incendiary</td>
      <td>NaN</td>
      <td>Minor (likely &lt; $1 million)</td>
      <td>-99.0</td>
      <td>A mosque was damaged in this attack.</td>
      <td>There is doubt that this incident meets terror...</td>
      <td>START Primary Collection</td>
      <td>25</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 29 columns</p>
</div>




```python
limits = ['Unknown', 'Explosives', 'Incendiary', 'Firearms', 'Chemical',
       'Melee', 'Sabotage Equipment',
       'Vehicle (not to include vehicle-borne explosives, i.e., car or truck bombs)',
       'Fake Weapons', 'Radiological', 'Other', 'Biological']
colors = ["rgb(0,116,217)","rgb(255,65,54)","rgb(133,20,75)","rgb(255,133,27)","rgb(0,255,127)","rgb(135,206,250)","rgb(0,100,0)","rgb(255,215,0)","rgb(205,92,92)","rgb(255,20,147)","rgb(186,85,211)","rgb(106,90,205)"]
```


```python
america2017.loc[america2017.weaptype1_txt == 'Unknown', 'color'] = 'rgb(0,116,217)'
america2017.loc[america2017.weaptype1_txt == 'Explosives', 'color'] = 'rgb(255,65,54)'
america2017.loc[america2017.weaptype1_txt == 'Incendiary', 'color'] = 'rgb(133,20,75)'
america2017.loc[america2017.weaptype1_txt == 'Firearms', 'color'] = 'rgb(255,133,27)'
america2017.loc[america2017.weaptype1_txt == 'Chemical', 'color'] = 'rgb(0,255,127)'
america2017.loc[america2017.weaptype1_txt == 'Melee', 'color'] = 'rgb(0,116,217)'
america2017.loc[america2017.weaptype1_txt == 'Sabotage Equipment', 'color'] = 'rgb(135,206,250)'
america2017.loc[america2017.weaptype1_txt == 'Vehicle (not to include vehicle-borne explosives, i.e., car or truck bombs)', 'color'] = 'rgb(0,100,0)'
america2017.loc[america2017.weaptype1_txt == 'Fake Weapons', 'color'] = 'rgb(255,215,0)'
america2017.loc[america2017.weaptype1_txt == 'Radiological', 'color'] = 'rgb(205,92,92)'
america2017.loc[america2017.weaptype1_txt == 'Other', 'color'] = 'rgb(255,20,147)'
america2017.loc[america2017.weaptype1_txt == 'Biological', 'color'] = 'rgb(186,85,211)'
```

    /Users/siyuxie/anaconda3/lib/python3.7/site-packages/pandas/core/indexing.py:362: SettingWithCopyWarning:
    
    
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
    
    /Users/siyuxie/anaconda3/lib/python3.7/site-packages/pandas/core/indexing.py:543: SettingWithCopyWarning:
    
    
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
    



```python
len(america2017)
```




    65




```python
activities = []
for i in range(len(america2017)):
    activity = dict(
        type = 'scattergeo',
        locationmode = 'USA-states',
        lon = america2017['longitude'],
        lat = america2017['latitude'],
        text = america2017['weaptype1_txt'],
        marker = dict(
            color = america2017['color'],
            line = dict(width=0.5, color='rgb(40,40,40)'),
            sizemode = 'area'
        ),)
    activities.append(activity)

layout = dict(
        title = 'Number Of Terrorist Activities in USA',
        showlegend = True,
        geo = dict(
            scope='usa',
            projection=dict( type='albers usa' ),
            showland = True,
            landcolor = 'rgb(217, 217, 217)',
            subunitwidth=1,
            countrywidth=1,
            subunitcolor="rgb(255, 255, 255)",
            countrycolor="rgb(255, 255, 255)"
        ),
    )

fig = dict(data=activities, layout=layout)
py.iplot(fig, validate=False, filename='d3-bubble-map-populations')
#size = america['weaptype1_txt']/scale,
```




<iframe id="igraph" scrolling="no" style="border:none;" seamless="seamless" src="https://plot.ly/~srveale/261.embed" height="525px" width="100%"></iframe>




```python
america2017treemap = america2017.drop_duplicates(['weaptype1_txt'])
america2017treemap = america2017treemap.replace('Vehicle (not to include vehicle-borne explosives, i.e., car or truck bombs)', 'Vehicle')

import matplotlib.pyplot as plt
import matplotlib
import squarify
cmap = matplotlib.cm.viridis

mini, maxi = america2017treemap.iday.min(), america2017treemap.iday.max()
norm = matplotlib.colors.Normalize(vmin=mini, vmax=maxi)
colors = [cmap(norm(value)) for value in america2017treemap.iday]
colors[1] = "#FBFCFE"
labels = [(label) for label in zip(america2017treemap.weaptype1_txt, america2017treemap.weapon_count)]

# make plot
fig = plt.figure(figsize=(12, 10))
fig.suptitle("USA", fontsize=20)
ax = fig.add_subplot(111, aspect="equal")
ax = squarify.plot(sizes = america2017treemap.weapon_count, label=labels, ax=ax, color = colors,alpha=.4 )
ax.set_xticks([])
ax.set_yticks([])
ax.set_title("Weapon Type vs Activity Count\n", fontsize=14)

plt.show()
```


![png](output_22_0.png)

