
## 1. The brief
<p>Imagine working for a digital marketing agency, and the agency is approached by a massive online retailer of furniture. They want to test our skills at creating large campaigns for all of their website. We are tasked with creating a prototype set of keywords for search campaigns for their sofas section. The client says that they want us to generate keywords for the following products: </p>
<ul>
<li>sofas</li>
<li>convertible sofas</li>
<li>love seats</li>
<li>recliners</li>
<li>sofa beds</li>
</ul>
<p><strong>The brief</strong>: The client is generally a low-cost retailer, offering many promotions and discounts. We will need to focus on such keywords. We will also need to move away from luxury keywords and topics, as we are targeting price-sensitive customers. Because we are going to be tight on budget, it would be good to focus on a tightly targeted set of keywords and make sure they are all set to exact and phrase match.</p>
<p>Based on the brief above we will first need to generate a list of words, that together with the products given above would make for good keywords. Here are some examples:</p>
<ul>
<li>Products: sofas, recliners</li>
<li>Words: buy, prices</li>
</ul>
<p>The resulting keywords: 'buy sofas', 'sofas buy', 'buy recliners', 'recliners buy',
          'prices sofas', 'sofas prices', 'prices recliners', 'recliners prices'.</p>
<p>As a final result, we want to have a DataFrame that looks like this: </p>
<table>
<thead>
<tr>
<th>Campaign</th>
<th>Ad Group</th>
<th>Keyword</th>
<th>Criterion Type</th>
</tr>
</thead>
<tbody>
<tr>
<td>Campaign1</td>
<td>AdGroup_1</td>
<td>keyword 1a</td>
<td>Exact</td>
</tr>
<tr>
<td>Campaign1</td>
<td>AdGroup_1</td>
<td>keyword 1a</td>
<td>Phrase</td>
</tr>
<tr>
<td>Campaign1</td>
<td>AdGroup_1</td>
<td>keyword 1b</td>
<td>Exact</td>
</tr>
<tr>
<td>Campaign1</td>
<td>AdGroup_1</td>
<td>keyword 1b</td>
<td>Phrase</td>
</tr>
<tr>
<td>Campaign1</td>
<td>AdGroup_2</td>
<td>keyword 2a</td>
<td>Exact</td>
</tr>
<tr>
<td>Campaign1</td>
<td>AdGroup_2</td>
<td>keyword 2a</td>
<td>Phrase</td>
</tr>
</tbody>
</table>
<p>The first step is to come up with a list of words that users might use to express their desire in buying low-cost sofas.</p>

```python
# List of words to pair with products
words = ['buy', 'discount', 'promotion', 'cheap', 'offer', 'purchase', 'sale']

# Print list of words
print(words)
```

    ['buy', 'discount', 'promotion', 'cheap', 'offer', 'purchase', 'sale']

```python
def test_words_in_long_word_list_task_1():
    correct_words = ['buy', 'price', 'discount', 'promotion', 'promo', 'shop',
                     'buying', 'prices', 'pricing', 'shopping', 'discounts',
                     'promos', 'ecommerce', 'e commerce', 'buy online',
                     'shop online', 'cheap', 'best price', 'lowest price',
                     'cheapest', 'best value', 'offer', 'offers', 'promotions',
                     'purchase', 'sale', 'bargain', 'affordable',
                     'cheap', 'low cost', 'low price', 'budget', 'inexpensive', 'economical',]
    assert all([word in correct_words for word in words]), \
    'The variable `words` should contain relevant words to the products in the brief.'

def test_len_words_task_1():
    assert 6 <= len(set(words)) <= 10, \
    "There should be six to ten brief-related words in the list `words`."
```

    2/2 tests passed

## 2. Combine the words with the product names
<p>Imagining all the possible combinations of keywords can be stressful! But not for us, because we are keyword ninjas! We know how to translate campaign briefs into Python data structures and can imagine the resulting DataFrames that we need to create.</p>
<p>Now that we have brainstormed the words that work well with the brief that we received, it is now time to combine them with the product names to generate meaningful search keywords. We want to combine every word with every product once before, and once after, as seen in the example above.</p>
<p>As a quick reminder, for the product 'recliners' and the words 'buy' and 'price' for example, we would want to generate the following combinations: </p>
<p>buy recliners<br>
recliners buy<br>
price recliners<br>
recliners price<br>
…  </p>
<p>and so on for all the words and products that we have.</p>

