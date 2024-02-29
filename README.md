# Case Study : Which coupon to offer drivers?
The dataset under study contains information on drivers who were offered a coupon to one of the following : Bar, Carry Out Food Place, Cheap Restaurant, Expensive Restaurant, Coffee House, and whether they accepted it or not along with other characteristics. The goal of this case study is to come up with rules which can help determine what coupon a particular driver with given characteristics will accept with high probability.

## 1. Business Understanding
To promote local businesses, coupons to those businesses are offered to drivers passing by. While the proximity of the business is a factor in determining what coupon to offer, the other important factor is to know whether the driver will be inclined to accept the coupon. For example, if  there is a Bar and a Coffee House nearby, which coupon would the driver accept if he has a minor in the vehicle? It will help to know the probability of accepting the coupons iven the conditions which in turn will help with the original goal of promoting local businesses.

### 1.1 Business Goals
1. Gain insight into characteristics that determine coupon acceptance
2. Put down rules to offer a particular coupon to a driver

## 2. Data Understanding
Here we take an initial look at the given data and explore the quality of it.

### 2.1 Gather Data And Describe
Data comes from UCI Machine Learning repository and was collected via a survey on Amazon Mechanical Turk.

Here is a sample of the data:

<div class="overflow-table">

|    | destination     | passanger   | weather   |   temperature | time   | coupon                | expiration   | gender   |   age | maritalStatus     |   has_children | education                | occupation   | income          |   car | Bar   | CoffeeHouse   |   CarryAway | RestaurantLessThan20   | Restaurant20To50   |   toCoupon_GEQ5min |   toCoupon_GEQ15min |   toCoupon_GEQ25min |   direction_same |   direction_opp |   Y |
|---:|:----------------|:------------|:----------|--------------:|:-------|:----------------------|:-------------|:---------|------:|:------------------|---------------:|:-------------------------|:-------------|:----------------|------:|:------|:--------------|------------:|:-----------------------|:-------------------|-------------------:|--------------------:|--------------------:|-----------------:|----------------:|----:|
|  0 | No Urgent Place | Alone       | Sunny     |            55 | 2PM    | Restaurant(<20)       | 1d           | Female   |    21 | Unmarried partner |              1 | Some college - no degree | Unemployed   | $37500 - $49999 |   nan | never | never         |         nan | 4~8                    | 1~3                |                  1 |                   0 |                   0 |                0 |               1 |   1 |
|  1 | No Urgent Place | Friend(s)   | Sunny     |            80 | 10AM   | Coffee House          | 2h           | Female   |    21 | Unmarried partner |              1 | Some college - no degree | Unemployed   | $37500 - $49999 |   nan | never | never         |         nan | 4~8                    | 1~3                |                  1 |                   0 |                   0 |                0 |               1 |   0 |
|  2 | No Urgent Place | Friend(s)   | Sunny     |            80 | 10AM   | Carry out & Take away | 2h           | Female   |    21 | Unmarried partner |              1 | Some college - no degree | Unemployed   | $37500 - $49999 |   nan | never | never         |         nan | 4~8                    | 1~3                |                  1 |                   1 |                   0 |                0 |               1 |   1 |
|  3 | No Urgent Place | Friend(s)   | Sunny     |            80 | 2PM    | Coffee House          | 2h           | Female   |    21 | Unmarried partner |              1 | Some college - no degree | Unemployed   | $37500 - $49999 |   nan | never | never         |         nan | 4~8                    | 1~3                |                  1 |                   1 |                   0 |                0 |               1 |   0 |
|  4 | No Urgent Place | Friend(s)   | Sunny     |            80 | 2PM    | Coffee House          | 1d           | Female   |    21 | Unmarried partner |              1 | Some college - no degree | Unemployed   | $37500 - $49999 |   nan | never | never         |         nan | 4~8                    | 1~3                |                  1 |                   1 |                   0 |                0 |               1 |   0 |
|  5 | No Urgent Place | Friend(s)   | Sunny     |            80 | 6PM    | Restaurant(<20)       | 2h           | Female   |    21 | Unmarried partner |              1 | Some college - no degree | Unemployed   | $37500 - $49999 |   nan | never | never         |         nan | 4~8                    | 1~3                |                  1 |                   1 |                   0 |                0 |               1 |   1 |
|  6 | No Urgent Place | Friend(s)   | Sunny     |            55 | 2PM    | Carry out & Take away | 1d           | Female   |    21 | Unmarried partner |              1 | Some college - no degree | Unemployed   | $37500 - $49999 |   nan | never | never         |         nan | 4~8                    | 1~3                |                  1 |                   1 |                   0 |                0 |               1 |   1 

