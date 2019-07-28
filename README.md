# Natural Language Processing and Classification of r/AskHistory and r/History
---

By: Blake Franey

The narrative presented in this project is fictitious designed to give a more interesting context or a potential application.

### Navigating the repo
1. The [data](./data) folder contains the raw, scraped data as well as the .csv files from the dataframes.  reddit_df.csv is the final dataframe that is used for the actual modeling.
2. The [notebooks](./notebooks) folder contains all of the notebooks in my workflow.  They are numbered in the order they should be followed.  More explicit titles/explanations are included in each of the notebooks.


## Problem Statement
---
AskHistorians is a large community for people to ask real historians questions who respond with detailed, well-sourced, answers.  In order to improve historical literacy AskHistorians would like to expand and develop a history learning platform that is widely accessible.  Using data scraped from the posts of r/AskHistorians and r/History, we would like to see if we can distinguish between the more academic and discussion based History subreddit and AskHistorians where anyone can post a question about a topic in history they are curious about.  Specifically we want to compare the difference in the language used and popular topics to help drive content on the new platform.

## Executive Summary
--- 

Khan Academy's reputation for robust and innovative approaches to self teaching is impossible to deny. It's mission to offer free world-class to anyone is an impressive goal and one that the moderators at [Ask Historians](https://www.reddit.com/r/AskHistorians/) share. 

As passionate History nerds that have devoted much of our life to study and research, we at Ask Historians are worried about the lack of historical literacy in today's world; from simple misconceptions to denial of significant events such as the Holocaust or Armenian genoice. To combat this issue, we would like to propose a partnership with Khan Academy to develop different tools and media that can be accessible and interesting to the general public.  Khan Academy's current history offerings are undoubtedly high quality and we would like to expand that and appeal to non-students.  

This can be tackled in a multitude of ways; our initial instinct was to build upon Ask Historians already popular [podcast](https://www.reddit.com/r/AskHistorians/wiki/podcast) series, develop a complementary app, and positive engagement in social media.  The backbone of this project would be data driven; statistical and machine learning models- such as text and sentiment analysis- will be used to give us insight on where our efforts are best placed.  Trending topics, primary topics of interest, as well as determining what events suffer most from lack of knowledge. AskHistorians has a diverse group of vetted contributors and a significant amount of posts to gather initial data from to help set the direction (which will be explored in this proposal). 

Time is running out to change this downward trend in historical literacy. With the advent of social media and the proliferation of bad-faith websites presenting themselves as legitimate academic voices is a problem that must be solved with continually evolving methods in order to be effective. Time is running out to change this downward trend in historical literacy. With the advent of social media and the proliferation of bad-faith websites presenting themselves as legitimate academic voices is a problem that must be solved with continually evolving methods in order to be effective.       
       
## Technologies and Packages Required
---
 - Python 3.x
 - Requests 2.22.0
 - Jupyter/ iPython 7.5
 - NumPy 1.16.4
 - Pandas 0.24.2
 - SciKit-Learn 0.21.2
 - nltk 3.4.3
 - Matplotlib 3.1.0
 - Seaborn - 0.9.0
 
 ## Data Collection
 ---
 [01 Web Scraper](./notebooks/01_Web_Scraper.ipynb)
 
 Data was collected using the ```requests``` library and calling [Reddit's API](https://www.reddit.com/dev/api/).
 
 ## Overview of Methods
 ---
 I will mostly follow the work flow designated in the notebooks folder.
 
 In order to scrape the data, I connected to Reddit's API and scraped about 1000 posts from each subreddit.  The main focus for this project was the post title and the selftext (text in the post itself).  Some posts had selftext and others didn't so I combined title and selftext into one column and performed preprocessing on that.  This involved handling null values, lemmatizing, removing stopwords, and combining into a single data frame.
 
 I applied a count vectorizer then fit it with a logistic regression.  I also attempted to apply a Vader sentiment analysis however this did not improve results.
 
 I also wanted to explore and compare a logistic regression using a term frequency-inverse document frequency vectorizer.  However this did not give improved results.
 
 Finally, using a pipeline, I fit a Multinomial Naive Bayes model for both a count vectorized and tf-idf version of the data.  This also didn't give better results so ultimately the logistic regression with the count vectorizer performed the best. 