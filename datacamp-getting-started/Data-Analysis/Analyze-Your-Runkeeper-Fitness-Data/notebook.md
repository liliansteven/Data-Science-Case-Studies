## 1. Obtain and review raw data
<p>One day, my old running friend and I were chatting about our running styles, training habits, and achievements, when I suddenly realized that I could take an in-depth analytical look at my training. I have been using a popular GPS fitness tracker called <a href="https://runkeeper.com/">Runkeeper</a> for years and decided it was time to analyze my running data to see how I was doing.</p>
<p>Since 2012, I've been using the Runkeeper app, and it's great. One key feature: its excellent data export. Anyone who has a smartphone can download the app and analyze their data like we will in this notebook.</p>
<p><img src="https://assets.datacamp.com/production/project_727/img/runner_in_blue.jpg" alt="Runner in blue" title="Explore world, explore your data!"></p>
<p>After logging your run, the first step is to export the data from Runkeeper (which I've done already). Then import the data and start exploring to find potential problems. After that, create data cleaning strategies to fix the issues. Finally, analyze and visualize the clean time-series data.</p>
<p>I exported seven years worth of my training data, from 2012 through 2018. The data is a CSV file where each row is a single training activity. Let's load and inspect it.</p>

```python
# Import pandas
import pandas as pd

# Define file containing dataset
runkeeper_file = 'datasets/cardioActivities.csv'

# Create DataFrame with parse_dates and index_col parameters
df_activities = pd.read_csv(runkeeper_file, parse_dates=True, index_col='Date')

# First look at exported data: select sample of 3 random rows
display(df_activities.sample(3))

# Print DataFrame summary
df_activities.info()
```

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Activity Id</th>
      <th>Type</th>
      <th>Route Name</th>
      <th>Distance (km)</th>
      <th>Duration</th>
      <th>Average Pace</th>
      <th>Average Speed (km/h)</th>
      <th>Calories Burned</th>
      <th>Climb (m)</th>
      <th>Average Heart Rate (bpm)</th>
      <th>Friend's Tagged</th>
      <th>Notes</th>
      <th>GPX File</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2017-01-23 18:39:10</th>
      <td>9a35d26a-e947-4374-b411-a28c07f0b153</td>
      <td>Running</td>
      <td>NaN</td>
      <td>11.98</td>
      <td>1:07:49</td>
      <td>5:40</td>
      <td>10.60</td>
      <td>850.0</td>
      <td>100</td>
      <td>150.0</td>
      <td>NaN</td>
      <td>TomTom MySports Watch</td>
      <td>2017-01-23-183910.gpx</td>
    </tr>
    <tr>
      <th>2014-05-12 18:06:22</th>
      <td>07034064-71cd-449e-9e4e-04320cc46555</td>
      <td>Running</td>
      <td>NaN</td>
      <td>12.63</td>
      <td>1:01:22</td>
      <td>4:51</td>
      <td>12.35</td>
      <td>906.0</td>
      <td>69</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2014-05-12-180622.gpx</td>
    </tr>
    <tr>
      <th>2014-09-04 18:55:54</th>
      <td>1c1779d8-5020-4bb9-b0ad-1e1f886afd46</td>
      <td>Running</td>
      <td>NaN</td>
      <td>9.61</td>
      <td>50:22</td>
      <td>5:14</td>
      <td>11.45</td>
      <td>690.0</td>
      <td>54</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2014-09-04-185554.gpx</td>
    </tr>
  </tbody>
</table>

    <class 'pandas.core.frame.DataFrame'>
    DatetimeIndex: 508 entries, 2018-11-11 14:05:12 to 2012-08-22 18:53:54
    Data columns (total 13 columns):
    Activity Id                 508 non-null object
    Type                        508 non-null object
    Route Name                  1 non-null object
    Distance (km)               508 non-null float64
    Duration                    508 non-null object
    Average Pace                508 non-null object
    Average Speed (km/h)        508 non-null float64
    Calories Burned             508 non-null float64
    Climb (m)                   508 non-null int64
    Average Heart Rate (bpm)    294 non-null float64
    Friend's Tagged             0 non-null float64
    Notes                       231 non-null object
    GPX File                    504 non-null object
    dtypes: float64(5), int64(1), object(7)
    memory usage: 55.6+ KB

```python
# One or more tests of the student's code
# The @solution should pass the tests
# The purpose of the tests is to try to catch common errors and
# to give the student a hint on how to resolve these errors

def test_pandas_loaded():
    assert 'pd' in globals(), \
    'Did you import the pandas library aliased as pd?'

def test_activities_correctly_loaded():
    correct_activities = pd.read_csv(runkeeper_file,  parse_dates=True, index_col='Date')
    assert correct_activities.equals(df_activities), \
    "The variable df_activities should contain data read from runkeeper_file with dates parsed and the index column set to date."

def strip_comment_lines(cell_input):
    """Returns cell input string with comment lines removed."""
    return '\n'.join(line for line in cell_input.splitlines() if not line.startswith('#'))

last_input = strip_comment_lines(In[-2])

def test_sample_command():
    assert ('df_activities.sample(n=3)' in last_input) or ('df_activities.sample(3)' in last_input), \
        "We expected the sample() method with the n parameter set to 3 in your input."

def test_info_command():
    assert 'df_activities.info()' in last_input, \
        "We expected the info() method to be called on df_activities in your input."
```

    4/4 tests passed

## 2. Data preprocessing
<p>Lucky for us, the column names Runkeeper provides are informative, and we don't need to rename any columns.</p>
<p>But, we do notice missing values using the <code>info()</code> method. What are the reasons for these missing values? It depends. Some heart rate information is missing because I didn't always use a cardio sensor. In the case of the <code>Notes</code> column, it is an optional field that I sometimes left blank. Also, I only used the <code>Route Name</code> column once, and never used the <code>Friend's Tagged</code> column.</p>
<p>We'll fill in missing values in the heart rate column to avoid misleading results later, but right now, our first data preprocessing steps will be to:</p>
<ul>
<li>Remove columns not useful for our analysis.</li>
<li>Replace the "Other" activity type to "Unicycling" because that was always the "Other" activity.</li>
<li>Count missing values.</li>
</ul>

```python
# Define list of columns to be deleted
cols_to_drop = ['Friend\'s Tagged','Route Name','GPX File','Activity Id','Calories Burned', 'Notes']

# Delete unnecessary columns
df_activities.drop(cols_to_drop, axis=1, inplace=True)

# Count types of training activities
display(df_activities['Type'].value_counts())

# Rename 'Other' type to 'Unicycling'
df_activities['Type'] = df_activities['Type'].str.replace('Other', 'Unicycling')

# Count missing values for each column
df_activities.isnull().sum()
```

    Running    459
    Cycling     29
    Walking     18
    Other        2
    Name: Type, dtype: int64

    Type                          0
    Distance (km)                 0
    Duration                      0
    Average Pace                  0
    Average Speed (km/h)          0
    Climb (m)                     0
    Average Heart Rate (bpm)    214
    dtype: int64

```python
# One or more tests of the student's code
# The @solution should pass the tests
# The purpose of the tests is to try to catch common errors and
# to give the student a hint on how to resolve these errors

last_output = _

cols_to_drop_correct = ['Friend\'s Tagged','Route Name','GPX File','Activity Id','Calories Burned', 'Notes']

def test_columns_deleted():
    for cld in cols_to_drop_correct:
        assert cld not in list(df_activities.columns), \
        "Did you drop unnecessary columns as described in the instructions?"

def strip_comment_lines(cell_input):
    """Returns cell input string with comment lines removed."""
    return '\n'.join(line for line in cell_input.splitlines() if not line.startswith('#'))

last_input = strip_comment_lines(In[-2])

def test_values_count():
    assert "df_activities" in last_input, \
        "We expected the df_activities variable in your input."
    assert 'value_counts' in last_input, \
        "We expected the value_counts() method in your input."

def test_replace():
    assert df_activities[df_activities['Type'] == 'Unicycling']['Type'].count() == 2, \
        "The count of activities of type 'Unicycling' is incorrect."

def test_missing_output():
    try:
        assert "214" in last_output.to_string()
    except AttributeError:
        assert False, \
        "Please use isnull().sum() as the last line of code in the cell to count missing values."
    except AssertionError:
        assert False, \
        "The output of the cell is not what we expected. You should see 214 missing values."
```

    4/4 tests passed

## 3. Dealing with missing values
<p>As we can see from the last output, there are 214 missing entries for my average heart rate.</p>
<p>We can't go back in time to get those data, but we can fill in the missing values with an average value. This process is called <em>mean imputation</em>. When imputing the mean to fill in missing data, we need to consider that the average heart rate varies for different activities (e.g., walking vs. running). We'll filter the DataFrames by activity type (<code>Type</code>) and calculate each activity's mean heart rate, then fill in the missing values with those means.</p>


```python
# Calculate sample means for heart rate for each training activity type
avg_hr_run = df_activities[df_activities['Type'] == 'Running']['Average Heart Rate (bpm)'].mean()
avg_hr_cycle = df_activities[df_activities['Type'] == 'Cycling']['Average Heart Rate (bpm)'].mean()

# Split whole DataFrame into several, specific for different activities
df_run = df_activities[df_activities['Type'] == 'Running'].copy()
df_walk = df_activities[df_activities['Type'] == 'Walking'].copy()
df_cycle = df_activities[df_activities['Type'] == 'Cycling'].copy()

# Filling missing values with counted means
df_walk['Average Heart Rate (bpm)'].fillna(110, inplace=True)
df_run['Average Heart Rate (bpm)'].fillna(int(avg_hr_run), inplace=True)
df_cycle['Average Heart Rate (bpm)'].fillna(int(avg_hr_cycle), inplace=True)

# Count missing values for each column in running data
df_run.isnull().sum()
```

    Type                        0
    Distance (km)               0
    Duration                    0
    Average Pace                0
    Average Speed (km/h)        0
    Climb (m)                   0
    Average Heart Rate (bpm)    0
    dtype: int64

```python
# One or more tests of the student's code
# The @solution should pass the tests
# The purpose of the tests is to try to catch common errors and
# to give the student a hint on how to resolve these errors


last_output = _

def strip_comment_lines(cell_input):
    """Returns cell input string with comment lines removed."""
    return '\n'.join(line for line in cell_input.splitlines() if not line.startswith('#'))

last_input = strip_comment_lines(In[-2])

def test_avg_hr_cycle():
    assert avg_hr_cycle == 124.4, \
    "The value of avg_hr_rate is not what we expected. Use code similar to avg_hr_run with 'Type' == 'Cycling'."

def test_df_cycle_correct():
    assert len(df_cycle) == 29, \
    "The variable df_cycle should contain data filtered from df_activities with 'Type' == 'Cycling'."

def test_df_cycle_fillna():
    assert df_cycle['Average Heart Rate (bpm)'].isnull().sum() == 0, \
    "There are missing values in df_cycle 'Average Heart Rate (bpm)' column."

def test_isnull_output():
    try:
        assert "Average Heart Rate (bpm)    0" in last_output.to_string()
    except AttributeError:
        assert False, "'Average Heart Rate (bpm)    0' should be the output of the cell. Please do not use the print() or display() functions; ensure the isnull().sum() code is the last line of code in the cell."
    except AssertionError:
        assert False, \
        "The output of the cell is not what we expected. You should see 'Average Heart Rate (bpm)    0'."
```

    4/4 tests passed

## 4. Plot running data
<p>Now we can create our first plot! As we found earlier, most of the activities in my data were running (459 of them to be exact). There are only 29, 18, and two instances for cycling, walking, and unicycling, respectively. So for now, let's focus on plotting the different running metrics.</p>
<p>An excellent first visualization is a figure with four subplots, one for each running metric (each numerical column). Each subplot will have a different y-axis, which is explained in each legend. The x-axis, <code>Date</code>, is shared among all subplots.</p>

```python
%matplotlib inline

# Import matplotlib, set style and ignore warning
import matplotlib.pyplot as plt
%matplotlib inline
import warnings
plt.style.use('ggplot')
warnings.filterwarnings(
    action='ignore', module='matplotlib.figure', category=UserWarning,
    message=('This figure includes Axes that are not compatible with tight_layout, so results might be incorrect.')
)

# Prepare data subsetting period from 2013 till 2018
runs_subset_2013_2018 = df_run.loc['20190101':'20130101']

# Create, plot and customize in one step
runs_subset_2013_2018.plot(subplots=True,
                           sharex=False,
                           figsize=(12,16),
                           linestyle='none',
                           marker='o',
                           markersize=3)

# Show plot
plt.show()
```

![png](images/output_10_0.png)

```python
# One or more tests of the student's code
# The @solution should pass the tests
# The purpose of the tests is to try to catch common errors and
# to give the student a hint on how to resolve these errors

def strip_comment_lines(cell_input):
    """Returns cell input string with comment lines removed."""
    return '\n'.join(line for line in cell_input.splitlines() if not line.startswith('#'))

last_input = strip_comment_lines(In[-2])

# def test_set_style():
#     assert "plt.style.use('ggplot')" in last_input, \
#         "We expected the plt.style.use('ggplot') in your input."

def test_subset_correct():
    correct_subset = df_run['2018':'2013']
    assert correct_subset.equals(runs_subset_2013_2018), \
    "The data in runs_subset_2013_2018 is not what we expected."

def test_subplots_param():
    assert "subplots=True" in last_input, \
        "We expected the subplots=True in your input WITHOUT whitespaces around '=' sign."

def test_plt_show():
    assert "plt.show()" in last_input, \
        "We expected plt.show() in your input."
```

    3/3 tests passed

## 5. Running statistics
<p>No doubt, running helps people stay mentally and physically healthy and productive at any age. And it is great fun! When runners talk to each other about their hobby, we not only discuss our results, but we also discuss different training strategies. </p>
<p>You'll know you're with a group of runners if you commonly hear questions like:</p>
<ul>
<li>What is your average distance?</li>
<li>How fast do you run?</li>
<li>Do you measure your heart rate?</li>
<li>How often do you train?</li>
</ul>
<p>Let's find the answers to these questions in my data. If you look back at plots in Task 4, you can see the answer to, <em>Do you measure your heart rate?</em> Before 2015: no. To look at the averages, let's only use the data from 2015 through 2018.</p>
<p>In pandas, the <code>resample()</code> method is similar to the <code>groupby()</code> method - with <code>resample()</code> you group by a specific time span. We'll use <code>resample()</code> to group the time series data by a sampling period and apply several methods to each sampling period. In our case, we'll resample annually and weekly.</p>

```python
# Prepare running data for the last 4 years
runs_subset_2015_2018 = df_run.loc['20190101':'20150101']

# Calculate annual statistics
print('How my average run looks in last 4 years:')
display(runs_subset_2015_2018.resample('A').mean())

# Calculate weekly statistics
print('Weekly averages of last 4 years:')
display(runs_subset_2015_2018.resample('W').mean().mean())

# Mean weekly counts
weekly_counts_average = runs_subset_2015_2018['Distance (km)'].resample('W').count().mean()
print('How many trainings per week I had on average:', weekly_counts_average)
```

    How my average run looks in last 4 years:

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Distance (km)</th>
      <th>Average Speed (km/h)</th>
      <th>Climb (m)</th>
      <th>Average Heart Rate (bpm)</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2015-12-31</th>
      <td>13.602805</td>
      <td>10.998902</td>
      <td>160.170732</td>
      <td>143.353659</td>
    </tr>
    <tr>
      <th>2016-12-31</th>
      <td>11.411667</td>
      <td>10.837778</td>
      <td>133.194444</td>
      <td>143.388889</td>
    </tr>
    <tr>
      <th>2017-12-31</th>
      <td>12.935176</td>
      <td>10.959059</td>
      <td>169.376471</td>
      <td>145.247059</td>
    </tr>
    <tr>
      <th>2018-12-31</th>
      <td>13.339063</td>
      <td>10.777969</td>
      <td>191.218750</td>
      <td>148.125000</td>
    </tr>
  </tbody>
</table>

    Weekly averages of last 4 years:

    Distance (km)                12.518176
    Average Speed (km/h)         10.835473
    Climb (m)                   158.325444
    Average Heart Rate (bpm)    144.801775
    dtype: float64

    How many trainings per week I had on average: 1.5

```python
# One or more tests of the student's code
# The @solution should pass the tests
# The purpose of the tests is to try to catch common errors and
# to give the student a hint on how to resolve these errors

last_output = _

def strip_comment_lines(cell_input):
    """Returns cell input string with comment lines removed."""
    return '\n'.join(line for line in cell_input.splitlines() if not line.startswith('#'))

last_input = strip_comment_lines(In[-2])

def test_subset_correct5():
    correct_subset = df_run['2018':'2015']
    assert correct_subset.equals(runs_subset_2015_2018), \
    "The data in runs_subset_2015_2018 is not what we expected."

def test_annual_stats():
    assert "resample('A').mean()" in last_input, \
    "Did you use resample('A').mean() to count annual averages for each year?"

def test_weekly_average():
    assert "resample('W').mean().mean()" in last_input, \
    "Did you use resample('W').mean().mean() to count average weekly statistics?"

def test_weekly_count_syntax():
    assert "runs_subset_2015_2018['Distance (km)']" in last_input, \
    "Did you filter column 'Distance (km)' from data subset using single quotes?"

def test_weekly_count():
    assert weekly_counts_average == 1.5, \
    "We expected 1.5 trainings per week on average."
```

    5/5 tests passed

## 6. Visualization with averages
<p>Let's plot the long term averages of my distance run and my heart rate with their raw data to visually compare the averages to each training session. Again, we'll use the data from 2015 through 2018.</p>
<p>In this task, we will use <code>matplotlib</code> functionality for plot creation and customization.</p>

```python
# Prepare data
runs_distance = runs_subset_2015_2018['Distance (km)']
runs_hr = runs_subset_2015_2018['Average Heart Rate (bpm)']

# Create plot
fig, (ax1, ax2) = plt.subplots(2, sharex=True, figsize=(12, 8))

# Plot and customize first subplot
runs_distance.plot(ax=ax1)
ax1.set(ylabel='Distance (km)', title='Historical data with averages')
ax1.axhline(runs_distance.mean(), color='blue', linewidth=1, linestyle='-.')

# Plot and customize second subplot
runs_hr.plot(ax=ax2, color='gray')
ax2.set(xlabel='Date', ylabel='Average Heart Rate (bpm)')
ax2.axhline(runs_hr.mean(), color='blue', linewidth=1, linestyle='-.')

# Show plot
plt.show()
```

![png](images/output_16_0.png)

```python
# One or more tests of the student's code
# The @solution should pass the tests
# The purpose of the tests is to try to catch common errors and
# to give the student a hint on how to resolve these errors

def test_data_correct6():
    cor_runs_distance = runs_subset_2015_2018['Distance (km)']
    cor_runs_hr = runs_subset_2015_2018['Average Heart Rate (bpm)']
    assert (cor_runs_distance.equals(runs_distance) & cor_runs_hr.equals(runs_hr)), \
    "Did you use the correct column names to select distance and heart rate?"

def test_plot_exist6():
    assert (ax2.get_geometry()[0] == 2 and fig.get_figwidth() == 12), \
    "The size of plot and the number of subplots are not as expected."

def test_first_subplot6():
    assert all(ax1.lines[0].get_ydata() == runs_distance.sort_index()), \
    "Did you use runs_distance.plot(ax=ax1) to plot the first plot?"

def test_horline6():
    assert ax2.lines[1].get_ydata()[0] == runs_hr.mean(), \
    "The value of average heart rate is incorrect on the plot."
```

    4/4 tests passed

## 7. Did I reach my goals?
<p>To motivate myself to run regularly, I set a target goal of running 1000 km per year. Let's visualize my annual running distance (km) from 2013 through 2018 to see if I reached my goal each year. Only stars in the green region indicate success.</p>

```python
# Prepare data
df_run_dist_annual = df_run.sort_index()['20130101':'20181231']['Distance (km)'] \
                    .resample('A').sum()

# Create plot
fig = plt.figure(figsize=(8, 5))

# Plot and customize
ax = df_run_dist_annual.plot(marker='*', markersize=14, linewidth=0,
                             color='blue')
ax.set(ylim=[0, 1210],
       xlim=['2012','2019'],
       ylabel='Distance (km)',
       xlabel='Years',
       title='Annual totals for distance')

ax.axhspan(1000, 1210, color='green', alpha=0.4)
ax.axhspan(800, 1000, color='yellow', alpha=0.3)
ax.axhspan(0, 800, color='red', alpha=0.2)

# Show plot
plt.show()
```

![png](images/output_19_0.png)

```python
# One or more tests of the student's code
# The @solution should pass the tests
# The purpose of the tests is to try to catch common errors and
# to give the student a hint on how to resolve these errors

def strip_comment_lines(cell_input):
    """Returns cell input string with comment lines removed."""
    return '\n'.join(line for line in cell_input.splitlines() if not line.startswith('#'))

last_input = strip_comment_lines(In[-2])

def test_data_correct7():
    cor_run_dist_annual = df_run['2018':'2013']['Distance (km)'].resample('A').sum()
    assert cor_run_dist_annual.equals(df_run_dist_annual), \
    "The data in df_run_dist_annual is not what we expected."

def test_figsize7():
    assert (fig.get_figwidth() == 8.0 and fig.get_figheight() == 5.0), \
    "The figure size is incorrect. Did you set figsize=(8, 5) in plt.figure()?"

def test_axspan7():
    assert len(ax.patches) == 3, \
    "Did you use ax.axhspan(0, 800, ...)?"

def test_show7():
    assert 'plt.show()' in last_input , \
    "We expected plt.show() in your input."
```

    4/4 tests passed

## 8. Am I progressing?
<p>Let's dive a little deeper into the data to answer a tricky question: am I progressing in terms of my running skills? </p>
<p>To answer this question, we'll decompose my weekly distance run and visually compare it to the raw data. A red trend line will represent the weekly distance run.</p>
<p>We are going to use <code>statsmodels</code> library to decompose the weekly trend.</p>

```python
# Import required library
import statsmodels.api as sm

# Prepare data
df_run_dist_wkly = df_run.loc['20190101':'20130101']['Distance (km)'] \
                    .resample('W').bfill()
decomposed = sm.tsa.seasonal_decompose(df_run_dist_wkly,
                                       extrapolate_trend=1, freq=52)

# Create plot
fig = plt.figure(figsize=(12, 5))

# Plot and customize
ax = decomposed.trend.plot(label='Trend', linewidth=2)
ax = decomposed.observed.plot(label='Observed', linewidth=0.5)

ax.legend()
ax.set_title('Running distance trend')

# Show plot
plt.show()
```

![png](images/output_22_0.png)

```python
'''
def strip_comment_lines(cell_input):
    """Returns cell input string with comment lines removed."""
    return '\n'.join(line for line in cell_input.splitlines() if not line.startswith('#'))

last_input = strip_comment_lines(In[-2])
'''

def test_sm_imported():
    assert 'sm' in globals(), \
    "Did you import statsmodels.api aliased as sm?"

def test_data_correct8():
    cor_run_dist_wkly = df_run['2018':'2013']['Distance (km)'].resample('W').bfill()
    assert cor_run_dist_wkly.equals(df_run_dist_wkly), \
    "The data in df_run_dist_wkly is not what we expected."

def test_figsize8():
    assert (fig.get_figwidth() == 12.0 and fig.get_figheight() == 5.0), \
    "The figure size is incorrect. Did you set figsize=(12, 5) in plt.figure()?"
```

    3/3 tests passed

## 9. Training intensity
<p>Heart rate is a popular metric used to measure training intensity. Depending on age and fitness level, heart rates are grouped into different zones that people can target depending on training goals. A target heart rate during moderate-intensity activities is about 50-70% of maximum heart rate, while during vigorous physical activity it’s about 70-85% of maximum.</p>
<p>We'll create a distribution plot of my heart rate data by training intensity. It will be a visual presentation for the number of activities from predefined training zones. </p>

```python
# Prepare data
hr_zones = [100, 125, 133, 142, 151, 173]
zone_names = ['Easy', 'Moderate', 'Hard', 'Very hard', 'Maximal']
zone_colors = ['green', 'yellow', 'orange', 'tomato', 'red']
df_run_hr_all = df_run.loc['20190101':'20150301']['Average Heart Rate (bpm)']

# Create plot
fig, ax = plt.subplots(figsize=(8, 5))

# Plot and customize
n, bins, patches = ax.hist(df_run_hr_all, bins=hr_zones, alpha=0.5)
for i in range(0, len(patches)):
    patches[i].set_facecolor(zone_colors[i])

ax.set(title='Distribution of HR', ylabel='Number of runs')
ax.xaxis.set(ticks=hr_zones)
ax.set_xticklabels(labels=zone_names, rotation=-30, ha='left')

# Show plot
plt.show()
```

![png](images/output_25_0.png)

```python
def strip_comment_lines(cell_input):
    """Returns cell input string with comment lines removed."""
    return '\n'.join(line for line in cell_input.splitlines() if not line.startswith('#'))

last_input = strip_comment_lines(In[-2])

def test_data_correct9():
    corr_data = df_run['2018':'2015-03']['Average Heart Rate (bpm)']
    assert corr_data.equals(df_run_hr_all), \
    "The data in df_run_hr_all is not what we expected."

def test_subplots_used9():
    assert 'plt.subplots' in last_input, \
    "We expected plt.subplots in your input."

def test_figsize9():
    assert (fig.get_figwidth() == 8.0 and fig.get_figheight() == 5.0), \
    "The figure size is incorrect. Did you set figsize=(8, 5) in plt.subplots()?"

def test_xticklabels9():
    lbls = [lb.get_text() for lb in ax.get_xticklabels()]
    del lbls[-1]
    assert lbls == zone_names, \
    "The x-axis labels are incorrect. Did you use ax.set_xticklabels(labels=zone_names, ...) ?"

def test_show9():
    assert 'plt.show()' in last_input , \
    "We expected plt.show() in your input."
```

    5/5 tests passed

## 10. Detailed summary report
<p>With all this data cleaning, analysis, and visualization, let's create detailed summary tables of my training. </p>
<p>To do this, we'll create two tables. The first table will be a summary of the distance (km) and climb (m) variables for each training activity. The second table will list the summary statistics for the average speed (km/hr), climb (m), and distance (km) variables for each training activity.</p>

```python
# Concatenating three DataFrames
df_run_walk_cycle = df_run.append([df_walk, df_cycle]).sort_index(ascending=False)

dist_climb_cols, speed_col = ['Distance (km)', 'Climb (m)'], ['Average Speed (km/h)']

# Calculating total distance and climb in each type of activities
df_totals = df_run_walk_cycle.groupby('Type')[dist_climb_cols].sum()

print('Totals for different training types:')
display(df_totals)

# Calculating summary statistics for each type of activities
df_summary = df_run_walk_cycle.groupby('Type')[dist_climb_cols + speed_col].describe()

# Combine totals with summary
for i in dist_climb_cols:
    df_summary[i, 'total'] = df_totals[i]

print('Summary statistics for different training types:')
df_summary.stack()
```

    Totals for different training types:

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Distance (km)</th>
      <th>Climb (m)</th>
    </tr>
    <tr>
      <th>Type</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Cycling</th>
      <td>680.58</td>
      <td>6976</td>
    </tr>
    <tr>
      <th>Running</th>
      <td>5224.50</td>
      <td>57278</td>
    </tr>
    <tr>
      <th>Walking</th>
      <td>33.45</td>
      <td>349</td>
    </tr>
  </tbody>
</table>

    Summary statistics for different training types:

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Average Speed (km/h)</th>
      <th>Climb (m)</th>
      <th>Distance (km)</th>
    </tr>
    <tr>
      <th>Type</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="9" valign="top">Cycling</th>
      <th>25%</th>
      <td>16.980000</td>
      <td>139.000000</td>
      <td>15.530000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>19.500000</td>
      <td>199.000000</td>
      <td>20.300000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>21.490000</td>
      <td>318.000000</td>
      <td>29.400000</td>
    </tr>
    <tr>
      <th>count</th>
      <td>29.000000</td>
      <td>29.000000</td>
      <td>29.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>24.330000</td>
      <td>553.000000</td>
      <td>49.180000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>19.125172</td>
      <td>240.551724</td>
      <td>23.468276</td>
    </tr>
    <tr>
      <th>min</th>
      <td>11.380000</td>
      <td>58.000000</td>
      <td>11.410000</td>
    </tr>
    <tr>
      <th>std</th>
      <td>3.257100</td>
      <td>128.960289</td>
      <td>9.451040</td>
    </tr>
    <tr>
      <th>total</th>
      <td>NaN</td>
      <td>6976.000000</td>
      <td>680.580000</td>
    </tr>
    <tr>
      <th rowspan="9" valign="top">Running</th>
      <th>25%</th>
      <td>10.495000</td>
      <td>54.000000</td>
      <td>7.415000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>10.980000</td>
      <td>91.000000</td>
      <td>10.810000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>11.520000</td>
      <td>171.000000</td>
      <td>13.190000</td>
    </tr>
    <tr>
      <th>count</th>
      <td>459.000000</td>
      <td>459.000000</td>
      <td>459.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>20.720000</td>
      <td>982.000000</td>
      <td>38.320000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>11.056296</td>
      <td>124.788671</td>
      <td>11.382353</td>
    </tr>
    <tr>
      <th>min</th>
      <td>5.770000</td>
      <td>0.000000</td>
      <td>0.760000</td>
    </tr>
    <tr>
      <th>std</th>
      <td>0.953273</td>
      <td>103.382177</td>
      <td>4.937853</td>
    </tr>
    <tr>
      <th>total</th>
      <td>NaN</td>
      <td>57278.000000</td>
      <td>5224.500000</td>
    </tr>
    <tr>
      <th rowspan="9" valign="top">Walking</th>
      <th>25%</th>
      <td>5.555000</td>
      <td>7.000000</td>
      <td>1.385000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>5.970000</td>
      <td>10.000000</td>
      <td>1.485000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>6.512500</td>
      <td>15.500000</td>
      <td>1.787500</td>
    </tr>
    <tr>
      <th>count</th>
      <td>18.000000</td>
      <td>18.000000</td>
      <td>18.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>6.910000</td>
      <td>112.000000</td>
      <td>4.290000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>5.549444</td>
      <td>19.388889</td>
      <td>1.858333</td>
    </tr>
    <tr>
      <th>min</th>
      <td>1.040000</td>
      <td>5.000000</td>
      <td>1.220000</td>
    </tr>
    <tr>
      <th>std</th>
      <td>1.459309</td>
      <td>27.110100</td>
      <td>0.880055</td>
    </tr>
    <tr>
      <th>total</th>
      <td>NaN</td>
      <td>349.000000</td>
      <td>33.450000</td>
    </tr>
  </tbody>
</table>

```python
# One or more tests of the student's code
# The @solution should pass the tests
# The purpose of the tests is to try to catch common errors and
# to give the student a hint on how to resolve these errors

def strip_comment_lines(cell_input):
    """Returns cell input string with comment lines removed."""
    return '\n'.join(line for line in cell_input.splitlines() if not line.startswith('#'))

last_input = strip_comment_lines(In[-2])
last_output = _

def test_data_correct10():
    corr_data = df_run.append(df_walk).append(df_cycle).sort_index(ascending=False)
    assert corr_data.equals(df_run_walk_cycle), \
    "The data in df_run_walk_cycle is not what we expected. Did you apply sort_index(ascending=False) ?"

def test_display_totals10():
    assert 'display(df_totals)' in last_input, \
    "Did you use display(df_totals) to show the calculations?"

def test_totals10():
    corr_tot = df_totals['Distance (km)']['Running'].round(1)
    assert corr_tot == 5224.5, \
    "We expected different values for totals. You should see 5224.5 km as total distance."

def test_stack_used10():
    assert 'stack()' in last_input, \
    "Did you use stack() to create a compact view of the results?"
```

    4/4 tests passed

## 11. Fun facts
<p>To wrap up, let’s pick some fun facts out of the summary tables and solve the last exercise.</p>
<p>These data (my running history) represent 6 years, 2 months and 21 days. And I remember how many running shoes I went through–7.</p>
<pre><code>FUN FACTS
- Average distance: 11.38 km
- Longest distance: 38.32 km
- Highest climb: 982 m
- Total climb: 57,278 m
- Total number of km run: 5,224 km
- Total runs: 459
- Number of running shoes gone through: 7 pairs
</code></pre>
<p>The story of Forrest Gump is well known–the man, who for no particular reason decided to go for a "little run." His epic run duration was 3 years, 2 months and 14 days (1169 days). In the picture you can see Forrest’s route of 24,700 km.  </p>
<pre><code>FORREST RUN FACTS
- Average distance: 21.13 km
- Total number of km run: 24,700 km
- Total runs: 1169
- Number of running shoes gone through: ...
</code></pre>
<p>Assuming Forest and I go through running shoes at the same rate, figure out how many pairs of shoes Forrest needed for his run.</p>
<p><img src="https://assets.datacamp.com/production/project_727/img/Forrest_Gump_running_route.png" alt="Forrest's route" title="Little run of Forrest Gump"></p>

```python
# Count average shoes per lifetime (as km per pair) using our fun facts
average_shoes_lifetime = 5224 / 7

# Count number of shoes for Forrest's run distance
shoes_for_forrest_run = 24700 // average_shoes_lifetime

print('Forrest Gump would need {} pairs of shoes!'.format(shoes_for_forrest_run))
```

    Forrest Gump would need 33.0 pairs of shoes!

```python
def test_forrest_shoes():
    assert shoes_for_forrest_run == 33, \
    "We expected shoes_for_forrest_run to be a whole integer. Forrest would need 33 pairs."
```

    1/1 tests passed
