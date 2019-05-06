# Introduction/Business Problem

Employees do not tend to stay in a single organization forever. It is common for a resource to seek opportunities that best suits his aspirations and in his attempt to satisfy requirements, seeks better opportunities outside current employment. However, better opportunity may also demand relocating to new places and it is difficult to find a suitable place to move with family and often results in multiple enquiries and prolonged decision making process while selecting a best neighborhood and still does not ensure satisfaction.

Employees seeking relocation is the Target audience of this solution. This use case will center around an employee named Luke, who is currently residing in New York in the Manhattan area and has found a suitable Job opportunity in Scarborough, Toronto. He has never been to Toronto and has limited friends in that area. He is not satisfied with his research and the locations suggested to him by friends and agents. He is looking for neighborhoods similar to his current neighborhood.

Can we find neighborhoods in Toronto that are similar to Luke's current area of residence?



# Data

In order to answer the question at hand, we would need the Newyork geo data pertaining to Luke's current area of residence. Additionally in order to find the venues associated with his current residence, we would need to source venue data from foursquate or Google. New York geo data is available at https://geo.nyu.edu/catalog/nyu_2451_34572. 
Similar geo data will be required to be sourced for Toronto, Scarborough. Geo data for Toronto is available at https://en.wikipedia.org/wiki/List_of_postal_codes_of_Canada:_M , Geospacial data from links provided in the labs, and venue category data from either foursquare or google.

The Neighborhood data will have Borough, neighborhood, latitude and longitude mainly.

Foursquare venue data will be extracted based on the latitude and longitude data of the Neighborhoods around a radius and limited by certain number of data sets due to computation limitations. 

Venue data used will mainly have Venue name, Venue latitude and longitude and Venue category data that will be processed to arrive at similarity scores in order to match the current neighborhood with the new neighborhood.

# Methodology 

Approach: Lukes current geo data and venue data will provide with top 10 venues in his current locality. This data will be matched with the venues within clusters in Scarborough that we will arrive at with our model. 

## New York data processing

Newyork JSON data was populated into dataframes for Borough, Neighborhood, Latitude and Lonfitude to help come up with venue data.

Using the geo latitude and longitude, the manatten venue data was arrived at giving the basic data required to come up with currnt neighborhood features.

Washington Heights in Manhattan data was further analysed based on the Venue category data imported earlier from foursquare and mean figures of frequency of occurance of the venues was arrived at.

Top 10 venues were derived form the data so as to have a basis for matching the toronto cluster data in similar format.

Result of NY data analysis: we get Lukes current Neighbourhood top 10 venues


## Toronto Data Analysis

Toronto data was obtained from wiki links and scraped of from the site to get the Borough, neighborhood data, which was further sanitized

Geo spacial data was merged with the wiki data to get a similar dataframe as the NEw York data to arrive at the base toronto data.

Toronto data was further augmented with venue data from foursquare using the web api

Toronto neighborhood data was analysed for venue category and encoding was appliued so as to form the basis of getting first 10 venues. Mean of frequency of venues was arrived at which was later utilized for clustering

From the processed data, top 10 venue was arrived at
we were able to get the venue catogory frequency of all lukes {lukes_new_Borough} neighbourhoods

## Matching Lukes current Venues against clusters drawn for toronto's neighbourhood venues

Data Preparation once complete, clustering was taken up for the similarity mathcing. kmeans clustering technique wad used. Elbow curev was plotted to see how the score would vary with the clusters size. It was observed that saturation reached at around 15 size.

Venue data was merged with Borough and Neighborhood data to arrive at the final dataset for similarity comparison which now had cluster details as well.

### Similarity computation

Similarity was computed between NY top venue data with clusters for toronto data. Certain generalization was made during comparison such that commonalty amongst venues was considered as a match e.g restaurant was considered as a similarity for various kinfds of restaurants.


# Results 

Cluster 0 and 3 have highest similarity and would indicate a better suggestion to Luke though, the deviation is small. 

# Discussion

One can drill down the similarity computation to neighborhood level and can further provide exact neighborood as a suggestion as well. Different similarity computation can be done and results compared. Similarity result will become more crisp if more venue can be added over and above the top 10 venues we limited to in this PoC. Suggestions can also include Lukes other preferences but has not been included in the scope of the study. Other clustering methods can also be studied as future work.

# Conclusion

Employees continue to look for better opportunities and relocation does not pose a limitation if such methodologies are adopted to come up with informed decisions before relaocation is finalized. It also saves om cost due to multiple visits to chose a best locality to live.


