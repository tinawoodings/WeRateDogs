# Introduction
WeRateDogs is a super popular twitter handle that will brighten anyone's day (even if you are a cat lover). In an effort to understand it's popularity, I analyzed information pulled from the twitter API, data produced from an image predition algorithm and twitter archive data. Some questions I was hoping to answer were:
* What is the relationship between retweet_count and favorite_count?
* What is the relationship between confidence value and whether the image was identified?
* Which breed of dogs gets most retweeted?
* At what time of day do tweets get the most favorites?

# Data
1. There are three pieces of data to gather for this project.
The WeRateDogs twitter archive is a csv file that has basic tweet data for all 5000+ of their tweets. Data includes timestamp, source, rating, dog categorization and retweet information to name a few. We downloaded this file (twitter-archive-enhanced.csv) manually.
2. This data was run through a neural network that classifies breeds of dogs and produced a data frame of image predictions. The table was posted on a website and needed to be downloaded programmatically using the Requests library. The url is: https://d17h27t6h515a5.cloudfront.net/topher/2017/August/599fd2ad_image-predictions/image-predictions.tsv
3. Some essential data was still missing including number of tweet favorites and retweets. For this we needed to utilize query the Twitter API for each tweet's JSON data using Python's Tweepy library. We then stored each tweet's entire set of JSON data in a file called tweet_json.txt file. We then read this .txt file line by line into a pandas dataframe. We chose to only pull the tweet id, retweets count and favorites count though there was more data available.

# Conclusions
On average there is 2.5 favorites for every retweet.
The image prediction was not very accurate. It only identified a dog breed 25% of the time. The confidence interval histogram was the same shape whether a dog breed was identified or not (though at a lower count).
Golden retrievers were the most retweeted dog followed by laborador retrievers.
A tweet written at midnight (UTC) gets the most favorites. The next spike is around 4pm.

# Limitations
One of the biggest issues with the image identification is that we don't have a confirmation whether or not the predicted breed actually matched the dog pictured. It's concerning that some of the predictions that were not dog breeds, but other objects had a high confidence level of above 0.9. There is a chance that the non-dog object was actually in the image (a ball, paper towel, etc) but one would have expected that the histogram of confidence be more right skewed.
Another issue is with the timezone. The data does not tell us when the favorite occurred, only when the tweet was first published. If WeRateDogs is wanting the chance for the most favorites, they would need to convert the 00:00 and 16:00 to their current timezone. It would be interesting to see the amount of favorites and retweets of all twitter handles at that time had the same trend as WeRateDogs.
