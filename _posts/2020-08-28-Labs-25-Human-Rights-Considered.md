---
layout: post
title: Human Rights Considered - A Labs 25 Project
bigimg: /img/hrf/seattlepolice.jpg
tags: 
published: true
---

[Human Rights First](<https://www.humanrightsfirst.org/> "Human Rights First") is a nonprofit that seeks to use American international influence to improve civil liberties both domestically globally. 
Since police brutality has been a key issue this year, HRF asked us to create a website and database recording police use of force across the United States. This website should have a map of the country with incidents displayed by location.
The database should be populated from social media sites like Twitter so that the data is constantly relevant to current events and each datapoint on the map can link back to evidence posted online. There should also be some search functionality of the database. 
HRF envisions that this tool would primarily be used by journalists, activists, and researchers to quickly gather information on trends and recent developments regarding police use of force across the country. 

## Deliverables

Our primary deliverable for my team -data science- is a database of incidents of police use of force pulled from social media sites across the internet. This database should have the time, location, short description, and links to evidence for each incident. 
Once this database is created, we can create our next deliverable, the map displaying these incidents across the country. HRF had a similar project done regarding COVID-19 cases at immigration detention facilities, and [provided it to us](<http://www.detainedindanger.org/> "Detained in Danger") for inspiration. 
Our team decided that the best way to meet this deliverable would be to pull data from the Twitter API, perform NLP on the tweets to analyze the incidents, and create a database. This was recommended by the stakeholder, who had some data science experience and thought that should be our general direction. 
We applied for Twitter developer credentials immediately and began working. We created a database schema draft (below) and lists of key terms and categories to use for querying the Twitter API. 

<p align="center">
  <img src="/img/hrf/dbschema1.jpg"/>
</p>

It was shortly after this period during the second week of Labs that we encountered our first speed bump: one of the DS team members had their Twitter developer credential application denied. We waited anxiously on the results of the other two applications.

<p align="left">
  <img src="/img/hrf/twittersad.png"/>
</p>

Luckily, the rest of the DS team members received their credentials, and began exploring the Twitter API. The other team member began to explore posts pulled from the Reddit API. 

## Speed Bumps

While the team had overcome our first hurdle relatively smoothly, nobody had anticipated the major blocker we were about to encounter. Shortly after the other DS team members received their Twitter developer credentials, they realized that Twitter was no longer providing location metadata on tweets since late 2019. 

This came as an enormous shock, as the change took place relatively recently and quietly, without much media attention. Whereas Twitter had once been used in numerous studies thanks to the plethora of information provided by the API, Twitter had now stopped providing tweet location metadata for privacy reasons. Our stakeholder's vision of the product had almost been entirely built upon the assumption that geolocation data on tweets would be readily available. 
We brainstormed several ways around this issue. First, looking into other social media sites, primarily Reddit as per the wishes of the stakeholder. Reddit posts proved difficult to extract meaningful location from. We explored NLP options to try and extract location from the text of posts, but realized that Reddit posts were significantly further behind current events on average compared to Tweets. So, we moved back to Twitter as the source of our data. 

Next, we attempted to extract location from tweets based on the only locational data provided by the Twitter API, the account location. However, this proved to be an inaccurate metric for determining the location of or the location of the subject of a tweet. Additionally, many twitter accounts entered joke locations, pronouns, or even emojis into the account location field, making the data even noisy and imprecise. 
Our next approach was to attempt to use named entity recognition (NER) on tweets extracted from the Twitter API via keyword queries. This was not entirely accurate, and we began encountering problems with rate limiting from the API. The API also was not returning tweets more than about a week old. 
While we were attempting to find a solution to our problem, a team member found the [Police Brutality 2020](<https://github.com/2020PB/police-brutality/> “Police Brutality 2020”) database, a repository started in order to track incidents of excessive use of force by police in the wake of the protests against police brutality sparked by the murder of George Floyd in March of 2020. 

The Police Brutality 2020 database had several significant advantages over the tweet scraping we were currently doing. First, it was already assembled by incident, so we would not have to create a model to link multiple news articles or social media posts by incident. Secondly, each incident had an explicitly designated location and short description of the event. While the most precise location provided in the database was the city the incident took place in, it was still an enormous improvement from trying to predict tweet location using NLP. So, we pulled the PB2020 data, cleaned and processed it, and added the city’s geolocation (latitude and longitude) for each incident into a new database. We were encouraged when we saw the snazzy logo for our project designed by the frontend team. 

<p align="left">
  <img src="/img/hrf/logo.png"/>
</p>

## Natural Language Processing

We then began to investigate NLP techniques to add categories to the data. These categories would be displayed on the frontend of the website as tags, where each incident would have tags associated with it in order to help the user extract information about that incident at a quick glance. For example, if an incident included tear gas, this would become a tag in order to help categorize the type of force used by officers in that incident. These tags could also aid the search function, and possibly allow for interactive selection of tags in order to display how those elements of police use of force have been deployed over time across the United States. 

<img align="right" width="200" height="370" src="/img/hrf/snorkel.png" />

Our team was recommended by a senior data scientist to investigate a tool called [Snorkel](<https://www.snorkel.org/> “Snorkel”), which essentially applies “weakly supervised” learning to text in a new form of Named Entity Recognition. We applied snorkel NER techniques to our incident data in order to extract tags based on the type of force used in the incident and the people involved. For example, an incident might have tags for tear gas and flash grenades, used by federal agents on protestors. Using Snorkel, we created a dataset which included the PB2020 incidents, their location data, and these tags for involved parties and the type of force applied. We then created a new database for our training dataset, which also serves to populate the map visualization created with Plotly for the website. While the process of learning this completeley new tool came with it's own challenges and chores, including creating the new database schema (below), it was enjoyable to dip my feet back into the waters of DS after two months of computer science. 

<p align="center">
  <img src="/img/hrf/dbschema2.jpg"/>
</p>

## Next Steps

With this dataset and a map to display it, we have currently met the MVP for our project! 🎉 
However, the weakness of our product at this time is the lack of live updates to the map and dataset. Providing this is a challenge because it will require us to run multiple models on tweets or other social media posts in order to accurately determine their location, incident description, types of force deployed and involved parties. 

Moving forward, we need to create a cron job which will regularly update our database with incidents from PB2020 as backup data. In addition, we should create a model pipeline which will allow us to source social media posts and tweets, analyze them, and add them to the database, like the stakeholder originally intended. 

We hope to work towards those goals in the next month of Labs25!


