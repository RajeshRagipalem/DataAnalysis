
Data Wrangling exercise
=================
First I started with exploring raw file data_analysis.json which is a list of JSON elements. Each element is a JSON record and it contain 10,00,000 records.


```python
from pandas import Series
import pandas as pd
from pandas import DataFrame
import numpy as np
import json

IDA_JSON_FILE_PATH = "/Users/raj5562/Documents/Interview/Radius/datascience-cc-1-master/data_analysis.json"
```

Reading **JSON** records


```python
df = pd.read_json(IDA_JSON_FILE_PATH, orient='records')
df
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>address</th>
      <th>category_code</th>
      <th>city</th>
      <th>headcount</th>
      <th>name</th>
      <th>phone</th>
      <th>revenue</th>
      <th>state</th>
      <th>time_in_business</th>
      <th>zip</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10085 SCRIPPS RANCH CT STE A</td>
      <td>44420000</td>
      <td>SAN DIEGO</td>
      <td>50 to 99</td>
      <td>AMD CUSTOM</td>
      <td>3123628000</td>
      <td>$20 to 50 Million</td>
      <td>CA</td>
      <td>10+ years</td>
      <td>92131</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2566 SHALLOWFORD RD NE STE 104 # 302</td>
      <td>31490000</td>
      <td>ATLANTA</td>
      <td>1 to 4</td>
      <td>Real Hope Real Estate Inc</td>
      <td>None</td>
      <td>Less Than $500,000</td>
      <td>GA</td>
      <td>10+ years</td>
      <td>30345</td>
    </tr>
    <tr>
      <th>2</th>
      <td>212 E MAIN ST</td>
      <td>53120000</td>
      <td>NEOSHO</td>
      <td>1 to 4</td>
      <td>Jimmy Sexton Photography</td>
      <td>4046331779</td>
      <td>Less Than $500,000</td>
      <td>MO</td>
      <td>10+ years</td>
      <td>64850</td>
    </tr>
    <tr>
      <th>3</th>
      <td>6032 CHEROKEE DR</td>
      <td>54000000</td>
      <td>CINCINNATI</td>
      <td>1 to 4</td>
      <td>YOU'RE ART</td>
      <td>4174513798</td>
      <td>Less Than $500,000</td>
      <td>OH</td>
      <td>10+ years</td>
      <td>45243</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1315 N WOOSTER AVE</td>
      <td>54100000</td>
      <td>STRASBURG</td>
      <td>1 to 4</td>
      <td>Hayberg Restoration Network LLC</td>
      <td>5135612584</td>
      <td>$500,000 to $1 Million</td>
      <td>OH</td>
      <td>10+ years</td>
      <td>44680</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1521 AZALEA RD</td>
      <td>23610000</td>
      <td>MOBILE</td>
      <td>5 to 9</td>
      <td>Venzon Engineering</td>
      <td>None</td>
      <td>$2.5 to 5 Million</td>
      <td>AL</td>
      <td>6-10 years</td>
      <td>36693</td>
    </tr>
    <tr>
      <th>6</th>
      <td>23513 PLAYVIEW ST</td>
      <td>54100000</td>
      <td>SAINT CLAIR SHORES</td>
      <td>1 to 4</td>
      <td>Sunrise Solutions Inc</td>
      <td>4082621271</td>
      <td>$1 to 2.5 Million</td>
      <td>MI</td>
      <td>10+ years</td>
      <td>48082</td>
    </tr>
    <tr>
      <th>7</th>
      <td>178 BOOTHBAY RD</td>
      <td>23611600</td>
      <td>EDGECOMB</td>
      <td>1 to 4</td>
      <td>Discount Hauling LLC</td>
      <td>None</td>
      <td>Less Than $500,000</td>
      <td>ME</td>
      <td>10+ years</td>
      <td>04556</td>
    </tr>
    <tr>
      <th>8</th>
      <td>7 HAZZARD ST</td>
      <td>56000000</td>
      <td>WEST PALM BEACH</td>
      <td>1 to 4</td>
      <td>Knight Equestrian Books</td>
      <td>None</td>
      <td>Less Than $500,000</td>
      <td>FL</td>
      <td>10+ years</td>
      <td>33406</td>
    </tr>
    <tr>
      <th>9</th>
      <td>8054 DARROW RD STE 3</td>
      <td>45100000</td>
      <td>TWINSBURG</td>
      <td>10 to 19</td>
      <td>CHILDRENS HOSPITAL PHYS. ASSOC.</td>
      <td>2078825494</td>
      <td>Less Than $500,000</td>
      <td>OH</td>
      <td>None</td>
      <td>44087</td>
    </tr>
    <tr>
      <th>10</th>
      <td>225 SAN PEDRO DR NE</td>
      <td>54100000</td>
      <td>ALBUQUERQUE</td>
      <td>1 to 4</td>
      <td>Bottom Line Management</td>
      <td>5616897900</td>
      <td>Less Than $500,000</td>
      <td>NM</td>
      <td>None</td>
      <td>87108</td>
    </tr>
    <tr>
      <th>11</th>
      <td>1059 PROSPECT ST</td>
      <td>62110000</td>
      <td>HONOLULU</td>
      <td>1 to 4</td>
      <td>METAL TOAD MEDIA LLC</td>
      <td>2166910471</td>
      <td>$2.5 to 5 Million</td>
      <td>HI</td>
      <td>None</td>
      <td>96822</td>
    </tr>
    <tr>
      <th>12</th>
      <td>530 LAKESIDE DR</td>
      <td>52230000</td>
      <td>SUNNYVALE</td>
      <td>5 to 9</td>
      <td>MULTICOREWARE INC</td>
      <td>5033361658</td>
      <td>None</td>
      <td>CA</td>
      <td>10+ years</td>
      <td>94085</td>
    </tr>
    <tr>
      <th>13</th>
      <td>9200 KEYSTONE XING STE 150</td>
      <td>54000000</td>
      <td>INDIANAPOLIS</td>
      <td>20 to 49</td>
      <td>St Mary Magdalen Parish</td>
      <td>None</td>
      <td>Less Than $500,000</td>
      <td>IN</td>
      <td>1-2 years</td>
      <td>46240</td>
    </tr>
    <tr>
      <th>14</th>
      <td>2170 STOCKBRIDGE AVE</td>
      <td>81300000</td>
      <td>WOODSIDE</td>
      <td>None</td>
      <td>Woodside Group Inc</td>
      <td>None</td>
      <td>None</td>
      <td>CA</td>
      <td>10+ years</td>
      <td>94062</td>
    </tr>
    <tr>
      <th>15</th>
      <td>133 MARJORIE DR</td>
      <td>52400000</td>
      <td>BUFFALO</td>
      <td>1 to 4</td>
      <td>Southern Management</td>
      <td>None</td>
      <td>Less Than $500,000</td>
      <td>NY</td>
      <td>None</td>
      <td>14223</td>
    </tr>
    <tr>
      <th>16</th>
      <td>210 9TH ST NW</td>
      <td>54100000</td>
      <td>CEDAR RAPIDS</td>
      <td>10 to 19</td>
      <td>COUNTY OF CLAY</td>
      <td>7168339295</td>
      <td>Less Than $500,000</td>
      <td>IA</td>
      <td>10+ years</td>
      <td>52405</td>
    </tr>
    <tr>
      <th>17</th>
      <td>142 N MOSLEY ST</td>
      <td>56100000</td>
      <td>WICHITA</td>
      <td>10 to 19</td>
      <td>Delima Corporation</td>
      <td>3193556657</td>
      <td>$1 to 2.5 Million</td>
      <td>KS</td>
      <td>10+ years</td>
      <td>67202</td>
    </tr>
    <tr>
      <th>18</th>
      <td>7604 FONTAINEBLEAU DR</td>
      <td>52390000</td>
      <td>NEW CARROLLTON</td>
      <td>100 to 249</td>
      <td>MOVIMENTO INC</td>
      <td>3162622500</td>
      <td>$20 to 50 Million</td>
      <td>MD</td>
      <td>6-10 years</td>
      <td>20784</td>
    </tr>
    <tr>
      <th>19</th>
      <td>649 N VAN DYKE RD</td>
      <td>92111000</td>
      <td>IMLAY CITY</td>
      <td>10 to 19</td>
      <td>Sherwin-Williams</td>
      <td>3017315977</td>
      <td>$1 to 2.5 Million</td>
      <td>MI</td>
      <td>3-5 years</td>
      <td>48444</td>
    </tr>
    <tr>
      <th>20</th>
      <td>100 W MISSISSIPPI ST</td>
      <td>56111000</td>
      <td>LIBERTY</td>
      <td>1 to 4</td>
      <td>PCAV</td>
      <td>8107211415</td>
      <td>$2.5 to 5 Million</td>
      <td>MO</td>
      <td>10+ years</td>
      <td>64068</td>
    </tr>
    <tr>
      <th>21</th>
      <td>444 WASHINGTON AVE</td>
      <td>44412002</td>
      <td>CARLSTADT</td>
      <td>100 to 249</td>
      <td>Publix</td>
      <td>8164158683</td>
      <td>Less Than $500,000</td>
      <td>NJ</td>
      <td>3-5 years</td>
      <td>07072</td>
    </tr>
    <tr>
      <th>22</th>
      <td>46029 FIVE MILE RD</td>
      <td>23000000</td>
      <td>PLYMOUTH</td>
      <td>5 to 9</td>
      <td>Jolles Associates Inc</td>
      <td>2019338405</td>
      <td>None</td>
      <td>MI</td>
      <td>6-10 years</td>
      <td>48170</td>
    </tr>
    <tr>
      <th>23</th>
      <td>1220 S MAIN ST</td>
      <td>44511000</td>
      <td>SOUTH BEND</td>
      <td>None</td>
      <td>Sullivan &amp; Worcester LLP</td>
      <td>None</td>
      <td>Less Than $500,000</td>
      <td>IN</td>
      <td>10+ years</td>
      <td>46601</td>
    </tr>
    <tr>
      <th>24</th>
      <td>310 PELHAM AVE SW</td>
      <td>54161800</td>
      <td>HUNTSVILLE</td>
      <td>1 to 4</td>
      <td>DEMOCRACY COUNCIL OF CALIFORNIA</td>
      <td>None</td>
      <td>Less Than $500,000</td>
      <td>AL</td>
      <td>10+ years</td>
      <td>35801</td>
    </tr>
    <tr>
      <th>25</th>
      <td>9903 GEORGETOWN PIKE</td>
      <td>54100000</td>
      <td>GREAT FALLS</td>
      <td>1 to 4</td>
      <td>TELWORX COMMUNICATIONS</td>
      <td>None</td>
      <td>Less Than $500,000</td>
      <td>VA</td>
      <td>10+ years</td>
      <td>22066</td>
    </tr>
    <tr>
      <th>26</th>
      <td>645 GRISWOLD ST STE 3080</td>
      <td>54100000</td>
      <td>DETROIT</td>
      <td>20 to 49</td>
      <td>North Woods Baptist Church</td>
      <td>None</td>
      <td>$5 to 10 Million</td>
      <td>MI</td>
      <td>10+ years</td>
      <td>48226</td>
    </tr>
    <tr>
      <th>27</th>
      <td>1875 I ST NW STE 500</td>
      <td>23000000</td>
      <td>WASHINGTON</td>
      <td>20 to 49</td>
      <td>RISK MANAGEMENT CO</td>
      <td>None</td>
      <td>$500,000 to $1 Million</td>
      <td>DC</td>
      <td>10+ years</td>
      <td>20006</td>
    </tr>
    <tr>
      <th>28</th>
      <td>1666 K ST NW</td>
      <td>54111000</td>
      <td>WASHINGTON</td>
      <td>5 to 9</td>
      <td>C TUCKER COPE &amp; ASSOC INC</td>
      <td>7038876562</td>
      <td>Less Than $500,000</td>
      <td>DC</td>
      <td>10+ years</td>
      <td>20006</td>
    </tr>
    <tr>
      <th>29</th>
      <td>555 CALIFORNIA ST STE 4</td>
      <td>52200000</td>
      <td>SAN FRANCISCO</td>
      <td>1 to 4</td>
      <td>Klemmt Orthopaedic Services</td>
      <td>None</td>
      <td>Less Than $500,000</td>
      <td>CA</td>
      <td>10+ years</td>
      <td>94104</td>
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
    </tr>
    <tr>
      <th>999970</th>
      <td>129 E 6TH ST</td>
      <td>56131000</td>
      <td>GRAFTON</td>
      <td>5 to 9</td>
      <td>MI Financial Services</td>
      <td>None</td>
      <td>Less Than $500,000</td>
      <td>ND</td>
      <td>10+ years</td>
      <td>58237</td>
    </tr>
    <tr>
      <th>999971</th>
      <td>305 DIVISION ST</td>
      <td>54100000</td>
      <td>YAKIMA</td>
      <td>1 to 4</td>
      <td>G V Jewelry</td>
      <td>None</td>
      <td>Less Than $500,000</td>
      <td>WA</td>
      <td>10+ years</td>
      <td>98902</td>
    </tr>
    <tr>
      <th>999972</th>
      <td>1281 E GOLFVIEW DR</td>
      <td>72100000</td>
      <td>PEMBROKE PINES</td>
      <td>5 to 9</td>
      <td>Allen Pools &amp; Spas</td>
      <td>None</td>
      <td>$1 to 2.5 Million</td>
      <td>FL</td>
      <td>10+ years</td>
      <td>33026</td>
    </tr>
    <tr>
      <th>999973</th>
      <td>3808 COOKSON RD</td>
      <td>62110000</td>
      <td>EAST SAINT LOUIS</td>
      <td>1 to 4</td>
      <td>DALLA TERRA</td>
      <td>4127881910</td>
      <td>$500,000 to $1 Million</td>
      <td>IL</td>
      <td>10+ years</td>
      <td>62201</td>
    </tr>
    <tr>
      <th>999974</th>
      <td>817 BROADWAY</td>
      <td>62110000</td>
      <td>NEW YORK</td>
      <td>1 to 4</td>
      <td>TGI Office Automation</td>
      <td>None</td>
      <td>$1 to 2.5 Million</td>
      <td>NY</td>
      <td>6-10 years</td>
      <td>10003</td>
    </tr>
    <tr>
      <th>999975</th>
      <td>365 FAUNCE CORNER RD</td>
      <td>54111000</td>
      <td>NORTH DARTMOUTH</td>
      <td>1 to 4</td>
      <td>Associated Cardiovascular</td>
      <td>None</td>
      <td>$10 to 20 Million</td>
      <td>MA</td>
      <td>10+ years</td>
      <td>02747</td>
    </tr>
    <tr>
      <th>999976</th>
      <td>18500 VON KARMAN AVE STE 530</td>
      <td>54111000</td>
      <td>IRVINE</td>
      <td>1 to 4</td>
      <td>Priority Artificial Lift</td>
      <td>None</td>
      <td>$20 to 50 Million</td>
      <td>CA</td>
      <td>10+ years</td>
      <td>92612</td>
    </tr>
    <tr>
      <th>999977</th>
      <td>14543 HIGHWAY 105 W</td>
      <td>23820000</td>
      <td>CONROE</td>
      <td>1 to 4</td>
      <td>INTERACTION INFO TECH INC</td>
      <td>None</td>
      <td>Less Than $500,000</td>
      <td>TX</td>
      <td>10+ years</td>
      <td>77304</td>
    </tr>
    <tr>
      <th>999978</th>
      <td>44 WHIPPANY RD STE 220</td>
      <td>53220000</td>
      <td>MORRISTOWN</td>
      <td>10 to 19</td>
      <td>CAWLEY GILLESPIE AND ASSOCIATES</td>
      <td>None</td>
      <td>$5 to 10 Million</td>
      <td>NJ</td>
      <td>10+ years</td>
      <td>7960</td>
    </tr>
    <tr>
      <th>999979</th>
      <td>2950 S ALL HALLOWS ST</td>
      <td>54000000</td>
      <td>WICHITA</td>
      <td>10 to 19</td>
      <td>Rhino Technologies</td>
      <td>8284034989</td>
      <td>$1 to 2.5 Million</td>
      <td>KS</td>
      <td>6-10 years</td>
      <td>67217</td>
    </tr>
    <tr>
      <th>999980</th>
      <td>4932 WINDY HILL DR STE A</td>
      <td>81200000</td>
      <td>RALEIGH</td>
      <td>10 to 19</td>
      <td>ECKERT HYUNDAI INC</td>
      <td>7195316600</td>
      <td>$1 to 2.5 Million</td>
      <td>NC</td>
      <td>None</td>
      <td>27609</td>
    </tr>
    <tr>
      <th>999981</th>
      <td>1525 FULTON ST</td>
      <td>54181001</td>
      <td>FRESNO</td>
      <td>5 to 9</td>
      <td>Bright Ideas</td>
      <td>3153701372</td>
      <td>$2.5 to 5 Million</td>
      <td>CA</td>
      <td>None</td>
      <td>93721</td>
    </tr>
    <tr>
      <th>999982</th>
      <td>594 MARRETT RD</td>
      <td>22130000</td>
      <td>LEXINGTON</td>
      <td>1 to 4</td>
      <td>Hardin County Road Department</td>
      <td>3077543634</td>
      <td>$500,000 to $1 Million</td>
      <td>MA</td>
      <td>10+ years</td>
      <td>2421</td>
    </tr>
    <tr>
      <th>999983</th>
      <td>10208 BENAVIDES RD SW</td>
      <td>52310000</td>
      <td>ALBUQUERQUE</td>
      <td>10 to 19</td>
      <td>COLDWELL BANKERS RESIDENTIAL</td>
      <td>9087663983</td>
      <td>$5 to 10 Million</td>
      <td>NM</td>
      <td>10+ years</td>
      <td>87121</td>
    </tr>
    <tr>
      <th>999984</th>
      <td>110 LONE PINE RD</td>
      <td>23820000</td>
      <td>BLOOMFIELD HILLS</td>
      <td>1 to 4</td>
      <td>Hje Group</td>
      <td>5074552929</td>
      <td>Less Than $500,000</td>
      <td>MI</td>
      <td>10+ years</td>
      <td>48304</td>
    </tr>
    <tr>
      <th>999985</th>
      <td>105 LANE AVE</td>
      <td>62400000</td>
      <td>HIGH POINT</td>
      <td>5 to 9</td>
      <td>STEELFISH DESIGN LLC</td>
      <td>7322901677</td>
      <td>Less Than $500,000</td>
      <td>NC</td>
      <td>None</td>
      <td>27260</td>
    </tr>
    <tr>
      <th>999986</th>
      <td>125 E MAIN ST</td>
      <td>54111000</td>
      <td>REEDSBURG</td>
      <td>20 to 49</td>
      <td>Alpine Electric</td>
      <td>None</td>
      <td>Less Than $500,000</td>
      <td>WI</td>
      <td>3-5 years</td>
      <td>53959</td>
    </tr>
    <tr>
      <th>999987</th>
      <td>4422 DOUGLAS AVE</td>
      <td>54121000</td>
      <td>RACINE</td>
      <td>1 to 4</td>
      <td>Walgreens</td>
      <td>8584950727</td>
      <td>$100 to 500 Million</td>
      <td>WI</td>
      <td>3-5 years</td>
      <td>53402</td>
    </tr>
    <tr>
      <th>999988</th>
      <td>3033 MAGAZINE ST</td>
      <td>31181100</td>
      <td>NEW ORLEANS</td>
      <td>5 to 9</td>
      <td>BNC National Bank</td>
      <td>None</td>
      <td>$1 to 2.5 Million</td>
      <td>LA</td>
      <td>10+ years</td>
      <td>70115</td>
    </tr>
    <tr>
      <th>999989</th>
      <td>503 E GOVERNMENT ST</td>
      <td>52230000</td>
      <td>PENSACOLA</td>
      <td>20 to 49</td>
      <td>LISA KALUS &amp; ASSOC.</td>
      <td>8082454572</td>
      <td>$2.5 to 5 Million</td>
      <td>FL</td>
      <td>3-5 years</td>
      <td>32502</td>
    </tr>
    <tr>
      <th>999990</th>
      <td>3000 BURR ST</td>
      <td>44400000</td>
      <td>GARY</td>
      <td>1 to 4</td>
      <td>NETWORKS INC</td>
      <td>2523997712</td>
      <td>$500,000 to $1 Million</td>
      <td>IN</td>
      <td>10+ years</td>
      <td>46406</td>
    </tr>
    <tr>
      <th>999991</th>
      <td>2320 PAUL ST</td>
      <td>22130000</td>
      <td>OMAHA</td>
      <td>5 to 9</td>
      <td>PULMONARY PHYSICIANS OF KANSAS CITY INC</td>
      <td>(516) 390-6802</td>
      <td>$20 to 50 Million</td>
      <td>NE</td>
      <td>10+ years</td>
      <td>68102</td>
    </tr>
    <tr>
      <th>999992</th>
      <td>16191 TABLE MOUNTAIN PKWY STE A</td>
      <td>61000000</td>
      <td>GOLDEN</td>
      <td>50 to 99</td>
      <td>Renton Church Of God</td>
      <td>8086710541</td>
      <td>Over $1 Billion</td>
      <td>CO</td>
      <td>10+ years</td>
      <td>80403</td>
    </tr>
    <tr>
      <th>999993</th>
      <td>11131 SHADY TRL</td>
      <td>72200000</td>
      <td>DALLAS</td>
      <td>1 to 4</td>
      <td>Sterling Plating Inc</td>
      <td>5613927799</td>
      <td>$500,000 to $1 Million</td>
      <td>TX</td>
      <td>None</td>
      <td>75229</td>
    </tr>
    <tr>
      <th>999994</th>
      <td>4554 WASHTENAW AVE</td>
      <td>56100000</td>
      <td>ANN ARBOR</td>
      <td>5 to 9</td>
      <td>Eachwin Lp</td>
      <td>None</td>
      <td>$5 to 10 Million</td>
      <td>MI</td>
      <td>10+ years</td>
      <td>48108</td>
    </tr>
    <tr>
      <th>999995</th>
      <td>318 W GRAND AVE STE 305</td>
      <td>62110000</td>
      <td>CHICAGO</td>
      <td>5 to 9</td>
      <td>PRESIDIO NETWORKED SOLUTIONS INC</td>
      <td>None</td>
      <td>Less Than $500,000</td>
      <td>IL</td>
      <td>10+ years</td>
      <td>60654</td>
    </tr>
    <tr>
      <th>999996</th>
      <td>8020 OLD ALEXANDRIA FERRY RD</td>
      <td>54180000</td>
      <td>CLINTON</td>
      <td>5 to 9</td>
      <td>INC Research</td>
      <td>9722403710</td>
      <td>Less Than $500,000</td>
      <td>MD</td>
      <td>None</td>
      <td>20735</td>
    </tr>
    <tr>
      <th>999997</th>
      <td>3025 BIG FLAT RD</td>
      <td>33290000</td>
      <td>MISSOULA</td>
      <td>20 to 49</td>
      <td>Metric &amp; Multistandard Components Corp</td>
      <td>5207456012</td>
      <td>Less Than $500,000</td>
      <td>MT</td>
      <td>6-10 years</td>
      <td>59804</td>
    </tr>
    <tr>
      <th>999998</th>
      <td>700 N STONE AVE</td>
      <td>81290000</td>
      <td>TUCSON</td>
      <td>10 to 19</td>
      <td>United Van Lines</td>
      <td>None</td>
      <td>Less Than $500,000</td>
      <td>AZ</td>
      <td>10+ years</td>
      <td>85705</td>
    </tr>
    <tr>
      <th>999999</th>
      <td>1001 W 54TH ST</td>
      <td>31599000</td>
      <td>ERIE</td>
      <td>1 to 4</td>
      <td>The Magrino Agency</td>
      <td>3084523531</td>
      <td>Less Than $500,000</td>
      <td>PA</td>
      <td>10+ years</td>
      <td>16509</td>
    </tr>
  </tbody>
</table>
<p>1000000 rows × 10 columns</p>
</div>



Now we got all records into a data frame.


```python
numOfRecords = len(df)
print "num Of Records = ", numOfRecords
print
```

    num Of Records =  1000000
    



```python
print list(df.columns)
```

    [u'address', u'category_code', u'city', u'headcount', u'name', u'phone', u'revenue', u'state', u'time_in_business', u'zip']


Above is the field list.

Task-1:
--

- **Fill Rate**: For each field, how many records have a value.

If a field is filled in a record, its value will be captured in `PANDAS` data frame, else it will be `NaN` which states the field is missing

using `count( )` function, we can get the number of not null records.


```python
fieldSummary = pd.DataFrame()
fieldSummary['fillRate'] = df.count();
#fieldSummary['%presentIn'] = ((fieldSummary['presentIn']/numOfRecords)*100).round(4)
fieldSummary
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>fillRate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>address</th>
      <td>999986</td>
    </tr>
    <tr>
      <th>category_code</th>
      <td>999986</td>
    </tr>
    <tr>
      <th>city</th>
      <td>999986</td>
    </tr>
    <tr>
      <th>headcount</th>
      <td>962352</td>
    </tr>
    <tr>
      <th>name</th>
      <td>999986</td>
    </tr>
    <tr>
      <th>phone</th>
      <td>590889</td>
    </tr>
    <tr>
      <th>revenue</th>
      <td>943092</td>
    </tr>
    <tr>
      <th>state</th>
      <td>999986</td>
    </tr>
    <tr>
      <th>time_in_business</th>
      <td>916125</td>
    </tr>
    <tr>
      <th>zip</th>
      <td>999988</td>
    </tr>
  </tbody>
