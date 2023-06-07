## 1. Importing the Data
<p><img src="https://assets.datacamp.com/production/project_1230/img/nyc.jpg" alt="New York City skyline" width="600px">
<br>
Welcome to New York City (NYC), one of the most-visited cities in the world. 
As a result, there are many <a href="https://www.airbnb.com/"><em>Airbnb</em></a> listings to meet the high demand for temporary lodging for anywhere between a few nights to many months. 
In this notebook, we will take a look at the NYC Airbnb market by combining data from multiple file types like <code>.csv</code>, <code>.tsv</code>, and <code>.xlsx</code>.</p>
<p><br><br>
We will be working with three datasets:</p>
<ol>
<li><p><code>"datasets/airbnb_price.csv"</code></p></li>
<li><p><code>"datasets/airbnb_room_type.xlsx"</code></p></li>
<li><p><code>"datasets/airbnb_last_review.tsv"</code></p></li>
</ol>
<p><br><br>
Our goals are to convert untidy data into appropriate formats to analyze, and answer key questions including:</p>
<ul>
<li>What is the average price, per night, of an Airbnb listing in NYC? </li>
<li>How does the average price of an Airbnb listing, per month, compare to the private rental market? </li>
<li>How many adverts are for private rooms? </li>
<li>How do Airbnb listing prices compare across the five NYC boroughs?</li>
</ul>

```python
import pandas as pd
import numpy as np
import datetime as dt

# Load airbnb_price.csv, prices
prices = pd.read_csv("datasets/airbnb_price.csv")

# Load airbnb_room_type.xlsx, xls
xls = pd.ExcelFile("datasets/airbnb_room_type.xlsx")

# Parse the first sheet from xls, room_types
room_types = xls.parse(0)

# Load airbnb_last_review.tsv, reviews
reviews = pd.read_csv("datasets/airbnb_last_review.tsv", sep="\t")

# Print the first five rows of each DataFrame
print(
    f"prices: {prices.head()}",
    "\n",
    f"room_types: {room_types.head()}",
    "\n",
    f"reviews: {reviews.head()}"
)
```

    prices:    listing_id        price                nbhood_full
    0        2595  225 dollars         Manhattan, Midtown
    1        3831   89 dollars     Brooklyn, Clinton Hill
    2        5099  200 dollars     Manhattan, Murray Hill
    3        5178   79 dollars  Manhattan, Hell's Kitchen
    4        5238  150 dollars       Manhattan, Chinatown 
     room_types:    listing_id                                description        room_type
    0        2595                      Skylit Midtown Castle  Entire home/apt
    1        3831            Cozy Entire Floor of Brownstone  Entire home/apt
    2        5099  Large Cozy 1 BR Apartment In Midtown East  Entire home/apt
    3        5178            Large Furnished Room Near B'way     private room
    4        5238         Cute & Cozy Lower East Side 1 bdrm  Entire home/apt 
     reviews:    listing_id    host_name   last_review
    0        2595     Jennifer   May 21 2019
    1        3831  LisaRoxanne  July 05 2019
    2        5099        Chris  June 22 2019
    3        5178     Shunichi  June 24 2019
    4        5238          Ben  June 09 2019

```python
prices_copy = pd.read_csv('datasets/airbnb_price.csv')
xls_copy = pd.ExcelFile('datasets/airbnb_room_type.xlsx')
room_types_copy = xls_copy.parse(0)
reviews_copy = pd.read_csv("datasets/airbnb_last_review.tsv", sep='\t')

def test_pandas_loaded():
    assert 'pd' in globals(), \
    "Have you imported pandas using the correct alias?"

def test_prices_loaded():
    assert isinstance(prices, pd.DataFrame), \
    "Have you created a DataFrame called prices by using pd.read_csv()?"
    assert prices_copy.equals(prices), \
    """"Did you correctly load "datasets/airbnb_price.csv"""

def test_room_types_loaded():
    assert isinstance(room_types, pd.DataFrame), \
    "Have you created a DataFrame called room_types by using pd.read_csv()?"
    assert room_types_copy.equals(room_types), \
    """Did you correctly load "datasets/airbnb_room_type.xlsx"""

def test_reviews_loaded():
    assert isinstance(reviews, pd.DataFrame), \
    """Have you created a DataFrame called reviews by using pd.read_csv() and setting sep="\t"?"""
    assert reviews_copy.equals(reviews), \
    """Did you correctly load "datasets/airbnb_last_review.tsv"""
```

    4/4 tests passed

