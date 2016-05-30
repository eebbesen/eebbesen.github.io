---
layout: post
title:  "Showing data over time: torque maps with CartoDB"
date:   2016-05-30 17:59:44 -0500
categories: cartodb torque
---

Sometimes you can make a dataset more informative and more impactful by displaying it over time.  Trends can become more clear for data that has a time compenent when viewers see the data visualized over time.  [CartoDB][carto-home] offers torque maps to allow you to do this.  Let's create a torque map of our own!

### Upload a dataset that has a time component
You probably already have data that you're interested in.  If not, you can browse the [CartoDB data library][carto-datasets] (look for 'Data library').  I will be using the [7-county Twin Cities Metropolitan Area residential building permit data from 2009 through 2014][residential-permits] dataset.

Your dataset should include a column that is date-specific.  [My dataset][residential-permits] has a column called `year`.

### Create a torque map from your data
* Open your dataset in [CartoDB][carto-home]
* Click Map View
* On the right hand side, locate the Wizards icon -- it looks like a paintbrush and sits directly below SQL
* Select your dataset's date column from the Time Column dropdown.  Your data should now be 'playing' on your map!


### Tweak your torque map
There are a number of knobs you can adjust to give your torque map the look you're going for.  Try setting Steps to a value that is close the number of data groupings in your dataset.  Try setting Duration(secs) to a value that isn't too fast or too slow.

Tip: If you click the CSS tab (just below your torque paintbrush) you can change values (like steps) to values that aren't available in the dropdowns.

See [CartoDB's Carto Academy][carto-academy] for more detailed training on all of the visualization features offered by [CartoDB][carto-home].

### Share your torque map
* Click the left-pointing arrow in the upper left of your browser to return to a list of your datasets
* Select your map by clicking on the icon to the left of it
* Click Create map at the top of the list of datasets.  Your map should appear with the settings you last applied
* When you are happy with the way your map looks, click Publish.  Copy the link(s) that you want to share or embed


[carto-academy]: https://academy.cartodb.com/
[carto-datasets]: https://ericebbesen.cartodb.com/dashboard/datasets
[carto-home]: https://cartodb.com
[residential-permits]: https://gisdata.mn.gov/dataset/us-mn-state-metc-econ-residential-building-permts