```python
products = ['sofas', 'convertible sofas', 'love seats', 'recliners', 'sofa beds']

# Create an empty list
keywords_list = []

# Loop through products
for product in products:
    # Loop through words
    for word in words:
        # Append combinations
        keywords_list.append([product, product + ' ' + word])
        keywords_list.append([product, word + ' ' + product])

# Inspect keyword list
print(keywords_list)
```

    [['sofas', 'sofas buy'], ['sofas', 'buy sofas'], ['sofas', 'sofas discount'], ['sofas', 'discount sofas'], ['sofas', 'sofas promotion'], ['sofas', 'promotion sofas'], ['sofas', 'sofas cheap'], ['sofas', 'cheap sofas'], ['sofas', 'sofas offer'], ['sofas', 'offer sofas'], ['sofas', 'sofas purchase'], ['sofas', 'purchase sofas'], ['sofas', 'sofas sale'], ['sofas', 'sale sofas'], ['convertible sofas', 'convertible sofas buy'], ['convertible sofas', 'buy convertible sofas'], ['convertible sofas', 'convertible sofas discount'], ['convertible sofas', 'discount convertible sofas'], ['convertible sofas', 'convertible sofas promotion'], ['convertible sofas', 'promotion convertible sofas'], ['convertible sofas', 'convertible sofas cheap'], ['convertible sofas', 'cheap convertible sofas'], ['convertible sofas', 'convertible sofas offer'], ['convertible sofas', 'offer convertible sofas'], ['convertible sofas', 'convertible sofas purchase'], ['convertible sofas', 'purchase convertible sofas'], ['convertible sofas', 'convertible sofas sale'], ['convertible sofas', 'sale convertible sofas'], ['love seats', 'love seats buy'], ['love seats', 'buy love seats'], ['love seats', 'love seats discount'], ['love seats', 'discount love seats'], ['love seats', 'love seats promotion'], ['love seats', 'promotion love seats'], ['love seats', 'love seats cheap'], ['love seats', 'cheap love seats'], ['love seats', 'love seats offer'], ['love seats', 'offer love seats'], ['love seats', 'love seats purchase'], ['love seats', 'purchase love seats'], ['love seats', 'love seats sale'], ['love seats', 'sale love seats'], ['recliners', 'recliners buy'], ['recliners', 'buy recliners'], ['recliners', 'recliners discount'], ['recliners', 'discount recliners'], ['recliners', 'recliners promotion'], ['recliners', 'promotion recliners'], ['recliners', 'recliners cheap'], ['recliners', 'cheap recliners'], ['recliners', 'recliners offer'], ['recliners', 'offer recliners'], ['recliners', 'recliners purchase'], ['recliners', 'purchase recliners'], ['recliners', 'recliners sale'], ['recliners', 'sale recliners'], ['sofa beds', 'sofa beds buy'], ['sofa beds', 'buy sofa beds'], ['sofa beds', 'sofa beds discount'], ['sofa beds', 'discount sofa beds'], ['sofa beds', 'sofa beds promotion'], ['sofa beds', 'promotion sofa beds'], ['sofa beds', 'sofa beds cheap'], ['sofa beds', 'cheap sofa beds'], ['sofa beds', 'sofa beds offer'], ['sofa beds', 'offer sofa beds'], ['sofa beds', 'sofa beds purchase'], ['sofa beds', 'purchase sofa beds'], ['sofa beds', 'sofa beds sale'], ['sofa beds', 'sale sofa beds']]

```python
def test_list_task_2():
    assert isinstance(keywords_list, list), 'The variable `keywords_list` is not a Python list.'

def test_keywords_list_created_correctly_task_2():
    test_keywords_list = []

    for product in products:
        for word in words:
            test_keywords_list.append([product, word + ' ' + product])
            test_keywords_list.append([product, product + ' ' + word])

    assert all([kl in test_keywords_list for kl in keywords_list]), \
     'Make sure you have \'product word\' or \'word product\' as the second element in each sublist.'
```

    2/2 tests passed

## 3. Convert the list of lists into a DataFrame
<p>Now we want to convert this list of lists into a DataFrame so we can easily manipulate it and manage the final output.</p>

```python
# Load library
import pandas as pd

# Create a DataFrame from list
keywords_df = pd.DataFrame.from_records(keywords_list)

# Print the keywords DataFrame to explore it
keywords_df.head()
```

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>sofas</td>
      <td>sofas buy</td>
    </tr>
    <tr>
      <th>1</th>
      <td>sofas</td>
      <td>buy sofas</td>
    </tr>
    <tr>
      <th>2</th>
      <td>sofas</td>
      <td>sofas discount</td>
    </tr>
    <tr>
      <th>3</th>
      <td>sofas</td>
      <td>discount sofas</td>
    </tr>
    <tr>
      <th>4</th>
      <td>sofas</td>
      <td>sofas promotion</td>
    </tr>
  </tbody>