## 2. Cleaning the price column
<p>Now the <code>DataFrames</code> have been loaded, the first step is to calculate the average price per listing by <code>room_type</code>. </p>
<p>You may have noticed that the <code>price</code> column in the <code>prices</code> DataFrame currently states each value as a string with the currency (dollars) following, i.e.,</p>
<pre><code>price
225 dollars
89 dollars
200 dollars</code></pre>
<p></p>
<p>We will need to clean the column in order to calculate the average price.</p>

```python
# Remove whitespace and string characters from prices column
prices["price"] = prices["price"].str.replace(" dollars", "")

# Convert prices column to numeric datatype
prices["price"] = pd.to_numeric(prices["price"])

# Print 1st 5 rows
print(prices["price"].head())

# Print descriptive statistics for the price column
print(prices["price"].describe())
```

    0    225
    1     89
    2    200
    3     79
    4    150
    Name: price, dtype: int64
    count    25209.000000
    mean       141.777936
    std        147.349137
    min          0.000000
    25%         69.000000
    50%        105.000000
    75%        175.000000
    max       7500.000000
    Name: price, dtype: float64

```python
prices_copy = pd.read_csv('datasets/airbnb_price.csv')
prices_copy = prices_copy['price'].str.replace(" dollars", "")
prices_copy = pd.to_numeric(prices_copy)

def test_prices_column():
    assert prices_copy.equals(prices['price']), \
    "Did you remove all string characters from the 'price' column?"
    assert prices['price'].dtype == 'int64' or prices['price'].dtype == 'float64', \
    "Did you correctly convert the 'price' column to numeric data type?"
```

    1/1 tests passed

## 3. Calculating average price
<p>We can see three quarters of listings cost \$175 per night or less. </p>
<p>However, there are some outliers including a maximum price of \$7,500 per night! </p>
<p>Some of listings are actually showing as free. Let's remove these from the <code>DataFrame</code>, and calculate the average price.</p>

```python
# Subset prices for listings costing $0 named "free_listings"
free_listings = prices["price"] == 0
print(type(free_listings))
print(free_listings.shape)

# Update prices by removing all free listings from prices
# Similar to SQL's concept of "NOT IN"
prices = prices.loc[~free_listings]

# Calculate the average price and round to nearest 2 decimal places, avg_price
avg_price = round(prices["price"].mean(),2)

# Print the average price
print("The average price per night for an Airbnb listing in NYC is ${}.".format(avg_price))
```

    <class 'pandas.core.series.Series'>
    (25209,)
    The average price per night for an Airbnb listing in NYC is $141.82.

```python
def test_prices():
    assert prices['price'].isin([0]).any() == False, \
    "Have all listings with a price of $0 been removed from the DataFrame?"

def test_avg_price():
    assert avg_price == round(prices['price'].mean(), 2) or avg_price == prices["price"].mean().round(2), \
    "Did you choose the correct method to calculate the average price?"
```

    2/2 tests passed

## 4. Comparing costs to the private rental market
<p>Now we know how much a listing costs, on average, per night, but it would be useful to have a benchmark for comparison. 
According to <a href="https://www.zumper.com/rent-research">Zumper</a>, a 1 bedroom apartment in New York City costs, on average, $3,100 per month. Let's convert the per night prices of our listings into monthly costs, so we can compare to the private market. </p>

```python
# Add a new column to the prices DataFrame, price_per_month
prices["price_per_month"] = prices["price"] * 365 / 12
# print(type(prices["price_per_month"]))

# Calculate average_price_per_month
average_price_per_month = round(prices["price_per_month"].mean(),2)                     
                                                       
# Compare Airbnb and rental market
print("Airbnb monthly costs are ${}, while in the private market you would pay {}.".format(average_price_per_month, "$3,100.00"))
```

    Airbnb monthly costs are $4313.61, while in the private market you would pay $3,100.00.

