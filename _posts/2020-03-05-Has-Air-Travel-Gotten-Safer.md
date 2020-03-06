---
layout: post
title: Has Air Travel Become Safer?
bigimg: img/plane/planewing.jpg
tags:
  - Travel
  - Safety
published: true
---




I have a massive fear of flying.

I'm not alone: up to 30% of the population have the same fears, with between 2-10% of people possessing a phobia of flying. Many people overestimate the likelihood of catastrophic events, and/or are misinformed about the dangers of air travel, which contribute to anxiety about flight or even the development of aviophobia.<sup name="a1">[1](#f1)</sup>

But whether you have family all over the world or demanding career, sometimes you just can't avoid air travel. In our busy, interconnected world, flying is practically a necessity. Despite my best efforts, I seem to manage to take at least one intercontinental round trip and several domestic flights every year. But still, every time I board a plane, I sweat and fidget until well after reaching cruising altitude. Every minor turbulent bump gives me flashes of panic. Landing makes my knees weak. And to compound all this, my own fear has led me to have a morbid fascination with plane crashes.

I decided to look at data on airplane crashes to try and better understand the reality of flight. How have trends in these accidents changed over time? Which aircraft carriers or planes are the most dangerous? Hopefully, this investigation will help me banish my anxiety once and for all.

