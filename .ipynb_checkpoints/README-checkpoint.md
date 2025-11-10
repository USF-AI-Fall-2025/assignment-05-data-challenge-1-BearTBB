# x62-data-challenge-student-pathways

# Null checking data

<class 'pandas.core.frame.DataFrame'>
RangeIndex: 20705 entries, 0 to 20704
Data columns (total 11 columns):
 #   Column              Non-Null Count  Dtype  
---  ------              --------------  -----  
 0   DISTRICT_TYPE       20705 non-null  object 
 1   DISTRICT_NAME       20705 non-null  object 
 2   DISTRICT_CODE       17960 non-null  float64
 3   ACADEMIC_YEAR       20705 non-null  object 
 4   DEMO_CATEGORY       20705 non-null  object 
 5   STUDENT_POPULATION  20705 non-null  object 
 6   AWARD_CATEGORY      20705 non-null  object 
 7   WAGE_YEAR1          20705 non-null  float64
 8   WAGE_YEAR2          20705 non-null  float64
 9   WAGE_YEAR3          20705 non-null  float64
 10  WAGE_YEAR4          20705 non-null  float64
dtypes: float64(5), object(6)
memory usage: 1.7+ MB
Some missing data for column DISTRICT_CODE. All other columns seem to be non-null for all rows.

Column numbers 0-6 seem to be of object Dtype, except for DISTRICT_CODE at column number 2, which is of Dtype float64. This is peculiar, because it does not seem like DISTRICT_CODE would need to be a float64. From my understanding of the data, DISTRICT_CODE is supposed to be a discrete, integer representation of the DISTRICT_NAME column. I will verify this information using value_counts().

DISTRICT_CODE
5373833.0    56
5310538.0    55
4210421.0    54
3768403.0    50
5110512.0    50
             ..
761796.0     16
461515.0     15
5472256.0    15
3868478.0    13
4870540.0    13
Name: count, Length: 571, dtype: int64

DISTRICT_NAME                             DISTRICT_CODE
Southern Trinity Joint Unified            5373833          56
Trinity County Office of Education        5310538          55
Santa Barbara County Office of Education  4210421          54
Spencer Valley Elementary                 3768403          50
Big Sur Unified                           2775150          50
                                                           ..
Hemet Unified                             3367082          16
Visalia Unified                           5472256          15
Oroville Union High                       461515           15
San Francisco Unified                     3868478          13
Fairfield-Suisun Unified                  4870540          13
Name: count, Length: 692, dtype: int64
The length of the created table seems to be equal for each value_counts(), which suggests that each existing DISTRICT_CODE maps exactly to one DISTRICT_NAME.

This also suggests that the null values for DISTRICT_CODE is because some DISTRICT_NAMEs are not yet assigned an official code.

I'll be changing the Dtype of DISTRICT_CODE to object to make it easier to work with, and also make it behave more closely to how the data is actually treated.


DISTRICT_TYPE	DISTRICT_NAME	DISTRICT_CODE	ACADEMIC_YEAR	DEMO_CATEGORY	STUDENT_POPULATION	AWARD_CATEGORY	WAGE_YEAR1	WAGE_YEAR2	WAGE_YEAR3	WAGE_YEAR4
0	School District	Duarte Unified	1964469	2018-2019	Race	None Reported	Bachelor's Degree - Did Not Transfer	0.0	0.0	0.0	0.0
1	School District	Coronado Unified	3768031	2018-2019	Race	None Reported	Associate Degree	0.0	0.0	0.0	0.0
2	School District	Gilroy Unified	4369484	2018-2019	Race	Black or African American	Bachelor's Degree - Did Not Transfer	0.0	0.0	0.0	0.0
3	School District	Pleasant Valley	5672553	2018-2019	Homeless Status	Did Not Experience Homelessness in K-12	Community College Certificate	0.0	0.0	0.0	0.0
4	Legislative District	Senate District 15	nan	2018-2019	Race	American Indian or Alaska Native	Community College Certificate	0.0	0.0	0.0	0.0
...	...	...	...	...	...	...	...	...	...	...	...
20700	School District	Armona Union Elementary	1663875	2018-2019	Race	American Indian or Alaska Native	Associate Degree	0.0	0.0	0.0	0.0
20701	School District	Taft Union High	1563818	2018-2019	Race	White	Community College Certificate	0.0	0.0	0.0	0.0
20702	School District	Bassett Unified	1964295	2018-2019	Foster Status	Foster Youth	Bachelor's Degree - Did Not Transfer	0.0	0.0	0.0	0.0
20703	School District	SBE - John Henry High	777354	2018-2019	Gender	Male	Bachelor's Degree - Did Not Transfer	0.0	0.0	0.0	0.0
20704	School District	Los Molinos Unified	5271571	2018-2019	Foster Status	Not Foster Youth	Associate Degree	0.0	0.0	0.0	0.0
20705 rows × 11 columns

