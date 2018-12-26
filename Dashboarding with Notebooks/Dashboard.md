---
title: 'Dashboarding with Notebooks: NYC Housing Authority'
output:
  html_document:
    df_print: paged
---

**An automated dashboard built to investigate structural patterns resulting from New York City & State transportation policy.**  





lines of questioning - EDA  
how many riders of L train  
how many cyclists  
how many bus riders  
refer to article predictions of where capacity will move to   
present general transit trends maybe  
show map of cyclist accidents?  
show time-series trends of accidents  
conclude with whether L train has increased accidents  
leaflet timeline is difficult at best, consider gganimate  
gganimate issues installing with R 3.5.1  
oof  

I was inspired by this [CityLab](https://www.citylab.com/perspective/2018/12/new-york-city-electric-bikes-transit-crisis-de-blasio/577969/) article detailing the impending transportation crisis due to the MTA L Line shutdown. Specifically, I am interested in observing whether the shutdown contributes to an increase in cyclist injuries due to motor vehicle collisions as L Train riders seek alternatives.  
  
I expect most people to shift to other public transit options as well as ride-sharing and hailing, and could investigate the dispersion of L Train riders to other options as a whole if data is available, but for now I will focus on cyclists (since the city certainly doesn't).  

<br> 

Let's start by looking at some performance metrics for the MTA subway network as a whole. 
<br>



```
## Error in loadNamespace(name): there is no package called 'webshot'
```


```
## Error in loadNamespace(name): there is no package called 'webshot'
```


```
## Error in loadNamespace(name): there is no package called 'webshot'
```


```
## Error in loadNamespace(name): there is no package called 'webshot'
```

Next, the L Line specifically: 
<br>

```
## Error in loadNamespace(name): there is no package called 'webshot'
```

Now let's compare the yearly average OTP between lines.
<br>


Now let's look at some two-wheeled data.
<br>




```
## Error in loadNamespace(name): there is no package called 'webshot'
```



<!-- ```{r message=FALSE, echo=FALSE} -->
<!-- # light data cleaning  -->
<!-- NYCHA <- NYCHA %>%  -->
<!-- slice(22:35) -->
<!-- ``` -->


<!-- ```{r echo=FALSE, fig.width=10} -->
<!-- p <- NYCHA %>%  -->
<!--   ggplot(aes(x = PROGRAM, y = `Total Families`)) +  -->
<!--   geom_bar(stat = 'identity', aes(fill = STATECITY_SECTION8_FLAG)) + -->
<!--   scale_fill_brewer('Blues', name = 'Household Type') +  -->
<!--   ylab('Total Families') + -->
<!--   xlab('Borough') + -->
<!--   theme(legend.position = 'top') +  -->
<!--   theme_classic()  -->

<!-- ggplotly(p) %>%  -->
<!--   layout(title = 'Households by Housing Type and Borough') -->
<!-- ``` -->






<!-- ```{r} -->
<!-- library(htmlwidgets) -->
<!-- library(htmltools) -->
<!-- library(leaflet) -->
<!-- library(geojsonio) -->
<!-- ``` -->

<!-- ```{r} -->
<!-- tst <- NYPD %>%  -->
<!--   slice(1:466)  -->

<!-- tst$DATE <- tst$DATE %>%  -->
<!--   ymd()  -->

<!-- tst$DATE <- format(tst$DATE, '%d-%b-%Y') -->

<!-- tst$DATE <- as.Date(tst$DATE, format = '%d-%b-%Y') -->

<!-- tst$START <- tst$DATE -->

<!-- tst <- tst %>%  -->
<!--   select(LATITUDE, LONGITUDE, START) %>%  -->
<!--   as.data.frame() -->

<!-- # set start same as end, adjust however you would like -->
<!-- tst$END <- tst$START + 30 -->

<!-- # use geojsonio to convert our data.frame to GeoJSON which timeline expects -->
<!-- tst_geo <- geojson_json(tst, lat = 'LATITUDE', lon = 'LONGITUDE', pretty = TRUE) -->

<!-- # create a leaflet map on which we will build -->
<!-- leaf <- leaflet() %>%  -->
<!--   addTiles() -->

<!-- # add leaflet-timeline as a dependency -->
<!-- leaf$dependencies[[length(leaf$dependencies)+1]] <- htmlDependency( -->
<!--     name = "leaflet-timeline", -->
<!--     version = "1.0.0", -->
<!--     src = c("href" = "http://skeate.github.io/Leaflet.timeline/"), -->
<!--     script = "javascripts/leaflet.timeline.js", -->
<!--     stylesheet = "stylesheets/leaflet.timeline.css" -->
<!-- ) -->

<!-- # use the new onRender in htmlwidgets to run this code once our leaflet map is rendered -->
<!-- # I did not spend time perfecting the leaflet-timeline options -->
<!-- leaf %>% -->
<!--     setView(-73.9665,40.74667,11) %>% -->
<!--     onRender(sprintf( -->
<!--         ' -->
<!--         function(el,x){ -->
<!--         var tst_data = %s; -->

<!--         var timelineControl = L.timelineSliderControl({ -->
<!--           formatOutput: function(date) { -->
<!--             return new Date(date).toString(); -->
<!--           } -->
<!--         }); -->

<!--         var timeline = L.timeline(tst_data, { -->
<!--         pointToLayer: function(data, latlng){ -->
<!--         var hue_min = 120; -->
<!--         var hue_max = 0; -->
<!--         var hue = hue_min; -->
<!--         return L.circleMarker(latlng, { -->
<!--         radius: 10, -->
<!--         color: "hsl("+hue+", 100%%, 50%%)", -->
<!--         fillColor: "hsl("+hue+", 100%%, 50%%)" -->
<!--         }); -->
<!--         }, -->
<!--         steps: 1000, -->
<!--         duration: 16438, -->
<!--         showTicks: true -->
<!--         }); -->
<!--         timelineControl.addTo(HTMLWidgets.find(".leaflet").getMap()); -->
<!--         timelineControl.addTimelines(timeline); -->
<!--         timeline.addTo(HTMLWidgets.find(".leaflet").getMap()); -->
<!--         } -->
<!--         ', -->
<!--         tst_geo -->
<!--     )) -->


<!-- ``` -->


<!-- ```{r} -->
<!-- #Build data.frame with 10 obs + 3 cols -->
<!-- power <- data.frame( -->
<!--     "Latitude" = c(33.515556, 38.060556, 47.903056, 49.71, 49.041667, 31.934167, 54.140586, 54.140586, 48.494444, 48.494444), -->
<!--     "Longitude" = c(129.837222, -77.789444, 7.563056, 8.415278, 9.175, -82.343889, 13.664422, 13.664422, 17.681944, 17.681944), -->
<!--     "start" = do.call( -->
<!--         "as.Date", -->
<!--         list( -->
<!--             x = c("15-Sep-1971", "1-Dec-1971", "1-Feb-1972", "1-Feb-1972", "1-Feb-1972", "1-Feb-1972", "1-Apr-1972", "1-Apr-1972", "24-Apr-1972", "24-Apr-1972"), -->
<!--             format = "%d-%b-%Y" -->
<!--         ) -->
<!--     ) -->
<!-- ) -->

<!-- # set start same as end -->
<!-- #  adjust however you would like -->
<!-- power$end <- power$start + 30 -->


<!-- # use geojsonio to convert our data.frame -->
<!-- #  to GeoJSON which timeline expects -->
<!-- power_geo <- geojson_json(power,lat="Latitude",lon="Longitude", pretty = T) -->

<!-- # create a leaflet map on which we will build -->
<!-- leaf <- leaflet() %>% -->
<!--     addTiles() -->

<!-- # add leaflet-timeline as a dependency -->
<!-- #  to get the js and css -->
<!-- leaf$dependencies[[length(leaf$dependencies)+1]] <- htmlDependency( -->
<!--     name = "leaflet-timeline", -->
<!--     version = "1.0.0", -->
<!--     src = c("href" = "http://skeate.github.io/Leaflet.timeline/"), -->
<!--     script = "javascripts/leaflet.timeline.js", -->
<!--     stylesheet = "stylesheets/leaflet.timeline.css" -->
<!-- ) -->

<!-- # use the new onRender in htmlwidgets to run -->
<!-- #  this code once our leaflet map is rendered -->
<!-- #  I did not spend time perfecting the leaflet-timeline -->
<!-- #  options -->
<!-- leaf %>% -->
<!--     setView(44.0665,23.74667,2) %>% -->
<!--     onRender(sprintf( -->
<!--         ' -->
<!--         function(el,x){ -->
<!--         var power_data = %s; -->

<!--         var timelineControl = L.timelineSliderControl({ -->
<!--           formatOutput: function(date) { -->
<!--             return new Date(date).toString(); -->
<!--           } -->
<!--         }); -->

<!--         var timeline = L.timeline(power_data, { -->
<!--         pointToLayer: function(data, latlng){ -->
<!--         var hue_min = 120; -->
<!--         var hue_max = 0; -->
<!--         var hue = hue_min; -->
<!--         return L.circleMarker(latlng, { -->
<!--         radius: 10, -->
<!--         color: "hsl("+hue+", 100%%, 50%%)", -->
<!--         fillColor: "hsl("+hue+", 100%%, 50%%)" -->
<!--         }); -->
<!--         }, -->
<!--         steps: 1000, -->
<!--         duration: 10000, -->
<!--         showTicks: true -->
<!--         }); -->
<!--         timelineControl.addTo(HTMLWidgets.find(".leaflet").getMap()); -->
<!--         timelineControl.addTimelines(timeline); -->
<!--         timeline.addTo(HTMLWidgets.find(".leaflet").getMap()); -->
<!--         } -->
<!--         ', -->
<!--         power_geo -->
<!--     )) -->
<!-- ``` -->
