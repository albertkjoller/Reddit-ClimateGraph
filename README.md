

# Human-made Climate Change discussion on Reddit

## Repository Overview
Divided into subparts following:
> - `data`: can be downloaded from [here](https://drive.google.com/drive/folders/1EajfDgDnhVdXMdhK4eUbx5wy7o5WdXKc?usp=sharing). Contains the relevant data sets - both previously created data files and data extracted from Reddit. 
> - `exploration`: contains all files that were used preliminarily to answering the research questions - i.e. `reddit_analysis.ipynb` and `extract_reddit.ipynb`.
> - `model`: can be downloaded from [here](https://drive.google.com/drive/folders/19D_XxBRs8-eabwBReffcahxWHNisFfF1?usp=sharing). Contains the pickled model that was trained and used throughout the project.
> - `preliminary_analysis.ipynb` carries out the [preliminary analysis](https://nbviewer.org/github/albertkjoller/Reddit-ClimateGraph/blob/main/preliminary_analysis.ipynb?flush_cache=true).
> - `RQ[1-3].ipynb`: answers to the research questions stated in this README-file.
> - `explainer.ipynb`: containing the answered research questions and analyses in a single [place](https://nbviewer.org/github/albertkjoller/Reddit-ClimateGraph/blob/main/explainer.ipynb?flush_cache=true). Hand-in requirement.

## Project description

#### What is the topic?
Climate Change debate on Reddit. 

The project investigates the "man-made or not"-discussion of Climate Change for Reddit submissions and comments posted in the period between the release of the 5th and the 6th edition of the IPCC assesment report (Fall 2014 - Spring 2022). Additionally, the behaviour of Reddit users - with respect to Climate Change - is investigated by analyzing the network of users engaged in the debate about Climate Change being man-made or not.

#### What is the data?

1. Reddit data
	- *Submissions and comments on Reddit related to climate change. The data was extracted using the* `PushshiftAPI` *with the queries* `climate change  climate`, `global warming  climate` and `warming planet  climate` *to get Reddit activity between the 1st of November 2014 and the 5th of April 2022.*
2. [Twitter Climate Change Sentiment dataset](https://www.kaggle.com/datasets/edqian/twitter-climate-change-sentiment-dataset)
	- *A dataset containing Tweets and their associated Climate Opinion-label, described by either being either "Anti", "Pro" or "Neutral"-ly associated to climate change. Furthermore, the label "News" occurs. Each Tweet was annotated by 3 different human beings - only Tweets for which all three annotators agreed on the label is provided.*
3. [EM-DAT Natural Disasters dataset](https://www.emdat.be/database) describes several aspect of Natural Disasters and their societal impact.

#### Research Questions:

This project aims at answering the following research questions:

1.  Does the association to Climate Change topics on Reddit relate to extreme climate events?
	- Hypothesis: *Yes, it does - there is a relation between physical events related to climate change and the activity on Reddit.*
2.  Are Reddit users more prone to comment on submissions that they agree with wrt. climate change topics?
	- Hypothesis: *Yes - the hypothesis is that the tendency of observing echo-chambers occurs within a Reddit network of the Climate Change discussion.*
3.  Do authorities within the Reddit-Climate network excite the debate particularly?
 	- Hypothesis: *Yes. We hypothesize that authority redditors defined by a high in-degree will excite the debate due to their wider outreach which potentially can elevate the discussion on the forum. Similarly, we hypothesize that authorities defined from Reddit awards received will excite the debate since awards might indicate a strong opinion to the topic, which can provide basis for the discussion to excite.*

### Approach

To address the stated research questions and hypothesis, the following assumptions were made: First of all, it is assumed that <ins>people have a static opinion to the topic "Climate Change" on social media</ins>. Secondly, the term opinion is <ins>restricted to being either Anti, Neutral or Pro</ins> Climate Change within the online Reddit discussion. This is not to be confused with sentiment, since sentiment deals with the emotional content of statements and comments related to Climate Change.

<ins>**RQ1: *Time-series investigation that includes punctual time events***</ins>

After extracting the textual and associated meta-data from Reddit, tokenization has to be done. When the text has been numerically represented, the data can be group by the date, in order to obtain time series data. Using this data, the number of Reddit posts and comments per day and the daily *Climate Change Opinion* is investigated by applying a "Climate Change Opinion"-classifier (trained on the Twitter Climate Change data) to the Reddit textual content. It will be examined whether correlation is high (and significant) to see if the opinion on Climate Change is affected by the "daily hype" about the topic. The main purpose is to get an intuitive visualization of the time series Reddit data but also a Granger Causality test is considered for determining significance.

The research question will be extended to include time series data of a real world physical or behavioral attribute - a fitted time-series of people affected by Natural Disasters - which will be analysed and compared to the textual content of Reddit submissions and comments in a similar manner as described above.

<ins>**RQ2: *Model tweet-author/replier graph and find clusters***</ins>

Apply opinion-analysis on the user-level. Model the Reddit-Climate network by building a graph with nodes corresponding to Reddit users and links corresponding to comments between Redditors. Compare the division of users based on positive/negative association to the topic with the communities found with network science algorithms for clustering.

By looking at the predicted association to the topic within the found communities, it will be determiend if users within communities in general share opinions related to climate change - thereby investigating if the concept of echo chambers occur.

We further want to analyze which words are important within each community and see if these relate to certain minor topics of the Climate Change discussion. This will be done using a TF-IDF mapping of the textual content.

<ins>**RQ3: *Access authority nodes in the graph***</ins>

Based on the modeled Reddit-Climate network, we will experiment with how to find authorities; 1) by thresholding the authority values based on the in-degree or 2) by thresholding based on the Redditor awards. Then, we will look at the opinion of the top N authorities within the network and analyze if the corresponding hub opinion (opinion of users that reply to the authority) is similar to the authority opinion. Since we want to find out if there is a trend of authority nodes' opinion affect hub nodes' opinion we will find a shared representation of the hub-nodes opinions and compare them to the authority node opinion - this shared representation will depend on the distribution of the scores (power-law or not). Based on these opinion pairs for the top N authority-hub candidates, we will apply a statistical test *determined form a preliminary analysis* to determine if there is a trend of authority node opinions being significantly different from hub nodes' opinion, when it comes to Climate Change Reddit submissions.


### Environment
The analyses were created using `python38`. Follow the instructions below to create a virtual environment.
```
conda create -n twitter_cc python=3.8
```
Activate the environment and install the dependencies.
```
conda activate twitter_cc

pip install -r requirements.txt
```
