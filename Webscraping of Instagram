#!/usr/bin/env python
# coding: utf-8

# In[1]:


pip install instagramy


# In[2]:


pip install instagramy --upgrade


# In[3]:


from instagramy import InstagramUser
from instagramy import InstagramPost
import pandas as pd
import numpy as np
from scipy import stats
from scipy import special
import seaborn as sns
import matplotlib.pyplot as plt
session_id = "49871308460%3ArXSb3fTaS1uPzK%3A21"
import datetime
from dateutil.parser import parse


# In[4]:


instagram = pd.read_csv('WithoutRanks.csv')
instagram.head()


# In[5]:


Handles = instagram['Instagram Handle']


# In[ ]:





# In[ ]:





# In[6]:


now = parse('December 2, 2021, 11:59pm')
now


# In[7]:


handle = InstagramUser(Handles[13], session_id)
handle.posts[11][len(handle.posts[11]) - 1]


# In[8]:


[29, 46, 797, 209, 23, 95, ]


# In[12]:


days_since_first = []
for i in np.arange(0, len(Handles)):
    player = InstagramUser(Handles[i], session_id)
    x = now - player.posts[11][len(player.posts[11]) - 1]
    days_since_first.append(x.days)


# In[ ]:


myList = days_since_first
myInt = len(player.posts)
post_freq = [x / myInt for x in myList]
post_freq


# In[ ]:


instagram['Post Frequency (Days)'] = post_freq


# In[ ]:


instagram


# In[ ]:


myList = days_since_first
myInt = 7
num_of_weeks = [x / myInt for x in myList]
num_of_weeks


# In[ ]:


Likes_Per_week = (instagram['Likes Per Post'] * len(handle.posts))/num_of_weeks


# In[ ]:


instagram.drop(['Post Frequency (Days)'], axis = 1)
instagram['Likes Per Week (I)'] = Likes_Per_week
instagram


# In[ ]:


Twitter = pd.read_csv('twitterIn.csv')
Twitter.head()


# In[ ]:


nba = pd.read_csv('sports_ref_csv.csv')
nba = nba.drop_duplicates('Player')
nba.head()


# In[ ]:


combined = instagram.merge(Twitter, on = 'Unnamed: 0')
combined.head()


# In[ ]:





# In[ ]:


combined_wo_dups = combined.drop(['Instagram Handle', 'name', 'Unnamed: 0'], axis = 1)
combined_wo_dups.head()


# In[ ]:


complete_combined = combined_wo_dups.rename(columns={'Likes Per Post': 'Likes Per Post (I)', 'Post Frequency (Days)': 'Post Frequency (Days) (I)', 'Comments Per Post': 'Comments Per Post (I)', 'Number of Followers': 'Number of Followers (I)', 'Engagement Rate': 'Engagement Rate (I)', 'replyCount': 'Reply Count (T)', 'retweetCount': 'Retweet Count (T)', 'likeCount': 'Like Count (T)', 'quoteCount': 'Quote Count (T)'}, errors="raise")
complete_combined.drop(['Likes Per Week'], axis = 1)


# In[ ]:


complete_combined.to_csv('instaplustwitter', index=False)


# In[ ]:


filt = nba['Player'].isin(complete_combined['Player Name'])
filt = nba[filt]
filt = filt.sort_values(['Player'])
filt.head(15)


# In[ ]:


alphabet = complete_combined.sort_values('Player Name')
alphabet.head()


# In[ ]:


alphabet['Age'] = filt['Age']
alphabet


# In[ ]:


big_follow = []
i = 0
while i < len(complete_combined['Number of Followers (I)']):
    if complete_combined['Number of Followers (I)'][i] > 10000000:
        big_follow.append('> 10M Instagram Followers')
    elif complete_combined['Number of Followers (I)'][i] > 5000000:
        big_follow.append('> 5M Instagram Followers')
    elif complete_combined['Number of Followers (I)'][i] > 1000000:
        big_follow.append('> 1M Instagram Followers')
    else:
        big_follow.append('< 1M Instagram Followers')
    i = i + 1
complete_combined['Followers Tier'] = big_follow


# In[ ]:


#Scatterplot of Instagram Likes Per post versus Twitter likes per tweet
sns.regplot(data = complete_combined, x = 'Likes Per Post (I)', y = 'Like Count (T)')


# In[ ]:


sns.scatterplot(data = complete_combined, x = 'Likes Per Post (I)', y = 'Like Count (T)', hue = 'Followers Tier')


# In[ ]:


#Correlation between likes per instagram post and twitter likes per tweet
Likes_corr = complete_combined['Likes Per Post (I)'].corr(complete_combined['Like Count (T)'])
Likes_corr


# In[ ]:


#Instagram Engagement = Likes + Comments
insta = []
i = 0
while i < len(complete_combined['Player Name']):
    insta.append(complete_combined['Likes Per Post (I)'][i] + complete_combined['Comments Per Post (I)'][i])
    i = i + 1


# In[ ]:


#Twitter Engagement = Reply Count + Retweet Count + Like Count + Quote Count
twee = []
i = 0
while i < len(complete_combined['Player Name']):
    twee.append(complete_combined['Reply Count (T)'][i] + complete_combined['Retweet Count (T)'][i] + complete_combined['Like Count (T)'][i] + complete_combined['Quote Count (T)'][i])
    i = i + 1


# In[ ]:


tbl = {'Player Name': complete_combined['Player Name'],
      'Instagram Engagement': insta,
       'Twitter Engagement': twee
      }
engagement = pd.DataFrame(tbl)
engagement.head()


# In[ ]:


#Scatterplot of engagement of instagram versus twitter
sns.scatterplot(data = engagement, x = 'Instagram Engagement', y = 'Twitter Engagement')


# In[ ]:


#Correlation between Instagram engagement and twitter engagement
engagement_corr = engagement['Instagram Engagement'].corr(engagement['Twitter Engagement'])
engagement_corr


# In[ ]:


engagement['Instagram zscore'] = (engagement['Instagram Engagement'] - engagement['Instagram Engagement'].mean())/engagement['Instagram Engagement'].std(ddof=0)


# In[ ]:


engagement['Twitter zscores'] = (engagement['Twitter Engagement'] - engagement['Twitter Engagement'].mean())/engagement['Twitter Engagement'].std(ddof=0)


# In[ ]:


engagement


# In[ ]:





# In[ ]:




