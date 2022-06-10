# Spotify: Sequential Track Skip Prediction 

In music streaming services, features like recommendation and shuffle
play a vital role in increasing user experience on aspects like
personalized playlists. Understanding a user’s interaction within a single
session will be beneficial in such cases to ensure better engagement.

This project gives a study about the interaction of people with music,
specifically with the skip button, and tries various statistical methods
and machine learning models to predict whether a particular user will
skip the next song given the interaction with the previous songs.

## About the Data
The challenge data consists of 160 million sessions with rich session and
track metadata. There’s also a sample of the same provided by Spotify
reflecting the same characteristics consisting of around 10000 such
sessions which are being used in this project.
The length of each session is up to 20 songs. For most sessions, a track
start and end reasons, a premium user flag, and timestamps are also
available. The dataset also includes track metadata like instrumentalness,
release year, and track acoustic features vectors.
Skip events are also given as three types,
    
    skip_1: “very briefly played”
    skip_2: “briefly played”
    skip_3: “most of the track was played”
    
    skip_2 serves as the ground truth label, which means that the song was
    only played very briefly or briefly.
    
## Feature Engineering 

 1. Handling curse of dimensionality using PCA on audio features
 2. Imposing sequential features
 
    A very important aspect in data preprocessing that has been done to this
    data is imposing features of previous historical sessional song data as
    individual features of the row. That is the last n songs played before the
    concerned session position will be added to the current song as an
    individual row. Where this n can be considered as a hyper parameter.
    For example : when n = 3. The last 3 songs of the user in the current
    session will be added to the current song.
    
## Model Training 

The model training has been in mainly two forms

1. Without sequential information: Same as predicting the skip with
just the information and interaction with the current song
2. With sequential information: Including the last ‘n’ songs
interaction along with the current song.

## Results 
![Evaluation](https://github.com/karthikrayan/spotify-track-skip-prediction/blob/main/Images/Results.png)

## Machine learning interpretation with LIME 

A brief analysis was done on how the features were used by the model
using feature importance scores and LIME ( Local Interpretable
Model-agnostic Explanations ). When looking at the interpretations,
The dataset features related to the user behavior such as
hist_user_behavior_reason_end, hist_user_behavior_reason_start for the
current song as well as the previous songs play a vital role in the
prediction process.

In this test case of the user skipping the song, we can see how the model
predicted this:
![lime1](https://github.com/karthikrayan/spotify-track-skip-prediction/blob/main/Images/Lime1.png)

For values of these historical features, we can see the weightage given
by the model, and the side/color signifies which class does the feature
provide importance.

![lime2](https://github.com/karthikrayan/spotify-track-skip-prediction/blob/main/Images/Lime2.png)

## Conclusion

    In this project the main focus was on understanding a user’s interaction
    within a single session. Hence the imposing of the sequential
    interactions was critical to compare and analyze. The results from the
    models do show that the sequential information does result in an
    improvement in the performance of the models. The Gradient Boosted
    Trees outperform the basic RNN with the help of the imposed sequential
    information. And from the inference from the model interpretations, we
    can conclude that user behavior pattern feedback signals like a reason
    for ending the previous song, which button leads to the current song, the
    click row, etc play a vital role in predicting the skip interactions.
