---
layout: single
permalink: /articles/30daymapchallenge_stats_en/  
title : "30 DayMapChallenge 2020 Statistics" 
classes: wide
header:
  overlay_image: https://dl01fbzxdpfby.cloudfront.net/images/30dmc_stats_header_sd.png
  overlay_filter: 0.3
  caption: "Poster created by [Haifeng Niu](https://twitter.com/niu_haifeng)"
  teaser: https://dl01fbzxdpfby.cloudfront.net/images/30dmc_stats_header_sd.png
excerpt:
  Some statistics about the 30DayMapChallenge 2020 with Python

og_image: https://dl01fbzxdpfby.cloudfront.net/images/30daymapchallenge_stats/30dmc_stats_header.webp

comments: true
share: true
toc: true
toc_label: "Statistics"
toc_icon: "chart-line"
---

Ok then ! Now the 30DayMapChallenge 2020 is over, we just have to go back to our daily stuff and wait 2021 to see so many amazing maps !

One of my personal interests is to represent data, geographical or not, and I began to learn Python this year, to complete my skilss.

So, I decided to use all the material which was produced during the challenge to train myself, and in the same time, produce some dataviz and looks for insights :smile:

You will find here, as it is written, all the dataviz and the figures that will come out of it.

## Dataset

To realize a good dataviz, we need a good dataset. I just pick up the awesome work done by [David Friggens](https://twitter.com/dakvid), which put all the submissions [he could get here.](https://david.frigge.nz/30DayMapChallenge2020/) I enhance his Google Spreadsheet crawling Twitter with [Twint](https://github.com/twintproject/twint), which is a really good tool by the way.  
_(If anyone is interested about how I've done all this part of work, I could write an article about it later)_

By the way, if you didn't know it David did an awesome work to collect all maps, and [you can see them here !](https://david.frigge.nz/30DayMapChallenge2020/maps.html)  
Moreover, if you see one map missing or if you want to add some metadata on it, [feel free to read some instructions here.](https://david.frigge.nz/30DayMapChallenge2020/index.html)

![site david maps](https://dl01fbzxdpfby.cloudfront.net/images/30daymapchallenge_stats/capture_david_site.webp "David Frigge's site, which collect all submissions"){: .align-center}

## Finishers

To start exploring the dataset, I decided to honour finishers :+1: ! Those crazy girls and boys who have done (at least) one map a day, for each daily theme.  
I really don't know for who you're working guys, but I guess geo-productivity just decreased during november :grin:.

For the moment, and for what I could get, I identified **76 finishers** !

You can see below the statistics linked to all of the finishers on the date of December 12th 2020.  
I did it with [Plotly](https://plotly.com/), and I'm gonna put the code on some gist soon.

In summary, it represents :

- **2,310 tweets** :bird:
- **2,366 replies** :raising_hand: -_the submission with the largest number of replies has 29_
- **9,243 retweets** :incoming_envelope: -_the submission with the largest number of retweets has 235_
- **53,056 likes** :heart: -_the submission with the largest number of likes has 941_

I'll develop this kind of social statistics later, with all submissions, for sure !

On the next viz, you'll find every finisher, with the number of tweets, and social statistics by hovering each bar.

> If you're on mobile device, I would advise you to put it on landscape mode.  
> You can [click here](https://aurelienchaumet.github.io/data/30daymapchallenge_stats/finisher_stats.html) too, to visualize it in full screen

<iframe width="100%" height="820"
    src="https://aurelienchaumet.github.io/data/30daymapchallenge_stats/finisher_stats.html">
</iframe>

## Global statistics

Regarding all the participations, I count:

- **833 participants**
- **7,184 maps**, with an average of 240 maps a day...
- **136,266 likes**
- **24,740 retweets**

It begins to make a bunch of maps, and liking and retweeting people!

To explore this data more visually, I designed a dashboard via [Bokeh](https://docs.bokeh.org/en/latest/), to continue to train in new tools and to change a bit of Plotly.

> The start-up displays the data per day, aggregated for all entries.  
> You can select a specific participant via the selection bar at the bottom of the application.

[_You can click here to display it on a new page._](http://stats-30daymapchallenge.herokuapp.com/bokeh_basics)  
_Unfortunately, I have not yet managed to find a way to display, for mobile devices, the data that is available by hovering the mouse over each bar..._

<iframe width="100%" height="820"
    src="https://stats-30daymapchallenge.herokuapp.com/bokeh_basics">
</iframe>

On the technical side, I hosted it on [Heroku](https:/www.heroku.com/).  
I'm thinking about to write a tutorial on the purely pythonesque path of all this (Twint, Plotly and Bokeh side) and on how to deploy an application on Heroku. All of this is not very complex, but it may deserve to keep in mind some tricks and pitfalls in which not to fall.

Some observations on this data :

- Huge success for starting the challenge, **day 1 (Points) was the one with the most likes (12,336) and retweets (2,365).**  
There is a sort of **median plateau around 4,500 likes** on the rest of the days, with 3 peaks for days 2 (Lines), 11 (3 D) and 12 (Maps made without GIS software). It is likely that these last 2 themes are more likely to produce more generic engagement.  
**Day 25 (COVID-19) is the one with the least likes (1,982)**, probably due to 2 factors: the overflow of people for this theme and the approach of Thanksgiving in the United States (as noted by [Nicolas Lambert on his own statistics](https://neocarto.hypotheses.org/12028))
- Finishers are huge providers of content (obviously) but also of likes and retweets.  
-- They represent **9% of participants** with 2,310 maps (32% of total submissions)  
-- Their maps represent **37% of every likes and tweets**

---

_**To be continued...**_
