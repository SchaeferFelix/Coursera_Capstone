# Business Report - Neighboorhood Microtrageting

## Applied Data Science Capstone Project

<p>All necessary data and jupyter notebooks are provided in the "Cologne" folder </p>

**Introduction** 

<p>Cologne is one of the biggest Cities in germany and with over 100.000 students a city with a deeply entrenched youth culture. The city and its 86 Neighboordhoods called "Veedel" (cologne dialect for: "Viertel) are very diverse and populated with around one million inhabittants. </p>
<br/>
<p>I want to consider a fictious Business Problem of a marketing consultancy that helps local companies with their advertising campain by visualising different clusters on a geographical map. The consultancy will deliver an algorithm that clusters the neighborhood according to different categorical inputs regarding demographical and socio-economical factors. For the most cost efficienct marketing mix it is necessary to approach the correct costumer. Cluster neighboorhood is a feasible step to distribute the marketing effort more efficienctly. The algorithm of the marketing consultancy will help local companies for a better approach on microtargeting the right costumers in the right Neighborhoods as different cluster may exhibit different consumer elasticities. I will show in the following the different opportunities to cluster a city with four different features that are aggregated and engineered from different data sources. It can be shown that an efficient clustering of the neighborhood is a consistent approach that delivers a clear output if the assumption of internally homogenous neighborhoods holds. A graphical visualisation is shown to distinghusih the different cluster on a complete city map.
</p>
<p>As a disclaimer: I won't discuss any implication from the assigned clusters on the neighboorhoods nor will I deliver any marketing advice. Furthermore it needs to be said that the clustering can exhibit "rational discrimination" that deilveres "segmeted monocultures" to quote the Whistleblower from Camebridge Analytica Christopher Wylie. I am against any of those resulting discrimination and very aware about the simplification on socio-economical factors that can result from clustering on those data.
</p>

**Data Source**

<p>First I gathered the demographical data for the analyis form the city of cologne open data platform  (only in german: https://www.offenedaten-koeln.de/) that is supported by the statisitcal department of the city governement (Stadt Köln). The platform is a open-source project from NuCivic (https://getdkan.org/) and all data is publically available. I used the following data sets that used the :
</p>
Data Sources (With reference date):
<br/>
Vehicle statistic: https://www.offenedaten-koeln.de/dataset/kfz-statistik-koeln (31.12.2017) <br/>
Population statistic: https://www.offenedaten-koeln.de/dataset/einwohner-statistik-koeln (31.12.2017) <br/>
Job market statistic: https://www.offenedaten-koeln.de/dataset/arbeitsmarkt-statistik-koeln (31.12.2017) <br/>
Election statistic: (German federal governent (Bundestag): https://www.offenedaten-koeln.de/dataset/bundestagswahl-2017-koeln (24.09.2017) <br/>
City quaters: https://www.offenedaten-koeln.de/dataset/stadtviertel <br/>
<br/>
Second I used the Foursquare location API to aggregate information about venues (location, category) around a given point on the map. I basically reused the functions from the preceded courses.<br/>
<br/>
**Data Granularity and Extraction
<br/>
All data sets, except for the election statistic, is stored in a GeoJSON Format that already coded the geospatial information of all neighborhoods polygon. The used features are furthermore aggregated on the level of all 86 city neighborhoods ("Stadtteil").<br/>
<br/>
For the Foursquare API I used the centroid of each polygon as the input to fetch the venues around a radius of 1000 meters. The problem with the Foursquare API is that it only delivers a maximum of 100 venues around the requested centroids. To get a higher resolution of the venue data, I used a deeper granularity than the neighborhoods level to obtain more city venues. The muncipal hierachy below the 86 neighborhoods are the 347 city quaters ("Stadtviertel") for which I used the centroids of each of those smaller polygon as the reference for the location API call.<br/>
<br/>
**Used features
<br/>
The following features are used for the clustering analysis. I sourced the data from the above links and joined the relevant datafields on the neighborhood.
<br/>
-vehicle ownership share (How many people own a car within a neighborhood)<br/>
-Unemployed (How many people are unemployed within a neighborhood)<br/>
-Migration from other cities (How many people move to a neighborhood from other cities)<br/>
-Voter turnout (How many people had cast a vote for the Bundestagswahl 2017)<br/>
-1st Most Common Venue (What is most common category within a neighborhood)<br/>
<br/>
I labled all features, except from the 1st most common venue, depending on their quintilized values with the following categories: Lowest, Low, Medium, High, Highest