</table>
</div>



Above is the fill rate table.


Task-2:
--

- **True-Valued Fill Rate**: For each field, how many records have relevant data in them. For example, a field which has string valued entries may have elements that contain something like ' '. This is a string but may not be 'good' data depending on the field.

We need to mark field values with only spaces, 'null', 'none' and '0' to NaN so that we get true fill rate. This is acheved by the following function. And the new dataframe **finalDF** is the processed data set.


```python
def cleanColumn (data):
    print data.count()
    print
    print data.value_counts(sort=True, ascending=True)
    print
    data = data.str.strip() #Gets rid of trailing blank spaces
    data = data.replace('',np.nan, regex=True) #Replace completely empty cells with nan
    data = data.replace('null',np.nan, regex=True) #Replace completely cells constaing 'null' with nan
    data = data.replace('none',np.nan, regex=True) #Replace completely cells constaing 'none' with nan
    #data = data.replace('0',np.nan, regex=True) #Replace completely empty cells with nan
    data[data == '0'] = np.nan #Replace completely empty cells with nan
    #data = data.replace(0,np.nan, regex=True) #Replace completely empty cells with nan
    print data.count()
    print
    print data.value_counts(sort=True, ascending=True)
    print
    return data
finalDF = pd.DataFrame()
finalDF["address"] = cleanColumn(df.address)
finalDF["category_code"] = cleanColumn(df.category_code)
finalDF["city"] = cleanColumn(df.city)
finalDF["headcount"] = cleanColumn(df.headcount)
finalDF["name"] = cleanColumn(df.name)
finalDF["phone"] = cleanColumn(df.phone)
finalDF["revenue"] = cleanColumn(df.revenue)
finalDF["state"] = cleanColumn(df.state)
finalDF["time_in_business"] = cleanColumn(df.time_in_business)
finalDF["zip"] = cleanColumn(df.zip)
finalDF.head(5)
```

    999986
    
    2207 W PARMER LN                         1
    1403 GREENBRIER PKWY STE 465             1
    1762 DIVIDEND DR                         1
    3419 HARTLEY RD                          1
    326 N EUCLID AVE STE 2N                  1
    729 HAYWOOD RD STE 3                     1
    1401 NE 42ND TER                         1
    608 RICHMOND DR STE 103                  1
    1835 LOCKHILL SELMA RD APT 337           1
    7510 PORTER RD                           1
    7920 INTERCHANGE RD                      1
    1001 E WARNER RD STE 104                 1
    307 W BUTLER AVE                         1
    25 NE 47TH AVE                           1
    100 DAVIS ST                             1
    293 WATERS WAY                           1
    403 S POPLAR ST STE B                    1
    105 S 12TH ST                            1
    399 EDGEWOOD AVE SE                      1
    442 W WASHINGTON ST                      1
    2483 E BAYSHORE RD STE 100               1
    16126 BRANDY RD                          1
    17202 S FIGUEROA ST                      1
    9324 MAIN ST                             1
    208 GLOUCESTER ST                        1
    7405 E MONTE CRISTO AVE                  1
    11772 SORRENTO VALLEY RD STE 201         1
    1166 AVENUE OF THE AMERICAS STE 1610     1
    14691 CLAYTON RD                         1
    20200 STATE RD                           1
                                            ..
    100 N MAIN ST                           28
    1000 MAIN ST                            28
    500 MAIN ST                             29
    100 E MAIN ST                           29
    201 E MAIN ST                           29
    300 MAIN ST                             30
    105 N MAIN ST                           30
    200 N MAIN ST                           31
    401 MAIN ST                             31
    101 MAIN ST                             31
    201 MAIN ST                             31
    101 W MAIN ST                           31
    200 S MAIN ST                           32
    50 MAIN ST                              32
    100 MAIN ST                             33
    301 N MAIN ST                           33
    4 TIMES SQ                              34
    101 E MAIN ST                           34
    400 MAIN ST                             34
    110 W MAIN ST                           35
    301 MAIN ST                             35
    201 W MAIN ST                           35
    200 E MAIN ST                           35
    102 S MAIN ST                           38
    100 S MAIN ST                           40
    1 MAIN ST                               40
    101 S MAIN ST                           42
    201 S MAIN ST                           43
    101 N MAIN ST                           46
    1 S DEARBORN ST                         76
    Name: address, dtype: int64
    
    999898
    
    9 HIGGINS ST                  1
    5358 HILL 23 DR               1
    1868 COMMON ST                1
    5520 GODFREY RD               1
    1112 GREENFIELD DR STE 2      1
    14950 US HIGHWAY 301          1
    145 KEEP CT                   1
    2802 DELMAR DR STE G          1
    3351 SAN GABRIEL BLVD         1
    100 FAIR OAKS LN              1
    6066 LEESBURG PIKE            1
    4001 GANTZ RD                 1
    2685 BUSINESS DR              1
    3507 OASIS BLVD               1
    7575 175TH ST                 1
    345 CALIFORNIA ST STE 160     1
    135 PEPPERIDGE CIR            1
    90 MARIPOSA AVE               1
    1120 SOUTH FWY                1
    7970 PATRIOT DR               1
    15264 CLYMER ST               1
    310 LAUREL RD E               1
    42877 KENAI SPUR HWY          1
    6040 N CUTTER CIR STE 309     1
    4200 W CYPRESS ST STE 900     1
    3395 E MALAGA AVE             1
    2 MLK JR BLVD                 1
    11730 STATE ROUTE 131         1
    8582 KATY FWY STE 201         1
    189 NORTH ST                  1
                                 ..
    100 N MAIN ST                28
    2 MAIN ST                    28
    201 E MAIN ST                29
    100 E MAIN ST                29
    500 MAIN ST                  29
    300 MAIN ST                  30
    105 N MAIN ST                30
    200 N MAIN ST                31
    101 MAIN ST                  31
    201 MAIN ST                  31
    101 W MAIN ST                31
    401 MAIN ST                  31
    50 MAIN ST                   32
    200 S MAIN ST                32
    100 MAIN ST                  33
    301 N MAIN ST                33
    4 TIMES SQ                   34
    400 MAIN ST                  34
    101 E MAIN ST                34
    301 MAIN ST                  35
    110 W MAIN ST                35
    201 W MAIN ST                35
    200 E MAIN ST                35
    102 S MAIN ST                38
    100 S MAIN ST                40
    1 MAIN ST                    40
    101 S MAIN ST                42
    201 S MAIN ST                43
    101 N MAIN ST                46
    1 S DEARBORN ST              76
    Name: address, dtype: int64
    
    999986
    
    62111174        1
    49312001        1
    51229003        1
    32121901        1
    81321902        1
    56221901        1
    31222100        1
    31491100        1
    72131000        1
    21111101        1
    33232104        1
    61169918        1
    72119901        1
    44419014        1
    48422009        1
    44815015        1
    62111129        1
    81140000        1
    21239200        1
    44419037        1
    62220000        1
    54193002        1
    81390000        1
    81119805        1
    33599905        1
    23821014        1
    21311201        1
    33721504        1
    81121103        1
    81391006        1
                ...  
    52412000     7765
    81111000     8142
    81211000     8273
    44400000     8544
    23610000     9323
    71300000     9447
    52200000     9473
    54161800     9504
    52390000    10816
    45000000    11590
    56000000    12160
    23611600    13293
    44000000    14114
    51000000    14867
    62130000    15243
    54121000    16343
    81300000    16514
    72200000    17026
    62000000    19143
    23820000    19235
    62400000    22004
    52420000    26887
    23000000    27538
    54100000    28693
    62110000    29205
    42000000    30171
    54000000    31745
    53120000    32577
    54111000    37891
    61111000    39461
    Name: category_code, dtype: int64
    
    999910
    
    44831006        1
    44815015        1
    81391006        1
    31529904        1
    45399832        1
    62111163        1
    56111008        1
    81411002        1
    62141004        1
    62220000        1
    62399003        1
    44619906        1
    33261200        1
    33299401        1
    81390000        1
    44419037        1
    33232104        1
    21239200        1
    23731002        1
    51119904        1
    44814006        1
    62139911        1
    31523200        1
    81291008        1
    31330000        1
    81121103        1
    81140000        1
    48422009        1
    22121008        1
    44229908        1
                ...  
    52412000     7765
    81111000     8142
    81211000     8273
    44400000     8544
    23610000     9323
    71300000     9447
    52200000     9473
    54161800     9504
    52390000    10816
    45000000    11590
    56000000    12160
    23611600    13293
    44000000    14114
    51000000    14867
    62130000    15243
    54121000    16343
    81300000    16514
    72200000    17026
    62000000    19143
    23820000    19235
    62400000    22004
    52420000    26887
    23000000    27538
    54100000    28693
    62110000    29205
    42000000    30171
    54000000    31745
    53120000    32577
    54111000    37891
    61111000    39461
    Name: category_code, dtype: int64
    
    999986
    
    HUSSER                        1
    PRESTON HOLLOW                1
    MT VERNON                     1
    MATFIELD GREEN                1
    MAYSLICK                      1
    JENNERS                       1
    ARPIN                         1
    EAST BURKE                    1
    AGRA                          1
    BREMO BLUFF                   1
    MOUNT CHARLESTON              1
    TINA                          1
    EAST RYEGATE                  1
    MARCH AIR RESERVE BASE        1
    HERBSTER                      1
    HARRIETTA                     1
    THRALL                        1
    BOOTH                         1
    PLUMMER                       1
    LITTLE PLYMOUTH               1
    LEIGH                         1
    TOWNSENDS INLET               1
    MEADVIEW                      1
    SUMMERTON                     1
    METCALF                       1
    BIG POOL                      1
    BOILING SPGS                  1
    MAUCKPORT                     1
    BOKOSHE                       1
    TOUCHET                       1
                              ...  
    ORLANDO                    3195
    CINCINNATI                 3209
    SAN JOSE                   3216
    LOUISVILLE                 3252
    SPRINGFIELD                3339
    JACKSONVILLE               3465
    TAMPA                      3469
    LAS VEGAS                  3564
    PHILADELPHIA               3770
    CHARLOTTE                  3861
    INDIANAPOLIS               3887
    SAN ANTONIO                4012
    COLUMBUS                   4236
    SAINT LOUIS                4350
    DENVER                     4500
    MIAMI                      4639
    SEATTLE                    4660
    MINNEAPOLIS                4832
    SAN FRANCISCO              4871
    PHOENIX                    4889
    WASHINGTON                 5170
    LOS ANGELES                5522
    AUSTIN                     5618
    PORTLAND                   5797
    ATLANTA                    5813
    SAN DIEGO                  5997
    DALLAS                     6317
    CHICAGO                    9023
    HOUSTON                   11109
    NEW YORK                  14264
    Name: city, dtype: int64
    
    999895
    
    GUILDHALL                  1
    LENORAH                    1
    NORTH NEW HYDE PARK        1
    CARROLLTOWN                1
    SOUTHFIELDS                1
    CHANDLERSVILLE             1
    EGREMONT                   1
    ST FRANCIS                 1
    REILES ACRES               1
    OGDEN DUNES                1
    HAGUE                      1
    MIDFIELD                   1
    RAGLAND                    1
    BODEGA                     1
    RANDALIA                   1
    HUSSER                     1
    FRENCHGLEN                 1
    CURRAN                     1
    SARGENT                    1
    ETTRICK                    1
    SUNDANCE                   1
    ULMAN                      1
    OKATON                     1
    PLAINS TOWNSHIP            1
    LOTTIE                     1
    ASSARIA                    1
    HONAKER                    1
    RENFRO VALLEY              1
    SYLVAN BEACH               1
    HOLABIRD                   1
                           ...  
    ORLANDO                 3195
    CINCINNATI              3209
    SAN JOSE                3216
    LOUISVILLE              3252
    SPRINGFIELD             3339
    JACKSONVILLE            3465
    TAMPA                   3469
    LAS VEGAS               3564
    PHILADELPHIA            3770
    CHARLOTTE               3861
    INDIANAPOLIS            3887
    SAN ANTONIO             4012
    COLUMBUS                4236
    SAINT LOUIS             4350
    DENVER                  4500
    MIAMI                   4639
    SEATTLE                 4660
    MINNEAPOLIS             4832
    SAN FRANCISCO           4871
    PHOENIX                 4889
    WASHINGTON              5170
    LOS ANGELES             5522
    AUSTIN                  5618
    PORTLAND                5797
    ATLANTA                 5813
    SAN DIEGO               5997
    DALLAS                  6317
    CHICAGO                 9023
    HOUSTON                11109
    NEW YORK               14264
    Name: city, dtype: int64
    
    962352
    
                       8
    0                 10
    null              12
    0                 15
                      17
    none              17
    500 to 999      5250
    Over 1,000      5600
    250 to 499     11138
    100 to 249     36475
    50 to 99       60526
    20 to 49      121264
    10 to 19      151412
    5 to 9        212401
    1 to 4        358207
    Name: headcount, dtype: int64
    
    962273
    
    500 to 999      5250
    Over 1,000      5600
    250 to 499     11138
    100 to 249     36475
    50 to 99       60526
    20 to 49      121264
    10 to 19      151412
    5 to 9        212401
    1 to 4        358207
    Name: headcount, dtype: int64
    
    999986
    
    WILLIAM NOBBE & CO INC                                              1
    Murphy Bob Contracting                                              1
    Family Podiatry Center                                              1
    Stephen DC Milligan Bcao                                            1
    Richard Mitchell Asla Inc                                           1
    Industrial Irrigation                                               1
    Bevard Automotive Inc                                               1
    Southwest Michigan Neonatology PC                                   1
    FELIX FOTOGRAPHY                                                    1
    PEACHTREE HOTEL GROUP LLC                                           1
    Tri-State Neurosurgery at Willis-Knighton North Medical Center      1
    Greenstreet Real Estate                                             1
    Grand Haven High School                                             1
    JOHN T MATHER MEMORIAL HOSPITAL OF PORT JEFFERSON                   1
    HURWITZ, BARBARA R                                                  1
    Diversey River Bowl                                                 1
    CATHOLIC EAST TEXAS                                                 1
    Diamond C Transport                                                 1
    SOUTHERN ALUMINUM MANUFACTURING INC                                 1
    R & R Petro Services Inc                                            1
    KBS ELECTRICAL DISTRIBUTORS INC                                     1
    Carver County Community Social Services                             1
    Volatile Free Inc                                                   1
    The Rock Cafe                                                       1
    Barefoot Farms                                                      1
    ACUTA DIGITAL INC                                                   1
    Community Programs Inc                                              1
    Ditronics                                                           1
    DCR Industrial Services Inc                                         1
    Roman Brushtein Medical LLC                                         1
                                                                     ... 
    H&R Block                                                         166
    Farmers Insurance Group                                           166
    First United Methodist Church                                     171
    Century 21                                                        171
    Fastenal                                                          173
    Primerica                                                         176
    Chicago Public Schools                                            179
    Express Employment Professionals                                  180
    Minuteman Press                                                   201
    Primerica Financial Services                                      205
    Budget Blinds                                                     206
    BB&T                                                              217
    Regions Bank                                                      223
    Verizon Wireless                                                  224
    CENTURY 21                                                        229
    U.S. BANK                                                         253
    Mary Kay Cosmetics                                                271
    Coldwell Banker                                                   273
    NAPA Auto Parts                                                   280
    McDonald's                                                        281
    Liberty Tax Service                                               282
    Walgreens                                                         290
    RE/MAX                                                            303
    State Farm Insurance                                              317
    First Baptist Church                                              332
    First Presbyterian Church                                         336
    YMCA                                                              364
    Keller Williams Realty                                            422
    Ameriprise Financial                                              667
    Farmers Insurance                                                 821
    Name: name, dtype: int64
    
    999877
    
    KINSBURSKY BROTHERS SUPPLY INC                                      1
    Li Benjamin MD Facs                                                 1
    Vision One                                                          1
    GORDON & ASSOCIATES REALTY INC                                      1
    BBK STUDIO INC                                                      1
    ROYAL ARCH MASONS OF STAT.                                          1
    Community Programs Inc                                              1
    MERITOR WABCO VEHICLE CONTROL SYSTEMS                               1
    ACUTA DIGITAL INC                                                   1
    Greenstreet Real Estate                                             1
    Murphy Bob Contracting                                              1
    Piscataqua Plastic Surgery                                          1
    Family Podiatry Center                                              1
    Richard Mitchell Asla Inc                                           1
    Industrial Irrigation                                               1
    Bevard Automotive Inc                                               1
    Southwest Michigan Neonatology PC                                   1
    FELIX FOTOGRAPHY                                                    1
    PEACHTREE HOTEL GROUP LLC                                           1
    Tri-State Neurosurgery at Willis-Knighton North Medical Center      1
    Grand Haven High School                                             1
    The Rock Cafe                                                       1
    JOHN T MATHER MEMORIAL HOSPITAL OF PORT JEFFERSON                   1
    Stephen DC Milligan Bcao                                            1
    HURWITZ, BARBARA R                                                  1
    Admark Inc                                                          1
    SELLER BROADCASTING INC                                             1
    Classic Nursery & Landscape Company                                 1
    CASTEEL AUCTION & REAL ESTATE                                       1
    GODFREY & KAHN                                                      1
                                                                     ... 
    Farmers Insurance Group                                           166
    H&R Block                                                         166
    Century 21                                                        171
    First United Methodist Church                                     171
    Fastenal                                                          173
    Primerica                                                         176
    Chicago Public Schools                                            179
    Express Employment Professionals                                  180
    Minuteman Press                                                   201
    Primerica Financial Services                                      205
    Budget Blinds                                                     206
    BB&T                                                              217
    Regions Bank                                                      223
    Verizon Wireless                                                  224
    CENTURY 21                                                        229
    U.S. BANK                                                         253
    Mary Kay Cosmetics                                                271
    Coldwell Banker                                                   273
    NAPA Auto Parts                                                   280
    McDonald's                                                        281
    Liberty Tax Service                                               282
    Walgreens                                                         290
    RE/MAX                                                            303
    State Farm Insurance                                              317
    First Baptist Church                                              332
    First Presbyterian Church                                         336
    YMCA                                                              364
    Keller Williams Realty                                            422
    Ameriprise Financial                                              667
    Farmers Insurance                                                 821
    Name: name, dtype: int64
    
    590889
    
    4402483463     1
    9898666331     1
    5058925811     1
    2029068655     1
    2535367740     1
    8606321485     1
    7187227900     1
    8438523348     1
    9097987321     1
    8474411886     1
    9856496333     1
    6165270990     1
    9513400312     1
    2123749115     1
    5133856100     1
    5107242036     1
    3148624050     1
    5303010884     1
    9724365892     1
    4805390111     1
    2187249369     1
    7036272077     1
    9378362639     1
    8059340466     1
    5032226105     1
    8589673111     1
    3169435797     1
    6508544300     1
    3368829493     1
    5053349324     1
                  ..
    3239323200    11
    2813584545    11
    4062382500    11
    6173579500    11
    null          11
    9042187922    11
    2033732211    12
    2017969400    12
    2022610780    12
                  12
    2175287541    13
    8668785865    14
    7043865681    15
    2149993000    15
    2016042100    15
    8055572300    17
    0             18
    0             18
    8009994328    18
    2022234777    19
    9728706000    20
    2025438060    21
    2017983300    21
    none          22
    2032450456    24
    2027202500    31
    2025475600    38
    6126255000    50
    8002574725    50
    3037705531    88
    Name: phone, dtype: int64
    
    590798
    
    4402483463     1
    5039750111     1
    5107242036     1
    9898666331     1
    5058925811     1
    2029068655     1
    2535367740     1
    8606321485     1
    7187227900     1
    8438523348     1
    9097987321     1
    8474411886     1
    9856496333     1
    6165270990     1
    9513400312     1
    7603446471     1
    2123749115     1
    3148624050     1
    9378362631     1
    5303010884     1
    9724365892     1
    4805390111     1
    2187249369     1
    7036272077     1
    9378362639     1
    8059340466     1
    5032226105     1
    8589673111     1
    3169435797     1
    6508544300     1
                  ..
    2818974200    10
    2025297411    10
    6109401740    10
    2813584545    11
    3239323200    11
    9042187922    11
    6082621234    11
    6173579500    11
    4062382500    11
    2485457056    11
    2022610780    12
    2033732211    12
    2017969400    12
    2175287541    13
    8668785865    14
    2016042100    15
    7043865681    15
    2149993000    15
    8055572300    17
    8009994328    18
    2022234777    19
    9728706000    20
    2017983300    21
    2025438060    21
    2032450456    24
    2027202500    31
    2025475600    38
    6126255000    50
    8002574725    50
    3037705531    88
    Name: phone, dtype: int64
    
    943092
    
                                  11
    0                             15
    0                             15
    none                          15
                                  16
    null                          19
    Over $500 Million           1579
    Over $1 Billion             1769
    $100 to 500 Million        10130
    $50 to 100 Million         12765
    $20 to 50 Million          32797
    $10 to 20 Million          48454
    $5 to 10 Million           83924
    $2.5 to 5 Million          99245
    $500,000 to $1 Million    153163
    $1 to 2.5 Million         169540
    Less Than $500,000        329635
    Name: revenue, dtype: int64
    
    943001
    
    Over $500 Million           1579
    Over $1 Billion             1769
    $100 to 500 Million        10130
    $50 to 100 Million         12765
    $20 to 50 Million          32797
    $10 to 20 Million          48454
    $5 to 10 Million           83924
    $2.5 to 5 Million          99245
    $500,000 to $1 Million    153163
    $1 to 2.5 Million         169540
    Less Than $500,000        329635
    Name: revenue, dtype: int64
    
    999986
    
    VI           1
    PR           2
    none         9
    0           11
                14
                15
    null        20
    0           21
    WY        1858
    ND        2315
    AK        2515
    DE        2849
    VT        3029
    WV        3217
    SD        3306
    HI        3754
    MT        3817
    RI        3880
    DC        4499
    NM        5076
    ID        5135
    ME        5793
    MS        5864
    NH        6139
    NV        6700
    NE        7080
    AR        7377
    UT        8873
    OK       10456
    KS       10523
    IA       10880
    KY       11393
    AL       12172
    LA       12229
    SC       12842
    CT       15107
    OR       15690
    AZ       18152
    TN       18445
    WI       18754
    MO       19558
    IN       19861
    MD       19973
    CO       21781
    MN       22243
    WA       24295
    VA       27161
    NJ       28837
    GA       29797
    MA       30014
    NC       30389
    MI       31237
    OH       36524
    PA       40609
    IL       44126
    NY       57411
    FL       63245
    TX       70301
    CA      122812
    Name: state, dtype: int64
    
    999896
    
    VI         1
    PR         2
    WY      1858
    ND      2315
    AK      2515
    DE      2849
    VT      3029
    WV      3217
    SD      3306
    HI      3754
    MT      3817
    RI      3880
    DC      4499
    NM      5076
    ID      5135
    ME      5793
    MS      5864
    NH      6139
    NV      6700
    NE      7080
    AR      7377
    UT      8873
    OK     10456
    KS     10523
    IA     10880
    KY     11393
    AL     12172
    LA     12229
    SC     12842
    CT     15107
    OR     15690
    AZ     18152
    TN     18445
    WI     18754
    MO     19558
    IN     19861
    MD     19973
    CO     21781
    MN     22243
    WA     24295
    VA     27161
    NJ     28837
    GA     29797
    MA     30014
    NC     30389
    MI     31237
    OH     36524
    PA     40609
    IL     44126
    NY     57411
    FL     63245
    TX     70301
    CA    122812
    Name: state, dtype: int64
    
    916125
    
    Less than a year         1
    0                        7
                            11
                            13
    none                    14
    0                       15
    null                    17
    1-2 years            12756
    3-5 years            38280
    6-10 years          106144
    10+ years           758867
    Name: time_in_business, dtype: int64
    
    916048
    
    Less than a year         1
    1-2 years            12756
    3-5 years            38280
    6-10 years          106144
    10+ years           758867
    Name: time_in_business, dtype: int64
    
    999988
    
    38347       1
    31798       1
    28456       1
    28455       1
    28453       1
    13103       1
    13101       1
    15258       1
    30441       1
    62481       1
    49705       1
    46974       1
    29827       1
    19884       1
    53595       1
    43413       1
    46626       1
    19732       1
    38670       1
    18844       1
    04284       1
    56280       1
    56285       1
    11948       1
    21821       1
    93283       1
    93285       1
    61418       1
    56713       1
    56710       1
             ... 
    77002     529
    94111     531
    33166     533
    78746     544
    20850     545
    10013     548
    10010     561
    20005     562
    10003     586
    19103     589
    10011     591
    80112     591
    85260     652
    43215     657
    80202     657
    78701     673
    22314     681
    92618     686
    60606     698
    92660     706
    10036     712
    92121     712
    10019     719
    92101     730
    20036     802
    10017     840
    10016    1036
    10018    1067
    10022    1090
    10001    1151
    Name: zip, dtype: int64
    
    999890
    
    38347       1
    30441       1
    31798       1
    15258       1
    28456       1
    28455       1
    28453       1
    19732       1
    38670       1
    13103       1
    29827       1
    62481       1
    19884       1
    43413       1
    49705       1
    46974       1
    46626       1
    13101       1
    04284       1
    18844       1
    59259       1
    61417       1
    61418       1
    56713       1
    56280       1
    56285       1
    11948       1
    56710       1
    56714       1
    21821       1
             ... 
    77002     529
    94111     531
    33166     533
    78746     544
    20850     545
    10013     548
    10010     561
    20005     562
    10003     586
    19103     589
    80112     591
    10011     591
    85260     652
    43215     657
    80202     657
    78701     673
    22314     681
    92618     686
    60606     698
    92660     706
    10036     712
    92121     712
    10019     719
    92101     730
    20036     802
    10017     840
    10016    1036
    10018    1067
    10022    1090
    10001    1151
    Name: zip, dtype: int64
    