```python
def test_price_per_month_in_df():
    assert 'price_per_month' in prices.columns, \
    "Has 'price_per_month' been added as a column in the 'prices' DataFrame?"
    
def test_price_per_month_correct_values():
    prices_per_month_copy = prices['price'] * 365 / 12
    assert prices_per_month_copy.equals(prices['price_per_month']), \
    "Have you correctly calculated the values in the 'price_per_month' column?"

def test_avg_price_per_month_correct_values():
    average_price_per_month_copy = round(prices['price_per_month'].mean(), 2)
    assert round(np.mean(prices['price_per_month']), 2) == average_price_per_month_copy, \
    "Have you correctly calculated the average price per month? Make sure you have rounded to the nearest two decimal places."
```

    3/3 tests passed

## 5. Cleaning the room type column
<p>Unsurprisingly, using Airbnb appears to be substantially more expensive than the private rental market. We should, however, consider that these Airbnb listings include single private rooms or even rooms to share, as well as entire homes/apartments. 
<br><br>
Let's dive deeper into the <code>room_type</code> column to find out the breakdown of listings by type of room. The <code>room_type</code> column has several variations for <code>private room</code> listings, specifically: </p>
<ul>
<li>"Private room"</li>
<li>"private room"</li>
<li>"PRIVATE ROOM"</li>
</ul>
<p>We can solve this by converting all string characters to lower case (upper case would also work just fine). </p>

```python
# Convert the room_type column to lowercase
room_types["room_type"] = room_types["room_type"].str.lower()

# Update the room_type column to category data type
room_types["room_type"] = room_types["room_type"].astype("category")

# Create the variable room_frequencies
room_frequencies = room_types["room_type"].value_counts()

# Print room_frequencies
print(room_frequencies)
```

    entire home/apt    13266
    private room       11356
    shared room          587
    Name: room_type, dtype: int64

```python
room_types_copy = pd.read_excel("datasets/airbnb_room_type.xlsx")
room_types_copy = room_types_copy['room_type'].str.lower()
room_types_copy = room_types_copy.astype('category')

def test_lower_case():
    assert np.all(room_types['room_type'].str.islower()) == True, \
    "Have you converted all string characters to lower case?"
    assert room_types['room_type'].equals(room_types_copy), \
    "Have all string characters in the column been converted to lower case?"

def test_room_frequencies():
    room_counts_copy = room_types_copy.value_counts()
    assert room_frequencies.equals(room_counts_copy), \
    "Have you correctly defined room_frequencies?"
```

    2/2 tests passed

## 6. What timeframe are we working with?
<p>It seems there is a fairly similar sized market opportunity for both private rooms (45% of listings) and entire homes/apartments (52%) on the Airbnb platform in NYC.
<br><br></p>
<p>Now let's turn our attention to the <code>reviews</code> DataFrame. The <code>last_review</code> column contains the date of the last review in the format of "Month Day Year" e.g., May 21 2019. We've been asked to find out the earliest and latest review dates in the DataFrame, and ensure the format allows this analysis to be easily conducted going forwards. </p>

```python
# Change the data type of the last_review column to datetime
reviews["last_review"] = pd.to_datetime(reviews["last_review"])
print(type(reviews["last_review"]))

# Create first_reviewed, the earliest review date
first_reviewed = reviews["last_review"].dt.date.min()

# Create last_reviewed, the most recent review date
last_reviewed = reviews["last_review"].dt.date.max()

# Print the oldest and newest reviews from the DataFrame
print("The latest Airbnb review is {}, the earliest review is {}".format(last_reviewed, first_reviewed))
```

    <class 'pandas.core.series.Series'>
    The latest Airbnb review is 2019-07-09, the earliest review is 2019-01-01