<class 'pandas.core.frame.DataFrame'>
RangeIndex: 20705 entries, 0 to 20704
Data columns (total 11 columns):
 #   Column              Non-Null Count  Dtype  
---  ------              --------------  -----  
 0   DISTRICT_TYPE       20705 non-null  object 
 1   DISTRICT_NAME       20705 non-null  object 
 2   DISTRICT_CODE       20705 non-null  object 
 3   ACADEMIC_YEAR       20705 non-null  object 
 4   DEMO_CATEGORY       20705 non-null  object 
 5   STUDENT_POPULATION  20705 non-null  object 
 6   AWARD_CATEGORY      20705 non-null  object 
 7   WAGE_YEAR1          20705 non-null  float64
 8   WAGE_YEAR2          20705 non-null  float64
 9   WAGE_YEAR3          20705 non-null  float64
 10  WAGE_YEAR4          20705 non-null  float64
dtypes: float64(4), object(7)
memory usage: 1.7+ MB

# Discrete Values Analysis
Let's move on to analyzing the unique values of the other discrete valued columns.

DISTRICT_TYPE
School District         17960
Legislative District     2702
All                        43
Name: count, dtype: int64

It seems like each district is categorized into two different types, where there are instances of a district being considered both School and Legislative.

ACADEMIC_YEAR
2018-2019    20705
Name: count, dtype: int64
Every data point is from the year 2018-2019. It seems like this feature can be safely removed from the dataset.

DEMO_CATEGORY
Race               12116
Foster Status       2754
Homeless Status     2308
Gender              2291
All                 1236
Name: count, dtype: int64

STUDENT_POPULATION
None Reported                                1927
American Indian or Alaska Native             1833
Native Hawaiian or Other Pacific Islander    1810
Foster Youth                                 1739
Two or More Races                            1539
Black or African American                    1484
Experienced Homelessness in K-12             1472
Asian                                        1372
All                                          1236
Male                                         1171
Female                                       1120
White                                        1089
Hispanic or Latino                           1062
Not Foster Youth                             1015
Did Not Experience Homelessness in K-12       836
Name: count, dtype: int64
It seems this DEMO_CATEGORY feature serves to categorize the STUDENT_POPULATION feature. Essentially, it describes the kind of grouping that the STUDENT_POPULATION column is currently applying to the data point.

Let's check if they are truly related or not by making new dataframe where the data points are grouped by DEMO_CATEGORY, then STUDENT_POPULATION.

0
DEMO_CATEGORY	STUDENT_POPULATION	
All	All	1236
Foster Status	Foster Youth	1739
Not Foster Youth	1015
Gender	Female	1120
Male	1171
Homeless Status	Did Not Experience Homelessness in K-12	836
Experienced Homelessness in K-12	1472
Race	American Indian or Alaska Native	1833
Asian	1372
Black or African American	1484
Hispanic or Latino	1062
Native Hawaiian or Other Pacific Islander	1810
None Reported	1927
Two or More Races	1539
White	1089

It seems the STUDENT_POPULATION feature fits quite logically with each greater category outlined in DEMO_CATEGORY.

