
## 1. The sisters and Google Trends
<p>While I'm not a fan nor a hater of the Kardashians and Jenners, the polarizing family intrigues me. Why? Their marketing prowess. Say what you will about them and what they stand for, they are great at the hype game. Everything they touch turns to content.</p>
<p>The sisters in particular over the past decade have been especially productive in this regard. Let's get some facts straight. I consider the "sisters" to be the following daughters of Kris Jenner. Three from her first marriage to lawyer <a href="https://en.wikipedia.org/wiki/Robert_Kardashian">Robert Kardashian</a>:</p>
<ul>
<li><a href="https://en.wikipedia.org/wiki/Kourtney_Kardashian">Kourtney Kardashian</a> (daughter of Robert Kardashian, born in 1979)</li>
<li><a href="https://en.wikipedia.org/wiki/Kim_Kardashian">Kim Kardashian</a> (daughter of Robert Kardashian, born in 1980)</li>
<li><a href="https://en.wikipedia.org/wiki/Khlo%C3%A9_Kardashian">Khloé Kardashian</a> (daughter of Robert Kardashian, born in 1984)</li>
</ul>
<p>And two from her second marriage to Olympic gold medal-winning decathlete, <a href="https://en.wikipedia.org/wiki/Caitlyn_Jenner">Caitlyn Jenner</a> (formerly Bruce):</p>
<ul>
<li><a href="https://en.wikipedia.org/wiki/Kendall_Jenner">Kendall Jenner</a> (daughter of Caitlyn Jenner, born in 1995)</li>
<li><a href="https://en.wikipedia.org/wiki/Kylie_Jenner">Kylie Jenner</a> (daughter of Caitlyn Jenner, born in 1997)</li>
</ul>
<p><img src="https://assets.datacamp.com/production/project_538/img/kardashian_jenner_family_tree.png" alt="Kardashian Jenner sisters family tree"></p>
<p>This family tree can be confusing, but we aren't here to explain it. We're here to explore the data underneath the hype, and we'll do it using search interest data from Google Trends. We'll recreate the Google Trends plot to visualize their ups and downs over time, then make a few custom plots of our own. And we'll answer the big question: <strong>is Kim even the most famous sister anymore?</strong></p>
<p>First, let's load and inspect our Google Trends data, which was downloaded in CSV form. The <a href="https://trends.google.com/trends/explore?date=2007-01-01%202019-03-21&q=%2Fm%2F0261x8t,%2Fm%2F043p2f2,%2Fm%2F043ttm7,%2Fm%2F05_5_yx,%2Fm%2F05_5_yh">query</a> parameters: each of the sisters, worldwide search data, 2007 to present day. (2007 was the year Kim became "active" according to Wikipedia.)</p>

```python
# Load pandas
import pandas as pd

# Read in dataset
trends = pd.read_csv('datasets/trends_kj_sisters.csv')

# Inspect data
trends.head()
```

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Month</th>
      <th>Kim Kardashian: (Worldwide)</th>
      <th>Khloé Kardashian: (Worldwide)</th>
      <th>Kourtney Kardashian: (Worldwide)</th>
      <th>Kendall Jenner: (Worldwide)</th>
      <th>Kylie Jenner: (Worldwide)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2007-01</td>
      <td>2</td>
      <td>&lt;1</td>
      <td>&lt;1</td>
      <td>&lt;1</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2007-02</td>
      <td>12</td>
      <td>&lt;1</td>
      <td>&lt;1</td>
      <td>&lt;1</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2007-03</td>
      <td>9</td>
      <td>&lt;1</td>
      <td>&lt;1</td>
      <td>&lt;1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2007-04</td>
      <td>6</td>
      <td>&lt;1</td>
      <td>&lt;1</td>
      <td>&lt;1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2007-05</td>
      <td>6</td>
      <td>&lt;1</td>
      <td>&lt;1</td>
      <td>&lt;1</td>
      <td>2</td>
    </tr>
  </tbody>
</table>

