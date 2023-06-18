
## 1. Tools for text processing
<p><img style="float: right ; margin: 5px 20px 5px 10px; width: 45%" src="https://assets.datacamp.com/production/project_38/img/Moby_Dick_p510_illustration.jpg"> </p>
<p>What are the most frequent words in Herman Melville's novel, Moby Dick, and how often do they occur?</p>
<p>In this notebook, we'll scrape the novel <em>Moby Dick</em> from the website <a href="https://gutenberg.org/">Project Gutenberg</a> (which contains a large corpus of books) using the Python package <code>requests</code>. Then we'll extract words from this web data using <code>BeautifulSoup</code>. Finally, we'll dive into analyzing the distribution of words using the Natural Language ToolKit (<code>nltk</code>) and <code>Counter</code>.</p>
<p>The <em>Data Science pipeline</em> we'll build in this notebook can be used to visualize the word frequency distributions of any novel that you can find on Project Gutenberg. The natural language processing tools used here apply to much of the data that data scientists encounter as a vast proportion of the world's data is unstructured data and includes a great deal of text.</p>
<p>Let's start by loading in the three main Python packages we are going to use.</p>

```python
# Importing requests, BeautifulSoup and nltk
import requests
import nltk
from bs4 import BeautifulSoup
```

```python
import sys

def test_example():
    assert ('requests' in sys.modules and
            'bs4' in sys.modules and
            'nltk' in sys.modules and
            'collections' in sys.modules), \
    'The modules requests, BeautifulSoup, nltk, and Counter should be imported.'
```

    1/1 tests passed

## 2. Request Moby Dick
<p>To analyze Moby Dick, we need to get the contents of Moby Dick from <em>somewhere</em>. Luckily, the text is freely available online at Project Gutenberg as an HTML file: https://gutenberg.org/files/2701/2701-h/2701-h.htm .</p>
<p><strong>Note</strong> that HTML stands for Hypertext Markup Language and is the standard markup language for the web.</p>
<p>To fetch the HTML file with Moby Dick we're going to use the <code>request</code> package to make a <code>GET</code> request for the website, which means we're <em>getting</em> data from it. This is what you're doing through a browser when visiting a webpage, but now we're getting the requested page directly into Python instead. </p>


```python
# Getting the Moby Dick HTML
r = requests.get('https://s3.amazonaws.com/assets.datacamp.com/production/project_147/datasets/2701-h.htm')

# Setting the correct text encoding of the HTML page
r.encoding = 'utf-8'

# Extracting the HTML from the request object
html = r.text

# Printing the first 2000 characters in html
print(html[:200])
```

    DEBUG:urllib3.connectionpool:Starting new HTTPS connection (1): s3.amazonaws.com
    DEBUG:urllib3.connectionpool:https://s3.amazonaws.com:443 "GET /assets.datacamp.com/production/project_147/datasets/2701-h.htm HTTP/1.1" 200 1501037

    <?xml version="1.0" encoding="utf-8"?>

    <!DOCTYPE html
       PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN"
       "http://w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd" >

    <html xmlns="http://w3.org/1999/

```python
def test_r_correct():
    assert r.request.path_url == '/assets.datacamp.com/production/project_147/datasets/2701-h.htm', \
    "r should be a get request for 'https://s3.amazonaws.com/assets.datacamp.com/production/project_147/datasets/2701-h.htm'"

def test_text_read_in_correctly():
    assert len(html) == 1500996, \
    'html should contain the text of the request r.'
```

    2/2 tests passed

## 3. Get the text from the HTML
<p>This HTML is not quite what we want. However, it does <em>contain</em> what we want: the text of <em>Moby Dick</em>. What we need to do now is <em>wrangle</em> this HTML to extract the text of the novel. For this we'll use the package <code>BeautifulSoup</code>.</p>
<p>Firstly, a word on the name of the package: Beautiful Soup? In web development, the term "tag soup" refers to structurally or syntactically incorrect HTML code written for a web page. What Beautiful Soup does best is to make tag soup beautiful again and to extract information from it with ease! In fact, the main object created and queried when using this package is called <code>BeautifulSoup</code>.</p>


