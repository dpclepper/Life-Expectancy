## Global Life Expectancy Exploration

### Introduction

Our focus is to better understand how the different demographic variables affect life expectancy. The data in question has been collected from the Global Health Observatory (GHO) data repository under World Health Organization (WHO) which keeps track of the health status, and other related factors that can affect the life expectancy in the countries [1]. The data has excluded countries such as Vanuatu, Tonga, Cabo Verde as their data was not readily available. The final dataset has 20 predicting variables and was prepared for use via a Kaggle dataset entitled Life Expectancy (WHO) [2]. We are interested in this data because we want to see the relationship of life expectancy when compared with factors such as infant death rate, adult mortality rate with respect to countries being developed or developing. We are also interested in seeing how the life expectancy is different for developing countries and developed countries. We have been able to find significant statistical differences between the life expectancy of countries across the two classes of state of country development. The motivation of our analysis is to see whether the amount of development in different countries accounts for a general better living standards, and increases the life expectancy or not.

### Background

The data presented here is life expectancy data from 193 unique countries over the years 2000-2015. This Data was gathered by the World Health Organization which cites 29 different sources which all combine to make this data set. The data was collected with the help of Deeksha Russell and Duan Wang from the WHO and United Nations Website. The data was collected by submitting data API requests to the Global Health Observatory(GHO) which then they compiled together. The variables we are focusing on are average life expectancy and status of country. The country status corresponds to either developed or developing. One important factor in understanding the data presented in this Life Expectancy Data is the criteria that decides the differentiation between Developed and Developing countries. This criteria includes HDI index which gives essentially a quality of life scale based on several factors. These factors include unemployment and poverty rates, food security levels, healthcare levels, mean years of schooling and Gross National Income per Capita. (Nations, U) In the following report, we intend to show the correlation between higher life expectancies and developed countries and lower life expectancies and developing countries. This correlation will be presented through graphs, t-tests and analysis.

## Hypothesis

Countries that are classified as developed will have a higher average life expectancy than countries that are classified as developing.

<br>
<p align="center">
  <img width="600" height="440" src="https://github.com/dpclepper/Life-Expectancy/blob/main/Images/Image1.png">
</p>

##### Model

The sample consists of 183 paired samples. We have data pairs (xi,yi) for i = 1, … ,183. Modeling the difference,

```math
D_i = X_i - Y_i
```

```math
D_i \sim N(\triangle, \sigma)
```

F is a generic distribution for the population of differences △ is the mean of this distribution σ is the standard deviation

##### Hypothesis

```math
H_0: \mu_1 - \mu_2 = 0
```

```math
H_1 : \mu_1 - \mu_2 \neq 0
```

The null hypothesis is that there is no difference in sample means of the two groups. The alternative hypothesis is that there is a difference in sample means.

We did not want to assume equal variance, so we performed a Welch two sample t-test. This type of t-test calculates the denominator of the t statistic differently, and also adjusts the degrees of freedom to compensate. We calculated a p-value of 1.042296*10^-297.

Next, we wanted to find a 95% Confidence Interval for μ1−μ2 (difference in sample means) using a Welch's two-sample-t-test, Filtering out each status category and pulling out life expectancy, followed by performing the t-test on both samples.

The observed p-value of ~0.0000 is statistically significant at the conventional 0.05 and 0.01 levels. This p-value provides strong evidence that there is a difference between the average life expectancy of all developed and developing countries. This p-value was also conservative as we allowed the possibility of rejecting the null hypothesis to occur if the difference had been in either direction. In terms of the confidence interval results, we are 95% confident that the mean life expectancy in developed countries is between 11.59881 and 12.67663 years higher than that among developing countries.

### Modeling

There are several factors that effect Life Expectancy in each country heavily. Among these factors include infant death rates per yer and adult mortality per year. Both of these variables are present in our data set and are represented with the amount of deaths occurring per 100,000 people per year. A death is considered an Infant Death when it occurs between the age of 0 and 1 and it is considered an Adult Death when it occurs between the age of 15 and 60.

<br>
<p align="center">
  <img width="600" height="440" src="https://github.com/dpclepper/Life-Expectancy/blob/main/Images/Image2.png">
</p>