```python
# One or more tests of the students code.
# The @solution should pass the tests.
# The purpose of the tests is to try to catch common errors and to 
# give the student a hint on how to resolve these errors.

last_output = _

def test_pandas_loaded():
    assert 'pd' in globals(), \
    'Did you import the pandas library aliased as pd?'
    
def test_trends_correctly_loaded():
    correct_trends = pd.read_csv('datasets/trends_kj_sisters.csv')
    assert correct_trends.equals(trends), "The variable trends should contain the data in trends_kj_sisters.csv."

def test_head_output():
    try:
        assert "2007-05" in last_output.to_string()
    except AttributeError:
        assert False, "Please use trends.head() as the last line of code in the cell to inspect the data, not the display() or print() functions."
    except AssertionError:
        assert False, "The output of the cell is not what we expected. You should see '2007-05' in the fifth row of the trends DataFrame."
```

    3/3 tests passed

## 2. Better "kolumn" names
<p>So we have a column for each month since January 2007 and a column for the worldwide search interest for each of the sisters each month. By the way, Google defines the values of search interest as:</p>
<blockquote>
  <p>Numbers represent search interest relative to the highest point on the chart for the given region and time. A value of 100 is the peak popularity for the term. A value of 50 means that the term is half as popular. A score of 0 means there was not enough data for this term.</p>
</blockquote>
<p>Okay, that's great Google, but you are not making this data easily analyzable for us. I see a few things. Let's do the column names first. A column named "Kim Kardashian: (Worldwide)" is not the most usable for coding purposes. Let's shorten those so we can access their values better. Might as well standardize all column formats, too. I like lowercase, short column names.</p>

```python
# Make column names easier to work with
trends.columns = ['month', 'kim', 'khloe', 'kourtney', 'kendall', 'kylie']

# Inspect data
trends.head()
```

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>month</th>
      <th>kim</th>
      <th>khloe</th>
      <th>kourtney</th>
      <th>kendall</th>
      <th>kylie</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2007-01</td>
      <td>2</td>
      <td>&lt;1</td>
      <td>&lt;1</td>
      <td>&lt;1</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2007-02</td>
      <td>12</td>
      <td>&lt;1</td>
      <td>&lt;1</td>
      <td>&lt;1</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2007-03</td>
      <td>9</td>
      <td>&lt;1</td>
      <td>&lt;1</td>
      <td>&lt;1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2007-04</td>
      <td>6</td>
      <td>&lt;1</td>
      <td>&lt;1</td>
      <td>&lt;1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2007-05</td>
      <td>6</td>
      <td>&lt;1</td>
      <td>&lt;1</td>
      <td>&lt;1</td>
      <td>2</td>
    </tr>
  </tbody>
</table>

```python
# One or more tests of the students code. 
# The @solution should pass the tests.
# The purpose of the tests is to try to catch common errors and to 
# give the student a hint on how to resolve these errors.

last_output = _

def test_column_names():
    assert list(trends.columns) == ['month', 'kim', 'khloe', 'kourtney', 'kendall', 'kylie'], \
    'At least one column name is incorrect or out of order.'
    
def test_head_output():
    try:
        assert "2007-05" in last_output.to_string()
    except AttributeError:
        assert False, "Please use trends.head() as the last line of code in the cell to inspect the data, not the display() or print() functions."
    except AssertionError:
        assert False, "The output of the cell is not what we expected. You should see '2007-05' in the fifth row of the trends DataFrame."
```

    2/2 tests passed

## 3. Pesky data types
<p>That's better. We don't need to scroll our eyes across the table to read the values anymore since it is much less wide. And seeing five columns that all start with the letter "k" … the aesthetics … we should call them "kolumns" now! (Bad joke.)</p>
<p>The next thing I see that is going to be an issue is that "&lt;" sign. If <em>"a score of 0 means there was not enough data for this term,"</em> "&lt;1" must mean it is between 0 and 1 and Google does not want to give us the fraction from google.trends.com for whatever reason. That's fine, but this "&lt;" sign means we won't be able to analyze or visualize our data right away because those column values aren't going to be represented as numbers in our data structure. Let's confirm that by inspecting our data types.</p>

```python
# Inspect data types
trends.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 147 entries, 0 to 146
    Data columns (total 6 columns):
    month       147 non-null object
    kim         147 non-null int64
    khloe       147 non-null object
    kourtney    147 non-null object
    kendall     147 non-null object
    kylie       147 non-null int64
    dtypes: int64(2), object(4)
    memory usage: 7.0+ KB

```python
# One or more tests of the students code. 
# The @solution should pass the tests.
# The purpose of the tests is to try to catch common errors and to 
# give the student a hint on how to resolve these errors.

