---
title: "income maps"
output: 
  html_document:
    keep_md: true
date: "2024-03-28"
---






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

Write some interpreation here.... 


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