</table>

```python
def test_pandas_loaded_task_3():
    assert 'pd' in globals(), \
    'Did you forget to import pandas aliased as pd?'

def test_keywords_df_created_correctly_task_3():
    import pandas as pd
    correct_keywords_df = pd.DataFrame.from_records(keywords_list)
    assert correct_keywords_df.equals(keywords_df), "The contents of `keywords_df` doesn't appear to be correct. Don't specify column names yet!"

#     correct_keywords_df = pd.DataFrame.from_records(keywords_list)

#     assert (correct_keywords_df
#             .sort_values(list(sorted(correct_keywords_df.columns.values)))
#             .reset_index(drop=True)
#             .equals(keywords_df
#                     .sort_values(list(sorted(keywords_df.columns.values)))
#                     .reset_index(drop=True))) , \
#     'The DataFrame you created doesn\'t seem to be the right one.'
```

    2/2 tests passed

## 4. Rename the columns of the DataFrame
<p>Before we can upload this table of keywords, we will need to give the columns meaningful names. If we inspect the DataFrame we just created above, we can see that the columns are currently named <code>0</code> and <code>1</code>. <code>Ad Group</code> (example: "sofas") and <code>Keyword</code> (example: "sofas buy") are much more appropriate names.</p>

```python
# Rename the columns of the DataFrame
keywords_df.columns = ['Ad Group', 'Keyword']
```

```python
def test_df_columns_renamed_correctly_task_4():
    assert 'Ad Group' in keywords_df.columns.values and 'Keyword' in keywords_df.columns.values , \
    'Make sure you are using the proper names for the columns. Capitalization matters!'
```

    1/1 tests passed

## 5. Add a campaign column
<p>Now we need to add some additional information to our DataFrame.
We need a new column called <code>Campaign</code> for the campaign name. We want campaign names to be descriptive of our group of keywords and products, so let's call this campaign 'SEM_Sofas'.</p>

```python
# Add a campaign column
keywords_df['Campaign'] = 'SEM_Sofas'
```

```python
def test_campaign_column_created_task_5():
    assert 'Campaign' in keywords_df.columns.values, \
    "`Campaign` needs to be the name of the new column. Capitalization matters!"

def test_campaign_name_task_5():
    assert len(set(keywords_df['Campaign'])) == 1 and set(keywords_df['Campaign']).pop() == 'SEM_Sofas', \
    "Is 'SEM_Sofas' the campaign name in every row of the `Campaign` column?"
```

    2/2 tests passed

## 6. Create the match type column
<p>There are different keyword match types. One is exact match, which is for matching the exact term or are close variations of that exact term. Another match type is broad match, which means ads may show on searches that include misspellings, synonyms, related searches, and other relevant variations.</p>
<p>Straight from Google's AdWords <a href="https://support.google.com/google-ads/answer/2497836?hl=en">documentation</a>:</p>
<blockquote>
  <p>In general, the broader the match type, the more traffic potential that keyword will have, since your ads may be triggered more often. Conversely, a narrower match type means that your ads may show less often—but when they do, they’re likely to be more related to someone’s search.</p>
</blockquote>
<p>Since the client is tight on budget, we want to make sure all the keywords are in exact match at the beginning.</p>

```python
# Add a criterion type column
keywords_df['Criterion Type'] = 'Exact'
```

```python
def test_criterion_type_column_created_task_6():
    assert 'Criterion Type' in keywords_df.columns.values, \
    "`Criterion Type` needs to be the name of the new column. Capitalization matters!"

def test_criterion_type_task_6():
    assert len(set(keywords_df['Criterion Type'])) == 1 and set(keywords_df['Criterion Type']).pop() == 'Exact', \
    "Is 'Exact' the campaign name in every row of the `Criterion Type` column?"
```

    2/2 tests passed

## 7. Duplicate all the keywords into 'phrase' match
<p>The great thing about exact match is that it is very specific, and we can control the process very well. The tradeoff, however, is that:  </p>
<ol>
<li>The search volume for exact match is lower than other match types</li>
<li>We can't possibly think of all the ways in which people search, and so, we are probably missing out on some high-quality keywords.</li>
</ol>
<p>So it's good to use another match called <em>phrase match</em> as a discovery mechanism to allow our ads to be triggered by keywords that include our exact match keywords, together with anything before (or after) them.</p>
<p>Later on, when we launch the campaign, we can explore with modified broad match, broad match, and negative match types, for better visibility and control of our campaigns.</p>