def strip_comment_lines(cell_input):
    """Returns cell input string with comment lines removed."""
    return '\n'.join(line for line in cell_input.splitlines() if not line.startswith('#'))

last_input = strip_comment_lines(In[-2])

def test_info_command():
    assert 'trends' in last_input, \
        "We expected the trend variable in your input."
    assert 'info' in last_input, \
        "We expected the info method in your input."
```

    1/1 tests passed

## 4. From object to integer
<p>Yes, okay, the <code>khloe</code>, <code>kourtney</code>, and <code>kendall</code> columns aren't integers like the <code>kim</code> and <code>kylie</code> columns are. Again, because of the "&lt;" sign that indicates a search interest value between zero and one. Is this an early hint at the hierarchy of sister popularity? We'll see shortly. Before that, we'll need to remove that pesky "&lt;" sign. Then we can change the type of those columns to integer.</p>

```python
# Loop through columns
for column in trends.columns:
    # Only modify columns that have the "<" sign
    if "<" in trends[column].to_string():
        # Remove "<" and convert dtype to integer
        trends[column] = trends[column].str.replace('<', '')
        trends[column] = pd.to_numeric(trends[column])

# Inspect data types and data
trends.info()
trends.head()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 147 entries, 0 to 146
    Data columns (total 6 columns):
    month       147 non-null object
    kim         147 non-null int64
    khloe       147 non-null int64
    kourtney    147 non-null int64
    kendall     147 non-null int64
    kylie       147 non-null int64
    dtypes: int64(5), object(1)
    memory usage: 7.0+ KB

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>month</th>
      <th>kim</th>
      <th>khloe</th>
      <th>kourtney</th>
      <th>kendall</th>
      <th>kylie</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2007-01</td>
      <td>2</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2007-02</td>
      <td>12</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2007-03</td>
      <td>9</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2007-04</td>
      <td>6</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2007-05</td>
      <td>6</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>2</td>
    </tr>
  </tbody>
</table>

```python
# One or more tests of the students code. 
# The @solution should pass the tests.
# The purpose of the tests is to try to catch common errors and to 
# give the student a hint on how to resolve these errors.

last_output = _

def test_removed_sign():
    assert "<" not in trends.to_string(), \
    'The "<" character is still present. Did you remember to overwrite each column with the output of str.replace().'
    
def test_kim_dtype():
    assert trends.kim.dtype == 'int64', \
    'The kim column is not of dtype int64.'
    
def test_khloe_dtype():
    assert trends.khloe.dtype == 'int64', \
    'The khloe column is not of dtype int64.'

def test_kourtney_dtype():
    assert trends.kourtney.dtype == 'int64', \
    'The kourtney column is not of dtype int64.'
    
def test_kendall_dtype():
    assert trends.kendall.dtype == 'int64', \
    'The kendall column is not of dtype int64.'

def test_kylie_dtype():
    assert trends.kylie.dtype == 'int64', \
    'The kylie column is not of dtype int64.'
    
def test_head_output():
    try:
        assert "2007-05" in last_output.to_string()
    except AttributeError:
        assert False, "Please use trends.head() as the last line of code in the cell to inspect the data, not the display() or print() functions."
    except AssertionError:
        assert False, "The output of the cell is not what we expected. You should see '2007-05' in the fifth row of the trends DataFrame."
```

    7/7 tests passed

## 5. From object to datetime
<p>Okay, great, no more "&lt;" signs. All the sister columns are of integer type.</p>
<p>Now let's convert our <code>month</code> column from type object to datetime to make our date data more accessible.</p>