AWARD_CATEGORY
Bachelor's Degree - Transferred         5594
Bachelor's Degree - Did Not Transfer    5220
Community College Certificate           5196
Associate Degree                        4695
Name: count, dtype: int64
This feature seems to describe the level of education that the data point has finished. This will likely be very useful when making the model.

# Continuous Value Analysis
Now on to analyzing the continuous values present within the dataset.

WAGE_YEAR1	WAGE_YEAR2	WAGE_YEAR3	WAGE_YEAR4
count	20705.000000	20705.000000	20705.000000	20705.000000
mean	4476.106834	6075.533253	7310.831635	8530.890413
std	11944.502346	16140.916903	19158.203471	22106.663179
min	0.000000	0.000000	0.000000	0.000000
25%	0.000000	0.000000	0.000000	0.000000
50%	0.000000	0.000000	0.000000	0.000000
75%	0.000000	0.000000	0.000000	0.000000
max	97993.000000	132847.000000	146728.000000	153910.000000

It seems all of the continuous values present within the dataset are all related to the wages that the data points get within each consecutive year they are in the workforce.The values seem to range all the way from $0 in wage to $153910 for the highest earner in year 4.

There seems to be a staggering percentage of the dataset earning $0. About +75%. This requires a bit more digging.

[picture of distribution plot]

From the distribution plots, it does seem like the majority of the dataset does not earn a wage, or has simply decided not to report their wage.

Changing gears, it is quite hard to see the trend in the data of those with a wage with the large amount of $0 earners. I will exclude them to take a closer look.

[more plots]

This is much clearer. The data is clearly not normally distributed. It seems to be mostly left skewed from year 1 to year 4. The data does progressively redistribute to the right, but year 2 is a bit of an anomally with some data points earning less than the previous year. A possible explanation could be that some data points failed to pass probation in their workplace, and had to transition to a lower paying job after their first year, but that is just speculation.

I'd like to check the kinds of data points that earn and don't earn a wage.


DISTRICT_TYPE	DISTRICT_NAME	DISTRICT_CODE	ACADEMIC_YEAR	DEMO_CATEGORY	STUDENT_POPULATION	AWARD_CATEGORY	WAGE_YEAR1	WAGE_YEAR2	WAGE_YEAR3	WAGE_YEAR4
6	Legislative District	Assembly District 56	nan	2018-2019	All	All	Community College Certificate	24039.0	25210.0	24293.0	28562.0
12	School District	Liberty Union High	761721	2018-2019	Homeless Status	Did Not Experience Homelessness in K-12	Bachelor's Degree - Did Not Transfer	39340.0	56250.0	66698.0	70569.0
21	School District	Campbell Union High	4369401	2018-2019	All	All	Bachelor's Degree - Did Not Transfer	46988.0	71062.0	84356.0	90041.0
41	Legislative District	Assembly District 10	nan	2018-2019	Homeless Status	Did Not Experience Homelessness in K-12	Bachelor's Degree - Transferred	29448.0	52323.0	64539.0	71298.0
54	School District	Los Alamitos Unified	3073924	2018-2019	Homeless Status	Did Not Experience Homelessness in K-12	Associate Degree	15495.0	27094.0	24070.0	52649.0
...	...	...	...	...	...	...	...	...	...	...	...
20663	School District	Walnut Valley Unified	1973460	2018-2019	All	All	Associate Degree	16991.0	25339.0	26844.0	46519.0
20673	Legislative District	Assembly District 22	nan	2018-2019	Foster Status	Not Foster Youth	Associate Degree	21305.0	26815.0	34758.0	40457.0
20678	Legislative District	Assembly District 20	nan	2018-2019	Race	Asian	Bachelor's Degree - Did Not Transfer	52247.0	65054.0	77501.0	86712.0
20683	Legislative District	Senate District 15	nan	2018-2019	Gender	Female	Community College Certificate	21872.0	37426.0	42437.0	45981.0
20693	School District	Alameda Unified	161119	2018-2019	All	All	Bachelor's Degree - Did Not Transfer	40949.0	65056.0	78760.0	86067.0
2935 rows × 11 columns