Infant deaths have a significant effect on Life Expectancy as the value of 0 is an out-lier and would decrease the predicted Life Expectancy significantly. As shown in the graph above, there are significantly more infant deaths in developing countries than developed countries which tend to hover around the 1 per 100,000 in population. This is important to note because this significant increase in Infant Deaths in developing countries could account for a large portion of the difference in life expectancies between developed and developing countries.

<br>
<p align="center">
  <img width="600" height="440" src="https://github.com/dpclepper/Life-Expectancy/blob/main/Images/Image3.png">
</p>

Adult Mortality rates are also important to factor in because these occur before what is considered old age and also significantly decrease the Life Expectancy of that country. As shown in the graph above, developed countries do not have nearly as low of Adult Mortality rates as they do Infant Death Rates but they average out to significantly lower than the average of developing countries. The difference in averages seems to be around 100 per 100,000 per year. This is also incredibly important to note because this may account for another large portion of the difference in Life Expectancy between developed and developing countries.

```math
Life\ Expectancy = 75.34\ -\ 0.042\times Adult\ Mortality\ -\ 0.0076\times Infant\ Deaths\ +\ 7.25\times Status
```

From the initial output of a logistic regression model using life expectancy as our target and infant mortality, adult mortality, and status (0 for Developing, 1 for Developed) as features, we found that the median life expectancy is 0.621, which is comparable with the normal life expectancy from our dataset. Additionally, there are now coefficients for each feature included in the model that we can interpret, such as an increase in 1 unit of the adult mortality variable corresponding to a 0.042139 decrease in life expectancy years. We do see a very low multiple R-squared of 0.602, which may increase as more features are added to the model or as we decide to pare off or modify correlated features. Additionally, we can look at how the theoretical life expectancy looks when plotted against the features going into the linear regression model through added-variable plots.

<br>
<p align="center">
  <img width="600" height="440" src="https://github.com/dpclepper/Life-Expectancy/blob/main/Images/Image4.png">
</p>

For various features such as adult mortality and development status, we can see that the linear regression is explained very well by this feature depicted by the data roughly following the life expectancy regression line. For others such as infant deaths, we have a more complex relationship where it is clear that other features are needed to make the linear regression model more accurate, and that life expectancy cannot just be easily predicted by those specific features alone.

<br>
<p align="center">
  <img width="610" height="440" src="https://github.com/dpclepper/Life-Expectancy/blob/main/Images/Image5.png">
</p>

From this graph of observed life expectancy vs predicted life expectancy based on regression, we can see that the they follow an overall positive linear trend as expected. This shows that our linear regression was successful in predicting life expectancy, except for some noise that is to be expected with regression models in general. There appears to be a bit of extra noise around the predictions of ~72-75 years life expectancy as well as predictions of ~82-83 years life expectancy, where observed ranges from less than 50 to greater than 80, indicating a moderate level of noise unexplained by the regression model. Overall, the regression model appears to model the actual data fairly successfully.

### Discussion

Through our analysis of the data our initial prediction is correct, there is a relationship between the life expectancy of a nation and the status of that nation. This shows that levels of healthcare, poverty rates, education rates and economic factors all seem to have a correlation to the actual life expectancy of a country. Some potential shortcomings could include there are a few missing data values that could potentially have changed our data slightly, but since there were only 13 missing data points in a set of over 1000 points it is not entirely necessary to account for these changes. Additionally, countries are not developed or developing for all of time, there are some countries that changed status over the course of the 15 years in the data set and this may not be accounted for properly. For future directions for additional work, it would be really interesting to see how the covid-19 pandemic has changed these factors. Since the start of the Covid-19 pandemic, how has the mean difference of life expectancy in developed countries and developing countries changed? With the death rates from Covid being higher in developing countries and this pandemic affecting economies, healthcare systems and poverty rates worldwide, it would be interesting to see if the average life expectancy depicts this.

Our primary conclusion is that countries who have a status of developed have a higher average life expectancy than countries that have a status of developing. This is supported by the 95 percent confidence interval we computed which shows the change in life expectancy from developed countries in comparison with developing countries is somewhere on the interval 11.59881 to 12.67663 years.

### References

[1] Nations, U. (2022, November 9). Human development index. Human Development Reports. Retrieved November 21, 2022, from https://hdr.undp.org/data-center/human-development-index#/indicies/HDI.

[2] Kumar, Rajarshi. “Life Expectancy (WHO).” Kaggle. Web. 12 Dec. 2022, from https://www.kaggle.com/datasets/kumarajarshi/life-expectancy-who.
