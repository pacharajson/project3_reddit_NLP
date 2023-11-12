# Project 3: Webscraping, API, and NLP

## Problem Statement
As watch owner shop, I would like to know social voice via Reddit.com, especially, "Garmin" and "Apple Watch" how these two brands effective on the reddit users in terms of technical, device usage, and other features of smart watch related. For example, when someone mentioned about Garmin or Apple Watch. They usually compared battery life, materials, toughness of watch body, and other aspects.

Well, I would like to know that which words are highly mentioned about these watches and predict the words from title and selftext which subreddit is Garmin or Apple Watch.

## Data Collection
To collect data from reddit.com, I used webscraping method by instansitating Chrome webdriver, and then set up start date. After that, I used beautifulsoup to scrape data from website. Before I scrape of all posts, I tried one post first to make sure that it can be scraped. Then, I scraped from year 2015-01-01 til 2019 (I tried to scrape the latest posts, but there are many posts I got here.)

## Data Cleaning
After I got the data, I concated 2 csv files (garmin_df and applew_df) into 1 csv file (watch_df), then I started to clean by using drop_dubplicate. 
Plus, I used regular expression to find emoji and \n, and then, I removed these two words and keep other words to their cells. After that,I used drop_null, `[deleted]`, and 
`[removed]`. Now, data is cleaned, and then I concated between title and text columns to be title_text column because it is going to be used for countvectorize.

I divided 2 notebooks (scrape_applew_reddit and scrape_garmin_reddit), and save to csv files(garmin_df.csv and applew.csv).

## Exploratory Data Analysis
![wordcloud.png](https://github.com/pacharajson/project3_reddit_NLP/blob/main/image/wordcloud.png)
This is wordcloud I got from before vectorize, tokenize and other methods. 

![freqdist_before_vec.png](https://github.com/pacharajson/project3_reddit_NLP/blob/main/image/freqdist_before_vec.png)
This is frequenct distribution before vectorize. There are many words which may not predict which one is garmin or apple watch.

![freqdist_after_vec.png](https://github.com/pacharajson/project3_reddit_NLP/blob/main/image/freqdist_after_vec.png)
When I felt the visualized above may not be effective. Then, I used custom stopwords by define function to remove punctuation marks, articles(a,an,the), Pronoun(I, he, she, it) to remove them.

## Evaluation and Conceptual Understanding
Before I create models, I used countvertorized (CVEC) and TVEC, and then I applied 10 models (Naive Bayes, Random Forest, Adaboost, Logistic Regression, and SVC)

### Multinomials Naive Bayes
![nb_cvec.png](https://github.com/pacharajson/project3_reddit_NLP/blob/main/image/nb_cvec.png)

![nb_tvec.png](https://github.com/pacharajson/project3_reddit_NLP/blob/main/image/nb_tvec.png)

### Random Forest
![rf_cvec.png](https://github.com/pacharajson/project3_reddit_NLP/blob/main/image/rf_cvec.png)

[![rf_tvec.png](https://github.com/pacharajson/project3_reddit_NLP/blob/main/image/rf_tvec.png)

### Logistic Regression
![lr_cvec.png](https://github.com/pacharajson/project3_reddit_NLP/blob/main/image/lr_cvec.png)

![lr_tvec.png](https://github.com/pacharajson/project3_reddit_NLP/blob/main/image/lr_tvec.png)

### Adaboost
![ada_cvec.png](https://github.com/pacharajson/project3_reddit_NLP/blob/main/image/ada_cvec.png)

![ada_tvec.png](https://github.com/pacharajson/project3_reddit_NLP/blob/main/image/ada_tvec.png)

### SVC
![svc_cvec.png](https://github.com/pacharajson/project3_reddit_NLP/blob/main/image/svc_cvec.png)

![svc_tvec.png](https://github.com/pacharajson/project3_reddit_NLP/blob/main/image/svc_tvec.png)

## Conclusion
Based on the results above, the best model is `Logistic Regression` with CVEC.
The model has a train score of 0.98 and a test score of 0.96.
For confustion matrix:
- precision score of 0.98
- recall score of 0.98.
- f1 score of 0.98.
- accuracy score of 0.98.

The model has a low variance of 0.01 and low bias of 0.01. The model is good fitting.

## Recommendation
1. To be make more prediction, tokenize and lemmatize can increase significant scores(precision, recall, F1 and other scores).
2. Use Gaussian Naive Bayes, Voting, and other models to find other resuls, not only models that I created.

## Limitation
There are 2 main limitations during preprocessing and modeling data in this following:
- When preprocessing on data from the AppleWatch and Garmin subreddit, there are many misspelled, slang words, and misunderstandable words which can make data leakage.
- The context or the meaning of a sentence or phrase can depend on behaviour of reddit users
