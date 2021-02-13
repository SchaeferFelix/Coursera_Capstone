# Business Report - Neighboorhood Microtrageting

## Applied Data Science Capstone Project

All necessary data and jupyter notebooks are provided in the "Cologne" folder


**Introduction** 

Cologne is one of the biggest Cities in germany and with over 100.000 students a city with a deeply entrenched youth culture. The city and its 86 Neighboordhoods called "Veedel" (cologne dialect for: "Viertel) are very diverse and populated with around one million inhabittants. _Intro BLABLA

I want to consider a fictious Business Problem of a marketing consultancy that helps local companies with their advertising campain. The consultancy will deliver an algorithm that clusters the neighborhood according to different categorical inputs regarding demographical and socio-economical factors. For the most cost efficienct marketing mix it is necessary to approach the correct costumer. Cluster neighboorhood is a feasible step to distribute the marketing effort more efficienctly. The algorithm of the marketing consultancy will help local companies for a better approach on microtargeting the right costumers in the right Neighborhoods as different cluster may exhibit different consumer elasticities. I will show in the following the different opportunities to cluster a city with four different features that are aggregated and engineered from different data sources. It can be shown that an efficient clustering of the neighborhood is a consistent approach that delivers a clear output if the assumption of internally homogenous neighborhoods holds. A graphical visualisation is shown to distinghusih the different cluster on a complete city map.

As a disclaimer: I won't discuss any implication from the assigned clusters on the neighboorhoods nor will I deliver any marketing advice. Furthermore it needs to be said that the clustering can exhibit "rational discrimination" that deilveres "segmeted monocultures" to quote the Whistleblower from Camebridge Analytica Christopher Wylie. I am against any of those resulting discrimination and very aware about the simplification on socio-economical factors that can result from clustering on those data.

**Data**

First I gathered the demographical data for the analyis form the city of cologne open data platform  (only in german: https://www.offenedaten-koeln.de/) that is supported by the statisitcal department of the city governement (Stadt Köln). The platform is a open-source project from NuCivic (https://getdkan.org/) and all data is publically available. I used the following data sets as raw data:

Data Sources (With reference date):
Vehicle statistic: https://www.offenedaten-koeln.de/dataset/kfz-statistik-koeln (31.12.2017)
Population statistic: https://www.offenedaten-koeln.de/dataset/einwohner-statistik-koeln (31.12.2017)
Job market statistic: https://www.offenedaten-koeln.de/dataset/arbeitsmarkt-statistik-koeln (31.12.2017)
Election statistic: (German federal governent (Bundestag): https://www.offenedaten-koeln.de/dataset/bundestagswahl-2017-koeln (24.09.2017)

All data sets, except for the election statistic, was delivered in a GeoJSON Format that already coded the geospatial information of all neighborhoods polygon. The analyis is conducted on neighborhood level ("Stadtteil")





