
Implementation Details
-----------------------

1. app.js - Server side implementation

- a HTTP server is created that listens to request on port 3000.
- a Websocket is created and the socket listens to anything coming to this server.
- only on establishing a connection with a client, the server requests for tweet stream from twitter.
- all tweets with words 'love' or 'hate' or both are subscribed for.
- JSON format data emitted to the client is as below.

  name: <Screen name of the owner of the tweet>,
  tweet: <Text of the tweet>,
  actualTweets: <Holds the total number of tweets received and NOT the sum of love tweets and hate tweets>,
  loveTweets: <Holds the number of tweets with 'love' word in it (includes tweets with 'love' AND 'hate')>,
  hateTweets: <Holds the number of tweets with 'hate' word in it (includes tweets with 'love' AND 'hate')>,
  lovePercent: <ratio of 'love' tweets to sum of 'love' and 'hate' tweets>,
  hatePercent: <ratio of 'love' tweets to sum of 'love' and 'hate' tweets>,
  tweetType: <'love' OR 'hate' OR 'both'>

- NOTE: The lovePercent and hatePercent are calculated w.r.t total sum of loveTweets and hateTweets.
	They are not calculated w.r.t actualCount as actualCount is the count of total number of 
	tweets flown in so far.

- tweetType is 'love' if there is only 'love' in the tweet text.
  tweetType is 'hate' if there is only 'hate' in the tweet text.
  tweetType is 'both' if there is are both 'love' and 'hate' in the tweet text.

- console prints the tweetType, screen_name and text of the tweet. 


2. ./public/javascripts/client.socket.io.js - Client Side implementation

- The client connects to server "http://127.0.0.1:3000/"
- loveList or $('#ss-love') refers to the list of love tweets.
- hateList or $('#ss-hate') refers to the list of hate tweets.
- msgElement or $('#ss-stats') is where the statistics w.r.t tweets are displayed

- NOTE: A tweet that contains both 'love' and 'hate' words are displayed in both columns.

- NOTE: At any point in time, 10 most recent love tweets and hate tweets are displayed. This implementation
	is done in order to prevent the list from growing infinitely and browser becoming slow.

- variables loveCount and hateCount are used to ensure that the lists are limited to size of 10

3. ./views/index.jade and ./views/layout.jade

- The implementation of front-end has been implemented in these 2 files.

4. ./package.json

- a list of dependency packages installed 

Interpretting Results
----------------------

Love Count   =  # of tweets with word 'love' in it.                   
Hate Count   =  # of tweets with word 'hate' in it.
Love Percent =  percentage of tweets with 'love' w.r.t sum of tweets with 'love' and 'hate'.
Hate Percent =  percentage of tweets with 'hate' w.r.t sum of tweets with 'love' and 'hate'.
Total Tweets =  Total number of tweets that have flown in so far.



