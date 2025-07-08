# Twitter_Sentiment_analysis_project

## Web Scrape methology:

#### 🛰️ How I Collected Data using RapidAPI

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
```

### 🗃️ How I Combined All Datasets

After collecting multiple CSV files of tweets (for example: `tweets_1_dataset.csv`, `tweets_2_dataset.csv`, ..., `tweets_n_dataset.csv`), I combined them into a single large dataset to make analysis easier and more efficient.

#### 💡 Why combine?

- Makes it easier to clean, preprocess, and analyze data in one place.
- Helps in performing consistent sentiment analysis and visualizations without repeating the same steps on separate files.

#### ⚙️ Steps to combine

1️⃣ **Upload all CSV files**

- In Google Colab, you can upload multiple files to the `/content` directory (or any folder you choose).

2️⃣ **Find and read all files**

- Use Python’s `glob` module to find all CSV files matching your file name pattern.
- Read each CSV into a pandas DataFrame.

3️⃣ **Merge all DataFrames**

- Append each DataFrame into a list.
- Concatenate them into a single DataFrame using `pd.concat()`.

4️⃣ **Save as one final file**

- Export the combined DataFrame as a single CSV file for further analysis.

---

#### 📝 Example Python code

```python
import pandas as pd
import glob

# Path where your CSV files are stored
path = '/content'  # Use your directory if local

# Find all CSV files starting with 'tweets_'
all_files = glob.glob(path + "/tweets_*.csv")

# List to hold individual DataFrames
dfs = []

for filename in all_files:
    df = pd.read_csv(filename)
    dfs.append(df)

# Combine all DataFrames into one
combined_df = pd.concat(dfs, ignore_index=True)

# Save the final combined CSV file
combined_df.to_csv('/content/Combined_Tweets_Dataset.csv', index=False)

print("✅ All CSV files successfully combined and saved as 'Combined_Tweets_Dataset.csv'")
```


```mermaid
flowchart TD
    A[Start] --> B[Create account on RapidAPI]
    B --> C[Subscribe to Twitter API on RapidAPI]
    C --> D[Get API Key & Host Header]
    D --> E[Write Python code using requests library]
    E --> F[Fetch tweets by query]
    F --> G[Store tweets as CSV files]
    G --> H[Combine datasets for analysis]
    H --> I[Perform sentiment analysis and visualization]
    I --> J[End]


