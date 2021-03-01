---
title: ":dna: Githaviour"
layout: post
date: 2019-03-31 22:10
tag:
- Flask
- IBM Watson
- d3.js
- Semantic UI
image: /assets/images/Githaviour1.png
headerImage: false
projects: true
hidden: true # don't count this post in blog pagination
description: "Githaviour"
category: project
author: prakhargupta
externalLink: false
---

![Screenshot](/assets/images/Githaviour1.png)

Project Link - https://githavior.heroku.com
Github Link - https://github.com/Ideas-Labs/githavior

## The problem GitHavior solves

Plenty of tools (like Sourcerer, gitfa.me, and so on) that extract developers' skillsets and tech choices using their GitHub profiles. However, there was no similar tool to extract their behavioral attributes using GitHub's data. As everyone in the tech community knows, even luminaries like Linus Torvalds can be at times be "jerks" and can hinder the productivity of other project collaborators. Thus, it has become important for companies to recognize whether a candidate is a right fit for their work culture and whether they fit the behavioral expectations of other employees, but there is no way to accomplish this at scale.

GitHavior attempts to address this, and builds a behavioral profile of a provided GitHub handle, by aggregating data from GitHub's API and processing it for later use by IBM Watson's Personality Insights API. It also uses IBM's Natural Language Understanding API for analysing the overall sentiment of a developer across GitHub throughout their open source journey.

The more active a developer is on GitHub, more accurate is the analysis provided by GitHavior. By providing significant insights into candidates' potential behavior patterns during work, GitHavior can be of great aid to recruiters, especially during the behavioral analysis of candidates.

## Challenges we ran into

GitHub's API provides limited support when it comes to accessing a user's activity across all of GitHub, so we had to implement custom aggregators to gather a user's entire public activity data. The API is very repository-specific, NOT user-specific - there is extended support when one queries for a specific repository's data. This also meant that we often crossed the API rate limits and that hindered our prototyping speed.

Another challenge for us was integrating the frontend with our data processing pipeline at the backend. Since we don't have much experience with FE technologies, it was challenging for us to implement UIs and charts that visualized our data. We were able to create separate plots but we were not able to combine all of them into a single webpage.

## Screenshots Of the project

![Screenshot](/assets/images/Githaviour1.png)
![Screenshot](/assets/images/Githaviour2.png)
![Screenshot](/assets/images/Githaviour3.png)
![Screenshot](/assets/images/Githaviour4.png)
