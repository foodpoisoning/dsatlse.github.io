+++
title = "SearchSmartly feature extraction"
date = 2020-06-22
[taxonomies]
tags = ["nlp", "computer-vision", "tensorflow", "recsys"]
+++

# Recommender System project for Property Tech startup

The team for this project was a tasked by a property tech startup to extract information (images, property descriptions) from a dataset of properties for the end-goal of building a recommender system for properties.

**NLP side**:  Tasked to extract information from a property's text description. 

+ Some labels (pre-existing data in their dataset) provided; Baseline performance for simple binary categories (e.g. propertyHasGarden, propertyHasPool) ~90% using Bag-Of-Words + Logistic Regression 
+ Former approach not as successful on more complex queries (e.g. NumberOfFloors, NumberOfBathrooms) & also no labels provided for some of the information. This necessitated exploring more complex language models, using preexisting implementations in Spacy for Named Entity Recognition (e.g. for Train Stations) and Parts-Of-Speech tagging to generate rules 
+ Also looked into Bi-Directional Representation Transformers (BERT) for Question-Answering

<img src = '/2019/property-wordcloud.png' width=50% height=20%>
<img src = '/2019/property-pos-tagging.png' width=50% height=20%>


**Computer Vision side**: Tasked to extract information from a property's images.

+ Wrote several scripts to extract heuristic from property images, e.g. colour, brightness
+ Looked into existing APIs for object detection (e.g. AWS Rekognition) on unlabelled images. Settled with using CVLib's implementation of YOLOV3

<img src = '/2019/property-object-detection.png' width=50% height=20%>


**Recommender System**: Build a model to target users with more relevant properties

+ Use of unsupervised methods, Principal Components Analysis + K-Means Clustering to identify implicit groups of users
+ After event data provided (user clicks and their associated properties), implemented a simple model to predict user clicks at different stages of the onboarding process using Gradient Boosted Trees (CatBoost) with \~70% ROC AUC Score for 3 events (e.g. property clicked, image clicked, )
+ Used SHAPley values, LIME, and CatBoost in-built feature importance (each future's contribution to loss reduction) to explore what features (thus preferences) important to users.

<img src = '/2019/property-feature-importance.png' width=50% height=20%>

All methods were then bundled as a simple Flask API server.

<img src = '/2019/recommender-architecture.png' width=50% height=20%>
