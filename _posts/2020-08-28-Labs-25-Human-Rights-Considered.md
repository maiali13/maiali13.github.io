---
layout: post
title: Human Rights Considered - A Labs 25 Project
bigimg: /img/hrf/seattlepolice.jpg
tags: 
published: true
---

[Human Rights First](<https://www.humanrightsfirst.org/> "Human Rights First") is a nonprofit that seeks to use American international influence to improve civil liberties both domestically and globally. 

Human Rights Considered is a project working to track incidents of police use of force on Americans for Human Rights First. This website should have a map of the country displaying localized incidents, based on a database populated with posts from social media sites like Twitter so that the data is constantly relevant to current events and each datapoint on the map can link back to evidence posted online. There should also be some search functionality of the database. HRF envisions that this tool would primarily be used by journalists, activists, and researchers in order to quickly gather information on trends and recent developments regarding police use of force across the country. 


While our initial goal was to develop a visualization that showcases instances of police use of force along with a data science model that helps classify possible instances of brutality. We quickly realized that our highest-priority data science task -in addition to creating a model to assess use of force- was to source and process the relevant data, create a database, and to host it in an accessible API.

Considering that police brutality has become an especially important issue to Americans this year, HRF asked us to create a website and database recording police use of force across the United States. 

<p align="center">
  <img src="/img/hrf/logo.png"/>
</p>

## Deliverables

Our primary deliverable for my team -data science- is a database of incidents of police use of force pulled from social media sites across the internet. This database should have the time, location, short description, and links to evidence for each incident. 

Once this database is created, we can create our next deliverable, the map displaying these incidents across the country. HRF had a similar project done regarding COVID-19 cases at immigration detention facilities, and [provided it to us](<http://www.detainedindanger.org/> "Detained in Danger") for inspiration. 

Our team decided that the best way to meet this deliverable would be to pull data from the Twitter API, perform NLP on the tweets to analyze the incidents, and create a database. This was recommended by the stakeholder, who had some data science experience and thought that should be our general direction. 
We applied for Twitter developer credentials immediately and began working. We created a database schema draft (below) and lists of key terms and categories to use for querying the Twitter API. 

It was shortly after this period during the second week of Labs that we encountered our first speed bump: one of the DS team members had their Twitter developer credential application denied. We waited anxiously on the results of the other two applications.

<p align="left">
  <img src="/img/hrf/twittersad.png"/>
</p>

Luckily, the rest of the DS team members received their credentials, and began exploring the Twitter API. The other team member began to explore posts pulled from the Reddit API. 

## Speed Bumps

While the team had overcome our first hurdle relatively smoothly, nobody had anticipated the major blocker we were about to encounter. Shortly after the other DS team members received their Twitter developer credentials, they realized that Twitter was no longer providing location metadata on tweets since late 2019. 

This came as an enormous shock, as the change took place relatively recently and quietly, without much media attention. Whereas Twitter had once been used in numerous studies thanks to the plethora of information provided by the API, Twitter had now stopped providing tweet location metadata for privacy reasons. Our stakeholder's vision of the product had almost been entirely built upon the assumption that geolocation data on tweets would be readily available. 
We brainstormed several ways around this issue. First, looking into other social media sites, primarily Reddit as per the wishes of the stakeholder. Reddit posts proved difficult to extract meaningful location data from. We explored NLP options to try and extract location from the text of posts, but realized that Reddit posts were significantly further behind current events on average compared to Tweets. So, we moved back to Twitter as the source of our data. 

Next, we attempted to extract location from tweets based on the only locational data provided by the Twitter API, the account location. However, this proved to be an inaccurate metric for determining the location of or the location of the subject of a tweet. Additionally, many twitter accounts entered joke locations, pronouns, or even emojis into the account location field, making the data even noisy and imprecise. 

Our next approach was to attempt to use named entity recognition (NER) on tweets extracted from the Twitter API via keyword queries. This was not entirely accurate, and we began encountering problems with rate limiting from the API. The API also was not returning tweets more than about a week old. 
While we were attempting to find a solution to our problem, a team member found the [Police Brutality 2020](<https://github.com/2020PB/police-brutality/> "Police Brutality 2020") database, a repository started in order to track incidents of excessive use of force by police in the wake of the protests against police brutality sparked by the murder of George Floyd in March of 2020. 

The Police Brutality 2020 database had several significant advantages over the tweet scraping we were attempting. First, it was already assembled by incident, so we would not have to create a model to link multiple news articles or social media posts by incident. Secondly, each incident had an explicitly designated location and short description of the event. While the most precise location provided in the database was the city the incident took place in, it was still an enormous improvement from trying to predict tweet location using NLP. So, we pulled the PB2020 data, cleaned and processed it, and used GeoPy to add each city’s geolocation metadata (latitude and longitude) for all incidents. 


## Natural Language Processing

We then began to eagerly investigate NLP techniques which would allow us to efficiently to add categories to the incident data. These categories would be displayed on the frontend of the website as tags, where each incident would have tags associated with it in order to help the user extract information about that incident at a quick glance. For example, if an incident included tear gas, this would become a tag in order to help categorize the type of force used by officers in that incident. These tags could also aid the search function, and possibly allow for interactive selection of tags in order to display how those elements of police use of force have been deployed over time across the United States. 

<img align="right" width="200" height="370" src="/img/hrf/snorkel.png" />

Our team was recommended by a senior data scientist to investigate a tool called [Snorkel](<https://www.snorkel.org/> "Snorkel"), which essentially applies “weakly supervised” learning to text in a new form of Named Entity Recognition. We applied snorkel NER techniques to our incident data in order to extract tags based on the type of force used in the incident and the people involved. For example, an incident might have tags for tear gas and flash grenades, used by federal agents on protestors. Using Snorkel, we created a dataset which included the PB2020 incidents, their location data, and these tags for involved parties and the type of force applied. We then created a new database for our training dataset, which also serves to temporarily populate the map visualization for the website. While the process of learning this completely new tool was challenging, it was enjoyable to metaphorically dip my feet back into the waters of DS after over two months of computer science coursework. 


## Evolution of the Database

First, when we were still trying to source incidents from Twitter, our schema reflected the complicated structure of relationality between tweet metadata. However, when we deiced to start our project with purely data from PB2020, the schema evolved into a much simpler set of tables. When creating this database in PostgreSQL, the tables were heavy and slow to create and query. Eventually, in order to optimize speed and more efficiently and accurately represent the relationalities in the data, we concluded with the final schema, seen in orange below. 

<p align="center">
  <img src="/img/hrf/dbschema1.jpg"/>
  <img src="/img/hrf/dbschema2.jpg"/>
  <img src="/img/hrf/dbschemafinal.png"/>
</p>

This schema represents our current relational database, deployed with FastAPI hosted with AWS ElasticBeanstalk . New incidents and additional evidence for existing incidents from Police Brutality 2020 will be added to the database via an AWS Lambda cron job, triggered by AWS CloudWatch at a weekly interval. 

<p align="center">
  <img src="/img/hrf/ds_structure.png"/>
</p>

## Next Steps

With this dataset and a map to display it, we have currently met the MVP for our project! 🎉 
However, the weakness of our product at this time is the lack of live updates to the map and dataset. Providing this is a challenge because it will require us to run multiple models on tweets or other social media posts in order to accurately determine their location, incident description, types of force deployed and involved parties. 

In the more immediate future, we need to put the finishing touches the cron job which will regularly update our database with incidents from PB2020. We have already created the AWS Lambda function handler for this purpose and simply need to deploy it and finish setting up the AWS CloudWatch trigger. 

An additional goal for future labs teams working on this project might be to use Snorkel to attempt to predict a more accurate location than just the city from an incident's description and evidence. For example, using Snorkel, future labs data scientists might be able to assess that an incident took place in front of the Los Angeles city hall, instead of simply occurring in Los Angeles. This will allow better visual representation of the data and help determine which precincts are committing violent offenses most frequently. 



The GitHub repository for Human Rights Considered data science team can be found [here](<https://github.com/Lambda-School-Labs/Labs25-Human_Rights_First-TeamC-DS> "Human Rights Considered DS Repo").
