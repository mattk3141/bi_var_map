**Project description:** The goal of this project was to understand how to build bivariate maps when creating choropleth maps. 
I decided to go with median income and median rent due to the correlation that I thought would be present that would be intresting to study. 



**Project Code:**
## Setup

```{r setup}
##Note: packages
library(tidyverse)
library(tidycensus)
library(sf)
library(ggplot2)

##Note: settings for tidycensus
options(tigris_class = "sf")
options(tigris_use_cache = TRUE)
##Note: no hasttag in front of api key once its installed on the computer
census_api_key("3414620c09213c7645396f11d911b42f70222c5b", install=TRUE)
##Note: where the files I create eventually go into the computer
setwd("D://GES 486//downloads")

## Get Census Data

```{r download census}
##Note: This gets median Income 2015-2019
bmore_MI_2019 <- get_acs(geography = "tract",
variables = c("med_hh_inc" = "B19013_001" # Median household income
            ),
year = 2019,
survey = "acs5",
state = c(24), 
county = c(510,5), 
geometry = TRUE, # download the shapefile with the data
output = "wide") # need this




#This gets Median Rent prices 2015-2019
#Before Using rent, tried rent asking price but found the data difficult to understand. 
bmore_RENT_2019 <- get_acs(geography = "tract",
variables = c("RENT" = "B25058_001" # RENT"
              ),
year = 2019,
survey = "acs5",
state = c(24), 
county = c(510,5), 
geometry = TRUE, # download the shapefile with the data
output = "wide") # need this

st_write(st_transform(bmore_RENT_2019, 3857), "bmore_RENT_2019.geojson")
st_write(st_transform(bmore_MI_2019, 3857), "bmore_MI_2019.geojson")

                         