<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>address</th>
      <th>category_code</th>
      <th>city</th>
      <th>headcount</th>
      <th>name</th>
      <th>phone</th>
      <th>revenue</th>
      <th>state</th>
      <th>time_in_business</th>
      <th>zip</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10085 SCRIPPS RANCH CT STE A</td>
      <td>44420000</td>
      <td>SAN DIEGO</td>
      <td>50 to 99</td>
      <td>AMD CUSTOM</td>
      <td>3123628000</td>
      <td>$20 to 50 Million</td>
      <td>CA</td>
      <td>10+ years</td>
      <td>92131</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2566 SHALLOWFORD RD NE STE 104 # 302</td>
      <td>31490000</td>
      <td>ATLANTA</td>
      <td>1 to 4</td>
      <td>Real Hope Real Estate Inc</td>
      <td>NaN</td>
      <td>Less Than $500,000</td>
      <td>GA</td>
      <td>10+ years</td>
      <td>30345</td>
    </tr>
    <tr>
      <th>2</th>
      <td>212 E MAIN ST</td>
      <td>53120000</td>
      <td>NEOSHO</td>
      <td>1 to 4</td>
      <td>Jimmy Sexton Photography</td>
      <td>4046331779</td>
      <td>Less Than $500,000</td>
      <td>MO</td>
      <td>10+ years</td>
      <td>64850</td>
    </tr>
    <tr>
      <th>3</th>
      <td>6032 CHEROKEE DR</td>
      <td>54000000</td>
      <td>CINCINNATI</td>
      <td>1 to 4</td>
      <td>YOU'RE ART</td>
      <td>4174513798</td>
      <td>Less Than $500,000</td>
      <td>OH</td>
      <td>10+ years</td>
      <td>45243</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1315 N WOOSTER AVE</td>
      <td>54100000</td>
      <td>STRASBURG</td>
      <td>1 to 4</td>
      <td>Hayberg Restoration Network LLC</td>
      <td>5135612584</td>
      <td>$500,000 to $1 Million</td>
      <td>OH</td>
      <td>10+ years</td>
      <td>44680</td>
    </tr>
  </tbody>