```python
# Creating a BeautifulSoup object from the HTML
soup = BeautifulSoup(html)

# Getting the text out of the soup
text = soup.get_text()

# Printing out text between characters 32000 and 34000
print(text[32000:34000])
```

    r which the beech tree
            extended its branches.” —Darwin’s Voyage of a Naturalist.

            “‘Stern all!’ exclaimed the mate, as upon turning his head, he saw the
            distended jaws of a large Sperm Whale close to the head of the boat,
            threatening it with instant destruction;—‘Stern all, for your
            lives!’” —Wharton the Whale Killer.

            “So be cheery, my lads, let your hearts never fail, While the bold
            harpooneer is striking the whale!” —Nantucket Song.

         “Oh, the rare old Whale, mid storm and gale
         In his ocean home will be
         A giant in might, where might is right,
         And King of the boundless sea.”
          —Whale Song.

          CHAPTER 1. Loomings.

          Call me Ishmael. Some years ago—never mind how long precisely—having
          little or no money in my purse, and nothing particular to interest me on
          shore, I thought I would sail about a little and see the watery part of
          the world. It is a way I have of driving off the spleen and regulating the
          circulation. Whenever I find myself growing grim about the mouth; whenever
          it is a damp, drizzly November in my soul; whenever I find myself
          involuntarily pausing before coffin warehouses, and bringing up the rear
          of every funeral I meet; and especially whenever my hypos get such an
          upper hand of me, that it requires a strong moral principle to prevent me
          from deliberately stepping into the street, and methodically knocking
          people’s hats off—then, I account it high time to get to sea as soon
          as I can. This is my substitute for pistol and ball. With a philosophical
          flourish Cato throws himself upon his sword; I quietly take to the ship.
          There is nothing surprising in this. If they but knew it, almost all men
          in their degree, some time or other, cherish very nearly the same feelings
          towards the ocean with me.

          Ther

```python
import bs4

def test_text_correct_type():
    assert isinstance(text, str), \
    'text should be a string.'

def test_soup_correct_type():
    assert isinstance(soup, bs4.BeautifulSoup), \
    'soup should be a BeautifulSoup object.'
```

    2/2 tests passed

## 4. Extract the words
<p>We now have the text of the novel! There is some unwanted stuff at the start and some unwanted stuff at the end. We could remove it, but this content is so much smaller in amount than the text of Moby Dick that, to a first approximation, it is okay to leave it in.</p>
<p>Now that we have the text of interest, it's time to count how many times each word appears, and for this we'll use <code>nltk</code> – the Natural Language Toolkit. We'll start by tokenizing the text, that is, remove everything that isn't a word (whitespace, punctuation, etc.) and then split the text into a list of words.</p>

```python
# Creating a tokenizer
tokenizer = nltk.tokenize.RegexpTokenizer('\w+')

# Tokenizing the text
tokens = tokenizer.tokenize(text)

# Printing out the first 8 words / tokens
print(tokens[:8])
```

    ['Moby', 'Dick', 'Or', 'the', 'Whale', 'by', 'Herman', 'Melville']

```python
import nltk

def test_correct_tokenizer():
    correct_tokenizer = nltk.tokenize.RegexpTokenizer('\w+')
    assert isinstance(tokenizer, nltk.tokenize.regexp.RegexpTokenizer), \
    'tokenizer should be created using the function nltk.tokenize.RegexpTokenizer.'

def test_correct_tokens():
    correct_tokenizer = nltk.tokenize.RegexpTokenizer('\w+')
    correct_tokens = correct_tokenizer.tokenize(text)
    assert isinstance(tokens, list) and len(tokens) > 150000 , \
    'tokens should be a list with the words in text.'
```

    2/2 tests passed

## 5. Make the words lowercase
<p>OK! We're nearly there. Note that in the above 'Or' has a capital 'O' and that in other places it may not, but both 'Or' and 'or' should be counted as the same word. For this reason, we should build a list of all words in <em>Moby Dick</em> in which all capital letters have been made lower case.</p>