```python
# Convert month to type datetime
trends.month = pd.to_datetime(trends.month)

# Inspect data types and data
trends.info()
trends.head()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 147 entries, 0 to 146
    Data columns (total 6 columns):
    month       147 non-null datetime64[ns]
    kim         147 non-null int64
    khloe       147 non-null int64
    kourtney    147 non-null int64
    kendall     147 non-null int64
    kylie       147 non-null int64
    dtypes: datetime64[ns](1), int64(5)
    memory usage: 7.0 KB

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>month</th>
      <th>kim</th>
      <th>khloe</th>
      <th>kourtney</th>
      <th>kendall</th>
      <th>kylie</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2007-01-01</td>
      <td>2</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2007-02-01</td>
      <td>12</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2007-03-01</td>
      <td>9</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2007-04-01</td>
      <td>6</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2007-05-01</td>
      <td>6</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>2</td>
    </tr>
  </tbody>
</table>

```python
# One or more tests of the students code. 
# The @solution should pass the tests.
# The purpose of the tests is to try to catch common errors and to 
# give the student a hint on how to resolve these errors.

last_output = _

def test_month_dtype():
    assert trends.month.dtype == 'datetime64[ns]', \
    'The month column is not of dtype datetime64[ns].'
    
def test_head_output():
    try:
        assert "2007-05-01" in last_output.to_string()
    except AttributeError:
        assert False, "Please use trends.head() as the last line of code in the cell to inspect the data, not the display() or print() functions."
    except AssertionError:
        assert False, "The output of the cell is not what we expected. You should see '2007-05-01' in the fifth row of the trends DataFrame."
```

    2/2 tests passed

## 6. Set month as index
<p>And finally, let's set the <code>month</code> column as our index to wrap our data cleaning. Having <code>month</code> as index rather than the zero-based row numbers will allow us to write shorter lines of code to create plots, where <code>month</code> will represent our x-axis.</p>

```python
# Set month as DataFrame index
trends = trends.set_index('month')

# Inspect the data
trends.head()
```

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>kim</th>
      <th>khloe</th>
      <th>kourtney</th>
      <th>kendall</th>
      <th>kylie</th>
    </tr>
    <tr>
      <th>month</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2007-01-01</th>
      <td>2</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2007-02-01</th>
      <td>12</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2007-03-01</th>
      <td>9</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2007-04-01</th>
      <td>6</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2007-05-01</th>
      <td>6</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>2</td>
    </tr>
  </tbody>
</table>

```python
# One or more tests of the students code. 
# The @solution should pass the tests.
# The purpose of the tests is to try to catch common errors and to 
# give the student a hint on how to resolve these errors.

last_output = _

def test_index_name():
    assert trends.index.name == 'month', \
    'The index of the DataFrame is not named month (case-sensitive).'
    
def test_trends_shape():
    assert trends.shape[1] == 5, \
    'There should be five columns in the DataFrame, one for the first name of each sister.'
    
def test_head_output():
    try:
        assert "2007-05-01" in last_output.to_string()
    except AttributeError:
        assert False, "Please use trends.head() as the last line of code in the cell to inspect the data, not the display() or print() functions."
    except AssertionError:
        assert False, "The output of the cell is not what we expected. You should see '2007-05-01' in the fifth row of the trends DataFrame."
```

    3/3 tests passed

## 7. The early Kim hype
<p>Okay! So our data is ready to plot. Because we cleaned our data, we only need one line of code (and just <em>thirteen</em> characters!) to remake the Google Trends chart, plus another line to make the plot show up in our notebook.</p>

```python
# Plot search interest vs. month
%matplotlib inline
trends.plot()
```

    <matplotlib.axes._subplots.AxesSubplot at 0x7f74fbb19978>

![png](images/output_19_1.png)

```python
# One or more tests of the students code. 
# The @solution should pass the tests.
# The purpose of the tests is to try to catch common errors and to 
# give the student a hint on how to resolve these errors.

last_value = _

def test_plot_exists_7():
    assert type(last_value) == type(trends.plot()), \
    'A plot was not the last output of the code cell.'
    
def test_x_data_7():
    assert len(last_value.get_lines()[0].get_xdata()) == len(list(trends.index)), \
    'The x-axis data looks incorrect.'
    
def test_y_data_7():
    assert len(last_value.get_lines()[0].get_ydata()) == len(list(trends.kim)), \
    'The y-axis data looks incorrect.'