</div>
The description of the attributes are as follows:
The attributes of this data set include:
1. User attributes
    -  Gender: male, female
    -  Age: below 21, 21 to 25, 26 to 30, etc.
    -  Marital Status: single, married partner, unmarried partner, or widowed
    -  Number of children: 0, 1, or more than 1
    -  Education: high school, bachelors degree, associates degree, or graduate degree
    -  Occupation: architecture & engineering, business & financial, etc.
    -  Annual income: less than \\$12500, \\$12500 - \\$24999, \\$25000 - \\$37499, etc.
    -  Number of times that he/she goes to a bar: 0, less than 1, 1 to 3, 4 to 8 or greater than 8
    -  Number of times that he/she buys takeaway food: 0, less than 1, 1 to 3, 4 to 8 or greater
    than 8
    -  Number of times that he/she goes to a coffee house: 0, less than 1, 1 to 3, 4 to 8 or
    greater than 8
    -  Number of times that he/she eats at a restaurant with average expense less than \\$20 per
    person: 0, less than 1, 1 to 3, 4 to 8 or greater than 8
    -  Number of times that he/she goes to a bar: 0, less than 1, 1 to 3, 4 to 8 or greater than 8
    

2. Contextual attributes
    - Driving destination: home, work, or no urgent destination
    - Location of user, coupon and destination: we provide a map to show the geographical
    location of the user, destination, and the venue, and we mark the distance between each
    two places with time of driving. The user can see whether the venue is in the same
    direction as the destination.
    - Weather: sunny, rainy, or snowy
    - Temperature: 30F, 55F, or 80F
    - Time: 10AM, 2PM, or 6PM
    - Passenger: alone, partner, kid(s), or friend(s)


3. Coupon attributes
    - time before it expires: 2 hours or one day



More info on the type of data:

RangeIndex: 12684 entries, 0 to 12683
Data columns (total 26 columns):
 id   Column                Non-Null Count  Dtype 
---  ------                --------------  ----- 
 0   destination           12684 non-null  object
 1   passanger             12684 non-null  object
 2   weather               12684 non-null  object
 3   temperature           12684 non-null  int64 
 4   time                  12684 non-null  object
 5   coupon                12684 non-null  object
 6   expiration            12684 non-null  object
 7   gender                12684 non-null  object
 8   age                   12684 non-null  object
 9   maritalStatus         12684 non-null  object
 10  has_children          12684 non-null  int64 
 11  education             12684 non-null  object
 12  occupation            12684 non-null  object
 13  income                12684 non-null  object
 14  car                   108 non-null    object
 15  Bar                   12577 non-null  object
 16  CoffeeHouse           12467 non-null  object
 17  CarryAway             12533 non-null  object
 18  RestaurantLessThan20  12554 non-null  object
 19  Restaurant20To50      12495 non-null  object
 20  toCoupon_GEQ5min      12684 non-null  int64 
 21  toCoupon_GEQ15min     12684 non-null  int64 
 22  toCoupon_GEQ25min     12684 non-null  int64 
 23  direction_same        12684 non-null  int64 
 24  direction_opp         12684 non-null  int64 
 25  Y                     12684 non-null  int64 
dtypes: int64(8), object(18)

Initial observations:
1. There are 'NaN' values in the dataset and 'car' column seems to have the most of it
2. passanger column name is misspelled
3. Many features are of dtype object
4. There are a lot of categorical features

### 2.2 Early Data Exploration and Quality Check
In this section, we determine the following:
1. Are there duplicates in the data?
2. What columns have NaN values and how many?
3. Are there any structural issues with the data including typos and dtype?

#### Duplicates:
Check for duplicates returned the following:

Number of duplicates: 74

Here is a sample of duplicated rows:
<div class="overflow-table">

