##Comparison of open source NLP tools for sentiment analysis on [Yelp Dataset Challenge](http://www.yelp.com/dataset_challenge)

For the results check the blogpost [here](http://fotiad.is/blog/sentiment-analysis-comparison/).

### Scope 
This is a project for the [Data Mining course](http://www.cs.uoi.gr/~tsap/teaching/cs059/index-en.html) taught in the undergraduate programme of the Computer Science & Engineering department of the Univerisity of Ioannina during the fall semester 2014/2015. 
For details checkout the [handout](http://www.cs.uoi.gr/~tsap/teaching/cs059/assignments/project-en.pdf).

###Goal

The objective of this project is to apply various sentiment analysis techniques(NLP) on the restaurant reviews and assess 
whether they can correctly identify the reviews as positive or negative. 

### Yelp Dataset Challenge

Yelp has released an anonymized part of their stored data to the public. This was accompanied by 
[a challenge] (http://www.yelp.com/dataset_challenge) with various awards in order to incentivize research 
and generate insights for the use of the data. 

Here follows a brief explanation of the dataset, from their website.

```
The Challenge Dataset includes data from Phoenix, Las Vegas, Madison, Waterloo and Edinburgh:

* 42,153 businesses
* 320,002 business attributes
* 31,617 check-in sets
* 252,898 users
* 955,999 edge social graph
* 403,210 tips
* 1,125,458 reviews
```

This project is not a participation in the challenge. 

### Open source tools

Three different open source tools have been used and assessed:

* Training and testing using the dataset on a Naive Bayes classifier
* Training with generic lexicons such as WordNet and SentiWordNet
* Stanford's CoreNLP

## Usage

The code can be found in [github](). A brief explanation on how to run the code.

### Dependencies

Make sure you have the following libraries installed before running the code.

* [NLTK](http://www.nltk.org)
* [Scikit-Learn](http://scikit-learn.org/stable/install.html)
* [Numpy](http://www.numpy.org)
* [Stanford CoreNLP](http://nlp.stanford.edu/software/corenlp.shtml)
* [JSON Simple](https://code.google.com/p/json-simple/)

Also you must have installed the *stopword corpora* of NLTK.
To bring up the NLTK downloader, run the following in a python console.

```
import nltk
nltk.download()
```

### Extracting reviews

**This must be done before runing any of the classifiers below.**

You need to provide the category of the businesses and the quantity of samples for each review class (pos/neg).
The script creates two json files one for each class.

```
python extract_reviews.py 'Restaurants' 1000
```

### Naive Bayes

You need to provide the category, the number of samples for each class and the number of folds for the k-fold cross validation.
It trains one classifier for each feature extraction filter (single words, stopwords removal, bigrams, bigrams & stopwords removal) and prints the overall accuracy.

```
python run_bayes 'Restaurants' 1000 5
```

### SentiwordNet

You only need to provided the category and the number of samples. 


```
python run_sentiwordnet 'Restaurants' 1000
```

### CoreNLP

You need to add to java's classpath the path to the simple-json and corenlp jar.
First compile the ```corenlp.java``` file to create the class.

```
javac -cp ".:PATH_TO_SIMPLE_JSON/*:PATH_TO_CORENLP/*" -d . corenlp.java 
```

Then run the compiled class providing the category and number of samples.

```
java -cp ".:PATH_TO_SIMPLE_JSON/*:PATH_TO_CORENLP/*" corenlp restaurants 1000
```