Using data from [planecrashinfo.com](<http://www.planecrashinfo.com/database.htm> "planecrashinfo.com"), we can investigate plane crashes over the last 101 years, from 1908 to 2019. This dataset includes all fatal civil and commercial aviation accidents, and all fatal, non-conflict military aviation accidents.

First, I wanted to get an understanding of the accidents by industry type. Do commercial flights crash more often than other types of flights?

<p align="center">
  <img src="https://github.com/maiali13/maiali13.github.io/blob/master/img/plane/pie.png">
</p>

Commercial flights, which are primarily passenger aircraft, make up 76% of total crashes. Delivery flights, or flights exclusively for mail and cargo, made up only about 2% of crashes. All recreational and private flights made up only 6% of total crashes. Military aircraft make up 16% of total crashes. Not much to dissuade my fears, here.


<p align="center">
  <img src="https://github.com/maiali13/maiali13.github.io/blob/master/img/plane/bar.png">
</p>


Further exploration of this dataset reveals that we can break down the summaries of crash incidents to see what is causing them. Of all crashes throughout history, weather and visibility were the leading cause of aircraft crashes, followed by mechanical failure. Fire in the cabin led to 18% of crashes, while violence including hijacking or shooting down of aircraft resulted in less than 2% of all crashes. Pure pilot error resulted in 5%. However, it is worth noting that studies in aviation have led to the realization that a large percentage of crashes, while not directly caused by human error factors, were escalated from mitigatable issues into crashes by human error.<sup name="a2">[2](#f2)</sup>

<img align="right" width="500" height="310" src="https://github.com/maiali13/maiali13.github.io/blob/master/img/plane/EA401.jpg">

An example of this is CFIT (controlled flight into terrain), which is type of crash in which a plane crashes into landscape or buildings. CFIT was exceedingly common in before modern aviation innovations like GPS, radar, and collision warning systems, and has caused over 9,000 fatalities since the beginning of flight. CFIT can be caused by low visibility, but it is also commonly caused by human error factors, like distracted crew.<sup name="a3">[3](#f3)</sup>  In 1972, Eastern Air Lines 401 crashed into the Florida Everglades, killing 99 people, due to crew fixation on a burned-out lightbulb in the instrumentation of the nose gear.



When we look at crash distribution throughout the history of aviation, we can get a bigger picture. Rises in crash numbers correspond to increases in the frequency and number of flights as technology improves, and economic and political factors change with time. Increases in crashes after 1945, for example, correspond to the boom in commercial aviation as WWII ended and newly-developed four-engine aircraft become available for non-military use.

<p align="center">
  <img src="https://github.com/maiali13/maiali13.github.io/blob/master/img/plane/hist.png">
</p>


Several important technological and regulatory innovations in the industry are credited with increasing safety, primarily the implementation of navigational and flights aids such as radio positioning and GPS, and technological and materials improvements allowing for better fire safety and other technical improvements to aircraft. Crew Resource Management (CRM), is a human-error and threat-response risk-mitigation system that was first theorized in the 1970s as a result of analysis of crashes like Eastern Air Lines 401. Unfortunately, CRM was not widely adopted until the early 1990s, largely due to the low buy-in of flight crews and crew adherence to traditionalist ideas of cockpit hierarchy. Studies in the 1980s showed that up to 70% of all aircraft accidents were escalated or caused by human factors, rather than pure mechanical failure.\[2\] The enforced regulation of CRM training and industry-wide buy-into CRM techniques due to the heroic actions of the United 232 crew are widely credited with the decline in aircraft crashes in the 1990s. <sup name="a4">[4](#f4)</sup>

Despite all these changes, a glimpse at just this graph and the total number of annual crashes makes it appear as though planes are still as dangerous now as they were in the 1940s. My intuition tells me that this can't quite be right. These ratios might be due to the ever-increasing volume of commercial flights. Unfortunately, the Plane Crash dataset doesn't include any information about air traffic over time to make better inferences about crash probabilities.

To get a more detailed picture of plane crash probabilities, We can use data from [the World Bank](<https://data.worldbank.org/indicator/IS.AIR.DPRT?most_recent_year_desc=false> "World Bank") on total number of flights from 1970-2018.

Now using this data, we can see directly how the number of flights has increased and the number of crashes decreased in the modern era of aviation (1970-present).

\[double y axis graph\]

\[double y axis graph\]

![][4]![][5]

As the data illustrates, the total number of crashes is slowly decreasing, while the total number of worldwide flights is increasing.

We can get a closer look at technological and regulatory improvements to aviation safety by comparing important dates with crash rate over time.

<p align="center">
  <img src="https://github.com/maiali13/maiali13.github.io/blob/master/img/plane/line.png">
</p>

FMS, or flight management systems, are essentially what a layman would consider to be autopilot technology. A plane's FMS may calculate everything from elevation, flightpath, engine power levels, wing flap orientations, etc. FMS systems in 2020 are even more complex, calculating precise instrumentation levels, and location data for the entirety of the flight trip.<sup name="a5">[5](#f5)</sup>

Traffic Alert and Collision Avoidance Systems (TACS II+) use radio signaling to give pilots warnings about objects in their flightpath. This technology helps avoid midair collision and help pilots coordinate with air traffic control for safe takeoff, landing, and taxiing at airports.

Regulations such as 14 CFR 117 placed a limit on the number of total and consecutive hours that a pilot can fly in certain periods of time, such as within 48hrs or a week. These regulations also mandated certain minimum periods of rest be provided to pilots and crew between flights.<sup name="a6">[6](#f6)</sup>

**Conclusion**


No endeavor is ever 100% safe. But flight has never been safer than it is today. In fact, such safety rates are a pinnacle of human innovation and achievement.

**Sources:**



<b name="f1">1 - </b> Ponton, L. \"Understanding the Fear of Flying.\" *Psych Central*. https://psychcentral.com/lib/understanding-the-fear-of-flying/ (retrieved March, 2020). [↩](#a1)

<b name="f2">2 - </b>  Wiener, Kanki, and Helmreich. *Cockpit Resource Management*. San Diego, CA: Acad. Press, 1995.[↩](#a2)

<b name="f3">3 - </b>  Kelly, and Efthymiou. "An Analysis of Human Factors in Fifty Controlled Flight into Terrain Aviation Accidents from 2007 to 2017." *Journal of Safety Research* (March 2019): 155--65. https://doi.org/10.1016/j.jsr.2019.03.009. [↩](#a3)

<b name="f4">4 - </b> Helmreich, Merritt, and Wilhelm. 1999. "The Evolution of Crew Resource Management Training in Commercial Aviation." *The International Journal of Aviation Psychology* 9 (1): 19--32. doi:10.1207/s15327108ijap0901\_2. [↩](#a4)

<b name="f5">5 - </b> Miller, et al. (2009). \"Contribution of Flight Systems to Performance-Based Navigation\". *AERO Magazine* (34, Qtr. 2).[↩](#a5)

<b name="f6">6 - </b> Rudari, Lukas, Johnson, Geske, and Sperlak. "Pilot Perceptions on Impact of Crew Rest Regulations on Safety and Fatigue." *International Journal of Aviation, Aeronautics, and Aerospace*, February 19, 2016. https://doi.org/10.15394/ijaaa.2016.1096. [↩](#a6)

  [1]: img/plane/pie.png
  [2]: img/plane/bar.png
  [3]: media/image3.png {width="6.489583333333333in" height="1.53125in"}
  [4]: media/image4.png {width="6.489583333333333in" height="3.3020833333333335in"}
  [5]: media/image5.png {width="6.489583333333333in" height="3.4166666666666665in"}
  [6]: media/image6.png {width="6.489583333333333in" height="2.1458333333333335in"}
