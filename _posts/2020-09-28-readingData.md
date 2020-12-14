---
toc: true
layout: post
description: Using Panda's Read Excel Method.
categories: [markdown]
title: "How Pandas's read_excel Saved My Life"
---

![](/images/pixabay.jpg)
### Introduction
As common amongst the majority of individuals under the category of *Data Scientist by Accident*, once in a while, you come across what I call
'moments of enlightenment' which more or less upgrade your knowledge about the 'tools of the trade'. I encountered one of such moments a couple of days ago. And since I just set up
a new blog courtesy of [**fastai**](https://github.com/fastai/fastpages), I decided to relay my experience on how I entered Zen from discovering the usefulness and existence of pandas's `read_html` methods!

### Data in the Data Science Process

I make bold to say that the entire Data Science process revolves around one main resource: **DATA**. Data is an essential raw material in the manufacturing of **Data Visualization**
**Models**. While drawing on the analogy to drive home my point about data and its importance in the data Science pipeline, I'm very much aware that we don't literally manufacture
anything rather a methodical transformation of inputs takes place. Thus raw data as an input is transformed into an output format that solves one problem or needs in the society.
No doubt data is very important in the data Science process, but how do we go about getting this data into our data science work environment?

### Getting Data into Jupyter Notebook
Before encountering Data Science, all I know about data and its handling was tied to one tool: **MS EXCEL**. Excel is an excellent tool in it own right but there come a time in your data handling experience when excel won't just cut it. Most of my challenges with excel started manifesting when my data became larger. Lucky for me after narrating my
challenges on **stackoverflow** and exposing myself to public ridicule from some not-too-kind responders, I went away with the knowledge of the existence of PANDAS and JUPYTER
NOTEBOOK. Of course, with these new set of tools, I became the go-to-guy in the office for any data wrangling exercise and functions.
Majority of the data I use comes from scraping them off websites pages and transforming the data into **csv** format which I then read into the jupyter notbook for onward processing, exploration and analysis. Aside from the pandas's `read_csv` method I knew from reading the documentation I could use `read_json`, `read_table`, `read_html` e.t.c to load data unto
jupyter notbook but never attempted using them until recently when I attended an online workshop, and the facilitator used the pandas's `read_html` method.

 ### Can Life be this fun and Easy?
 My excitement knew no bounds when it occurred to me that I can improve productivity levels by just reading and loading data directly from websites pages especially when the data
 I'm interested in are housed within html's table tags. For example, to scrape this [site](https://covid19.ncdc.gov.ng/) normally, I will write the following code:
 ```python
 def get_site_html(url):
    try:
        html = requests.get(url)
    except HTTPError as e:
        return None
    try:
        bs = BeautifulSoup(html.content, 'html.parser')
        title = bs
    except AttributeError as e:
        return None
    return title
def get_data():
    site_html = get_site_html('https://covid19.ncdc.gov.ng/')

    the_table = site_html.find('table', {'id': 'custom1'})
    head_table = the_table.thead.get_text().split('\n')[2:6]
    # print(the_table)
    body_table = the_table.find_all('tr')
    table_head = body_table[0]
    # print(table_head)
    table_row = body_table[1:]
    # print(table_row)
    headings = [ht.get_text() for ht in table_head.find_all('th')]
    # print(headings)
    gey = []
    all_rows = [table_row[i].find_all('td') for i in range(len(table_row))]
    for j in all_rows:
        one_row = []
        for h in j:
            one_row.append(h.get_text().replace('\n', ''))
        gey.append(one_row)

    df = pd.DataFrame(data=gey, columns=headings)
    return df
```



 As much as I suspect the above sample code code be more concise, with pandas `read_html` method I can achieve the same purpose with just these few lines:

`import pandas as pd
data = pd.read_html('https://covid19.ncdc.gov.ng/')
data.head()`

I bet you can't get more concise than that. These few lines have saved me alot of time and boosted my productivity to the roof. Hope you learnt a thing or two from this post.
Watch out for my next post. Bye!
