# What factors influence the nightly price of an Airbnb in Amsterdam?

The goal of this project is twofold: 1) to practice working with geospatial data and 2) to demonstrate my skills in Statistical Data Analysis. I load data consisting of around 10 000 Airbnb listings, with columns such as nightly price, average review, amenities available at the site, location (in latitude and longitude). The goal is to clean up the data and then run statistical tests to determine which factors influence the nightly price, and maybe make a predictive model for the price later on. 

So far, the following steps have been done.

1) Obtaining the Airbnb data using an API, and performing exploratory data exploration through numerical and graphical summaries
2) Data cleaning: removing rows with missing price, identifying columns with a lot of missing data and the exact missing data mechanism: MAR, MCAR and MNAR, etc.
3) Obtaining the neighbourhood of each listing (to study if the neighbourhood is a factor in price):  I first looked at the neighbourhood the host reported, but this input was unreliable (many missing or useless datapoints). Therefore I used reverse geocoding on the latitude and longitude data to obtain an address. To this end, I first tried working with an API, but this proved too time-consuming. So I dowloaded the geometry data of the nine districts of Amsterdam from the website of Gemeente Amsterdam, and used a spatial join in GeoPandas. This results in the following graph.

<div align="center">
<img src = "https://github.com/user-attachments/assets/21ac0191-9e59-4b18-8e6e-89b82cf093c4" width = "500">
</div>


4) Statistical testing on whether neighbourhood plays a role in price: checking the assumptions of ANOVA -> both homoscedascity and normality assumptions are violated, with the prices in one Amsterdam neighbourhood exhibiting a density more similar to a chi-squared distribution, as shown in the histogram below.
   
<div align="center">
<img src = "https://github.com/user-attachments/assets/657b9e91-79f4-4a75-b05e-ac357267d3d2" width = "500">
</div>

Therefore we run the non-parametric version of this test, the Kruskal-Wallis test. The outcome is a rejection of the null hypothesis, suggesting (as expected) that the neighbourhood is a factor in the listing's price.