```python
# Make a copy of the keywords DataFrame
keywords_phrase = keywords_df.copy()

# Change criterion type match to phrase
keywords_phrase['Criterion Type'] = 'Phrase'

# Append the DataFrames
keywords_df_final = keywords_df.append(keywords_phrase)
```

```python
def test_criterion_type_task_7():
    assert len(set(keywords_phrase['Criterion Type'])) == 1 and set(keywords_phrase['Criterion Type']).pop() == 'Phrase', \
    "Is 'Phrase' the campaign name in every row of the `Criterion Type` column in `keyword_phrase`?"

def test_phrase_df_created_task_7():
    test_keywords_df_final = keywords_df.append(keywords_phrase)
    assert test_keywords_df_final.equals(keywords_df_final), \
    'The final DataFrame does not seem to be created correctly.'
```

    2/2 tests passed

## 8. Save and summarize!
<p>To upload our campaign, we need to save it as a CSV file. Then we will be able to import it to AdWords editor or BingAds editor. There is also the option of pasting the data into the editor if we want, but having easy access to the saved data is great so let's save to a CSV file!</p>
<p>Looking at a summary of our campaign structure is good now that we've wrapped up our keyword work. We can do that by grouping by ad group and criterion type and counting by keyword. This summary shows us that we assigned specific keywords to specific ad groups, which are each part of a campaign. In essence, we are telling Google (or Bing, etc.) that we want any of the words in each ad group to trigger one of the ads in the same ad group. Separately, we will have to create another table for ads, which is a task for another day and would look something like this:</p>
<table>
<thead>
<tr>
<th>Campaign</th>
<th>Ad Group</th>
<th>Headline 1</th>
<th>Headline 2</th>
<th>Description</th>
<th>Final URL</th>
</tr>
</thead>
<tbody>
<tr>
<td>SEM_Sofas</td>
<td>Sofas</td>
<td>Looking for Quality Sofas?</td>
<td>Explore Our Massive Collection</td>
<td>30-day Returns With Free Delivery Within the US. Start Shopping Now</td>
<td>DataCampSofas.com/sofas</td>
</tr>
<tr>
<td>SEM_Sofas</td>
<td>Sofas</td>
<td>Looking for Affordable Sofas?</td>
<td>Check Out Our Weekly Offers</td>
<td>30-day Returns With Free Delivery Within the US. Start Shopping Now</td>
<td>DataCampSofas.com/sofas</td>
</tr>
<tr>
<td>SEM_Sofas</td>
<td>Recliners</td>
<td>Looking for Quality Recliners?</td>
<td>Explore Our Massive Collection</td>
<td>30-day Returns With Free Delivery Within the US. Start Shopping Now</td>
<td>DataCampSofas.com/recliners</td>
</tr>
<tr>
<td>SEM_Sofas</td>
<td>Recliners</td>
<td>Need Affordable Recliners?</td>
<td>Check Out Our Weekly Offers</td>
<td>30-day Returns With Free Delivery Within the US. Start Shopping Now</td>
<td>DataCampSofas.com/recliners</td>
</tr>
</tbody>
</table>
<p>Together, these tables get us the sample <strong>keywords -> ads -> landing pages</strong> mapping shown in the diagram below.</p>
<p><img src="https://assets.datacamp.com/production/project_400/img/kwds_ads_lpages.png" alt="Keywords-Ads-Landing pages flow"></p>

```python
# Save the final keywords to a CSV file
keywords_df_final.to_csv('keywords.csv', index=False)

# View a summary of our campaign work
summary = keywords_df_final.groupby(['Ad Group', 'Criterion Type'])['Keyword'].count()
summary
```

    Ad Group           Criterion Type
    convertible sofas  Exact             14
                       Phrase            14
    love seats         Exact             14
                       Phrase            14
    recliners          Exact             14
                       Phrase            14
    sofa beds          Exact             14
                       Phrase            14
    sofas              Exact             14
                       Phrase            14
    Name: Keyword, dtype: int64

```python
import os

# def test_df_saved_to_csv_task_8():
#     test_keywords_df = pd.read_csv('keywords.csv')
#     assert keywords_df_final.equals(test_keywords_df), \
#     'The \'keywords.csv\' file isn\'t saved correctly.'

def test_file_exists_task_8():
    assert os.path.exists("keywords.csv"), \
    'Did you save the `keywords_df_final` DataFrame to \'keywords.csv\'?'

def test_index_excluded_task_8():
    test_keywords_csv = pd.read_csv('keywords.csv')
    assert len(pd.read_csv('keywords.csv').columns) == 4, \
    'Did you exclude the DataFrame index in \'keywords.csv\' using `index=False`?'
```

    2/2 tests passed