```python
# A new list to hold the lowercased words
words = []

# Looping through the tokens and make them lower case
for word in tokens:
    words.append(word.lower())

# Printing out the first 8 words / tokens
print(words[:8])
```

    ['moby', 'dick', 'or', 'the', 'whale', 'by', 'herman', 'melville']

```python
correct_words = [token.lower() for token in tokens]

def test_correct_words():
    assert correct_words == words, \
    'words should contain every element in tokens, but in lower-case.'
```

    1/1 tests passed

## 6. Load in stop words
<p>It is common practice to remove words that appear a lot in the English language such as 'the', 'of' and 'a' because they're not so interesting. Such words are known as <em>stop words</em>. The package <code>nltk</code> includes a good list of stop words in English that we can use.</p>

```python
# Getting the English stop words from nltk
sw = nltk.corpus.stopwords.words('english')

# Printing out the first eight stop words
print(sw[:8])
```

    ['i', 'me', 'my', 'myself', 'we', 'our', 'ours', 'ourselves']

```python
def test_correct_sw():
    correct_sw = nltk.corpus.stopwords.words('english')
    assert correct_sw == sw, \
    'sw should contain the stop words from nltk.'
```

    1/1 tests passed

## 7. Remove stop words in Moby Dick
<p>We now want to create a new list with all <code>words</code> in Moby Dick, except those that are stop words (that is, those words listed in <code>sw</code>).</p>

```python
# A new list to hold Moby Dick with No Stop words
words_ns = []

# Appending to words_ns all words that are in words but not in sw
for word in words:
    if word not in sw:
        words_ns.append(word)

# Printing the first 5 words_ns to check that stop words are gone
print(words_ns[:5])
```

    ['moby', 'dick', 'whale', 'herman', 'melville']

```python
def test_correct_words_ns():
    correct_words_ns = []
    for word in words:
        if word not in sw:
            correct_words_ns.append(word)
    assert correct_words_ns == words_ns, \
    'words_ns should contain all words of Moby Dick but with the stop words removed.'
```

    1/1 tests passed

## 8. We have the answer
<p>Our original question was:</p>
<blockquote>
  <p>What are the most frequent words in Herman Melville's novel Moby Dick and how often do they occur?</p>
</blockquote>
<p>We are now ready to answer that! Let's answer this question using the <code>Counter</code> class we imported earlier.</p>

```python
from collections import Counter

# Initialize a Counter object from our processed list of words
count = Counter(words_ns)

# Store 10 most common words and their counts as top_ten
top_ten = count.most_common(10)

# Print the top ten words and their counts
print(top_ten)
```

    [('whale', 1246), ('one', 925), ('like', 647), ('upon', 568), ('man', 527), ('ship', 519), ('ahab', 517), ('ye', 473), ('sea', 455), ('old', 452)]

```python
def test_correct_count():
    correct_counter = Counter(words_ns)
    assert ((count == correct_counter)), \
    'Did you correctly initailize a `Counter` object with `words_ns`?'

def test_top_ten():
    top_ten_correct = count.most_common(10)
    assert ((top_ten == top_ten_correct)), \
    'Did you correctly store the top ten words and their counts in the variable `top_ten`?'
```

    2/2 tests passed

## 9. The most common word
<p>Nice! Using our variable <code>top_ten</code>, we now have an answer to our original question.</p>
<p>The natural language processing skills we used in this notebook are also applicable to much of the data that Data Scientists encounter as the vast proportion of the world's data is unstructured data and includes a great deal of text. </p>
<p>So, what word turned out to (<em>not surprisingly</em>) be the most common word in Moby Dick?</p>

```python
# What's the most common word in Moby Dick?
most_common_word = 'whale'
```

```python
def test_most_common_word():
    assert most_common_word.lower() == 'whale', \
    "That's not the most common word in Moby Dick."
```

    1/1 tests passed