DISTRICT_TYPE	DISTRICT_NAME	DISTRICT_CODE	ACADEMIC_YEAR	DEMO_CATEGORY	STUDENT_POPULATION	AWARD_CATEGORY	WAGE_YEAR1	WAGE_YEAR2	WAGE_YEAR3	WAGE_YEAR4
0	School District	Duarte Unified	1964469	2018-2019	Race	None Reported	Bachelor's Degree - Did Not Transfer	0.0	0.0	0.0	0.0
1	School District	Coronado Unified	3768031	2018-2019	Race	None Reported	Associate Degree	0.0	0.0	0.0	0.0
2	School District	Gilroy Unified	4369484	2018-2019	Race	Black or African American	Bachelor's Degree - Did Not Transfer	0.0	0.0	0.0	0.0
3	School District	Pleasant Valley	5672553	2018-2019	Homeless Status	Did Not Experience Homelessness in K-12	Community College Certificate	0.0	0.0	0.0	0.0
4	Legislative District	Senate District 15	nan	2018-2019	Race	American Indian or Alaska Native	Community College Certificate	0.0	0.0	0.0	0.0
...	...	...	...	...	...	...	...	...	...	...	...
20700	School District	Armona Union Elementary	1663875	2018-2019	Race	American Indian or Alaska Native	Associate Degree	0.0	0.0	0.0	0.0
20701	School District	Taft Union High	1563818	2018-2019	Race	White	Community College Certificate	0.0	0.0	0.0	0.0
20702	School District	Bassett Unified	1964295	2018-2019	Foster Status	Foster Youth	Bachelor's Degree - Did Not Transfer	0.0	0.0	0.0	0.0
20703	School District	SBE - John Henry High	777354	2018-2019	Gender	Male	Bachelor's Degree - Did Not Transfer	0.0	0.0	0.0	0.0
20704	School District	Los Molinos Unified	5271571	2018-2019	Foster Status	Not Foster Youth	Associate Degree	0.0	0.0	0.0	0.0
17770 rows × 11 columns

with wage:
STUDENT_POPULATION
All                                          672
Female                                       421
Not Foster Youth                             419
Male                                         411
Hispanic or Latino                           293
White                                        244
Did Not Experience Homelessness in K-12      236
Asian                                        174
Experienced Homelessness in K-12              33
Black or African American                     15
Two or More Races                              9
Foster Youth                                   2
None Reported                                  2
Native Hawaiian or Other Pacific Islander      2
American Indian or Alaska Native               2
Name: count, dtype: int64

without wage
STUDENT_POPULATION
None Reported                                1925
American Indian or Alaska Native             1831
Native Hawaiian or Other Pacific Islander    1808
Foster Youth                                 1737
Two or More Races                            1530
Black or African American                    1469
Experienced Homelessness in K-12             1439
Asian                                        1198
White                                         845
Hispanic or Latino                            769
Male                                          760
Female                                        699
Did Not Experience Homelessness in K-12       600
Not Foster Youth                              596
All                                           564
Name: count, dtype: int64
It seems as though there is a clear group of the student population that end up earning a wage. The biggest discrepancies are within the DEMO_CATEGORY of race. Those that are not White, hispanic or latino, or Asian seem to be less likely to earn, or report, a wage. In other categories, it seems those that experience homelessness in K-12 do not have any data points that earn a wage.

Let's look at a more comparative visualization of this data to learn more. But, before that, I would like to see the importance of the level of education to the wage that is earned by an individual.

[scatterplot]

Through this graph, it seems as though there is a clear trend where those with a higher education gets paid more. There is no discernable difference between associate degree earners and community college certificate earners, but there is a clear separation between those and the data points that have a bachelor's degree. Within the bachelor's degree demographic, there is also a clear divide between those that transer and the ones that did not transfer. Let's compile all of this info together into one graph.

[another plot]

This last graph makes it quite clear the relationships between the STUDEN_POPULATION feature and the AWARD_CATEGORY with the wage that data points earn in year 4.