```python
reviews_copy = pd.read_csv("datasets/airbnb_last_review.tsv", sep='\t')
reviews_copy['last_review'] = pd.to_datetime(reviews_copy['last_review'])

def test_first_review_date():
    first_reviewed_copy = reviews_copy['last_review'].dt.date.min()
    assert first_reviewed == first_reviewed_copy, \
    "Has 'first_reviewed' been calculated correctly?"

def test_last_review_date():
    last_reviewed_copy = reviews_copy['last_review'].dt.date.max()
    assert last_reviewed == last_reviewed_copy, \
    "Has 'last_reviewed' been calculated correctly?"
```

    2/2 tests passed

## 7. Joining the DataFrames.
<p>Now we've extracted the information needed, we will merge the three DataFrames to make any future analysis easier to conduct. Once we have joined the data, we will remove any observations with missing values and check for duplicates.</p>

```python
# Merge prices and room_types to create rooms_and_prices
rooms_and_prices = pd.merge(prices, room_types, 
                            how="outer", 
                            on="listing_id")

# Merge rooms_and_prices with the reviews DataFrame to create airbnb_merged
airbnb_merged = pd.merge(rooms_and_prices, reviews, 
                         how="outer", 
                         on="listing_id")

# Drop missing values from airbnb_merged
airbnb_merged.dropna(inplace=True)

# Check if there are any duplicate values
print("There are {} duplicates in the DataFrame.".format(airbnb_merged.duplicated().sum()))
```

    There are 0 duplicates in the DataFrame.

```python
prices_copy = pd.read_csv('datasets/airbnb_price.csv')
xls_copy = pd.ExcelFile('datasets/airbnb_room_type.xlsx')
room_types_copy = xls_copy.parse(0)
reviews_copy = pd.read_csv("datasets/airbnb_last_review.tsv", sep='\t')
prices_copy['price'] = prices_copy['price'].str.replace(" dollars", "")
prices_copy['price'] = pd.to_numeric(prices_copy['price'])
free_listings = prices_copy['price'] == 0
prices_copy = prices_copy.loc[~free_listings]
prices_copy['price_per_month'] = prices_copy['price'] * 365 / 12
room_types_copy['room_type'] = room_types_copy['room_type'].str.lower()
room_types_copy['room_type'] = room_types_copy['room_type'].astype('category')
reviews_copy['last_review'] = pd.to_datetime(reviews_copy['last_review'])
rooms_and_prices_copy = prices_copy.merge(room_types_copy, how='outer', on='listing_id')

def test_rooms_and_prices_shape():
    assert rooms_and_prices.shape[0] == 25209, \
    "Have you correctly merged the 'prices' and 'room_types' DataFrames? Expected the new DataFrame to have a different length."
    assert rooms_and_prices.shape[1] == 6, \
    "'rooms_and_prices' doesn't contain the correct number of columns. Did you use the correct join method and specify the relevant column to merge on?"

def test_airbnb_merged_shape():
    assert airbnb_merged.shape[0] == 25184, \
    "Have you correctly merged the 'rooms_and_prices' and 'reviews' DataFrames? Expected the new DataFrame to have a different length."
    assert airbnb_merged.shape[1] == 8, \
    "'airbnb_merged' doesn't contain the correct number of columns. Did you use the correct join method and specify the relevant column to merge on?"

def test_rooms_and_prices():
    assert rooms_and_prices.equals(rooms_and_prices_copy), \
    "Have you correctly merged 'prices' and 'room_types'? Expected different values."

def test_airbnb_merged():
    airbnb_merged_copy = rooms_and_prices_copy.merge(reviews_copy, how='outer', on='listing_id')
    airbnb_merged_copy = airbnb_merged_copy.dropna()
    assert airbnb_merged.equals(airbnb_merged_copy), \
    "Have you correctly merged 'rooms_and_prices' with 'reviews'? Expected different values."
```

    4/4 tests passed

