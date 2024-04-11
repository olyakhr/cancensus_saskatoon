---
title: "Income maps"
output: 
  html_document:
    keep_md: true
date: "2024-03-28"
---
### We will create income maps using the "cancensus" package and CensusMapper data
###### In this code I am using the latest 2021 census data.




```
## Downloading: 7.4 kB     Downloading: 7.4 kB     Downloading: 7.4 kB     Downloading: 7.4 kB     Downloading: 7.6 kB     Downloading: 7.6 kB     Downloading: 7.6 kB     Downloading: 7.6 kB     Downloading: 12 kB     Downloading: 12 kB     Downloading: 16 kB     Downloading: 16 kB     Downloading: 32 kB     Downloading: 32 kB     Downloading: 36 kB     Downloading: 36 kB     Downloading: 36 kB     Downloading: 36 kB     Downloading: 56 kB     Downloading: 56 kB     Downloading: 80 kB     Downloading: 80 kB     Downloading: 89 kB     Downloading: 89 kB     Downloading: 89 kB     Downloading: 89 kB     Downloading: 130 kB     Downloading: 130 kB     Downloading: 140 kB     Downloading: 140 kB     Downloading: 150 kB     Downloading: 150 kB     Downloading: 150 kB     Downloading: 150 kB
```

```
## Classes 'sf' and 'data.frame':	371 obs. of  18 variables:
##  $ Shape Area          : num  2.8764 0.102 0.1532 0.0551 0.1451 ...
##  $ Type                : Factor w/ 1 level "DA": 1 1 1 1 1 1 1 1 1 1 ...
##  $ Households          : int  256 122 184 116 132 219 242 91 203 151 ...
##  $ Quality Flags       : chr  "0" "0" "0" "0" ...
##  $ name                : chr  "47110021" "47110022" "47110027" "47110028" ...
##  $ GeoUID              : chr  "47110021" "47110022" "47110027" "47110028" ...
##  $ CSD_UID             : chr  "4711066" "4711066" "4711066" "4711066" ...
##  $ Population          : int  720 344 519 397 364 595 492 236 437 418 ...
##  $ CT_UID              : chr  "7250021.05" "7250021.05" "7250021.05" "7250021.05" ...
##  $ Dwellings           : int  260 127 188 120 135 229 252 93 212 154 ...
##  $ CD_UID              : chr  "4711" "4711" "4711" "4711" ...
##  $ CMA_UID             : chr  "47725" "47725" "47725" "47725" ...
##  $ Region Name         : Factor w/ 371 levels "47110021","47110022",..: 1 2 3 4 5 6 7 8 9 10 ...
##  $ Area (sq km)        : num  2.8764 0.102 0.1532 0.0551 0.1451 ...
##  $ median_total_income : num  64000 57600 55600 39200 51600 49200 40000 NA 35600 53200 ...
##  $ median_female_income: num  53600 53200 47200 38400 46800 45200 34800 NA 35200 44400 ...
##  $ median_male_income  : num  73000 58800 68000 41200 57600 54400 46800 NA 36400 65000 ...
##  $ geometry            :sfc_MULTIPOLYGON of length 371; first list element: List of 1
##   ..$ :List of 1
##   .. ..$ : num [1:86, 1:2] -107 -107 -107 -107 -107 ...
##   ..- attr(*, "class")= chr [1:3] "XY" "MULTIPOLYGON" "sfg"
##  - attr(*, "sf_column")= chr "geometry"
##  - attr(*, "agr")= Factor w/ 3 levels "constant","aggregate",..: 1 1 1 1 1 1 1 1 1 1 ...
##   ..- attr(*, "names")= chr [1:17] "Shape Area" "Type" "Households" "Quality Flags" ...
```


```r
ggplot(census_data) + geom_sf(aes(fill = median_total_income), colour = "grey") +
  scale_colour_brewer("Median Total Income", labels = scales::dollar) + theme_void() +
  theme(panel.grid = element_blank(),
        axis.text = element_blank(),
        axis.ticks = element_blank()) + 
  coord_sf(datum=NA) +
  labs(title = "Median Total Income in 2020", subtitle = "Saskatoon, 2021 Census")
```

![](income_maps_files/figure-html/unnamed-chunk-2-1.png)<!-- -->

This map shows that the highest median total income is on the outskirts of Saskatoon, while the lowest income values are represented by University Heights Suburban Center and U of S campus, *apparently because of the predominant student population*.


```r
ggplot(census_data) + geom_sf(aes(fill = median_female_income), colour = "grey") +
  scale_fill_viridis_c("Median Female Income", labels = scales::dollar, option = "cividis") + theme_void() +
  theme(panel.grid = element_blank(),
        axis.text = element_blank(),
        axis.ticks = element_blank()) + 
  coord_sf(datum=NA) +
  labs(title = "Median Female Income in 2020", subtitle = "Saskatoon, 2021 Census")
```

![](income_maps_files/figure-html/unnamed-chunk-3-1.png)<!-- -->

Unfortunately, median female income in Saskatoon shows the lowest max values. The only neighborhood which represents a median income among women higher than 60000CAD is **Nutana**. Most of Saskatoon's female population gets *between 40000CAD and 50000CAD* annually.


```r
ggplot(census_data) + geom_sf(aes(fill = median_male_income), colour = "grey") +
  scale_fill_viridis_c("Median Male Income", labels = scales::dollar, option = "cividis") + theme_void() +
  theme(panel.grid = element_blank(),
        axis.text = element_blank(),
        axis.ticks = element_blank()) + 
  coord_sf(datum=NA) +
  labs(title = "Median Male Income in 2020", subtitle = "Saskatoon, 2021 Census")
```

![](income_maps_files/figure-html/unnamed-chunk-4-1.png)<!-- -->

Comparing with median total and female income, male population shows the highest median income values across the neighborhoods. 
There's a significant difference between the west bank of the city with the predominant median income of **60000CAD+** and east bank with **up to 60000CAD** of annual income. 
