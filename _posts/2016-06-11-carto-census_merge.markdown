---
layout: post
title:  "Working with Census American Community Survey data and CartoDB"
date:   2016-06-11 12:21:12 -0500
categories: cartodb census acs merge shape tract
---

[CartoDB][carto-home] needs shape files or latitude/longitude values to place your data on a map.  Some datasets don't have these by default so you need to convert this data or merge it.  In this example I'll be merging census tract-level data with data that provides shape boundaries for the census tracts.  

## Identify and upload datasets

### Identify datasets

[American Community Survey (ACS) data][census_acs_home] is provided by the United States Census Buerau.  For this exercise I'm using [POVERTY STATUS IN THE PAST 12 MONTHS 2010-2014 American Community Survey 5-Year Estimates][poverty_ramsey_acs] census tract-level data, and merging that with [a census tract-level shapfile dataset][census_tiger_shapefiles].  I'll call the ACS data my primary dataset and the shapefile data my secondary dataset.

I need to merge in this case because one dataset (primary) has the data in which I'm interested, but only has alphanumeric values representing census tracts -- it doesn't have any geographic identifiers that are understood by [CartoDB][carto-home].

### Modify datasets if necessary

#### CartoDB column restriction

[CartoDB][carto-home] imposes a 250 column limit for free accounts, so some datasets may need to be trimmed down.  I needed to remove about twenty columns from the dataset I'm using.

### Upload datasets

Now that you have your data in your desired state, upload all three to [CartoDB][carto-home].  Remember that our dataset with the ACS data is our primary dataset and our secondary dataset is the the one we'll use to help [CartoDB][carto-home] understand the geography in our primary dataset.


## Merge the datasets

### Merge primary and secondary datasets

This will add geographic data that [CartoDB][carto-home] can understand

1. In the lower right hand of the browser, look for the merge datasets icon.  At the time of this writing it should be the third icon from the bottom, but this is subject to change over time.  Click the merge datasets icon.
2. Select Column join
3. From your primary dataset select the `geo_id` column.  From the secondary dataset select the `affgeoid` column.
4. Click Next Step
5. For the secondary dataset, click Select all columns (at the bottom) twice so that no columns from the second dataset are selected.  From the secondary dataset click the_geom so that it alone is selected from the secondary dataset.  This should deselect the_geom from the primary dataset.
6. Click Merge Datasets

### Remove null records from primary dataset (optional)
This will remove shapes from outside Ramsey County from our dataset.
View the primary dataset in the Data View.  Note that the column named `the_geom` is empty and if you click Map View [CartoDB][carto-home] prompts you to tell it which columns to use for mapping.  Also note there are a few columns with mostly `null` values -- this is because our primary dataset has records only for Ramsey County, Minnesota, but our secondary dataset has records for all census tracts in the state.  We can filter those out to help our map look better.

1. On the right hand side of the browser you'll see a bar with the number "1" near the top.  Click the SQL icon right below it.  
2. Change the query by adding `WHERE geo_id IS NOT NULL`
3. Click Apply query
4. At the top of the dataset click "create dataset from query"
5. Select Map View and you'll see Ramsey County outlined on the map

<iframe width="100%" height="520" frameborder="0" src="https://ericebbesen.cartodb.com/viz/ef998112-302a-11e6-a103-0ea31932ec1d/embed_map" allowfullscreen webkitallowfullscreen mozallowfullscreen oallowfullscreen msallowfullscreen></iframe>



[census_acs_home]: https://www.census.gov/programs-surveys/acs/data.html
[poverty_ramsey_acs]: http://factfinder.census.gov/bkmk/table/1.0/en/ACS/14_5YR/S1701/0500000US27123.14000|610U400US53002
[carto-home]: https://cartodb.com
[census_tiger_shapefiles]: https://www.census.gov/geo/maps-data/data/tiger-cart-boundary.html
[census_state_shapefiles]: https://www.census.gov/geo/maps-data/data/tract_rel_download.html
