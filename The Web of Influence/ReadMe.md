# Problem
How can I use twitter to determine what kind of influence users have on the people that follow them?

# Goals
- Determine who influential users are

- Use the Twitter/Tweepy API to find information on user tweets

- Determine who retweets influential users the most

- Look at the retweeters tweets to determine what they tweet about the most

# Reference
Single user requests can be found in The_chainsmoker.ipynb

All user requests can be found in Web of influence.ipynb

All user tweets can be found in artists tweets folder seperated by twitter handles
#Data

The data that I am collecting is coming from Twitter. I am using the Tweepy API to pull my data from Twitter. I am collecting my data locally and converting the data into dictionaries from JSON. 

My 10 influential users are an arbitrary list of people involved in music. I chose these influetntial users from the domain knowledge that I have about who is popular in music.

Those users are: Kaskade, Calvin Harris, The Chainsmokers, Martin Garrix, Diddy, DJ Khaled, Chance the Rapper, Marshmello, Ultra Music Festival, and James Corden

# Data use
My dictionaries that I returned showed the user, tweet id, date created, retweet count and tweet text.

For each influential user, I am only able to return their last 3200 tweets. From those 3200 tweets per user, I was interested in looking at the retweeters of each influential users tweets.

One of the first hurdles that I had to overcome was that I was only able to request retweeter information off of original tweets, so I had to filter out all the retweets of influential users. After that, I was able to take the tweet ID's for each tweet to return the retweet information.

# Rate Limiting
Twitter has a rate limit when using its API. I was limited to doing 75 requests every 15 minutes. That came out to be 300 requests per hour. Each request on a tweet was counted towards my limit. So I had to figure out a way to do a request on 32000 tweets. With one set of API keys, it would take over 100 hours to get all the data that I needed. The way I overcame this was to create 10 different Twitter accounts in order to have more API keys. This made it possible to do these requests in about 10 hours. 

When doing each individual request, I had to set a timer between each pull. I set a timer to do a request every 13 seconds. What I also found was that I would get hit with errors during these requests, so I also added a try accept into my code to ignore errors.

After doing a request on each tweet id, I found that it would only retrun the last 18 retweeters of each tweet. Due to time constraints, I allowed my search to only go this far, but I intend to try and make it so I can call back on each retweeter.

# Retweeters

The way that I returned each of the retweeeters information was to return the original tweet id, retweeters id, and their location. I returned all of these to a csv that was saved locally.

Once I had all of the retweeters returned, I had to figure out a way to do a group by to aggregate all the tweets and locations to the original tweet id. I did this by aggregating the retweeters id's, and locations into a set. After this I did a get dummies to show all the retweeters that retweeted the original tweets.

From here I took the top 10 retweeters of each influential user. What I found when looking at all the retweeters is that they do more retweeting that original tweets.

# Retweeter Voice

I decided to keep all the retweeters retweets with their tweets, because they are influenced by what others say and is part of their voice. 

Using a Tf-IDF vectorizor and Truncated SVD, I found what the top words or phrases, and locations were for the retweeters of a particular influential user.

# Results

What I found is that the influential user was the most talked about thing in 9/10 of the influential users. I was also able to look at where the most tweeting was occuring about particular users. I also found that there are other influential users that they are talking about.

# Real World Application

I believe that this information can be used to determine who a user should collaborate with. I also believe that it shows who work well together at a festial or tour for maximizing what the people want. It also shows that there are places that would want that artist to perform at. I believe record labels, club owners and festival organizers would find this information the most useful.

# What's Next

I want to be able to go back and get more data about the retweeters and try to get more influential users to broaden the spectrum and get a better analysis. I also want to compare the corpus of music to the rest of the world that is on Twitter.