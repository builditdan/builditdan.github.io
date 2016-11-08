---
layout: post
title: MyPlaceIQ.com
---
I just brought the first iteration of my project live. The site is called [MyPlaceIQ](https://myplaceiq.herokuapp.com/). I wanted to learn more about RoR development by building a real application. I built MyPlaceIQ because I saw an opportunity to help realtors and consumers with a problem they face. Possible one they did not even think was a problem.

That is - we live in neighborhoods not just homes or cities or states. Many real estate search sites start with a blank search box where you type in a state, city, address, or even a neighborhood. But what if you don't know that answer yet. That is where MyPlaceIQ comes in. I wanted to start with a series of intelligent questions that would help get those answers for you. My top level questions help you find the state and then it is a matter of browsing the cities until you find one that interests you. Reviewing the provided information about each state and city. Once you have found a city you can view all of it's respective neighborhoods and start your own research.

**Development Information**

The site was developed using Ruby on Rails and a PostgreSQL database. A little bit of Javascript where needed. It is hosted on Heroku. City listings were attained from [Uscitieslist.org](https://www.uscitieslist.org/) and neighborhood listings are pulled in real-time from [Zillow's open neighborhood api](http://www.zillow.com/howto/api/APIOverview.htm). I pulled price and link information from Zillow's API as well. Other information was linked directly to their respective site. Google mapping was used throughout the site and Wikipedia was leveraged for summary information on states, cities, and neighborhoods.


**Next Steps**

The website is in it's first iteration and could be expanded with additional questions and information. My biggest limitation is the neighborhood data that is provided by Zillow. Although very powerful and rich, the data appears to be incomplete and possibly stale. I don't believe it is actively maintained but I will be researching that with them. I would appreciate feedback on this site and will be looking into some funding to purchase neighborhood information that I can load directly into the database.

Feel free to [contact me](http://builditdan.github.io/contact.html) with any questions you may have