## 8. Analyzing listing prices by NYC borough
<p>Now we have combined all data into a single DataFrame, we will turn our attention to understanding the difference in listing prices between <a href="https://en.wikipedia.org/wiki/Boroughs_of_New_York_City">New York City boroughs</a>. 
We can currently see boroughs listed as the first part of a string within the <code>nbhood_full</code> column, e.g., </p>
<pre><code>Manhattan, Midtown
Brooklyn, Clinton Hill
Manhattan, Murray Hill
Manhattan, Hell's Kitchen
Manhattan, Chinatown</code></pre>
<p></p>
<p>We will therefore need to extract this information from the string and store in a new column, <code>borough</code>, for analysis.</p>

```python
# Extract information from the nbhood_full column and store as a new column, borough
airbnb_merged["borough"] = airbnb_merged["nbhood_full"].str.partition(",", expand=True)[0]

# Group by borough and calculate summary statistics
boroughs = airbnb_merged.groupby("borough")["price"].agg(["sum", "mean", "median", "count"])

# Round boroughs to 2 decimal places, and sort by mean in descending order
boroughs = boroughs.round(2).sort_values("mean", ascending=False)

# Print boroughs
print(boroughs)
```

                         sum    mean  median  count
    borough                                        
    Manhattan      1898417.0  184.04   149.0  10315
    Brooklyn       1275250.0  122.02    95.0  10451
    Queens          320715.0   92.83    70.0   3455
    Staten Island    22974.0   86.04    71.0    267
    Bronx            55156.0   79.25    65.0    696

```python
prices_copy = pd.read_csv('datasets/airbnb_price.csv')
xls_copy = pd.ExcelFile('datasets/airbnb_room_type.xlsx')
room_types_copy = xls_copy.parse(0)
reviews_copy = pd.read_csv("datasets/airbnb_last_review.tsv", sep='\t')
prices_copy['price'] = prices_copy['price'].str.replace(" dollars", "")
prices_copy['price'] = pd.to_numeric(prices_copy['price'])
free_listings = prices_copy['price'] == 0
prices_copy = prices_copy.loc[~free_listings]
prices_copy['price_per_month'] = prices_copy['price'] * 365 / 12
room_types_copy['room_type'] = room_types_copy['room_type'].str.lower()
room_types_copy['room_type'] = room_types_copy['room_type'].astype('category')
reviews_copy['last_review'] = pd.to_datetime(reviews_copy['last_review'])
correct_airbnb_merged = rooms_and_prices.merge(reviews, how='outer', on='listing_id')
correct_airbnb_merged = correct_airbnb_merged.dropna()
correct_airbnb_merged['borough'] = correct_airbnb_merged['nbhood_full'].str.partition(',')[0]
correct_boroughs = correct_airbnb_merged.groupby('borough')['price'].agg(['sum', 'mean', 'median', 'count']).round(2).sort_values('mean', ascending=False)

def test_borough_column_exists():
    assert 'borough' in airbnb_merged.columns, \
    "Did you add 'borough' as a column to the 'airbnb_merged' DataFrame?"
    
def test_summary_statistics():
    assert 'sum' in boroughs.columns, \
    "Did you include 'sum' as one of the summary statistics? Can't find this column in 'boroughs'."
    assert 'mean' in boroughs.columns, \
    "Did you include 'mean' as one of the summary statistics? Can't find this column in 'boroughs'."
    assert 'median' in boroughs.columns, \
    "Did you include 'median' as one of the summary statistics? Can't find this column in 'boroughs'."
    assert 'count' in boroughs.columns, \
    "Did you include 'count' as one of the summary statistics? Can't find this column in 'boroughs'."
    
def test_borough_column_values():
    borough_list = ['Manhattan', 'Brooklyn', 'Queens', 'Staten Island', 'Bronx']
    assert airbnb_merged['borough'].isin(borough_list).any(), \
    "Did you correctly split the 'nbhood_full' column? Expected different values in the 'borough' column."
    
def test_boroughs():
    assert boroughs.iloc[-1].values.tolist() == [55156.0, 79.25, 65.0, 696.0], \
    """Did you sort the values by "mean" in descending order? Expected the lowest average price to be in the final row of the DataFrame."""
    assert boroughs.iloc[0].values.tolist() == [1898417.0, 184.04, 149.0, 10315.0], \
    """Did you sort the values by "mean" in descending order? Expected the highest average price to be in the first row of the DataFrame."""
```

    4/4 tests passed