</table>
</div>




```python
fieldSummary['True-ValuedFillRate'] = finalDF.count();
#fieldSummary['%presentIn'] = ((fieldSummary['presentIn']/numOfRecords)*100).round(4)
fieldSummary
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>fillRate</th>
      <th>True-ValuedFillRate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>address</th>
      <td>999986</td>
      <td>999898</td>
    </tr>
    <tr>
      <th>category_code</th>
      <td>999986</td>
      <td>999910</td>
    </tr>
    <tr>
      <th>city</th>
      <td>999986</td>
      <td>999895</td>
    </tr>
    <tr>
      <th>headcount</th>
      <td>962352</td>
      <td>962273</td>
    </tr>
    <tr>
      <th>name</th>
      <td>999986</td>
      <td>999877</td>
    </tr>
    <tr>
      <th>phone</th>
      <td>590889</td>
      <td>590798</td>
    </tr>
    <tr>
      <th>revenue</th>
      <td>943092</td>
      <td>943001</td>
    </tr>
    <tr>
      <th>state</th>
      <td>999986</td>
      <td>999896</td>
    </tr>
    <tr>
      <th>time_in_business</th>
      <td>916125</td>
      <td>916048</td>
    </tr>
    <tr>
      <th>zip</th>
      <td>999988</td>
      <td>999890</td>
    </tr>
  </tbody>
</table>
</div>



Above is the summary of True Valued Fill Rate along with normal fill rate.

Task-3:
--

- **Cardinality**: The cardinality of each field.

To measure Cardinality, we need to count number of unique values in the field. It is acheived by the following code.


```python
fieldSummary['Cardinality'] = finalDF.apply(pd.Series.nunique);
fieldSummary
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>fillRate</th>
      <th>True-ValuedFillRate</th>
      <th>Cardinality</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>address</th>
      <td>999986</td>
      <td>999898</td>
      <td>892114</td>
    </tr>
    <tr>
      <th>category_code</th>
      <td>999986</td>
      <td>999910</td>
      <td>1178</td>
    </tr>
    <tr>
      <th>city</th>
      <td>999986</td>
      <td>999895</td>
      <td>13714</td>
    </tr>
    <tr>
      <th>headcount</th>
      <td>962352</td>
      <td>962273</td>
      <td>9</td>
    </tr>
    <tr>
      <th>name</th>
      <td>999986</td>
      <td>999877</td>
      <td>890685</td>
    </tr>
    <tr>
      <th>phone</th>
      <td>590889</td>
      <td>590798</td>
      <td>575148</td>
    </tr>
    <tr>
      <th>revenue</th>
      <td>943092</td>
      <td>943001</td>
      <td>11</td>
    </tr>
    <tr>
      <th>state</th>
      <td>999986</td>
      <td>999896</td>
      <td>53</td>
    </tr>
    <tr>
      <th>time_in_business</th>
      <td>916125</td>
      <td>916048</td>
      <td>5</td>
    </tr>
    <tr>
      <th>zip</th>
      <td>999988</td>
      <td>999890</td>
      <td>26391</td>
    </tr>
  </tbody>
