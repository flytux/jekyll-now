
# Facebook scrapping

## Scrapping Facebook page and groups from python

- Create facebook app ID, secret Code and related access token from facebook developer page
- Get short-term access token from facebook's GRAPH API tool and request long-term acess token
- Identity page ID, group ID of scrapping data
- Call facebook's GRAPH endpoint to get feed data

### Import requires libraries


```python
import json
import csv
import datetime
import time
import urllib.request
import pandas as pd
import requests
```

### Create app ID and secret code from facebook developer's site and get access token

Get long-term access token from short-term access token

Identify page id of scrapping data


```python
# facebook app ID, secret code for accessing fb page
# my facebook app ID and secret code for facebook scrapping

app_id = "xxxxxxxxxxxxx"
app_secret = "xxxxxxxxxxxxxxx" # DO NOT SHARE WITH ANYONE!

# long term access token from stackoverflow 
https://stackoverflow.com/questions/12168452/long-lasting-fb-access-token-for-server-to-pull-fb-page-info/21927690#21927690
access_token = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"


# sample site my secret group - administrator previledge required
page_id = 'yyyyyyyyyyyyyyy'
```

### Call facebook GRAPH API for scrappong data

url request for facebook GRAPH API's endpoint to get data


```python
def getFacebookPageFeedData(page_id, access_token, num_statuses):
    
    # construct the URL string
    base = "https://graph.facebook.com/v2.12"
    node = "/zzzzzzzzzzzzzzzzz?fields=feed&"
    parameters ="/&access_token=%s" % access_token
    url = base + node + parameters
    print(url)
    req = urllib.request.Request(url)
    response = urllib.request.urlopen(req)
    # retrieve data
    data = json.loads(response.read())
    
    return data

getFacebookPageFeedData(page_id, access_token, 5)






    {'feed': {'data': [{'id': 'z',
        'message': 'One of Fintech conference',
        'story': "aaa shared CB Insights's photo to the group: AI Ops.",
        'updated_time': '2018-02-05T23:33:10+0000'},
       {'id': 'z',
        'message': 'Fintech trends in 2018',
        'story': "aaa shared CB Insights's post to the group: AI Ops.",
        'updated_time': '2018-02-05T23:32:19+0000'},
       {'id': 'z',
        'message': 'digital leadership requires new skills',
        'story': "aaa shared World Economic Forum's post to the group: AI Ops.",
        'updated_time': '2018-02-05T23:29:54+0000'},
       {'id': 'z',
        'story': 'aaa created the group AI Ops.',
        'updated_time': '2018-02-05T00:59:15+0000'}],
      'paging': {'next': 'https://graph.facebook.com/v2.12/z/feed?access_token=z&limit=25&until=1517792355&__paging_token=z',
       'previous': 'https://graph.facebook.com/v2.12/z/feed?since=1517873590&access_token=z&limit=25&__paging_token=z&__previous=1'}},
     'id': 'z'}