|      | destination   | passanger   | weather   |   temperature | time   | coupon                | expiration   | gender   |   age | maritalStatus   |   has_children | education                              | occupation                 | income           |   car | Bar   | CoffeeHouse   | CarryAway   | RestaurantLessThan20   | Restaurant20To50   |   toCoupon_GEQ5min |   toCoupon_GEQ15min |   toCoupon_GEQ25min |   direction_same |   direction_opp |   Y |
|-----:|:--------------|:------------|:----------|--------------:|:-------|:----------------------|:-------------|:---------|------:|:----------------|---------------:|:---------------------------------------|:---------------------------|:-----------------|------:|:------|:--------------|:------------|:-----------------------|:-------------------|-------------------:|--------------------:|--------------------:|-----------------:|----------------:|----:|
| 4191 | Work          | Alone       | Sunny     |            80 | 7AM    | Carry out & Take away | 1d           | Male     |    26 | Single          |              0 | Associates degree                      | Unemployed                 | Less than $12500 |   nan | less1 | never         | 1~3         | less1                  | less1              |                  1 |                   1 |                   1 |                0 |               1 |   1 |
| 4192 | Work          | Alone       | Sunny     |            80 | 7AM    | Carry out & Take away | 1d           | Male     |    26 | Single          |              0 | Associates degree                      | Unemployed                 | Less than $12500 |   nan | less1 | never         | 1~3         | less1                  | less1              |                  1 |                   1 |                   1 |                0 |               1 |   1 |
| 4235 | Work          | Alone       | Sunny     |            80 | 7AM    | Carry out & Take away | 1d           | Male     |    26 | Single          |              0 | Graduate degree (Masters or Doctorate) | Management                 | $25000 - $37499  |   nan | 4~8   | gt8           | gt8         | 4~8                    | less1              |                  1 |                   1 |                   1 |                0 |               1 |   1 |
| 4236 | Work          | Alone       | Sunny     |            80 | 7AM    | Carry out & Take away | 1d           | Male     |    26 | Single          |              0 | Graduate degree (Masters or Doctorate) | Management                 | $25000 - $37499  |   nan | 4~8   | gt8           | gt8         | 4~8                    | less1              |                  1 |                   1 |                   1 |                0 |               1 |   1 |
| 4279 | Work          | Alone       | Sunny     |            80 | 7AM    | Carry out & Take away | 1d           | Female   |    26 | Single          |              0 | Bachelors degree                       | Education&Training&Library | $50000 - $62499  |   nan | 1~3   | never         | 4~8         | 1~3                    | less1              |                  1 |                   1 |                   1 |                0 |               1 |   1 |
| 4280 | Work          | Alone       | Sunny     |            80 | 7AM    | Carry out & Take away | 1d           | Female   |    26 | Single          |              0 | Bachelors degree                       | Education&Training&Library | $50000 - $62499  |   nan | 1~3   | never         | 4~8         | 1~3                    | less1              |                  1 |                   1 |                   1 |                0 |               1 |   1 |
| 4323 | Work          | Alone       | Sunny     |            80 | 7AM    | Carry out & Take away | 1d           | Female   |    46 | Single          |              0 | Some college - no degree               | Protective Service         | $25000 - $37499  |   nan | 1~3   | never         | 4~8         | 1~3                    | 1~3                |                  1 |                   1 |                   1 |                0 |               1 |   1 |

</div>

#### Null Values:

Null value check returned the following:

destination                 0
passanger                   0
weather                     0
temperature                 0
time                        0
coupon                      0
expiration                  0
gender                      0
age                         0
maritalStatus               0
has_children                0
education                   0
occupation                  0
income                      0
car                     12576
Bar                       107
CoffeeHouse               217
CarryAway                 151
RestaurantLessThan20      130
Restaurant20To50          189
toCoupon_GEQ5min            0
toCoupon_GEQ15min           0
toCoupon_GEQ25min           0
direction_same              0
direction_opp               0
Y                           0

By far, the `car` column has a large number of missing values. Most likey desicion would be to drop this column.

#### Structural Issues

First lets view the value counts for each column to understand the structure:

<details>
<ValueCounts>
------------------------

destination
No Urgent Place    6283
Home               3237
Work               3164
Name: count, dtype: int64
------------------------

passanger
Alone        7305
Friend(s)    3298
Partner      1075
Kid(s)       1006
Name: count, dtype: int64
------------------------

weather
Sunny    10069
Snowy     1405
Rainy     1210
Name: count, dtype: int64
------------------------