</table>
</div>



Above is the summary of Cardinality along with True Valued Fill Rate and normal fill rate. The same can be acheved by the below code as well.


```python
finalDF.describe()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>address</th>
      <th>category_code</th>
      <th>city</th>
      <th>headcount</th>
      <th>name</th>
      <th>phone</th>
      <th>revenue</th>
      <th>state</th>
      <th>time_in_business</th>
      <th>zip</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>999898</td>
      <td>999910</td>
      <td>999895</td>
      <td>962273</td>
      <td>999877</td>
      <td>590798</td>
      <td>943001</td>
      <td>999896</td>
      <td>916048</td>
      <td>999890</td>
    </tr>
    <tr>
      <th>unique</th>
      <td>892114</td>
      <td>1178</td>
      <td>13714</td>
      <td>9</td>
      <td>890685</td>
      <td>575148</td>
      <td>11</td>
      <td>53</td>
      <td>5</td>
      <td>26391</td>
    </tr>
    <tr>
      <th>top</th>
      <td>1 S DEARBORN ST</td>
      <td>61111000</td>
      <td>NEW YORK</td>
      <td>1 to 4</td>
      <td>Farmers Insurance</td>
      <td>3037705531</td>
      <td>Less Than $500,000</td>
      <td>CA</td>
      <td>10+ years</td>
      <td>10001</td>
    </tr>
    <tr>
      <th>freq</th>
      <td>76</td>
      <td>39461</td>
      <td>14264</td>
      <td>358207</td>
      <td>821</td>
      <td>88</td>
      <td>329635</td>
      <td>122812</td>
      <td>758867</td>
      <td>1151</td>
    </tr>
  </tbody>
</table>
</div>




Task-4:
--

- **Data Exploration**:

A basic preprocessing to have better visualization later on.


```python
t1 = finalDF.revenue
t1[t1 == 'Less Than $500,000'] = '1 - Less Than $500,000'
t1[t1 == '$500,000 to $1 Million'] = '2 - $500,000 to $1 Million'
t1[t1 == '$1 to 2.5 Million'] = '3 - $1 to 2.5 Million'
t1[t1 == '$2.5 to 5 Million'] = '4 - $2.5 to 5 Million'
t1[t1 == '$5 to 10 Million'] = '5 - $5 to 10 Million'
t1[t1 == '$10 to 20 Million'] = '6 - $10 to 20 Million'
t1[t1 == '$20 to 50 Million'] = '7 - $20 to 50 Million'
t1[t1 == '$50 to 100 Million'] = '8 - $50 to 100 Million'
t1[t1 == '$100 to 500 Million'] = '9 - $100 to 500 Million'
t1[t1 == 'Over $500 Million'] = 'a10 - Over $500 Million'
t1[t1 == 'Over $1 Billion'] = 'b11 - Over $1 Billion'
print t1.value_counts()
finalDF.revenue = t1
```

    1 - Less Than $500,000        329635
    3 - $1 to 2.5 Million         169540
    2 - $500,000 to $1 Million    153163
    4 - $2.5 to 5 Million          99245
    5 - $5 to 10 Million           83924
    6 - $10 to 20 Million          48454
    7 - $20 to 50 Million          32797
    8 - $50 to 100 Million         12765
    9 - $100 to 500 Million        10130
    b11 - Over $1 Billion           1769
    a10 - Over $500 Million         1579
    Name: revenue, dtype: int64


Around **33%** of the companies in the data set have revnenues less than **$500k**.


```python
t1 = finalDF.headcount
t1[t1 == '1 to 4'] = '1 - 1 to 4'
t1[t1 == '5 to 9'] = '2 - 5 to 9'
t1[t1 == '10 to 19'] = '3 - 10 to 19'
t1[t1 == '20 to 49'] = '4 - 20 to 49'
t1[t1 == '50 to 99'] = '5 - 50 to 99'
t1[t1 == '100 to 249'] = '6 - 100 to 249'
t1[t1 == '250 to 499'] = '7 - 250 to 499'
t1[t1 == '500 to 999'] = '8 - 500 to 999'
t1[t1 == 'Over 1,000'] = '9 - Over 1,000'
print t1.value_counts()
finalDF.headcount = t1
```

    1 - 1 to 4        358207
    2 - 5 to 9        212401
    3 - 10 to 19      151412
    4 - 20 to 49      121264
    5 - 50 to 99       60526
    6 - 100 to 249     36475
    7 - 250 to 499     11138
    9 - Over 1,000      5600
    8 - 500 to 999      5250
    Name: headcount, dtype: int64


Around **57%** of the companies in the data set have headcount less than **10**. This two facts show that most of the companies in the data set are small businesses.


```python
t1 = finalDF.time_in_business
t1[t1 == 'Less than a year'] = '1 - Less than a year'
t1[t1 == '1-2 years'] = '2 - 1-2 years'
t1[t1 == '3-5 years'] = '3 - 3-5 years'
t1[t1 == '6-10 years'] = '4 - 6-10 years'
t1[t1 == '10+ years'] = '5 - 10+ years'
print t1.value_counts()
#finalDF.time_in_business = t1
```

    5 - 10+ years           758867
    4 - 6-10 years          106144
    3 - 3-5 years            38280
    2 - 1-2 years            12756
    1 - Less than a year         1
    Name: time_in_business, dtype: int64


Around **75%** of the companies in the data set are into business more than a decade (**10+ years old**).


```python
print finalDF.groupby(['headcount', 'revenue']).size().to_string()
```

    headcount       revenue                   
    1 - 1 to 4      1 - Less Than $500,000        118413
                    2 - $500,000 to $1 Million     54860
                    3 - $1 to 2.5 Million          60658
                    4 - $2.5 to 5 Million          35200
                    5 - $5 to 10 Million           30066
                    6 - $10 to 20 Million          17335
                    7 - $20 to 50 Million          11656
                    8 - $50 to 100 Million          4586
                    9 - $100 to 500 Million         3654
                    a10 - Over $500 Million          582
                    b11 - Over $1 Billion            655
    2 - 5 to 9      1 - Less Than $500,000         69714
                    2 - $500,000 to $1 Million     32718
                    3 - $1 to 2.5 Million          36065
                    4 - $2.5 to 5 Million          21032
                    5 - $5 to 10 Million           17965
                    6 - $10 to 20 Million          10275
                    7 - $20 to 50 Million           6965
                    8 - $50 to 100 Million          2735
                    9 - $100 to 500 Million         2150
                    a10 - Over $500 Million          330
                    b11 - Over $1 Billion            389
    3 - 10 to 19    1 - Less Than $500,000         49889
                    2 - $500,000 to $1 Million     23159
                    3 - $1 to 2.5 Million          25877
                    4 - $2.5 to 5 Million          15092
                    5 - $5 to 10 Million           12724
                    6 - $10 to 20 Million           7184
                    7 - $20 to 50 Million           4961
                    8 - $50 to 100 Million          1934
                    9 - $100 to 500 Million         1494
                    a10 - Over $500 Million          244
                    b11 - Over $1 Billion            239
    4 - 20 to 49    1 - Less Than $500,000         40057
                    2 - $500,000 to $1 Million     18361
                    3 - $1 to 2.5 Million          20444
                    4 - $2.5 to 5 Million          12147
                    5 - $5 to 10 Million           10090
                    6 - $10 to 20 Million           5960
                    7 - $20 to 50 Million           4090
                    8 - $50 to 100 Million          1542
                    9 - $100 to 500 Million         1191
                    a10 - Over $500 Million          194
                    b11 - Over $1 Billion            245
    5 - 50 to 99    1 - Less Than $500,000         20020
                    2 - $500,000 to $1 Million      9350
                    3 - $1 to 2.5 Million          10152
                    4 - $2.5 to 5 Million           6095
                    5 - $5 to 10 Million            4988
                    6 - $10 to 20 Million           2959
                    7 - $20 to 50 Million           1995
                    8 - $50 to 100 Million           764
                    9 - $100 to 500 Million          638
                    a10 - Over $500 Million           94
                    b11 - Over $1 Billion             87
    6 - 100 to 249  1 - Less Than $500,000         12061
                    2 - $500,000 to $1 Million      5553
                    3 - $1 to 2.5 Million           6137
                    4 - $2.5 to 5 Million           3677
                    5 - $5 to 10 Million            2996
                    6 - $10 to 20 Million           1828
                    7 - $20 to 50 Million           1175
                    8 - $50 to 100 Million           450
                    9 - $100 to 500 Million          399
                    a10 - Over $500 Million           48
                    b11 - Over $1 Billion             63
    7 - 250 to 499  1 - Less Than $500,000          3689
                    2 - $500,000 to $1 Million      1684
                    3 - $1 to 2.5 Million           1888
                    4 - $2.5 to 5 Million           1103
                    5 - $5 to 10 Million             953
                    6 - $10 to 20 Million            551
                    7 - $20 to 50 Million            336
                    8 - $50 to 100 Million           154
                    9 - $100 to 500 Million          105
                    a10 - Over $500 Million           12
                    b11 - Over $1 Billion             16
    8 - 500 to 999  1 - Less Than $500,000          1671
                    2 - $500,000 to $1 Million       807
                    3 - $1 to 2.5 Million            882
                    4 - $2.5 to 5 Million            533
                    5 - $5 to 10 Million             438
                    6 - $10 to 20 Million            292
                    7 - $20 to 50 Million            173
                    8 - $50 to 100 Million            65
                    9 - $100 to 500 Million           64
                    a10 - Over $500 Million           12
                    b11 - Over $1 Billion              9
    9 - Over 1,000  1 - Less Than $500,000          1826
                    2 - $500,000 to $1 Million       893
                    3 - $1 to 2.5 Million            937
                    4 - $2.5 to 5 Million            547
                    5 - $5 to 10 Million             492
                    6 - $10 to 20 Million            265
                    7 - $20 to 50 Million            186
                    8 - $50 to 100 Million            76
                    9 - $100 to 500 Million           56
                    a10 - Over $500 Million            9
                    b11 - Over $1 Billion             11


Its surprising to see that companies with headcount < 10 are **59%** of the companies with over **$1 Billion** in revennues. Large work force is not resulting in higher revenues.


```python
finalDF.groupby(['time_in_business', 'revenue']).size()
```




    time_in_business      revenue                   
    1 - Less than a year  4 - $2.5 to 5 Million              1
    2 - 1-2 years         1 - Less Than $500,000          4190
                          2 - $500,000 to $1 Million      1918
                          3 - $1 to 2.5 Million           2163
                          4 - $2.5 to 5 Million           1217
                          5 - $5 to 10 Million            1097
                          6 - $10 to 20 Million            666
                          7 - $20 to 50 Million            457
                          8 - $50 to 100 Million           174
                          9 - $100 to 500 Million          140
                          a10 - Over $500 Million           15
                          b11 - Over $1 Billion             18
    3 - 3-5 years         1 - Less Than $500,000         12627
                          2 - $500,000 to $1 Million      5844
                          3 - $1 to 2.5 Million           6558
                          4 - $2.5 to 5 Million           3794
                          5 - $5 to 10 Million            3149
                          6 - $10 to 20 Million           1822
                          7 - $20 to 50 Million           1220
                          8 - $50 to 100 Million           497
                          9 - $100 to 500 Million          414
                          a10 - Over $500 Million           54
                          b11 - Over $1 Billion             65
    4 - 6-10 years        1 - Less Than $500,000         35055
                          2 - $500,000 to $1 Million     16400
                          3 - $1 to 2.5 Million          17912
                          4 - $2.5 to 5 Million          10467
                          5 - $5 to 10 Million            8906
                          6 - $10 to 20 Million           5047
                          7 - $20 to 50 Million           3542
                          8 - $50 to 100 Million          1380
                          9 - $100 to 500 Million         1085
                          a10 - Over $500 Million          167
                          b11 - Over $1 Billion            189
    5 - 10+ years         1 - Less Than $500,000        249921
                          2 - $500,000 to $1 Million    116260
                          3 - $1 to 2.5 Million         128463
                          4 - $2.5 to 5 Million          75614
                          5 - $5 to 10 Million           63853
                          6 - $10 to 20 Million          36851
                          7 - $20 to 50 Million          24813
                          8 - $50 to 100 Million          9670
                          9 - $100 to 500 Million         7640
                          a10 - Over $500 Million         1215
                          b11 - Over $1 Billion           1339
    dtype: int64



As the time in business increases, the companies are performing well in terms of their revenues.


```python
print finalDF.groupby(['time_in_business', 'headcount', 'revenue']).size().to_string()
```

    time_in_business  headcount       revenue                   
    2 - 1-2 years     1 - 1 to 4      1 - Less Than $500,000         1488
                                      2 - $500,000 to $1 Million      656
                                      3 - $1 to 2.5 Million           780
                                      4 - $2.5 to 5 Million           433
                                      5 - $5 to 10 Million            380
                                      6 - $10 to 20 Million           230
                                      7 - $20 to 50 Million           168
                                      8 - $50 to 100 Million           55
                                      9 - $100 to 500 Million          52
                                      a10 - Over $500 Million           4
                                      b11 - Over $1 Billion             8
                      2 - 5 to 9      1 - Less Than $500,000          893
                                      2 - $500,000 to $1 Million      389
                                      3 - $1 to 2.5 Million           458
                                      4 - $2.5 to 5 Million           277
                                      5 - $5 to 10 Million            227
                                      6 - $10 to 20 Million           151
                                      7 - $20 to 50 Million            84
                                      8 - $50 to 100 Million           49
                                      9 - $100 to 500 Million          26
                                      a10 - Over $500 Million           3
                                      b11 - Over $1 Billion             5
                      3 - 10 to 19    1 - Less Than $500,000          630
                                      2 - $500,000 to $1 Million      327
                                      3 - $1 to 2.5 Million           310
                                      4 - $2.5 to 5 Million           170
                                      5 - $5 to 10 Million            187
                                      6 - $10 to 20 Million            92
                                      7 - $20 to 50 Million            69
                                      8 - $50 to 100 Million           26
                                      9 - $100 to 500 Million          24
                                      a10 - Over $500 Million           5
                                      b11 - Over $1 Billion             2
                      4 - 20 to 49    1 - Less Than $500,000          510
                                      2 - $500,000 to $1 Million      229
                                      3 - $1 to 2.5 Million           285
                                      4 - $2.5 to 5 Million           151
                                      5 - $5 to 10 Million            134
                                      6 - $10 to 20 Million            87
                                      7 - $20 to 50 Million            62
                                      8 - $50 to 100 Million           12
                                      9 - $100 to 500 Million          15
                                      a10 - Over $500 Million           3
                                      b11 - Over $1 Billion             2
                      5 - 50 to 99    1 - Less Than $500,000          256
                                      2 - $500,000 to $1 Million      135
                                      3 - $1 to 2.5 Million           120
                                      4 - $2.5 to 5 Million            55
                                      5 - $5 to 10 Million             53
                                      6 - $10 to 20 Million            40
                                      7 - $20 to 50 Million            34
                                      8 - $50 to 100 Million            7
                                      9 - $100 to 500 Million          10
                      6 - 100 to 249  1 - Less Than $500,000          167
                                      2 - $500,000 to $1 Million       67
                                      3 - $1 to 2.5 Million            67
                                      4 - $2.5 to 5 Million            58
                                      5 - $5 to 10 Million             44
                                      6 - $10 to 20 Million            25
                                      7 - $20 to 50 Million            13
                                      8 - $50 to 100 Million           10
                                      9 - $100 to 500 Million           5
                      7 - 250 to 499  1 - Less Than $500,000           52
                                      2 - $500,000 to $1 Million       20
                                      3 - $1 to 2.5 Million            30
                                      4 - $2.5 to 5 Million            11
                                      5 - $5 to 10 Million             10
                                      6 - $10 to 20 Million             6
                                      7 - $20 to 50 Million             4
                                      8 - $50 to 100 Million            1
                                      9 - $100 to 500 Million           1
                      8 - 500 to 999  1 - Less Than $500,000           17
                                      2 - $500,000 to $1 Million        9
                                      3 - $1 to 2.5 Million            14
                                      4 - $2.5 to 5 Million            11
                                      5 - $5 to 10 Million              5
                                      6 - $10 to 20 Million             5
                                      7 - $20 to 50 Million             2
                                      8 - $50 to 100 Million            1
                      9 - Over 1,000  1 - Less Than $500,000           28
                                      2 - $500,000 to $1 Million       13
                                      3 - $1 to 2.5 Million            17
                                      4 - $2.5 to 5 Million             3
                                      5 - $5 to 10 Million              7
                                      6 - $10 to 20 Million             5
                                      7 - $20 to 50 Million             2
                                      8 - $50 to 100 Million            2
                                      9 - $100 to 500 Million           2
    3 - 3-5 years     1 - 1 to 4      1 - Less Than $500,000         4537
                                      2 - $500,000 to $1 Million     2087
                                      3 - $1 to 2.5 Million          2395
                                      4 - $2.5 to 5 Million          1406
                                      5 - $5 to 10 Million           1140
                                      6 - $10 to 20 Million           693
                                      7 - $20 to 50 Million           414
                                      8 - $50 to 100 Million          180
                                      9 - $100 to 500 Million         165
                                      a10 - Over $500 Million          19
                                      b11 - Over $1 Billion            33
                      2 - 5 to 9      1 - Less Than $500,000         2712
                                      2 - $500,000 to $1 Million     1268
                                      3 - $1 to 2.5 Million          1390
                                      4 - $2.5 to 5 Million           768
                                      5 - $5 to 10 Million            664
                                      6 - $10 to 20 Million           369
                                      7 - $20 to 50 Million           278
                                      8 - $50 to 100 Million          105
                                      9 - $100 to 500 Million          90
                                      a10 - Over $500 Million           9
                                      b11 - Over $1 Billion            10
                      3 - 10 to 19    1 - Less Than $500,000         1873
                                      2 - $500,000 to $1 Million      912
                                      3 - $1 to 2.5 Million           950
                                      4 - $2.5 to 5 Million           593
                                      5 - $5 to 10 Million            484
                                      6 - $10 to 20 Million           266
                                      7 - $20 to 50 Million           190
                                      8 - $50 to 100 Million           89
                                      9 - $100 to 500 Million          64
                                      a10 - Over $500 Million          11
                                      b11 - Over $1 Billion             6
                      4 - 20 to 49    1 - Less Than $500,000         1546
                                      2 - $500,000 to $1 Million      640
                                      3 - $1 to 2.5 Million           797
                                      4 - $2.5 to 5 Million           483
                                      5 - $5 to 10 Million            380
                                      6 - $10 to 20 Million           222
                                      7 - $20 to 50 Million           157
                                      8 - $50 to 100 Million           56
                                      9 - $100 to 500 Million          41
                                      a10 - Over $500 Million           8
                                      b11 - Over $1 Billion             8
                      5 - 50 to 99    1 - Less Than $500,000          763
                                      2 - $500,000 to $1 Million      380
                                      3 - $1 to 2.5 Million           380
                                      4 - $2.5 to 5 Million           203
                                      5 - $5 to 10 Million            165
                                      6 - $10 to 20 Million           117
                                      7 - $20 to 50 Million            65
                                      8 - $50 to 100 Million           26
                                      9 - $100 to 500 Million          25
                                      a10 - Over $500 Million           2
                                      b11 - Over $1 Billion             5
                      6 - 100 to 249  1 - Less Than $500,000          449
                                      2 - $500,000 to $1 Million      210
                                      3 - $1 to 2.5 Million           235
                                      4 - $2.5 to 5 Million           133
                                      5 - $5 to 10 Million            122
                                      6 - $10 to 20 Million            54
                                      7 - $20 to 50 Million            38
                                      8 - $50 to 100 Million           16
                                      9 - $100 to 500 Million          10
                                      a10 - Over $500 Million           2
                      7 - 250 to 499  1 - Less Than $500,000          128
                                      2 - $500,000 to $1 Million       61
                                      3 - $1 to 2.5 Million            82
                                      4 - $2.5 to 5 Million            30
                                      5 - $5 to 10 Million             41
                                      6 - $10 to 20 Million            13
                                      7 - $20 to 50 Million            15
                                      8 - $50 to 100 Million            3
                                      9 - $100 to 500 Million           1
                      8 - 500 to 999  1 - Less Than $500,000           63
                                      2 - $500,000 to $1 Million       31
                                      3 - $1 to 2.5 Million            32
                                      4 - $2.5 to 5 Million            18
                                      5 - $5 to 10 Million             17
                                      6 - $10 to 20 Million            13
                                      7 - $20 to 50 Million             4
                                      8 - $50 to 100 Million            2
                                      9 - $100 to 500 Million           3
                                      b11 - Over $1 Billion             1
                      9 - Over 1,000  1 - Less Than $500,000           64
                                      2 - $500,000 to $1 Million       39
                                      3 - $1 to 2.5 Million            40
                                      4 - $2.5 to 5 Million            23
                                      5 - $5 to 10 Million             22
                                      6 - $10 to 20 Million            11
                                      7 - $20 to 50 Million             7
                                      8 - $50 to 100 Million            1
                                      9 - $100 to 500 Million           1
                                      a10 - Over $500 Million           1
    4 - 6-10 years    1 - 1 to 4      1 - Less Than $500,000        12641
                                      2 - $500,000 to $1 Million     5941
                                      3 - $1 to 2.5 Million          6506
                                      4 - $2.5 to 5 Million          3758
                                      5 - $5 to 10 Million           3221
                                      6 - $10 to 20 Million          1809
                                      7 - $20 to 50 Million          1271
                                      8 - $50 to 100 Million          478
                                      9 - $100 to 500 Million         383
                                      a10 - Over $500 Million          54
                                      b11 - Over $1 Billion            67
                      2 - 5 to 9      1 - Less Than $500,000         7506
                                      2 - $500,000 to $1 Million     3421
                                      3 - $1 to 2.5 Million          3788
                                      4 - $2.5 to 5 Million          2232
                                      5 - $5 to 10 Million           1898
                                      6 - $10 to 20 Million          1089
                                      7 - $20 to 50 Million           766
                                      8 - $50 to 100 Million          310
                                      9 - $100 to 500 Million         230
                                      a10 - Over $500 Million          30
                                      b11 - Over $1 Billion            45
                      3 - 10 to 19    1 - Less Than $500,000         5238
                                      2 - $500,000 to $1 Million     2470
                                      3 - $1 to 2.5 Million          2730
                                      4 - $2.5 to 5 Million          1580
                                      5 - $5 to 10 Million           1323
                                      6 - $10 to 20 Million           729
                                      7 - $20 to 50 Million           526
                                      8 - $50 to 100 Million          224
                                      9 - $100 to 500 Million         183
                                      a10 - Over $500 Million          27
                                      b11 - Over $1 Billion            22
                      4 - 20 to 49    1 - Less Than $500,000         4138
                                      2 - $500,000 to $1 Million     1976
                                      3 - $1 to 2.5 Million          2143
                                      4 - $2.5 to 5 Million          1256
                                      5 - $5 to 10 Million           1095
                                      6 - $10 to 20 Million           615
                                      7 - $20 to 50 Million           446
                                      8 - $50 to 100 Million          172
                                      9 - $100 to 500 Million         124
                                      a10 - Over $500 Million          27
                                      b11 - Over $1 Billion            24
                      5 - 50 to 99    1 - Less Than $500,000         2203
                                      2 - $500,000 to $1 Million      987
                                      3 - $1 to 2.5 Million          1058
                                      4 - $2.5 to 5 Million           627
                                      5 - $5 to 10 Million            544
                                      6 - $10 to 20 Million           313
                                      7 - $20 to 50 Million           199
                                      8 - $50 to 100 Million           68
                                      9 - $100 to 500 Million          60
                                      a10 - Over $500 Million           6
                                      b11 - Over $1 Billion             8
                      6 - 100 to 249  1 - Less Than $500,000         1289
                                      2 - $500,000 to $1 Million      592
                                      3 - $1 to 2.5 Million           625
                                      4 - $2.5 to 5 Million           399
                                      5 - $5 to 10 Million            315
                                      6 - $10 to 20 Million           176
                                      7 - $20 to 50 Million           125
                                      8 - $50 to 100 Million           64
                                      9 - $100 to 500 Million          51
                                      a10 - Over $500 Million           7
                                      b11 - Over $1 Billion             9
                      7 - 250 to 499  1 - Less Than $500,000          386
                                      2 - $500,000 to $1 Million      189
                                      3 - $1 to 2.5 Million           194
                                      4 - $2.5 to 5 Million           118
                                      5 - $5 to 10 Million             90
                                      6 - $10 to 20 Million            63
                                      7 - $20 to 50 Million            32
                                      8 - $50 to 100 Million           13
                                      9 - $100 to 500 Million           7
                                      a10 - Over $500 Million           2
                                      b11 - Over $1 Billion             2
                      8 - 500 to 999  1 - Less Than $500,000          172
                                      2 - $500,000 to $1 Million       84
                                      3 - $1 to 2.5 Million            96
                                      4 - $2.5 to 5 Million            67
                                      5 - $5 to 10 Million             47
                                      6 - $10 to 20 Million            29
                                      7 - $20 to 50 Million            19
                                      8 - $50 to 100 Million            3
                                      9 - $100 to 500 Million           2
                                      a10 - Over $500 Million           6
                                      b11 - Over $1 Billion             1
                      9 - Over 1,000  1 - Less Than $500,000          201
                                      2 - $500,000 to $1 Million      113
                                      3 - $1 to 2.5 Million           100
                                      4 - $2.5 to 5 Million            61
                                      5 - $5 to 10 Million             54
                                      6 - $10 to 20 Million            24
                                      7 - $20 to 50 Million            20
                                      8 - $50 to 100 Million            5
                                      9 - $100 to 500 Million           6
                                      a10 - Over $500 Million           1
    5 - 10+ years     1 - 1 to 4      1 - Less Than $500,000        89865
                                      2 - $500,000 to $1 Million    41670
                                      3 - $1 to 2.5 Million         45844
                                      4 - $2.5 to 5 Million         26693
                                      5 - $5 to 10 Million          22785
                                      6 - $10 to 20 Million         13116
                                      7 - $20 to 50 Million          8845
                                      8 - $50 to 100 Million         3514
                                      9 - $100 to 500 Million        2729
                                      a10 - Over $500 Million         450
                                      b11 - Over $1 Billion           494
                      2 - 5 to 9      1 - Less Than $500,000        52729
                                      2 - $500,000 to $1 Million    24827
                                      3 - $1 to 2.5 Million         27363
                                      4 - $2.5 to 5 Million         16077
                                      5 - $5 to 10 Million          13654
                                      6 - $10 to 20 Million          7816
                                      7 - $20 to 50 Million          5223
                                      8 - $50 to 100 Million         2043
                                      9 - $100 to 500 Million        1634
                                      a10 - Over $500 Million         263
                                      b11 - Over $1 Billion           293
                      3 - 10 to 19    1 - Less Than $500,000        37899
                                      2 - $500,000 to $1 Million    17475
                                      3 - $1 to 2.5 Million         19625
                                      4 - $2.5 to 5 Million         11525
                                      5 - $5 to 10 Million           9696
                                      6 - $10 to 20 Million          5519
                                      7 - $20 to 50 Million          3770
                                      8 - $50 to 100 Million         1408
                                      9 - $100 to 500 Million        1110
                                      a10 - Over $500 Million         185
                                      b11 - Over $1 Billion           185
                      4 - 20 to 49    1 - Less Than $500,000        30382
                                      2 - $500,000 to $1 Million    14041
                                      3 - $1 to 2.5 Million         15504
                                      4 - $2.5 to 5 Million          9177
                                      5 - $5 to 10 Million           7681
                                      6 - $10 to 20 Million          4541
                                      7 - $20 to 50 Million          3061
                                      8 - $50 to 100 Million         1178
                                      9 - $100 to 500 Million         909
                                      a10 - Over $500 Million         146
                                      b11 - Over $1 Billion           189
                      5 - 50 to 99    1 - Less Than $500,000        15139
                                      2 - $500,000 to $1 Million     7092
                                      3 - $1 to 2.5 Million          7705
                                      4 - $2.5 to 5 Million          4744
                                      5 - $5 to 10 Million           3846
                                      6 - $10 to 20 Million          2243
                                      7 - $20 to 50 Million          1537
                                      8 - $50 to 100 Million          614
                                      9 - $100 to 500 Million         490
                                      a10 - Over $500 Million          78
                                      b11 - Over $1 Billion            66
                      6 - 100 to 249  1 - Less Than $500,000         9131
                                      2 - $500,000 to $1 Million     4246
                                      3 - $1 to 2.5 Million          4697
                                      4 - $2.5 to 5 Million          2776
                                      5 - $5 to 10 Million           2277
                                      6 - $10 to 20 Million          1411
                                      7 - $20 to 50 Million           899
                                      8 - $50 to 100 Million          324
                                      9 - $100 to 500 Million         302
                                      a10 - Over $500 Million          37
                                      b11 - Over $1 Billion            45
                      7 - 250 to 499  1 - Less Than $500,000         2816
                                      2 - $500,000 to $1 Million     1288
                                      3 - $1 to 2.5 Million          1442
                                      4 - $2.5 to 5 Million           862
                                      5 - $5 to 10 Million            730
                                      6 - $10 to 20 Million           428
                                      7 - $20 to 50 Million           258
                                      8 - $50 to 100 Million          127
                                      9 - $100 to 500 Million          83
                                      a10 - Over $500 Million           7
                                      b11 - Over $1 Billion            14
                      8 - 500 to 999  1 - Less Than $500,000         1292
                                      2 - $500,000 to $1 Million      618
                                      3 - $1 to 2.5 Million           666
                                      4 - $2.5 to 5 Million           400
                                      5 - $5 to 10 Million            337
                                      6 - $10 to 20 Million           216
                                      7 - $20 to 50 Million           133
                                      8 - $50 to 100 Million           53
                                      9 - $100 to 500 Million          51
                                      a10 - Over $500 Million           5
                                      b11 - Over $1 Billion             4
                      9 - Over 1,000  1 - Less Than $500,000         1365
                                      2 - $500,000 to $1 Million      660
                                      3 - $1 to 2.5 Million           681
                                      4 - $2.5 to 5 Million           413
                                      5 - $5 to 10 Million            375
                                      6 - $10 to 20 Million           200
                                      7 - $20 to 50 Million           148
                                      8 - $50 to 100 Million           63
                                      9 - $100 to 500 Million          38
                                      a10 - Over $500 Million           7
                                      b11 - Over $1 Billion            10


Above summary shows that our previous analysis holds good and in each segment we have more companies with lesser revenues than higher revenues.
