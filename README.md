# GDP Per Capita PPP vs Subjective Wellbeing

### Project Overview:

Conventional wisdom dictates that more money translates into higher life satisfaction. Of course, life satisfaction increases significantly if a person manages to climb their way out of poverty. However, the law of diminishing marginal utility also suggests that at some point, the rate at which life satisfaction increases per dollar will diminish. At some point, more money won't result into significantly higher life satisfaction.

This study utilises two datasets to analyse the above tension: [The World Bank GDP per capita PPP dataset from 2024](https://data360.worldbank.org/en/indicator/WB_WDI_NY_GDP_PCAP_PP_CD?view=datatable&average=WLD), and the [World Happiness Report of 2024](https://www.worldhappiness.report/ed/2024/). It tries to answer 2 questions:

1) Considering life satisfaction grows with increasing GDP per capita PPP, at what level of GDP per capita PPP does the growth in life satisfaction (subjective wellbeing) become stagnant? (Both concepts- 'GDP per capita PPP' and 'subjective wellbeing' are explained below)
2) Which are the satisfaction-outlier countries (relatively lower GDP and higher satisfaction score) and what is their secret?

Here are the key findings:

1) At ~85,000 dollars GDP per capita PPP, growth in the life evaluation scores begins to flatten significantly. This means that once countries around the world reach the material living standards compared to what a US Citizen can roughly purchase with 85000 dollars, further economic improvements marginally increase one's wellbeing.
2) Nordic countries like Finland, Denmark and Iceland are surely satisfaction-outlier countries. These countries report higher subjective well-being scores at much lower GDP per capita PPP (compared to countries like Switzerland and Luxembourg). They are strong real-life examples of the well known hypothesis that money is not all it takes to ensure wellbeing. Factors like life expectancy, generosity, freedom of choice, and others matter tremendously in deciding what one rates their quality of life as.

Here are the assets utilised in the making of this study:

