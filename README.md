## Evaluating Hudson County Transit Accessblity with 2SFCA

**Hudson County as the site of study**
<br> Hudson county is a major hub for commerce and transportation in the region. The county is served by several major public transportation systems, including the Hudson-Bergen Light Rail, the Port Authority Trans-Hudson (PATH) rail system, and New Jersey Transit buses, making it an ideal site to study transit.<br>

**2-step-floating-catchment-area method** 
<br> Comparing with the buffer zone approach for measuring accessbility, the strength of 2SFCA is that it takes into consideration demand and supply interaction of the facility. <a href='https://journals.sagepub.com/doi/abs/10.1068/b29120?casa_token=iICd4Til9h0AAAAA:SxXYNHQgqoxAckICc0AxylFChpgLaEPwoH_qUVOD2E1-l7EzVXcEP8sUcvCg4T1Ql7CqkltGtX9u'>(Luo and Wang, 2002)</a>. 
    
Step 1 (on the facility supply side):
 - For each facility location $j$, given a threshold travel distance $d_{0}$, create a catachment area. 
 - Search for all tract $k$ whose centroid falls within the catchment $j$ and calculate the sum of population served in this catchment area. 
 - Compute the score of the facility $R_{j}$ as the number of supply divided by the sum population. 
    
Step 2 (on the population demand side):
 - Create a populatio-weighted centroid for each population location $i$. From each populaiton centroid, given a threshold travel distance$d_{0}$, create a catchment area.
 - Search for all facility point $j$ that are within the catchment area and sum up the facility score.
 - Assign the summed facility scores back to original population locations. 

For this project, I'm trying to evaluate how accessble by foot those transit stops are. So I will be using the walkable graphs to create catchment areas and setting the distance at 1000m, about 15 min walking distance. 

**Data sources** 
<br/>Transit point data: found on NJGinOpenData, maintained by NJ Transit GIS Department. Recent updates are in October 18,2022. The original dataset is is downloaded in GeoJson format. Since the original data covers the whole NJ, I clipped them using a Hudson county polygon to get transit stops in Hudson 
  county. After clipping, I noticed that there are more than 3000 bus stops, so I further applied drop duplicates by the same coordination, which leave me with about 1400 unique bus stops.  
Census shape data: found on and maintained by NHGIS. Downloaded the 2019 acs5 census tract data and block group data in GeoJson format. Both data are cropped to shoreline. 


**Static Map1: Hudson basic information** 
![Map1](https://github.com/springalrilmay/CommandLineGIS_FinalProject/main/images/viz1.png?raw=true)
<br/>The maps show a clear pattern of two spines of high population density running in a northeastern-southwestern direction. One spine is along the eastern coast in Hoboken and Jersey city, the other is parallel to it in Kearny. Between these two strips of high density are census tracts with larger area sizes and lower population density.

**Static Map2: Hudson transit stops** 
<br/>There are four types of transit running in Hudson, with a total of 1465 non-overlapping transit stops.
- Bus stops, which account for more than 97.8% of the total transit stops, run mostly along the two population density spines. The bus network is dense and stops almost at every intersection, serving mostly local needs.
- Light rail runs only along the eastern spine, with a total of 24 stops.
- The PATH train connects Hudson to Manhattan, with a total of 6 stops.
- Hudson has two rail stations, Secaucus Junction and Lincoln Harbor Station, which serve more regional needs.

**Static Map3: Catchment areas from the weighted census tract centroid and transit points**
<br/>To create the catchment areas, nearest nodes on the network are used as the proxies for the two set of points. Where the network is denser and more connected, the catchment is more in a shape of a complete polygon. The deeper the color, the more times the graph is covered by multiple catchment areas. 

**Interactive Map** 
The final interactive map has 5 layers in total, and can be find here. 
1 base layer, using the map tile from CartoDB positron.
2 choropleth map layers, 1 on census tract population density, 1 on census tract accessbility score.
1 point layer, with 4 types of transit stops.
1 polyline layer, with the network graph.