temperature
80    6528
55    3840
30    2316
Name: count, dtype: int64
------------------------

time
6PM     3230
7AM     3164
10AM    2275
2PM     2009
10PM    2006
Name: count, dtype: int64
------------------------

coupon
Coffee House             3996
Restaurant(<20)          2786
Carry out & Take away    2393
Bar                      2017
Restaurant(20-50)        1492
Name: count, dtype: int64
------------------------

expiration
1d    7091
2h    5593
Name: count, dtype: int64
------------------------

gender
Female    6511
Male      6173
Name: count, dtype: int64
------------------------

age
21         2653
26         2559
31         2039
50plus     1788
36         1319
41         1093
46          686
below21     547
Name: count, dtype: int64
------------------------

maritalStatus
Married partner      5100
Single               4752
Unmarried partner    2186
Divorced              516
Widowed               130
Name: count, dtype: int64
------------------------

has_children
0    7431
1    5253
Name: count, dtype: int64
------------------------

education
Some college - no degree                  4351
Bachelors degree                          4335
Graduate degree (Masters or Doctorate)    1852
Associates degree                         1153
High School Graduate                       905
Some High School                            88
Name: count, dtype: int64
------------------------

occupation
Unemployed                                   1870
Student                                      1584
Computer & Mathematical                      1408
Sales & Related                              1093
Education&Training&Library                    943
Management                                    838
Office & Administrative Support               639
Arts Design Entertainment Sports & Media      629
Business & Financial                          544
Retired                                       495
Food Preparation & Serving Related            298
Healthcare Practitioners & Technical          244
Healthcare Support                            242
Community & Social Services                   241
Legal                                         219
Transportation & Material Moving              218
Architecture & Engineering                    175
Personal Care & Service                       175
Protective Service                            175
Life Physical Social Science                  170
Construction & Extraction                     154
Installation Maintenance & Repair             133
Production Occupations                        110
Building & Grounds Cleaning & Maintenance      44
Farming Fishing & Forestry                     43
Name: count, dtype: int64
------------------------

income
$25000 - $37499     2013
$12500 - $24999     1831
$37500 - $49999     1805
$100000 or More     1736
$50000 - $62499     1659
Less than $12500    1042
$87500 - $99999      895
$75000 - $87499      857
$62500 - $74999      846
Name: count, dtype: int64
------------------------

car
Scooter and motorcycle                      22
Mazda5                                      22
do not drive                                22
crossover                                   21
Car that is too old to install Onstar :D    21
Name: count, dtype: int64
------------------------

Bar
never    5197
less1    3482
1~3      2473
4~8      1076
gt8       349
Name: count, dtype: int64
------------------------

CoffeeHouse
less1    3385
1~3      3225
never    2962
4~8      1784
gt8      1111
Name: count, dtype: int64
------------------------

CarryAway
1~3      4672
4~8      4258
less1    1856
gt8      1594
never     153
Name: count, dtype: int64
------------------------

RestaurantLessThan20
1~3      5376
4~8      3580
less1    2093
gt8      1285
never     220
Name: count, dtype: int64
------------------------

Restaurant20To50
less1    6077
1~3      3290
never    2136
4~8       728
gt8       264
Name: count, dtype: int64
------------------------

toCoupon_GEQ5min
1    12684
Name: count, dtype: int64
------------------------

toCoupon_GEQ15min
1    7122
0    5562
Name: count, dtype: int64
------------------------

toCoupon_GEQ25min
0    11173
1     1511
Name: count, dtype: int64
------------------------

direction_same
0    9960
1    2724
Name: count, dtype: int64
------------------------

direction_opp
1    9960
0    2724
Name: count, dtype: int64
------------------------

Y
1    7210
0    5474

</ValueCounts>
</details>

Based on analysing the above, the following decisions are taken:

1. destination - change value No Urgent Place to NonUrgent to be concise
2. passanger - rename column name to 'passenger' to fix typo and remove () in the values to keep it simple
3. education - simplify value by changing 'Graduate degree (Masters or Doctorate)' to 'Graduate degree' and 'Some college - no degree' to 'Some college'
4. occupation - remove spaces between & and professions
5. income - use average value of the given range
6. Convert Bar, CarryAway, RestaurantX, CoffeeHouse columns to numeric
7. Convert age column to numeric

