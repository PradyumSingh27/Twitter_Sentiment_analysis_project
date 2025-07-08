# Twitter_Sentiment_analysis_project

## 🛰️ How I Collected Data using RapidAPI

For this project, I collected tweets directly from Twitter using the [Twitter API](https://rapidapi.com/collection/twitter-apis) provided on RapidAPI.

### 🔗 Why RapidAPI?

- RapidAPI provides an easy interface to access Twitter data without needing to create your own Twitter developer application.
- It allows you to use pre-built endpoints (such as searching tweets, getting user details, etc.) with a single API key.

### ⚙️ How it works

1️⃣ **Sign up for RapidAPI**

- Create a free account on [RapidAPI](https://rapidapi.com).

2️⃣ **Subscribe to a Twitter API**

- Search for a Twitter API, such as "Twitter API v2" or "Twitter API 45".
- Subscribe to a free or paid plan depending on your requirements.

3️⃣ **Get your API key**

- After subscribing, get your `X-RapidAPI-Key` and `X-RapidAPI-Host` headers.

4️⃣ **Write code to fetch tweets**

Example Python code to fetch tweets using RapidAPI:

```python
import requests

url = "https://twitter-api45.p.rapidapi.com/search.php"

querystring = {"query":"Indian election", "count":"100"}

headers = {
    "X-RapidAPI-Key": "YOUR_RAPIDAPI_KEY_HERE",
    "X-RapidAPI-Host": "twitter-api45.p.rapidapi.com"
}

response = requests.get(url, headers=headers, params=querystring)
data = response.json()

for tweet in data['statuses']:
    print(tweet['text'])