## 9. Price range by borough
<p>The above output gives us a summary of prices for listings across the 5 boroughs. In this final task we would like to categorize listings based on whether they fall into specific price ranges, and view this by borough. 
<br><br>
We can do this using percentiles and labels to create a new column, <code>price_range</code>, in the DataFrame.
Once we have created the labels, we can then group the data and count frequencies for listings in each price range by borough.
<br><br>
We will assign the following categories and price ranges:</p>
<table>
<thead>
<tr>
<th>label</th>
<th>price</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>Budget</code></td>
<td>\$0-69</td>
</tr>
<tr>
<td><code>Average</code></td>
<td>\$70-175</td>
</tr>
<tr>
<td><code>Expensive</code></td>
<td>\$176-350</td>
</tr>
<tr>
<td><code>Extravagant</code></td>
<td>&gt; \$350</td>
</tr>
</tbody>
</table>

```python
# Create labels for the price range, label_names
label_names = ["Budget", "Average", "Expensive", "Extravagant"]

# Create the label ranges, ranges
ranges = [0, 69, 175, 350, np.inf]

# Insert new column, price_range, into DataFrame
# Useful for going from a continuous variable to a categorical variable 
airbnb_merged["price_range"] = pd.cut(airbnb_merged["price"], bins=ranges, labels=label_names)

# Calculate borough and price_range frequencies, prices_by_borough
prices_by_borough = airbnb_merged.groupby(["borough", "price_range"])["price_range"].agg("count")
print(prices_by_borough)
```

    borough        price_range
    Bronx          Budget          381
                   Average         285
                   Expensive        25
                   Extravagant       5
    Brooklyn       Budget         3194
                   Average        5532
                   Expensive      1466
                   Extravagant     259
    Manhattan      Budget         1148
                   Average        5285
                   Expensive      3072
                   Extravagant     810
    Queens         Budget         1631
                   Average        1505
                   Expensive       291
                   Extravagant      28
    Staten Island  Budget          124
                   Average         123
                   Expensive        20
    Name: price_range, dtype: int64

```python
def test_label_names():
    correct_labels = ['Budget', 'Average', 'Expensive', 'Extravagant']
    assert correct_labels == label_names, \
    "Have you correctly specified the 'label_names', expected something else?"

def test_ranges():
    correct_ranges = [0, 69, 175, 350, np.inf]
    assert correct_ranges == ranges, \
    "Have you entered the correct values for 'ranges', expected something different?"
    
def test_budget_prices():
    budget = airbnb_merged[airbnb_merged['price_range'] == 'Budget']
    average = airbnb_merged[airbnb_merged['price_range'] == 'Average']
    expensive = airbnb_merged[airbnb_merged['price_range'] == 'Expensive']
    extravagant = airbnb_merged[airbnb_merged['price_range'] == 'Extravagant']
    assert budget['price'].max() == 69, \
    "Have you correctly mapped the labels and ranges to the 'price_range' column?"
    assert average['price'].min() > 69 and average['price'].max() == 175, \
    "Have you correctly mapped the labels and ranges to the 'price_range' column?"
    assert expensive['price'].min() > 175 and expensive['price'].max() == 350, \
    "Have you correctly mapped the labels and ranges to the 'price_range' column?"
    assert extravagant['price'].min() > 350, \
    "Have you correctly mapped the labels and ranges to the 'price_range' column?"

def test_correct_grouping():
    prices_by_borough_copy = airbnb_merged.groupby(['borough', 'price_range'])['price_range'].count()
    assert prices_by_borough.equals(prices_by_borough_copy) or prices_by_borough.equals(airbnb_merged.groupby(['borough', 'price_range'])['price_range'].agg({"price_range": "count"})), \
    "Have you grouped airbnb_merged on the correct columns? Did you specify the appropriate method to count observations?"
```

    4/4 tests passed