# def test_x_label_7():
#     assert last_value.get_xlabel() == 'month', \
#     'The x-axis is not labeled `month`.'
```

    3/3 tests passed

![png](images/output_20_2.png)

## 8. Kylie's rise
<p>Oh my! There is so much to make sense of here. Kim's <a href="https://en.wikipedia.org/wiki/Kim_Kardashian#2007%E2%80%932009:_Breakthrough_with_reality_television">sharp rise in 2007</a>, with the beginning of <a href="https://en.wikipedia.org/wiki/Keeping_Up_with_the_Kardashians"><em>Keeping Up with the Kardashians</em></a>, among other things. There was no significant search interest for the other four sisters until mid-2009 when Kourtney and Khloé launched the reality television series, <a href="https://en.wikipedia.org/wiki/Kourtney_and_Kim_Take_Miami"><em>Kourtney and Khloé Take Miami</em></a>. Then there was Kim's rise from famous to <a href="https://trends.google.com/trends/explore?date=all&geo=US&q=%2Fm%2F0261x8t,%2Fm%2F0d05l6">literally more famous than God</a> in 2011. This Cosmopolitan <a href="https://www.cosmopolitan.com/uk/entertainment/a12464842/who-is-kim-kardashian/">article</a> covers the timeline that includes the launch of music videos, fragrances,  iPhone and Android games, another television series, joining Instagram, and more. Then there was Kim's ridiculous spike in December 2014: posing naked on the cover of Paper Magazine in a bid to break the internet will do that for you.</p>
<p>A curious thing starts to happen after that bid as well. Let's zoom in…</p>

```python
# Zoom in from January 2014
trends.loc['2014-01-01':].plot()
```

    <matplotlib.axes._subplots.AxesSubplot at 0x7f74fbbb5d30>

![png](images/output_22_1.png)

```python
# One or more tests of the students code. 
# The @solution should pass the tests.
# The purpose of the tests is to try to catch common errors and to 
# give the student a hint on how to resolve these errors.

last_value = _

def test_plot_exists_8():
    assert type(last_value) == type(trends.loc['2014-01-01':].plot()), \
    'A plot was not the last output of the code cell.'
    
def test_x_data_8():
    assert len(last_value.get_lines()[0].get_xdata()) == len(list(trends.loc['2014-01-01':].index)), \
    'The x-axis data looks incorrect.'
    
def test_y_data_8():
    assert len(last_value.get_lines()[0].get_ydata()) == len(list(trends.loc['2014-01-01':].kim)), \
    'The y-axis data looks incorrect.'
```

    3/3 tests passed

![png](images/output_23_2.png)


## 9. Smooth out the fluctuations with rolling means
<p>It looks like my suspicion may be true: Kim is not always the most searched Kardashian or Jenner sister. Since late-2016, at various months, Kylie overtakes Kim. Two big spikes where she smashed Kim's search interest: in September 2017 when it was reported that Kylie was expecting her first child with rapper <a href="https://en.wikipedia.org/wiki/Travis_Scott">Travis Scott</a> and in February 2018 when she gave birth to her daughter, Stormi Webster. The continued success of Kylie Cosmetics has kept her in the news, not to mention making her the "The Youngest Self-Made Billionaire Ever" <a href="https://www.forbes.com/sites/natalierobehmed/2019/03/05/at-21-kylie-jenner-becomes-the-youngest-self-made-billionaire-ever/#57e612c02794">according to Forbes</a>.</p>
<p>These fluctuations are descriptive but do not really help us answer our question: is Kim even the most famous sister anymore? We can use rolling means to smooth out short-term fluctuations in time series data and highlight long-term trends. Let's make the window twelve months a.k.a. one year.</p>

```python
# Smooth the data with rolling means
trends.rolling(window=12).mean().plot()
```

    <matplotlib.axes._subplots.AxesSubplot at 0x7f74fb933ba8>

![png](images/output_25_1.png)

```python
# One or more tests of the students code. 
# The @solution should pass the tests.
# The purpose of the tests is to try to catch common errors and to 
# give the student a hint on how to resolve these errors.

last_value = _
# print(last_value.get_lines()[0].get_ydata())
# print(trends.rolling(window=12).mean().kim.values)

def test_plot_exists_9():
    assert type(last_value) == type(trends.rolling(window=12).mean().plot()), \
    'A plot was not the last output of the code cell.'
    
def test_x_data_9():
    assert len(last_value.get_lines()[0].get_xdata()) == len(list(trends.index)), \
    'The x-axis data looks incorrect.'