- Python Script- [code.ipynb](https://github.com/maanaskauntia/GDP_vs_Life_Satisfaction/blob/main/code.ipynb)
- World Bank Dataset- [2024_WB_GDP_PerCapita_PPP.csv](https://drive.google.com/file/d/17LIhcHjpVwTLrlClfnZ3gk1XH4mBVHTe/view?usp=sharing)
- World Happiness Report Dataset- [WHR2024_Data.csv](https://github.com/maanaskauntia/GDP_vs_Life_Satisfaction/blob/main/WHR2024_Data.csv)

With that said, let's dive deeper into the concepts, the analysis methodology and the findings that will help us build nations where citizens feel like their lives are at least a solid 7, instead of a dull 4.

--------------------------------------

### Quick Concept Catch-Up:

Brevity is important. However, the following two concepts require a few seconds to get used to. Thus, they have been given some time in this report, making it slightly more voluminous.

GDP Per Capita PPP:

The Gross Domestic Product (GDP) of a country is the total income earned through the production of goods and services in that country during an accounting period (in this case, 2024). The GDP _Per Capita_ is the economic value contributed by the average person of that country. It is calculated using a simple average: GDP / Population. We can, for the sake of GDP comparison between countries, convert their currencies into dollars based on the current exchange rates. However, this measure is not ideal for cross-country comparisons because **when measured in dollars, one dollar's worth in India (Rs. 95) buys much more than a dollar in the US**. So when an Indian citizen says they are quite happy at 10 dollars GDP per capita and a US citizen says the same thing, that does not mean they have the same material reality and economic level (as the same amount in dollars goes further in India).

To resolve this inconsistency, economists developed Purchasing Power Parity (PPP). This is an imaginary currency used to account for the disparities in living-standards that the same dollar number might have in different countries. Economists calculate PPP numbers based on baskets of goods, prices, living costs and other such factors that influence living standards. For instance, exchange rates in PPP are significantly based on how much a certain basket of goods costs in India and how much the same basket containing the same goods costs in the US. Thus, a dollar could be worth Rs. 95 in exchange rate, but only worth Rs. 20 in PPP.

Subjective Wellbeing:

Subjective wellbeing is a measure of people's own accounts of their happiness and life satisfaction. The World Happiness Report (WHR) is the world's leading publication on global 'subjective wellbeing' and the factors that improve it. Subjective wellbeing of different countries is measured based on a single life evaluation question asked to its citizens:

Please imagine a ladder with steps numbered from 0 at the bottom to 10 at the top. The top of the ladder represents the best possible life for you and the bottom of the ladder represents the worst possible life for you. On which step of the ladder would you say you personally feel you stand at this time?

Importantly, the question does not mention concepts like happiness, wellbeing, or satisfaction, so it can be easily translated and understood in many different languages. Moreover, to provide a more precise estimate of the average life evaluation in each country, the World Happiness Report combines responses from the last three years. For example, the 2026 rankings would be based on combined data from 2023 to 2025.

--------------------------------------

### Analysis Methodology and Findings:

- The Python script utilised for this analysis first merges the two datasets (World Bank's GDP dataset and World Happiness Report's Ladder Scores) based on country names. The year 2024 was chosen for this study because that was the last year for which the World Bank data was available.
- The WHR dataset initially contained 140 countries, out of which, data for 124 countries was available in the World Bank Dataset. Thus, this analysis was conducted for 124 countries.
- The study calculated the correlation between the two variables (GDP per capita PPP and Average Ladder Scores), and found it to be 0.73 (which is a strong correlation).

Let us take a deeper look into the relationship between GDP per capita PPP and subjective wellbeing.

<div align="center">
  <img src="https://lh3.googleusercontent.com/d/1HRGoUA_EeL-3ckPrYDv0X8_5YUIiGSmI" alt="LOWESS curve" width="800">
</div>

The red line above is not a linear regression line, but a LOWESS (Locally Weighted Scatterplot Smoothing) curve. It is made out of stitching many tiny local regressions around neighbouring points into one smooth curve. The reason for choosing this trend line instead of a linear regression was that it makes obvious the point at which we see significantly diminishing marginal returns.

We can see that the curve nearly flattens at ~85000 dollars. Considering these are PPP numbers, this means that when citizens around the world reach the material living standards compared to what a US Citizen can purchase with 85000 dollars, further economic prosperity marginally increases wellbeing.

It is even more interesting to note that near the 60,000 GDP per capita PPP mark, many countries report higher subjective wellbeing than significantly richer countries (visible on the far right of the graph). To find out which countries fall into this category, the code snippet below gives us countries with a GDP per capita PPP greater than 40,000 dollars, and a ladder score that's greater than 7.

We use plotly to plot these specific countries on a graph and see exactly which ones are happiness-outliers.


As we can note from the above graph, Finland, Denmark and Iceland lie way above on the ladder than countries with either the same or even higher gdp per capita PPP (like Switzerland and Luxembourg).

There is a popular notion that Nordic countries (here, Finland, Denmark and Iceland) are much better on all wellbeing indicators because of their small, homogenous population. It is often assumed that it is easier to build welfare societies in small and homogenous countries compared to larger, more diverse ones. However, research has not found a relationship (-ve or +ve) between a country's population size and life satisfaction. Moreover, smaller countries are on average not more homogenous than larger countries ([link to study](https://www.sciencedirect.com/science/article/abs/pii/S0889158306000517) on size of population, homogeneity and subjective well being).

So what is it that brings these countries to the top of the ladder apart from high GDP per capita? The World Happiness Report of 2020 found that the most prominent explanations for this exceptional performance of the Nordics include the quality of their institutions, reliable and extensive welfare benefits, low corruption, and well-functioning democracy and state institutions. Furthermore, Nordic citizens experience a high sense of autonomy and freedom, as well as high levels of social trust towards each other, which also play a significant role in determining life satisfaction.

--------------------------------------

### Conclusion:

This study utilised correlation, linear regression and the LOWESS curve to understand the strength of the relationship between subjective wellbeing and GDP per capita PPP. We found that post the 85000 dollars GDP per capita PPP mark, the gains in subjective wellbeing are marginal. With the example of the Nordic countries, we also saw that subjective wellbeing involves a lot more than economic prosperity. Factors including reliable state welfare benefits, low corruption, individual autonomy, and others significantly influence how satisfied people are with their lives. From these findings, we learn that economic, institutional, and cultural factors together make way for citizen happiness and wellbeing- which, as we all must agree, are the ultimate goals of government.
