---
layout: post
title: Building Occupant Data Platform
date: 2018-07-07 00:00:00 -0000
tags: [buildings, software]
image: CyAura.jpg
type: project
---

In the summer of 2017 I started a software project with some friends to help occupants get the most out of the buildings they use everyday. 
The concept was to layer information over indoor environments as viewed through a mobile phone camera. 
We were creating an augmented reality (AR) interface for occupants to add information their environment to a shared database, and query it in a similarly spatial way.

The application we focused on linked these concepts of immersive computing with building management. 
Occupants would be empowered to collaborate amongst themselves and with building operators to improve their buildings in small but meaningful ways: reporting issues, requesting changes, and asking/answering FAQs.
This would be a free mobile-first web app for tenants to get answers about their building, and building management to understand their tenant’s needs and experience in real-time. Building professionals could then guide the discussion of their building online and make decisions with data informed insights. In return, tenants get support and self-efficacy when interacting with their building. Ideally the outcome would be better relationships between tenants, buildings, and management.

This concept followed from the [SPH Innovation Challenge][ETH_article] workshop I did with the ETH Student Project House (SPH). I was inspired by recent work by new technologies in SLAM (Simultaneous Localization And Mapping), machine learning, computer vision (in particular [YOLO: Real-Time Object Detection](https://pjreddie.com/darknet/yolo/)), and AR. 
We also drew inspiration from project Tango (succeeded by [ARCore](https://developers.google.com/ar/discover/)) and [ARKit](https://developer.apple.com/arkit/), however these tools at the time did not offer the features we needed on deployed mobile devices of remembering objects within a specific environment. Finally, the rising popularity of 311 apps like [SeeClickFix](https://seeclickfix.com/) made me think that something like this could work indoors and be a good first demonstration of AR for the built environment. The diagrams below give an idea of what using the service could look like for someone reporting a leaky window as an example.

<div style="text-align: center;">
{% include captioned-image.html url="obp_mockup_1.png" description="" style="height: auto; width: auto; max-height: 700px;" %}
</div>

The "building news" feature was increase engagement, both occupant-occupant and occupant-FM. Allowing direct messages from the FM team, but also bubble-up popular queries, views, and discussion topics.

The "query" feature was something exciting I wanted to explore further but remains quite vague. The idea was to allow occupants to search the indoor spaces. The example I had in mind was finding the nearest study space that is not too noisy, has good lighting, and has an empty desk. On the ETH campus during exam periods this can be quite time consuming. As well, at University of Waterloo I had the same problem, sometimes spending up to 40 minutes to find a suitable study space, other times having to relocate after 15 unproductive minutes wondering if noise would subside. For this application acquiring accurate data would be quite difficult so we didn't pursue it. People are creatures of habit, and this hinders our ability to see the best spaces of our campus, neighborhood, and city. It's kind of incredible once you start to think of all the amazing places and events you walk by everyday without knowing. However the concept of an interactive spatial search system for everyday life - that searches through AR and real world content - is really fascinating. This led to the project being named CyAura for Cybernetic + Aura.

<div style="text-align: center;">
{% include captioned-image.html url="obp_mockup_2.png" description="" style="height: auto; width: auto; max-height: 700px;" %}
</div>

The really interesting thing about how we proposed to do the object detection here is that we did it on the client side (i.e. on users phones). This had two major benefits, 1) we could save on computing power 2) we never had to actually see the user's video feed, a good design for privacy. In fact, once the model was well trained for a specific place we didn't need any communication from the user, in a way we would let them download an offline map of the building spaces.

<div style="text-align: center;">
{% include captioned-image.html url="obp_mockup_3.png" description="" style="height: auto; width: auto; max-height: 700px;" %}
</div>

Our strategy was to collect initially these hand annotated video/image sequences, but as the system matured we would detect issues in the building from the video feed alone, allowing for a simple robotic camera to easily detect even aesthetic issues that today only occupants pick up on.

<div style="text-align: center;">
{% include captioned-image.html url="obp_mockup_4.png" description="" style="height: auto; width: auto; max-height: 700px;" %}
</div>

The FAQ section would be a collaboratively curated list of common issues and questions, with the FM team having final say. 

<div style="text-align: center;">
{% include captioned-image.html url="obp_mockup_5.png" description="" style="height: auto; width: auto; max-height: 700px;" %}
</div>

This info section is maybe quite useless for most occupants, but for technicians and architecture or history buffs potential an amazing resource. Allowing someone who wants to know something about a building to query our database with images from a mobile phone could also enhance curiosity and knowledge transfer in the built environment.

<div style="text-align: center;">
{% include captioned-image.html url="obp_mockup_6.png" description="" style="height: auto; width: auto; max-height: 700px;" %}
</div>

This scenario may not be very realistic in that a service person appears to have been called directly from this reported issue. What we want to communicate is that there is a good chance that the user is not the first to notice it, and there may be existing plans in place to fix it. In which case, the response can be generated automatically. While this can be seen as FM micro management, if it's largely an automatic flow of knowledge, then the strengthening of occupant-FM relationships can perhaps justify the cost of running such a system.

<div style="text-align: center;">
{% include captioned-image.html url="obp_mockup_7.png" description="" style="height: auto; width: auto; max-height: 700px;" %}
</div>

We met with all the facility managers, building owners, and building occupants that would talk to us to see what pain points we could actually address before fully fleshing out our concept. From our interviews with residential facility managers it was apparent that they spent a significant portion of their day responding to emails, for example co-ordinating times to enter flats. The ETH Facility Management team was very open and gave us several interviews. It was understood that the existing online service and request portal they had (Meldeportal) was difficult to use and only the "tip of the ice berg" was ever reported. Facility managers each had different ideas on what data and types of data should be collected though.

We also found that building owners were the most keen on acquiring data on the occupants/tenants within their buildings. This makes sense because, for example with the ETH Immobilien (property) team, they are the ones that make the requirements for new spaces and space utilization (i.e. what % of time is space being used? and to what % capacity?) in practice is one of their key metrics. There are many sensing solutions for utilization, however user experience information is typically not available. In retrospect we should have engaged more with them as we could have offered a solution here, but decided (incorrectly) that this would be secondary. Indeed, outside of institutional settings like ETH they are the ones that profit directly from keeping strong relationships with their tenants.

The building occupants we interviewed in offices on ETH campus each had some story about a small issue, or question they had that bugged them. Most of them also expressed some interest in reporting issues or even solving them directly if they had a sense of self-efficacy about it (i.e. that it would work and they could do it). This is something we really thought we could improve, for example if an occupant had seen an answer from another occupant saying how to make something work (for example a washing machine) they would be able to get it to work themselves and not require intervention from the facility manager.

<div style="text-align: center;">
{% include captioned-image.html url="cyaura_pilot_project.jpg" description="Growing ETH Hönggerberg campus" style="height: auto; width: auto; max-height: 700px;" %}
</div>

We finally proposed a [pilot project][presentation] on the ETH Hönggerberg campus to at the ETH FM section heads meeting in September. We would develop the software and deploy it with ETH FM for free in return for their cooperation. Unfortunately they decided not to accept or proposal, concluding that they could only use software that was developed for their internal CAFM and distributed by their CAFM software vendor. Without knowing the details of their agreement with the vendor it's hard to comment on how insurmountable an obstacle this would be. Nevertheless we were very grateful to the people at ETH FM for the time they had given us to discuss the project.

In the end while everyone we spoke with was generally interested in the project, their interest was vague. No one saw what we were proposing as a real way to reduce costs, which was top of mind at ETH FM given recent budget cuts. Within this context the potential for enhancing the speed or quality of their services was not seen as greatly valuable.
During a Responsive Cities lecture Christian Gees from the City of Zürich gave a talk about how they implemented the [Züri wie neu](https://www.zueriwieneu.ch/) app for citizens to report local issues. 
I asked them how they were able to get the city works and infrastructure department to adopt the platform. 
They responded that it was ultimately a top down decision where a budget was created to provide this service on top of what they already did. There was no consideration of how the additional information would be able to streamline existing processes.

In conclusion this appears to be true in many cases of implementing a new feature within an existing organization. Even if the people within an organization understand that a new feature/service will improve their level of service and save them time and money in the long run, they foremost see having to support their legacy systems and the new one without having the time or budget for it. 
Bootstrapping a new service with funds from savings on existing services is seen as too risky, unless the problems with existing systems are excruciating. We didn't have the right target audience or concept it seems with this project, though I am still excited by the potentials for AR and ML to build collaborative relationships between people and their spaces. If you're also interested in this topic send me an email and maybe we can work together!

[presentation]: https://drive.google.com/open?id=1Q_0rFfH5bwphscDs2H3b3qXP3LrMAZ2gLJQMIweIgUE
[ETH_article]: http://www.smi.ethz.ch/content/main/en/news-und-veranstaltungen/eth-news/news/2017/03/von-den-nutzern-her-denken.html
