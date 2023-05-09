# R-Code-Example
An example R code chunk that demonstrates my ability to create detailed maps.

# Introduction / Context

While in my graduate-level R class, our professor encouraged us to expand our coding skills whenever we had the time. For one assignment, I decided to learn how to create country-level maps in R. I downloaded a dataset from the [Uppsala Conflict Data Program](https://ucdp.uu.se/) that covered organized violence events in Mali between 1989 and 2021. The dataset, included in this repo, contains key variables like year, type of violence, estimated number of deaths per event, and location data (latitude and longitude). 

The final map created is a geospatial representation of organized violence events in Mali between 1989 and 2021. Each red circle represents one violent event in the dataset. Click [here](https://jcook125.github.io/R-Code-Example/) to view this code and visualization.

# Data Source

Source: Uppsala Conflict Data Program (Date of retrieval: 23/02/13) UCDP Conflict Encyclopedia: www.ucdp.uu.se, Uppsala University
![image](https://github.com/jcook125/R-Code-Example/assets/123001199/46fa3408-edc4-47c1-912d-c2c6531b30d2)

# Code Sample

```r
# Packages Used
library(tidyverse)
library(maps)

# Import the Dataset
Mali = read_csv("Mali_Violence_Data.csv")

# Code for Map

  map_mali = map_data('world', region = "Mali") 
  # the map_data function creates a dataframe with Mali, used in one of the geoms
  
  # The ggplot consists of 3 stacked geoms, a base layer, the country map, and the points
  ggplot() +
    geom_polygon(data = map_data("world"), # This creates the base layer "world" map
                 aes(x = long, y = lat, group = group),
                 color = 'black', fill = 'tan') + # I wanted black borders and tan countries
    geom_polygon(data = map_mali, # This creates the shape of Mali, referring to the df created
                 aes(x = long, y = lat, group = group)) + 
    geom_point(data = Mali, aes(x = longitude, y = latitude), # Points from the Uppsala df
               color = 'red', shape = 1, alpha = 0.5) + #specify color, shape, transparency
    coord_map() + 
    coord_fixed( # this lets you select your map's borders by coordinates
      ratio = 1,
      xlim = c(-12,4),
      ylim = c(10.5,25)) + 
    labs(title = "Organized Violence-Related Deaths Across Mali", x = "",
         y = "") +
    theme(
      axis.text = element_blank())


```

