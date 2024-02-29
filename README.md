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

