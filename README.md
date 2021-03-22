# Sentiment-Analysis

Sentiment Analysis (also known as opinion mining or emotion AI) can be considered a tool within natural language processing that allows to identify, quantify, and study subjective information. It helps to detect the emotions, opinion, assessment, attitudes, and thus helps to understand the audience better. Several companies use this kinf of textual data to run semantic analysis and extract information about the view of people on thier products and services.

The goal is to extract attributes (eg. positive or negative opinions about a subject) from BigData, huge amount of data produced every day and use this attributes to classify the tweets released by the people.

For this project the information taken into account are tweets that I have extracted through the Twitter API and stored on the cloud (Google BigQuery). The dataset contains millions of results including emoticons to express emotions like happiness, sadness, anger and more. Emotions can be positive, negative as well as neutral. For example, :) in a tweet indicates that the tweet contains positive sentiment and :( indicates that the tweet contains negative sentiment.

Data:
- Tweets - generally, tweets are not as thoughtfully composed as reviews, yet, they still offer companies an additional avenue to gather feedback.
- Sentiment: “a personal positive or negative feeling.”
- Labelled data in order to train a classifier
- Limited to 140 characters of text  

To evaluate the performance of the models I used the following evaluation metrics:

- Accuracy and Kappa
- Confusion matrix with plot
- ROC Curve



## BigQuery

Twitter Api stored in a relational database in the cloud (Google BigQuery). 
