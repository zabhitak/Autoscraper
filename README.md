# Self-learning Web Scraping with AutoScraper in Python

[AutoScraper](https://github.com/alirezamika/autoscraper) is a Smart, Automatic, Fast and Lightweight Web Scraper for Python.

Developed by [Alireza Mika](https://github.com/alirezamika), it can be downloaded at https://github.com/alirezamika/autoscraper

## Concept and problem solved

Despite the availability of tools such as [Beautiful Soup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/) Web Scraping is difficult.

A library such Beautiful Soup helps you to:

- query a Web page
- parse the result of the query into a structured data structure: a tree
- query the resulting tree with an idiomatic way

But a Web Scraper doesn't write the query for you.

The purpose of a web page is to be consumed by humans not machines:

- the format of the page can change over time, and so the query could stop to work
- writing a "web scraping query" is time-consuming

**What if a library could learn from an example and then can write the scrap query for you : it's "the reason d'être of AutoScraper"**.

## How to use **AutoScraper**

### Problem

I want to create a Web scraper for the Web site [Quora](https://www.quora) to all the questions about a subject.

### Phase 1 : the learning phase

- We train our library on a specific page: "https://www.amazon.in/s?i=aps&k=iphones"
- We give to the library an example about what we seek on the page for example "When will deep learning finally die out?"

#### Install AutoScraper from Github

```bash
pip install git+https://github.com/alirezamika/autoscraper.git
```

#### Create the file amazon_scrapper.ipynb

```python

from autoscraper import AutoScraper

# Parameters
url = "https://www.amazon.in/s?i=aps&k=iphones"
model_name = "amazon-search"

wanted_list = ["₹58,400","New Apple iPhone 11 (128GB) - Black"]

# We instanciate the AutoScraper
scraper = AutoScraper()

# We train the Scraper
# Here we can also pass html content via the html parameter instead of the url (html=html_content)
result = scraper.build(url, wanted_list)

# We display the results if any
if(result):
  print("🚀 Great a query has been inferred !! Great gob.")
  print(result)

# If no result we leave with an error code
if(result == None):
  print("Sorry no query can be inferred ... 😿")
  exit(-1)

# We save the model for future use
print(f"💿 > Save the model {model_name}")
scraper.save(model_name)

```

#### We execute the file amazon_scrapper.ipynb

```bash
python3 amazon_scrapper.ipynb
```

```plain
🚀 Great a query has been inferred !! Great gob.
['₹58,400', '₹59,900', '₹1,25,900', '₹1,29,900', '₹82,400', '₹84,900', '₹66,900', '₹69,900', '₹1,35,900', '₹1,39,900', '₹93,900', '₹1,23,900', '₹1,15,900', '₹1,19,900', '₹77,900', '₹79,900', '₹82,900', '₹1,31,900', 'New Apple iPhone 11 (128GB) - Black', 'New Apple iPhone 12 Pro Max (128GB) - Pacific Blue', 'New Apple iPhone 12 (128GB) - Blue', 'New Apple iPhone 11 (128GB) - White', 'New Apple iPhone 11 (128GB) - Green', 'New Apple iPhone 11 (128GB) - (Product) RED', 'New Apple iPhone 12 Mini (64GB) - Blue', 'New Apple iPhone 12 Pro Max (256GB) - Graphite', 'Apple iPhone 11 Pro Max (256GB) - Midnight Green', 'New Apple iPhone 12 Pro (128GB) - Pacific Blue', 'New Apple iPhone 12 (64GB) - Blue', 'New Apple iPhone 12 Mini (64GB) - White', 'New Apple iPhone 12 (128GB) - Black', 'New Apple iPhone 12 (64GB) - Black', 'Apple iPhone 11 Pro Max (256GB) - Gold']
💿 > Save the model amazon-search
```

### Phase 2 : the usage phase

A model has been saved in the preceding step that contains all the rules of scraping.

Now, we can apply our model on a page that shares the same structure with the page we have used during the training phase.

#### We create a new file called amazon_scrapper.ipynb

```python
from autoscraper import AutoScraper

# AutoScraper must be installed with
#  pip install git+https://github.com/alirezamika/autoscraper.git

question = "iphone"
time = "year"
url = f"https://www.amazon.in/s?i=aps&k=mi"
model_name = "amazon-search"

scraper = AutoScraper()
scraper.load(f"./{model_name}")
# Get all the results in the page similar to our model
results = scraper.get_result_similar(url)

# if no results
if results:
  for r in results:
    print(r)
else:
  print("No result found")

```

#### We test if the scraper works

```bash
python3 amazon_scrapper.ipynb
```

#### Result of the execution of amazon_scrapper.ipynb

```plain
['Mi 10i 5G (Atlantic Blue, 6GB RAM, 128GB Storage) - 108MP Quad Camera | Snapdragon 750G Processor | Upto 6 Months No Cost EMI',
 'Redmi Note 9 Pro (Champagne Gold, 4GB RAM, 64GB Storage) - Latest 8nm Snapdragon 720G & Alexa Hands-Free',
 'Redmi Note 9 Pro Max (Champagne Gold, 6GB RAM, 64GB Storage) - 64MP Quad Camera & Latest 8nm Snapdragon 720G & Alexa Hands...',
 'Mi Redmi 6A (Black, 2GB RAM, 16GB Storage)',
 'Redmi 9 (Sky Blue, 4GB RAM, 64GB Storage)',
 'Mi 11X Pro (Celestial Silver, 8GB RAM, 256GB Storage) | Upto INR 4000 Off on HDFC Bank Cards and EMI | Upto 12 Months No C...',
 'Redmi Note 10 (Shadow Black, 6GB RAM, 128GB Storage)',
 'Redmi 9A (Nature Green, 2GB Ram, 32GB Storage) | 2GHz Octa-core Helio G25 Processor',
 'Samsung Galaxy M31 (Ocean Blue, 6GB RAM, 128GB Storage)',
 'Samsung Galaxy M31s (Mirage Blue, 6GB RAM, 128GB Storage)']
```

### Conclusion

The scraper must be trained again if the structure of the page changes.

The real advantage of the is approach is to be very reactive when a new format is available and to propose a new model quickly to continue the data extraction.

The library is very new. It's not perfect, but a big thanks to [Alireza Mika](https://github.com/alirezamika) for this great approach.

Writen by Raphaël MANSUY CTO at https://www.elitizon.com



  
{"mode":"full","isActive":false}