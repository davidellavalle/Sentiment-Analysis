# Sentiment-Analysis

Sentiment Analysis (also known as opinion mining or emotion AI) can be considered a tool within natural language processing that allows to identify, quantify, and study subjective information. It helps to detect the emotions, opinion, assessment, attitudes, and thus helps to understand the audience better. Several companies use this kinf of textual data to run semantic analysis and extract information about the view of people on thier products and services.

The goal is to extract attributes (eg. positive or negative opinions about a subject) from BigData, huge amount of data produced every day and use this attributes to classify the tweets released by the people.

## Data

For this project the information taken into account are tweets stored in training.1600000.processed.noemoticon.csv
It contains 1,600,000 tweets extracted using the twitter API. The dataset contains millions of results including emoticons to express emotions like happiness, sadness, anger and more. Emotions can be positive, negative as well as neutral. For example, :) in a tweet indicates that the tweet contains positive sentiment and :( indicates that the tweet contains negative sentiment.

The dataset contains the following 6 fields:
- **label**: the polarity of the tweet (0 = negative, 2 = neutral, 4 = positive)
- **id**: The id of the tweet
- **date**: the date of the tweet (Mon Apr 06 22:19:45 PDT 2009)
- **flag**: The query (lyx). If there is no query, then this value is NO_QUERY.
- **username**: the user that tweeted (_TheSpecialOne_)
- **text**: the text of the tweet (my whole body feels itchy and like its on fire)

| Emoticons mapped to positive | Emoticons mapped to negative|
| ------------- | ------------- |
:) | :(
:-) | :-(
: ) | : (
:D |
=)  |

- Tweets - generally, tweets are not as thoughtfully composed as reviews, yet, they still offer companies an additional avenue to gather feedback.
- Sentiment: “a personal positive or negative feeling.”
- Labelled data in order to train a classifier
- Limited to 140 characters of text  

## Required tools, Applications and Process flow

- [**Twitter developer account**](https://developer.twitter.com/en/apply-for-access): once approved I could use the Twitter API
I will need the *Consumer Key*, *Consumer Secret*, *Access Token* and *Access Token Secret*
- **Google Cloud Platform Account** with appropriate IAM permissions  

To setup the pipeline and collect Tweets from Twitter, store it on Google Cloud and run some analysis using BigQuery I used the setup flow provided at [GoogleCloudPlatform Github](https://github.com/GoogleCloudPlatform/kubernetes-bigquery-python/tree/master/pubsub#create-and-configure-a-google-cloud-platform-project)

Some of the steps are summarized here below:
- Create *Google Cloud Platform project**
- Enable all required APIs:  
**Cloud Pub/Sub API  
Kubernetes Engine API    
Cloud Dataproc API  
BigQuery API  
Cloud Storage API    
Compute Engine API  
Google Cloud Storage JSON APIs**    
- Create a **Service Account** (Adding all roles)
- Set up a **PubSub topic** in the project
- Create GKE ([Google Kubernetes Engine](https://cloud.google.com/kubernetes-engine/)) cluster and assing it to the Service Account created
![image](https://user-images.githubusercontent.com/73824871/112852417-31d8d280-90ac-11eb-9239-388a174a60e9.png)
- App configuration, this requires editing two Kubernetes .yaml config files ([bigquery-controller.yaml](https://github.com/davidellavalle/Social-media-and-Big-Data/blob/main/bigquery-controller.yaml) and [twitter-stream.yaml](https://github.com/davidellavalle/Social-media-and-Big-Data/blob/main/twitter-stream.yaml))
- Deployment of the app
- Tweets are finally available on BigQuery for analysis

- Do not forget to shit down the replicated pods and cluster once you are done with it or you will get charged

## BigQuery

Twitter Api stored in a relational database in the cloud (Google BigQuery).

[Create Dataset](https://cloud.google.com/bigquery/docs/datasets)  
[Create Table](https://cloud.google.com/bigquery/docs/tables)

![image](https://user-images.githubusercontent.com/73824871/112867145-d8c46b00-90ba-11eb-91af-03c7356093a8.png)



## Data Preprocessing
Data preprocessing is a required first step before any machine learning machinery can be applied, because the algorithms learn from the data and the learning outcome for problem solving heavily depends on the proper data needed to solve a particular problem.  
Of all data, text is the most unstructured form and this implies a lot of cleaning.  
The following pre-processing steps help convert noise from high dimensional features to the low dimensional space to obtain as much accurate information as possible from the text.

Once downloaded the data needed to be cleaned before applying the deep learning method and proceed with Sentiment Analysis:

- Check on data structure
- Remove null data: since I am using sentiment as target (the variable I will be predicting) I cannot have any null values so these are dropped, luckily no null values were present in the database.
- Conversion of labeled classes (0 = negative, 2 = neutral, 4 = positive) to 0 and 1, drop neutral voncert positive
- All string values to lower case
**Data cleaning** 
- Remove punctuations from dataset
- Remove Urls
- Remove digits.
- Remove **stopwords**: most common words in a language like “the”, “a”, “on”, “is”, “all”. These words do not carry important meaning and are usually removed from texts
- [Tokenizations](https://www.analyticsvidhya.com/blog/2019/07/how-get-started-nlp-6-unique-ways-perform-tokenization/): splitting sentences into words. This is considered the firs step for stemming and lemmatization.
There are several tools to implement it (Spacy, NLTK, MBSP), here I have used NLTK.
- STEMMING and LEMMATIZATION  
Text normalization techniques within the field of Natural language Processing (NLP) that are used to prepare text, words, and documents for further processing.
Lemmatize and stem both generate the root form of the word except stem may generate a word that doesn’t exist in the dictionary therefore lemmatization is used more widely than stemming. The core principal behind these 2 approaches is that we need to convert all words to their base form in order to reduce the number of unique words.
Stemming: process of reducing words to their word stem, base or root form. It essentially chops off letters from the end until the stem is reached (eg boater, boating, boats -> "Boat")

To achieve several of these results I have used the **Regular Expressions (Regex)**: a special character sequence that helps matching or finding other strings or set of strings using that sequence as a pattern.  

To evaluate the performance of the models I used the following evaluation metrics:

- Accuracy and Kappa
- Confusion matrix with plot
- ROC Curve

## Plots

Positive and negative wordlcoud - [instructions followed](https://re-thought.com/creating-wordclouds-in-python/)
distribution of Tweets - Positive vs Negative 

## NLP


