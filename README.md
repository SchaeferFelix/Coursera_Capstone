# Business Report - Neighborhood Microtargeting

## Applied Data Science Capstone Project

<p>All necessary data and jupyter notebooks are provided in the "Cologne" folder </p>
<p> Notebook is renderd here: https://nbviewer.jupyter.org/github/SchaeferFelix/Coursera_Capstone/blob/main/Cologne/Cologne.ipynb </p>

### Introduction

<p>Cologne is one of the biggest cities in Germany and with over 100.000 students a city with a deeply entrenched youth culture. The city and its 86 Neighborhoods called "Veedel" (Cologne dialect for: "Viertel) are very diverse and populated with around one million inhabitants. </p>

<p>I want to consider a fictitious Business Problem of a marketing consultancy that helps local companies with their advertising campaigns by visualizing different clusters on a geographical map. The consultancy will deliver an algorithm that clusters the neighborhood according to different categorical inputs regarding demographical and socio-economical factors. For the most cost-efficient marketing mix, it is necessary to approach the correct customer. A clustered neighborhood is a feasible step to distribute the marketing effort more efficiently. The algorithm of the marketing consultancy will help local companies for a better approach to microtargeting the right customers in the right Neighborhoods as different clusters may exhibit different consumer elasticities. I will show in the following the different opportunities to cluster a city with four different features that are aggregated and engineered from different data sources. It can be shown that an efficient clustering of the neighborhood is a consistent approach that delivers a clear output if the assumption of internally homogenous neighborhoods holds. A graphical visualization is shown to distinguish the different clusters on a complete city map.
</p>
<p>As a disclaimer: I won't discuss any implication from the assigned clusters on the neighborhoods nor will I deliver any marketing advice. Furthermore, it needs to be said that the clustering can exhibit "rational discrimination" that delivers "segmented monocultures" to quote the Whistleblower from Cambridge Analytica Christopher Wylie. I am against any of those resulting discrimination and very aware of the simplification of socio-economical factors that can result from clustering on those data.
</p>

### Data Source

<p>First I gathered the demographical data for the analysis from the city of cologne open data platform  (only in german: https://www.offenedaten-koeln.de/) that is supported by the statistical department of the city government (Stadt Köln). The platform is an open-source project from NuCivic (https://getdkan.org/) and all data is publically available. I used the following data sets that used:
</p>
<p>Data Sources (With reference date): </p>

Vehicle statistic: https://www.offenedaten-koeln.de/dataset/kfz-statistik-koeln (31.12.2017) <br/>
Population statistic: https://www.offenedaten-koeln.de/dataset/einwohner-statistik-koeln (31.12.2017) <br/>
Job market statistic: https://www.offenedaten-koeln.de/dataset/arbeitsmarkt-statistik-koeln (31.12.2017) <br/>
Election statistic: (German federal government (Bundestag): https://www.offenedaten-koeln.de/dataset/bundestagswahl-2017-koeln (24.09.2017) <br/>
City quaters: https://www.offenedaten-koeln.de/dataset/stadtviertel <br/>
<br/>
Second I used the Foursquare location API to aggregate information about venues (location, category) around a given point on the map. I reused the functions from the preceded courses.<br/>
<br/>
### Data Granularity
<br/>
All data sets, except for the election statistic, is stored in a GeoJSON Format that already coded the geospatial information of all neighborhoods polygon. The used features are furthermore aggregated on the level of all 86 city neighborhoods ("Stadtteil").<br/>
<br/>
For the Foursquare API, I used the centroid of each polygon as the input to fetch the venues around a radius of 1000 meters. The problem with the Foursquare API is that it only delivers a maximum of 100 venues around the requested centroids. To get a higher resolution of the venue data, I used a deeper granularity than the neighborhood level to obtain more city venues. The municipal hierarchy below the 86 neighborhoods are the 374 city quarters ("Stadtviertel") for which I used the centroids of each of those smaller polygons as the reference for the location API call.<br/>
<br/>

### Features
<br/>
The following features are used for the clustering analysis. I sourced the data from the above links and joined the relevant data fields on the neighborhood.
<br/>
-vehicle ownership share (How many people own a car within a neighborhood)<br/>
-Unemployed (How many people are unemployed within a neighborhood)<br/>
-Migration from other cities (How many people move to a neighborhood from other cities)<br/>
-Voter turnout (How many people had cast a vote for the Bundestagswahl 2017)<br/>
-1st Most Common Venue (What is a most common category within a neighborhood)<br/>
<br/>
I labeled all features, except the 1st most common venue, depending on their quintilized values with the following categories: Lowest, Low, Medium, High, Highest

### Methodology
<br/>
To analyze the data I joined all data into one new data frame that includes all the above-mentioned features and their respected neighborhood. Before merging I checked all datasets visually on a city map to double-check the data consistency. I used the folium library (Python API for leaflet) to visualize the geospatial data on the map. An important input here is the polygonal shapes of the neighborhoods formatted as GeoJSON that can be matched with new input (Neighborhood columns will be joined for visualization). I checked the data frame for correlations afterward and did not find any highly correlated features (As I dropped them already in a preliminary exploratory data analysis I conducted before).

The next step in the application of machine learning on the data set is the choice of a fitting clustering algorithm. All entries in the new data frame are now categorical and therefore not feasible for the KMeans Algorithm (It only can be fitted with numerical data). It is possible to install an implementation of the Kmodes algorithm that was proposed by Huang (Huang, Z.: Extensions to the k-modes algorithm for clustering large data sets with categorical values, Data Mining and Knowledge Discovery 2(3), pp. 283-304, 1998.).

To chose the right amount of cluster, I visualized the clustering cost (defined as the sum distance of all points to their respective cluster centroids) independence of the used clusters. Using the elbow method it can be seen that five clusters are the perfect fit for the underlying data.

### Results and Discussion
<br/>
The delimitation of all five clusters works very well as seen on the map (inside the jupyter notebook).    The intra-homogeneity of each cluster according to the feature: "Unemployed" is pretty high, same for the feature "Voter turnout". Cluster 1 and cluster 4 seem to have the highest unemployment rates, but they have differences in vehicle ownership shares. Hotels and Bakeries are to be the most common venues in clusters 1 to 4. It is noticeable that cluster 5 has the lowest unemployment and the highest voter turnout compared to all other clusters. The most common venues here are cafes.

Relying on these insights it is now possible to steer a client's marketing campaign more precisely and spend the budget on more efficient measurements. The cluster can be addressed depending on the advertised product, as this needs to be coordinated with the customer. 

A point open for discussion is the problem with the assumption of homogenous neighborhoods. All data is aggregated only on the neighborhood level, leaving no room for disparate data distribution within each neighborhood. It would be good if more granular data would be available to strengthen the model and therefore the output. 

### Summary
<br/>
It was shown that it is possible to conduct a thorough analysis of a known business problem with a few lines of code from an openly available data source. I applied the learned techniques of machine learning to a self-defined business problem. The result was a broad visualization of the technique placed in a business context. Even though the problem was fictional it does not lower the overall relevance of the topic. The IBM Course helped me to understand the basic principles of ML and the necessary methods. 