def test_y_data_9():
    assert all(last_value.get_lines()[0].get_ydata()[11:] == trends.rolling(window=12).mean().kim.values[11:]), \
    'The y-axis data looks incorrect.'
```

    3/3 tests passed

![png](images/output_26_2.png)

## 10. Who's more famous? The Kardashians or the Jenners?
<p>Whoa, okay! So by this metric, Kim is still the most famous sister despite Kylie being close and nearly taking her crown. Honestly, the biggest takeaway from this whole exercise might be Kendall not showing up that much. It makes sense, though, despite her <a href="http://time.com/money/5033357/kendall-jenner-makes-more-than-gisele-bundchen/">wildly successful modeling career</a>. Some have called her "<a href="https://www.nickiswift.com/5681/kendall-jenner-normal-one-family/">the only normal one in her family</a>" as she tends to shy away from the more dramatic and controversial parts of the media limelight that generate oh so many clicks.</p>
<p>Let's end this analysis with one last plot. In it, we will plot (pun!) the Kardashian sisters against the Jenner sisters to see which family line is more popular now. We will use average search interest to make things fair, i.e., total search interest divided by the number of sisters in the family line.</p>
<p><strong>The answer?</strong> Since 2015, it has been a toss-up. And in the future? With this family and their penchant for big events, who knows?</p>

```python
# Average search interest for each family line
trends['kardashian'] = (trends.kim + trends.khloe + trends.kourtney) / 3
trends['jenner'] = (trends.kendall + trends.kylie) / 2

# Plot average family line search interest vs. month
trends[['kardashian', 'jenner']].plot()
```

    <matplotlib.axes._subplots.AxesSubplot at 0x7f74fb8767f0>

![png](images/output_28_1.png)

```python
last_value = _

# One or more tests of the students code. 
# The @solution should pass the tests.
# The purpose of the tests is to try to catch common errors and to 
# give the student a hint on how to resolve these errors.

def test_kardashian_created():
    assert 'kardashian' in list(trends.columns), \
    'The kardashian column (case-sensitive) does not look like it was added to the DataFrame correctly.'

def test_jenner_created():
    assert 'jenner' in list(trends.columns), \
    'The jenner column (case-sensitive) does not look like it was added to the DataFrame correctly.'

def test_kim_remains():
    assert 'kim' in list(trends.columns), \
    'The kim column looks like it was removed from the trends DataFrame. It should remain.'

def test_khloe_remains():
    assert 'khloe' in list(trends.columns), \
    'The khloe column looks like it was removed from the trends DataFrame. It should remain.'
    
def test_kourtney_remains():
    assert 'kourtney' in list(trends.columns), \
    'The kourtney column looks like it was removed from the trends DataFrame. It should remain.'
    
def test_kendall_remains():
    assert 'kendall' in list(trends.columns), \
    'The kendall column looks like it was removed from the trends DataFrame. It should remain.'
    
def test_kylie_remains():
    assert 'kylie' in list(trends.columns), \
    'The kylie column looks like it was removed from the trends DataFrame. It should remain.'

def test_kardashian_correct():
    assert all(trends['kardashian'].round() == ((trends.kim + trends.khloe + trends.kourtney) / 3).round()), \
    'The data in the kardashian column looks incorrect.'
    
def test_jenner_correct():
    assert all(trends['jenner'].round() == ((trends.kendall + trends.kylie) / 2).round()), \
    'The data in the kardashian column looks incorrect.'

def test_plot_exists_10():
    assert type(last_value) == type(trends[['kardashian', 'jenner']].plot()), \
    'A plot was not the last output of the code cell.'
    
def test_x_data_10():
    assert len(last_value.get_lines()[0].get_xdata()) == len(list(trends.index)), \
    'The x-axis data looks incorrect. It should contain every month from 2007-01-01 through 2019-03-01.'
    
def test_y_legend_10():
    assert set(last_value.get_legend_handles_labels()[1]) == set(['kardashian', 'jenner']), \
    'The y-axis data looks incorrect. It should contain the average search interest for each family line, i.e., the newly created kardashian and jenner columns.'
```

    12/12 tests passed

![png](images/output_29_2.png)
