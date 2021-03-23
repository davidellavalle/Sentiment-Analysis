# Sentiment-Analysis

Sentiment Analysis (also known as opinion mining or emotion AI) can be considered a tool within natural language processing that allows to identify, quantify, and study subjective information. It helps to detect the emotions, opinion, assessment, attitudes, and thus helps to understand the audience better. Several companies use this kinf of textual data to run semantic analysis and extract information about the view of people on thier products and services.

The goal is to extract attributes (eg. positive or negative opinions about a subject) from BigData, huge amount of data produced every day and use this attributes to classify the tweets released by the people.

For this project the information taken into account are tweets that I have extracted through the Twitter API and stored on the cloud (Google BigQuery). The dataset contains millions of results including emoticons to express emotions like happiness, sadness, anger and more. Emotions can be positive, negative as well as neutral. For example, :) in a tweet indicates that the tweet contains positive sentiment and :( indicates that the tweet contains negative sentiment.

| Emoticons mapped to :)  | Emoticons mapped to :( |
| ------------- | ------------- |
:) | :(
:-) | :-(
: ) | : (
:D |
=)  |

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

## Data Preprocessing
Data preprocessing is a required first step before any machine learning machinery can be applied, because the algorithms learn from the data and the learning outcome for problem solving heavily depends on the proper data needed to solve a particular problem.  
Of all data, text is the most unstructured form and this implies a lot of cleaning.  
The following pre-processing steps help convert noise from high dimensional features to the low dimensional space to obtain as much accurate information as possible from the text.

Once downloaded the data needed a lot of cleaning:

- Check on data structure
- Remove null data: since I am using sentiment as target (the variable I will be predicting) I cannot have any null values so these are dropped, luckily no null values were present in the database.
- Conversion of labeled classes (0 = negative, 2 = neutral, 4 = positive) to 0 and 1, drop neutral voncert positive
- All string values to lower case
- Remove stopwords: commonly used word (such as “the”, “a”, “an”, “in”) that create a lot of noise.
- Remove punctuations
- Remove repeating characters
- Remove Urls
- Remove digits.
- Tokenizations: splitting sentences into words. Tokenization is the process of demarcating and possibly classifying sections of a string of input characters. The resulting tokens are then passed on to some other form of processing. The process can be considered a sub-task of parsing input. [Wikipedia](https://en.wikipedia.org/wiki/Lexical_analysis#Tokenization).
- STEMMING and LEMMATIZATION 
Lemmatize and stem both generate the root form of the word except stem may generate a word that doesn’t exist in the dictionary therefore lemmatization is used more widely than stemming. The core principal behind tese 2 approaches is that we need to convert all words to their base form in order to reduce the number of unique words. The problem is that many times we lose the context of a word by converting it to its base form.

