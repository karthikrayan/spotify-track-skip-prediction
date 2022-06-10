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


