


In this Blog I'll show you how can you pull the data or tweets from twitter using Twitter API.
Follow the steps below -

 1. In order to get Twitter API access You need to sign up on the Twitter developer page - https://developer.twitter.com/   

For Your help You can refer this -
> https://developer.twitter.com/en/docs/tutorials/step-by-step-guide-to-making-your-first-request-to-the-twitter-api-v2
 
 Now your Twitter developer account is ready and Hopefully you have all the keys and token saved in your system.If Not,Don't worry Just generate them again and Save it at a safe place this time.Now it's Time to write code/script. For this we are going to use Python.
 
 2. Install Python and Tweepy (https://docs.tweepy.org/en/stable/) and Pandas (https://pandas.pydata.org/docs/).
 3.  Now we are All set to write a script using Python and Don't forget to Thank Amazing libraries available in Python which will make it really easy for us.
 

   

    import tweepy
    import pandas as pd 
    import json
    from datetime import datetime
    access_key = "nl*****lxQvSskvK**bDXjafM" 
    access_secret = "IVj6R1LOYuE7WeIYIEcbQ******EEQXO7doTH8uHfjclM992Hi" 
    consumer_key = "1577048165005594646-*********ziTqSeACjHt9HL98VN4bk"
    consumer_secret = "pZv7zOsXINtjk0M**********figbInYUZvqa4nqi7RMZ"
    
    
        # Twitter authentication
    auth = tweepy.OAuthHandler(access_key, access_secret)   
    auth.set_access_token(consumer_key, consumer_secret) 
    
        # # # Creating an API object 
    api = tweepy.API(auth)
    tweets = api.user_timeline(screen_name='@elonmusk', 
                            # 200 is the maximum allowed count
                            count=200,
                            include_rts = False,
                            # Necessary to keep full_text 
                            # otherwise only the first 140 words are extracted
                            tweet_mode = 'extended'
                            )
    
    list = []
    for tweet in tweets:
        text = tweet._json["full_text"]
    
        refined_tweet = {"user": tweet.user.screen_name,
                        'text' : text,
                        'favorite_count' : tweet.favorite_count,
                        'retweet_count' : tweet.retweet_count,
                        'created_at' : tweet.created_at}
            
        list.append(refined_tweet)
    
    df = pd.DataFrame(list)
    df.to_csv('elon_musk.csv')

> I Use Visual Studio code for my programming stuff it's just easy to use and provide lots of plugins to make it better.

Once You Hit this Script It will extract the 200 tweets and create a csv file for you automatically. 


