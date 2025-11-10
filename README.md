# x62-data-challenge-student-pathways

# Null checking data

<img width="363" height="316" alt="image" src="https://github.com/user-attachments/assets/1744ad42-ad26-40e2-a4c4-68900f717480" />

Some missing data for column DISTRICT_CODE. All other columns seem to be non-null for all rows.

Column numbers 0-6 seem to be of object Dtype, except for DISTRICT_CODE at column number 2, which is of Dtype float64. This is peculiar, because it does not seem like DISTRICT_CODE would need to be a float64. From my understanding of the data, DISTRICT_CODE is supposed to be a discrete, integer representation of the DISTRICT_NAME column. I will verify this information using value_counts().

<img width="295" height="228" alt="image" src="https://github.com/user-attachments/assets/4bbd5759-7895-4cfb-9d6d-081ff57dcecd" />

Indeed, there are multiple instances of each number. Let's see if each number is associated with a specific DISTRIC_NAME.

<img width="468" height="236" alt="image" src="https://github.com/user-attachments/assets/f5b24066-60f3-4947-ba2a-5a57bda06334" />

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

<img width="373" height="311" alt="image" src="https://github.com/user-attachments/assets/a5937161-465e-4bd5-96fd-d89dab4fa277" />

# Discrete Values Analysis
Let's move on to analyzing the unique values of the other discrete valued columns.

<img width="229" height="93" alt="image" src="https://github.com/user-attachments/assets/cfcc4fff-d65b-47e5-9ceb-1a22705b70e2" />

It seems like each district is categorized into two different types, where there are instances of a district being considered both School and Legislative.

<img width="190" height="56" alt="image" src="https://github.com/user-attachments/assets/e4d2e3a7-154d-4a10-ab5b-df3ff1b2cc11" />

Every data point is from the year 2018-2019. It seems like this feature can be safely removed from the dataset.

<img width="196" height="129" alt="image" src="https://github.com/user-attachments/assets/f7c2fe91-d417-4de1-972d-d66c5a9c3cdd" />

<img width="368" height="297" alt="image" src="https://github.com/user-attachments/assets/d4179cd7-cd05-4e52-90e2-aa41474eb2fe" />

It seems this DEMO_CATEGORY feature serves to categorize the STUDENT_POPULATION feature. Essentially, it describes the kind of grouping that the STUDENT_POPULATION column is currently applying to the data point.

Let's check if they are truly related or not by making new dataframe where the data points are grouped by DEMO_CATEGORY, then STUDENT_POPULATION.

<img width="443" height="490" alt="image" src="https://github.com/user-attachments/assets/181f338c-f90a-4456-b0f2-0e2297741d4a" />

It seems the STUDENT_POPULATION feature fits quite logically with each greater category outlined in DEMO_CATEGORY.

<img width="335" height="114" alt="image" src="https://github.com/user-attachments/assets/5edf57e8-3847-4a69-b902-c78f692e8550" />

This feature seems to describe the level of education that the data point has finished. This will likely be very useful when making the model.

# Continuous Value Analysis
Now on to analyzing the continuous values present within the dataset.

<img width="452" height="268" alt="image" src="https://github.com/user-attachments/assets/05c75885-3b5a-4409-9a77-1c712279de07" />

It seems all of the continuous values present within the dataset are all related to the wages that the data points get within each consecutive year they are in the workforce.The values seem to range all the way from $0 in wage to $153910 for the highest earner in year 4.

There seems to be a staggering percentage of the dataset earning $0. About +75%. This requires a bit more digging.

<img width="1103" height="280" alt="image" src="https://github.com/user-attachments/assets/81277fdd-ef30-4cb7-b753-5565168926f4" />

From the distribution plots, it does seem like the majority of the dataset does not earn a wage, or has simply decided not to report their wage.

Changing gears, it is quite hard to see the trend in the data of those with a wage with the large amount of $0 earners. I will exclude them to take a closer look.

<img width="397" height="764" alt="image" src="https://github.com/user-attachments/assets/b08c75b9-49f1-4c3b-a3b1-7d8609fb6ae8" />

<img width="382" height="750" alt="image" src="https://github.com/user-attachments/assets/9e9f03e2-ae38-466f-9565-d3fa9bdef429" />

This is much clearer. The data is clearly not normally distributed. It seems to be mostly left skewed from year 1 to year 4. The data does progressively redistribute to the right, but year 2 is a bit of an anomally with some data points earning less than the previous year. A possible explanation could be that some data points failed to pass probation in their workplace, and had to transition to a lower paying job after their first year, but that is just speculation.

I'd like to check the kinds of data points that earn and don't earn a wage.

with wage:
<img width="365" height="298" alt="image" src="https://github.com/user-attachments/assets/75196507-e28c-460e-924d-7160763926c7" />

without wage:
<img width="367" height="296" alt="image" src="https://github.com/user-attachments/assets/bac25fe1-4851-41df-ba1a-fa2c1a6cf545" />

It seems as though there is a clear group of the student population that end up earning a wage. The biggest discrepancies are within the DEMO_CATEGORY of race. Those that are not White, hispanic or latino, or Asian seem to be less likely to earn, or report, a wage. In other categories, it seems those that experience homelessness in K-12 do not have any data points that earn a wage.

Let's look at a more comparative visualization of this data to learn more. But, before that, I would like to see the importance of the level of education to the wage that is earned by an individual.

<img width="830" height="467" alt="image" src="https://github.com/user-attachments/assets/85838cfe-8105-4244-8f7e-3845f03862b6" />

Through this graph, it seems as though there is a clear trend where those with a higher education gets paid more. There is no discernable difference between associate degree earners and community college certificate earners, but there is a clear separation between those and the data points that have a bachelor's degree. Within the bachelor's degree demographic, there is also a clear divide between those that transer and the ones that did not transfer. Let's compile all of this info together into one graph.

<img width="1106" height="417" alt="image" src="https://github.com/user-attachments/assets/a4ac1810-b37f-4a6e-aebe-497f352c2e3c" />

This last graph makes it quite clear the relationships between the STUDEN_POPULATION feature and the AWARD_CATEGORY with the wage that data points earn in year 4.


