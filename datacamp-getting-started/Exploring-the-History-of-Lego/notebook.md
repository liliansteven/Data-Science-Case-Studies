
## 1. Introduction
<p>Everyone loves Lego (unless you ever stepped on one). Did you know by the way that "Lego" was derived from the Danish phrase leg godt, which means "play well"? Unless you speak Danish, probably not. </p>
<p>In this project, we will analyze a fascinating dataset on every single Lego block that has ever been built!</p>
<p><img src="https://s3.amazonaws.com/assets.datacamp.com/production/project_10/datasets/lego-bricks.jpeg" alt="lego"></p>

```python
# Nothing to do here
```

```python
def test_default():
  assert True
```

    1/1 tests passed

## 2. Reading Data
<p>A comprehensive database of lego blocks is provided by <a href="https://rebrickable.com/downloads/">Rebrickable</a>. The data is available as csv files and the schema is shown below.</p>
<p><img src="https://s3.amazonaws.com/assets.datacamp.com/production/project_10/datasets/downloads_schema.png" alt="schema"></p>
<p>Let us start by reading in the colors data to get a sense of the diversity of Lego sets!</p>

```python
# Import pandas
import pandas as pd

# Read colors data
colors = pd.read_csv('datasets/colors.csv')

# Print the first few rows
colors.head()
```

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>name</th>
      <th>rgb</th>
      <th>is_trans</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-1</td>
      <td>Unknown</td>
      <td>0033B2</td>
      <td>f</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0</td>
      <td>Black</td>
      <td>05131D</td>
      <td>f</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>Blue</td>
      <td>0055BF</td>
      <td>f</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2</td>
      <td>Green</td>
      <td>237841</td>
      <td>f</td>
    </tr>
    <tr>
      <th>4</th>
      <td>3</td>
      <td>Dark Turquoise</td>
      <td>008F9B</td>
      <td>f</td>
    </tr>
  </tbody>
</table>

```python
test_colors = pd.read_csv('datasets/colors.csv')
def test_colors_exists():
    assert 'colors' in globals(), "You should read the data into a variable named `colors`"
    assert colors.equals(test_colors), "Did you read in the correct csv file?"
```

    1/1 tests passed

## 3. Exploring Colors
<p>Now that we have read the <code>colors</code> data, we can start exploring it! Let us start by understanding the number of colors available.</p>

```python
# How many distinct colors are available?
num_colors = colors.rgb.size

# Print num_colors
print('Number of distinct colors:', num_colors)
```

    Number of distinct colors: 135

```python
def test_num_colors():
    assert num_colors == 135, "The variable num_colors should equal 135"
```

    1/1 tests passed

## 4. Transparent Colors in Lego Sets
<p>The <code>colors</code> data has a column named <code>is_trans</code> that indicates whether a color is transparent or not. It would be interesting to explore the distribution of transparent vs. non-transparent colors.</p>

```python
# Summarize colors based on whether they are transparent or not?
colors_summary = colors.groupby('is_trans').count()
colors_summary
```

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>name</th>
      <th>rgb</th>
    </tr>
    <tr>
      <th>is_trans</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>f</th>
      <td>107</td>
      <td>107</td>
      <td>107</td>
    </tr>
    <tr>
      <th>t</th>
      <td>28</td>
      <td>28</td>
      <td>28</td>
    </tr>
  </tbody>
</table>

```python
def test_colors_summary_exists():
    assert 'colors_summary' in globals(), "You should have defined a variable named `colors_summary`"
def test_colors_summary():
    assert colors_summary.shape == (2, 3), "The DataFrame colors_summary should contain 2 rows and 3 columns"
```

    2/2 tests passed

## 5. Explore Lego Sets
<p>Another interesting dataset available in this database is the <code>sets</code> data. It contains a comprehensive list of sets over the years and the number of parts that each of these sets contained. </p>
<p><img src="https://imgur.com/1k4PoXs.png" alt="sets_data"></p>
<p>Let us use this data to explore how the average number of parts in Lego sets has varied over the years.</p>

```python
%matplotlib inline
# Read sets data as `sets`
sets = pd.read_csv('datasets/sets.csv')

# Create a summary of average number of parts by year: `parts_by_year`
parts_by_year = sets[['year', 'num_parts']].groupby('year').mean()

# Plot trends in average number of parts by year
parts_by_year.plot()
```

    DEBUG:matplotlib.pyplot:Loaded backend module://ipykernel.pylab.backend_inline version unknown.

    <AxesSubplot:xlabel='year'>

![png](images/output_13_2.png)

```python
test_sets = pd.read_csv('datasets/sets.csv')

def test_sets_exists():
    assert 'sets' in globals(), "You should read the data into a variable named `sets`"
    assert sets.equals(test_sets), "Did you read in the correct csv file?"

def test_parts_by_year_exists():
    assert 'parts_by_year' in globals(), "You should have defined a variable named `parts_by_year`"
    assert len(parts_by_year) == 66, "Did you correctly group the `sets` DataFrame by year?"
```

    2/2 tests passed

## 6. Lego Themes Over Years
<p>Lego blocks ship under multiple <a href="https://shop.lego.com/en-US/Themes">themes</a>. Let us try to get a sense of how the number of themes shipped has varied over the years.</p>

```python
# themes_by_year: Number of themes shipped by year
themes_by_year = sets.groupby('year')[['theme_id']].nunique()
themes_by_year.head()
```

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>theme_id</th>
    </tr>
    <tr>
      <th>year</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1950</th>
      <td>2</td>
    </tr>
    <tr>
      <th>1953</th>
      <td>1</td>
    </tr>
    <tr>
      <th>1954</th>
      <td>2</td>
    </tr>
    <tr>
      <th>1955</th>
      <td>4</td>
    </tr>
    <tr>
      <th>1956</th>
      <td>3</td>
    </tr>
  </tbody>
</table>

```python
def test_themes_by_year_exists():
    assert 'themes_by_year' in globals(), "You should have defined a variable named `themes_by_year`"
def test_themes_by_year():
    assert len(themes_by_year) == 66, "The DataFrame `themes_by_year` should contain 66 rows."
def test_themes_by_year_names():
    colnames = ['theme_id']
    assert all(name in themes_by_year for name in colnames), "Your DataFrame, bnames, should have the column `theme_id`."
```

    3/3 tests passed

## 7. Wrapping It All Up!
<p>Lego blocks offer an unlimited amount of fun across ages. We explored some interesting trends around colors, parts, and themes. Before we wrap up, let's take a closer look at the <code>themes_by_year</code> DataFrame you created in the previous step.</p>

```python
# Get the number of unique themes released in 1999
num_themes = themes_by_year.loc[1999,'theme_id']

# Print the number of unique themes released in 1999
print(num_themes)
```

    71

```python
def test_default():
  assert True
```

    1/1 tests passed
