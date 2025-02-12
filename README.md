# Sentiment-Analysis on Big Data

The project is structured in 2 parts.
The first couple of weeks were dedicated to extracting data from Twitter using a bunch of different tools and Applications, the process is shown in the below section ["Required tools, Applications and Process flow"](https://github.com/davidellavalle/Social-media-and-Big-Data/blob/main/README.md#required-tools-applications-and-process-flow).  
Finally almost 22 million different tweets were extracted and a first analysis was run using GoogleCloudPlatform applications like [BigQuery](https://github.com/davidellavalle/Social-media-and-Big-Data/blob/main/README.md#bigquery) for SQL queries and DataStudio for visualizations.  

Since this data was not labelled, therefore unuseful to train an algorithm to classify the records as positive or negative, and the manual labelling process of it would have taken a long time, a second set of data was required to run my Sentiment Analysis. In the [Data](https://github.com/davidellavalle/Social-media-and-Big-Data/blob/main/README.md#data) section more information about it are provided.  
This data was first [preprocessed](https://github.com/davidellavalle/Social-media-and-Big-Data/blob/main/README.md#data-preprocessing) and cleaned to be then ready for training the deep learning model in form of a Sentiment Analysis.    

<p align="center">
  <img width="460" height="300" src="https://user-images.githubusercontent.com/73824871/113128318-f825da00-9219-11eb-9cdf-e4f2241eeea1.png">
</p>

## NLP - Natural Processing Language 

Sentiment Analysis (also known as opinion mining or emotion AI) can be considered a tool within natural language processing that allows to identify, quantify, and study subjective information. It helps to detect the emotions, opinion, assessment, attitudes, and thus helps to understand the audience better. Several companies use this kinf of textual data to run semantic analysis and extract information about the view of people on thier products and services.

The goal is to extract attributes (eg. positive or negative opinions about a subject) from BigData, huge amount of data produced every day and use this attributes to classify the tweets released by the people.


## Data

Even though I was able to retrieve 22 million Tweets from the platform Twitter, the data was unlabeled and a manual labeling process would have taken a long time before completion. To overcome this issue I found on Kaggle a database ["training.1600000.processed.noemoticon.csv"](https://www.kaggle.com/kazanova/sentiment140) with all necessary features and labels I needed to complete my project.  
The dataset contains 1,600,000 results including emoticons to express emotions like happiness, sadness, anger and more. Emotions can be positive, negative as well as neutral. For example, :) in a tweet indicates that the tweet contains positive sentiment and :( indicates that the tweet contains negative sentiment.  

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
- Do not forget to shut down the replicated pods and cluster once you are done with it or you will get charged

## BigQuery

I stored the downloaded data ina  relation database on Google Cloud and then used BigQuery, a cloud data warehouse that enables SQL like queries, to run some analysis and prepare some smaller database for representation through Data Studio.
Below some pictures referring to the creation of a dataset, table and performing queries on BigQuery.

[Create Dataset](https://cloud.google.com/bigquery/docs/datasets)  
[Create Table](https://cloud.google.com/bigquery/docs/tables)  

![image](https://user-images.githubusercontent.com/73824871/112867145-d8c46b00-90ba-11eb-91af-03c7356093a8.png)

## Data Studio

This is an other free tool offered by Google that turns data into informative, easy to read, easy to share, and fully customizable dashboards and reports. Similar to Tableau.
Here below are reported some basics visualization of the downloaded data.
Tweets Distribution by language
<p align="center">
  <img width="460" height="300" src="https://user-images.githubusercontent.com/73824871/113753166-143fe480-970e-11eb-9286-22e89953052e.png">
</p>
Map showing origin of Tweets 
<p align="center">
  <img width="460" height="300" src="https://user-images.githubusercontent.com/73824871/113753285-36d1fd80-970e-11eb-9dec-9271f37fad20.png">
</p>

## Data Preprocessing
Data preprocessing is a required first step before any machine learning machinery can be applied, because the algorithms learn from the data and the learning outcome for problem solving heavily depends on the proper data needed to solve a particular problem.  
Of all data, text is the most unstructured form and this implies a lot of cleaning.  
The following pre-processing steps help convert noise from high dimensional features to the low dimensional space to obtain as much accurate information as possible from the text:    

- Check on data structure
- Remove null data: since I am using sentiment as target (the variable I will be predicting) I cannot have any null values so these are dropped, luckily no null values were present in the database.
- Conversion of labeled classes (0 = negative, 2 = neutral, 4 = positive) to 0 and 1, drop neutral  
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
Since Lemmatization between the 2 is probably a far better method I have only used that.  

To achieve several of these results I have used the **Regular Expressions (Regex)**: a special character sequence that helps matching or finding other strings or set of strings using that sequence as a pattern.  

## Plots

Positive and negative wordlcoud - [How to create a wordcloud](https://re-thought.com/creating-wordclouds-in-python/)  
Distribution of Tweets in dataset - Positive vs Negative 


