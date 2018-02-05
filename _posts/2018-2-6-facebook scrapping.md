
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

app_id = "334452787037301"
app_secret = "4955f503a3c1779a8840aa1f8931f0ee" # DO NOT SHARE WITH ANYONE!

# long term access token from stackoverflow 
https://stackoverflow.com/questions/12168452/long-lasting-fb-access-token-for-server-to-pull-fb-page-info/21927690#21927690
access_token = "EAAEwLtuQxHUBAI7ZCwvZA1UFvISah0wadM59RRtpwnUoHx4dbhofzUBHl3awZAGIQFZCRVSJ2ZBGpnZAQ6HK3HDzVntlCKMlAMZA6ZAzj0IcKlU1Xs404EZC9Lw66YLC8LmcM3i6XqFZAW88pZCf8gfQsPbhOBJiDHVY6jnAdeeqVy4zwZDZD"


# sample site my secret group - administrator previledge required
page_id = '1899709987026304'
```

### Call facebook GRAPH API for scrappong data

url request for facebook GRAPH API's endpoint to get data


```python
def getFacebookPageFeedData(page_id, access_token, num_statuses):
    
    # construct the URL string
    base = "https://graph.facebook.com/v2.12"
    node = "/1899709987026304?fields=feed&"
    parameters ="/&access_token=%s" % access_token
    url = base + node + parameters
    print(url)
    req = urllib.request.Request(url)
    response = urllib.request.urlopen(req)
    # retrieve data
    data = json.loads(response.read())
    
    return data

getFacebookPageFeedData(page_id, access_token, 5)

#https://graph.facebook.com/v2.12/1899709987026304?fields=feed&since=1517815673&limit=25&access_token=EAAEwLtuQxHUBAA0GmfcZCUcnLQJ0KbmQFvouV82tVtiCmoID6cykBEkOWzhpiU7Isi88Xo8c2adPV1ooGu5XePpWJUy7QTY6P7ZBGVfZCO0e3IP8ScBKNlUCYqZAkX7RFXymWSnESkIaSl9vQZAHZBlmfoknHGfwAxdaSmAwbPHHKVNd8VAG0dbYZAX3QE4smMHFgnqGYOZBcgZDZD
```

    https://graph.facebook.com/v2.12/1899709987026304?fields=feed&/&access_token=EAAEwLtuQxHUBAI7ZCwvZA1UFvISah0wadM59RRtpwnUoHx4dbhofzUBHl3awZAGIQFZCRVSJ2ZBGpnZAQ6HK3HDzVntlCKMlAMZA6ZAzj0IcKlU1Xs404EZC9Lw66YLC8LmcM3i6XqFZAW88pZCf8gfQsPbhOBJiDHVY6jnAdeeqVy4zwZDZD
    




    {'feed': {'data': [{'id': '1899709987026304_1900134376983865',
        'message': 'One of Fintech conference',
        'story': "정재훈 shared CB Insights's photo to the group: AI Ops.",
        'updated_time': '2018-02-05T23:33:10+0000'},
       {'id': '1899709987026304_1900134243650545',
        'message': 'Fintech trends in 2018',
        'story': "정재훈 shared CB Insights's post to the group: AI Ops.",
        'updated_time': '2018-02-05T23:32:19+0000'},
       {'id': '1899709987026304_1900133833650586',
        'message': 'digital leadership requires new skills',
        'story': "정재훈 shared World Economic Forum's post to the group: AI Ops.",
        'updated_time': '2018-02-05T23:29:54+0000'},
       {'id': '1899709987026304_1899709993692970',
        'story': '정재훈 created the group AI Ops.',
        'updated_time': '2018-02-05T00:59:15+0000'}],
      'paging': {'next': 'https://graph.facebook.com/v2.12/1899709987026304/feed?access_token=EAAEwLtuQxHUBAI7ZCwvZA1UFvISah0wadM59RRtpwnUoHx4dbhofzUBHl3awZAGIQFZCRVSJ2ZBGpnZAQ6HK3HDzVntlCKMlAMZA6ZAzj0IcKlU1Xs404EZC9Lw66YLC8LmcM3i6XqFZAW88pZCf8gfQsPbhOBJiDHVY6jnAdeeqVy4zwZDZD&limit=25&until=1517792355&__paging_token=enc_AdDqoZCQet1msTeLxFbhMUnuMSMay3uZCI7wmUck6qWVHhsrvoecTJKGDwp2BUGxuXD5rarmcdkLOXrwRqOWyNzLSsVfp8zP7dEDbPHozyK2JYYwZDZD',
       'previous': 'https://graph.facebook.com/v2.12/1899709987026304/feed?since=1517873590&access_token=EAAEwLtuQxHUBAI7ZCwvZA1UFvISah0wadM59RRtpwnUoHx4dbhofzUBHl3awZAGIQFZCRVSJ2ZBGpnZAQ6HK3HDzVntlCKMlAMZA6ZAzj0IcKlU1Xs404EZC9Lw66YLC8LmcM3i6XqFZAW88pZCf8gfQsPbhOBJiDHVY6jnAdeeqVy4zwZDZD&limit=25&__paging_token=enc_AdDRgw6NV9TQTh3taCQ7ewKTFtbZBKcTZAdIdGZAh9N6WtdZBiZC7anDgrqfJBgVMblSZBSwBlZCu5N0WQHY7e2cJ0M5istzctoyGXei4L16pankihCSgZDZD&__previous=1'}},
     'id': '1899709987026304'}


