# Project 3: NLP, Web scraping, and classification models

### Problem Statement 

For this particular project we are provided with the following problem statement:
_What characteristics of a post on Reddit are most predictive of the overall interaction on a thread (as measured by number of comments)?_

On top of this predetermined problem statement, I will measure success by choosing the best classification model that will predict classes consistently over the class majority baseline, based on classification metrics such as cross val score, confidence intervals, and confusion matrix metrics. 

### Summary

We are tasked with acquiring our own data from the popular website Reddit.com. We have used the Python Reddit API Wrapper (PRAW) in order to gather the chosen datapoints from the /r/hot posts of reddit. This process was taken over the course of a few days so as to get a good variation of unique posts. The dataframe that we are using is saved to a .csv file for use during the cleaning and EDA phase. 

During the cleaning phase we check to make sure there are no null values in the dataframe, in this case we had none. We drop all duplicate rows based on the post title column (since reddit locks post titles once published they cannot be changed). The descriptive statistics was inspected to check for any extremes in ranges of our datapoints and any outliers were dealt with accordingly. First we create needed to create our target feature of the median amount of posts. Then, some feature engineering was conducted to get additional value from the data we had on hand. We take a look at some plots to get a grasp of the overall picture of the data. The Titles column was cleaned of extra characters, punctuation, and was lemmatized before being put through a TD-IDF vectorizer. The subreddit column was only subjected to TD-IDF vectorizer since reddit controls this datapoint and will remain the same throughout all posts. Out of all the features we now have a new working dataframe is formed to be used for our modeling.

After testing several different models the "Random Forest" classification model was chosen as it has shown the best ability to predict our target variable. Once this model was selected we went back and worked on the model parameters in order to attain the best possible score. Some changes to which features we predicted on was also tested in order to find the best fit and predictive ability of our model. Visuals were generated and used in a slide presentation to stakeholders.

The Data Dictionary of our chosen dataframe is shown below:

### Data Dictionary

|Feature|Type|Description|
|---|---|---|
|**titles**|*object*|Reddit post titles| 
|**Subreddits**|*object*|Subreddit where post is published| 
|**num_comments**|*int64*|Raw number of comments at the time the post was pulled| 
|**upvotes**|*int64*|Raw number of upvotes at the time the post was pulled| 
|**age_post**|*object*|Age of reddit post based on the time delta of when the post was published, and when the post was pulled| 
|**title_word_count**|*int64*|Engineered feature based on how many words are in the title| 
|**ups_ss**|*float64*|Engineered feature where the upvotes were standard scaled| 
|**target_y**|*int64*|Our target variable, 1 if over median number of comments, or 0 if below| 
|**age_post_sec**|*int64*|The age_post was converted to seconds for use in modeling|
|**time_sec_ss**|*float64*|Engineered feature where the age_post_sec was standard scaled| 
|**titles vectorized**|*TFIDF*|The words in the titles were cleaned of extra characters, punctuation, and lemmatized -> TF-IDF| 
|**subreddits vectorized**|*TFIDF*|The subreddits were put through TF-IDF vectorizer as is| 




### Conclusions and Findings

 After getting the best scores while using the random forest model with our chosen parameters, we extracted which features were of greatest importance to the model itself. It has shown that far and above the amount of upvotes were important in predicting the target feature. Followed by title word count and our standard scaled time in seconds. From this we can deduce that given enough time as a /r/hot post and upvotes start to increase, so too will the number of comments on the post. 

 Furthermore, we have extracted the top words and subreddits that help our model predict the class with an accuracy of 74.24%. Below is the top 15 words and top 15 subreddits that are of importance to our predictive model:

#### Words and associated importance values
Variable	Importance
0	game	0.006590
1	people	0.005591
2	art	0.005246
3	cat	0.003070
4	gun	0.002290
5	kid	0.002178
6	say	0.001936
7	need	0.001856
8	fuck	0.001750
9	update	0.001747
10	new	0.001657
11	bot	0.001618
12	wa	0.001499
13	happy	0.001489
14	use	0.001311

#### Subreddits and associated importance values
Variable	Importance
0	sub_squaredcircle	0.005523
1	sub_politicalcompassmemes	0.004910
2	sub_politics	0.004304
3	sub_publicfreakout	0.003908
4	sub_nba	0.003476
5	sub_facepalm	0.002565
6	sub_tumblr	0.002282
7	sub_baseball	0.002149
8	sub_hololive	0.002123
9	sub_formula1	0.001971
10	sub_hockey	0.001926
11	sub_gme	0.001620
12	sub_news	0.001586
13	sub_idiotsincars	0.001414
14	sub_funny	0.001407

 
 
#### My recommendation to the stakeholders:  
 The strongest association to correctly predicting the correct class in our model has been upvotes, title length, and time.
It would be easy to say that you need to create a post that will get a lot of upvotes and to allow it to sit a length of time, and you will get a fair amount of engagement by way of comments but it doesnt exactly work that way. 

 My recommendation would be as follows:
 - Try posting in the subreddits I have outlined above.
 - Try to include words that are of importance as listed above.
 - If you see your post getting lots of upvotes early on, it is usually indicative of user engagement that will also come with a fair amount of comments. 
 
#### Room for improvement:
 As in any research conducted there can always be room for improvement. If I were to be tasked with this objective again, or my contract is extended, I would like to do the following as well:

- More datapoints would be gathered per reddit post. Such as the type of post (video, picture, link, article, etc.) to see if this has any influence in user engagement.
- As well as taking the amount of time it has been on reddit I would get the posting date and time itself, so time of day, day of week, weekend/weekday can be analyzed as influential as well. 
- I would really like to also gather posts from /r/new as well. The posts that are in /r/hot are already deemed as "hot" by how many views, upvotes, comments, and shares they are gathering since time of posts. I want to see which posts that are posted to /r/new actually make it to hot, and which ones just fade into obscurity. I think this would really help differentiate the posts that will garnish more user engagement vs the ones that fizzle out and die. 
- Hire an assistant!
