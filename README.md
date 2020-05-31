# What does my Instagram message data say about me?
## Exploratory data analysis using Plotly

I’ll admit it. I’ve been using Matplotlib for my data visualizations for way too long now. Clear data visualizations are crucial for any data professional to convey their message to both technical and non-technical audiences. After reading Chris Brownlie’s article ‘3.5 Years of a Relationship, in Whatsapp Messages’ [1], I was inspired to level up my own data visualization skills using the Python library Plotly and requestable Instagram data.

## Data source

For apps like Spotify, Facebook, WhatsApp, and Instagram, you can easily request and download all the personal data that they store on you. The exploratory data analysis conducted in this article uses the ‘messages.json’ files from my Instagram data request. After loading the JSON file and normalizing it, I end up with 12507 rows of messages (5755 sent messages and 6752 received messages).
Why use Plotly?

There are two advantages I have found to using Plotly over Matplotlib. Firstly, Plotly provides interactive visualizations that can be embedded into websites/blogs using HTML or a link. Secondly, Plotly has a cloud service called Chart Studio that enables you to save visualizations to a free online account (100 public visualizations with a free account).

## My findings

## 1) My Instagram message usage has soared since 2018


![alt text](https://github.com/parekhmihir98/Instagram-Message-EDA-using-Plotly/blob/master/Graphs/A.png?raw=true)


Since 2018, my Instagram message usage has soared. Intuitively, I can think of two reasons that have driven this change. Firstly, with the release of Instagram stories in the second half of 2016, I slowly began to transition away from using Snapchat as a primary messaging platform. Secondly, I interned at Facebook during the summer of 2018 and summer 2019. This can explain the spikes during these summer months. Maybe I subconsciously started to use their platforms more when I was working with them? Or because my colleagues were more active users?

[This analysis was conducted by grouping my messages by month and using the count function. The smoothed trend is a Savitzky–Golay filter(39,5)]

## 2) I respond to over 80% of my Instagram messages in under 30 minutes


![alt text](https://github.com/parekhmihir98/Instagram-Message-EDA-using-Plotly/blob/master/Graphs/B.png?raw=true)


This was the graph that surprised me the most. Although there are some messages which I take hours or even days to respond to, in the majority of cases I respond fairly fast.

[For each row of messaging data, I created a lagged variable of the ‘sender’ and the time sent. This allowed me to filter messages where the lagged sender was not me and the current sender was me. As a result, I could calculate the time between receiving a message and responding. I used a heuristic that filtered these messages to ones where the response time was less than 24 hours to prevent incorporating ‘new conversations’. A standard cumulative distribution function was calculated using numpy’s histogram and cumulative sum functions.]

## 3) 6 out of 10 of my most commonly used words in 2017 were the same in 2019


![alt text](https://github.com/parekhmihir98/Instagram-Message-EDA-using-Plotly/blob/master/Graphs/C.png?raw=true)


Although the majority of my common vocabulary hasn’t changed over the last few years, some words such as ‘cheers’ have disappeared from my common vocabulary while saying ‘yes’ has transitioned to ‘yeah’. ‘London’ also makes an entrance in 2019 given that I moved there in the summer and was trying to get my friends to visit me.

[To conduct this analysis, I used NLTK’s tweet tokenizer to split my messages into words. The tweet tokenizer seemed to do a better job than the standard word tokenizer due to the informality of my language and the use of emojis. Following this, I removed all emojis and stopwords (commonly used words like ‘the’, ‘a’, ‘an’ etc). The Counter function in the collections library was then used to find the most common words.]

## 4) I love using the laughing emoji


![alt text](https://github.com/parekhmihir98/Instagram-Message-EDA-using-Plotly/blob/master/Graphs/D.png?raw=true)


I’d attribute the use of the laughing emoji partly due to the increasing number of incoming memes (YoungKingsTV, Chabuddyg, and Gujumemes seem to be the most prevalent) that are shared through Instagram messages. The 3rd most common emoji is the brown skin tone which is used with a variety of different emojis such as 👌🏽 or 👍🏽 but seems to have grouped under one collective block.

[This analysis was conducted by joining all my message text into one string, splitting it into characters using the list function, and then using the emoji library to extract all the emojis. The Counter function in the collections library was then used to find the most common emojis.]

## 5) I’m most active in the evening and particularly between 9pm and 10pm


![alt text](https://github.com/parekhmihir98/Instagram-Message-EDA-using-Plotly/blob/master/Graphs/E.png?raw=true)


I’m not sure if this is a good trend. Understandably, my Instagram message usage at night is much higher given that I’m usually out and about during the day or doing university work. However, with the knowledge that screen time before bed is bad for sleep hygiene [2], I’m going to make a conscious effort to try and reduce my usage late at night.
[For this, I created a new ‘hour’ variable, grouped all my messaged by ‘hour’, and then applied the count function.]

Explore your data!

I hope this article has given you some inspiration to use Plotly and explore your own data. If anyone is interested, Google has some very detailed locational data that could be super cool to do some geographic visualizations and Spotify has a breakdown of the time you’ve spent listening to songs. If you want to use the code in this article, I’ve uploaded it to my Github here.

[1] Chris Brownlie, 3.5 Years of a Relationship, in Whatsapp Messages (2019), https://medium.com/data-slice/3-5-years-of-a-relationship-in-whatsapp-messages-4f4c95073c9d
[2] Lemola, Sakari, et al. “Adolescents’ electronic media use at night, sleep disturbance, and depressive symptoms in the smartphone age.” Journal of youth and adolescence 44.2 (2015): 405–418.
