
## 1. Cosmetics, chemicals... it's complicated
<p>Whenever I want to try a new cosmetic item, it's so difficult to choose. It's actually more than difficult. It's sometimes scary because new items that I've never tried end up giving me skin trouble. We know the information we need is on the back of each product, but it's really hard to interpret those ingredient lists unless you're a chemist. You may be able to relate to this situation.</p>
<p><img src="https://assets.datacamp.com/production/project_695/img/image_1.png" style="width:600px;height:400px;"></p>
<p>So instead of buying and hoping for the best, why don't we use data science to help us predict which products may be good fits for us? In this notebook, we are going to create a content-based recommendation system where the 'content' will be the chemical components of cosmetics. Specifically, we will process ingredient lists for 1472 cosmetics on Sephora via <a href="https://en.wikipedia.org/wiki/Word_embedding">word embedding</a>, then visualize ingredient similarity using a machine learning method called t-SNE and an interactive visualization library called Bokeh. Let's inspect our data first.</p>


```python
# Import libraries
import pandas as pd
import numpy as np
from sklearn.manifold import TSNE

# Load the data
df = pd.read_csv("datasets/cosmetics.csv")

# Check the first five rows
display(df.sample(5))

# Inspect the types of products
display(df['Label'].value_counts())
```


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Label</th>
      <th>Brand</th>
      <th>Name</th>
      <th>Price</th>
      <th>Rank</th>
      <th>Ingredients</th>
      <th>Combination</th>
      <th>Dry</th>
      <th>Normal</th>
      <th>Oily</th>
      <th>Sensitive</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>930</th>
      <td>Face Mask</td>
      <td>DIOR</td>
      <td>Hydra Life Jelly Sleeping Mask</td>
      <td>69</td>
      <td>4.4</td>
      <td>Visit the Dior boutique</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1455</th>
      <td>Sun protect</td>
      <td>COOLA</td>
      <td>Mineral Sport Sunscreen Stick SPF 50</td>
      <td>26</td>
      <td>3.1</td>
      <td>*Certified Organic</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1204</th>
      <td>Eye cream</td>
      <td>FOREO</td>
      <td>IRIS™ Illuminating Eye Massager</td>
      <td>139</td>
      <td>3.5</td>
      <td>Visit the Foreo boutique</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>335</th>
      <td>Cleanser</td>
      <td>TATA HARPER</td>
      <td>Regenerating Cleanser</td>
      <td>42</td>
      <td>4.2</td>
      <td>*Ingredients from organic farming. **Clinical ...</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>630</th>
      <td>Treatment</td>
      <td>KIEHL'S SINCE 1851</td>
      <td>Hydro-Plumping Re-Texturizing Serum Concentrate</td>
      <td>59</td>
      <td>4.7</td>
      <td>Water, Glycerin, Dimethicone, Propanediol, Dim...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>



    Moisturizer    298
    Cleanser       281
    Face Mask      266
    Treatment      248
    Eye cream      209
    Sun protect    170
    Name: Label, dtype: int64



```python
%%nose
# %%nose needs to be included at the beginning of every @tests cell

# One or more tests of the student's code
# The @solution should pass the tests
# The purpose of the tests is to try to catch common errors and
# to give the student a hint on how to resolve these errors

# last_output = _

def strip_comment_lines(cell_input):
    """Returns cell input string with comment lines removed."""
    return '\n'.join(line for line in cell_input.splitlines() if not line.startswith('#'))

last_input = strip_comment_lines(In[-2])

def test_importing_library():
    assert 'pd' in globals(), 'Did you import the pandas library aliased as pd?'
    assert 'np' in globals(), 'Did you import the numpy library aliased as np?'
    assert 'TSNE' in globals(), 'Did you import the TSNE from sklearn.manifold library?'

def test_importing_data():
    correct_df = pd.read_csv('datasets/cosmetics.csv')
    assert correct_df.equals(df), 'The DataFrame df should contain the data in cosmetics.csv.'

def test_sample_command():
    assert 'df.sample(' in last_input, \
        "Did you use the sample() method to inspect the data?"

def test_sample_command():
    assert 'df.Label.value_counts()' in last_input or "df['Label'].value_counts()" in last_input, \
        "Did you use the value_counts() method on df.Label (or df['Label']) to inspect the cosmetic category counts?"

# def test_head_output():
#     try:
#         assert ("Label" in last_output.to_string() and len(last_output) == 5)
#     except AttributeError:
#         assert False, \
#             "Please use df.sample() as the last line of code in the cell to inspect the data, not the display() or print() functions."
#     except AssertionError:
#         assert False, \
#             "Hmm, the output of the cell is not what we expected. You should see Label as the first column of the df DataFrame, which should have five rows displayed."
```






    3/3 tests passed




## 2. Focus on one product category and one skin type
<p>There are six categories of product in our data (<strong><em>moisturizers, cleansers, face masks, eye creams</em></strong>, and <strong><em>sun protection</em></strong>) and there are five different skin types (<strong><em>combination, dry, normal, oily</em></strong> and <strong><em>sensitive</em></strong>). Because individuals have different product needs as well as different skin types, let's set up our workflow so its outputs (a t-SNE model and a visualization of that model) can be customized. For the example in this notebook, let's focus in on moisturizers for those with dry skin by filtering the data accordingly.</p>


```python
# Filter for moisturizers
moisturizers = df[df['Label'] == "Moisturizer"]

# Filter for dry skin as well
moisturizers_dry = moisturizers[moisturizers["Dry"] == 1]

# Reset index
moisturizers_dry = moisturizers_dry.reset_index(drop=True)
```


```python
%%nose
# %%nose needs to be included at the beginning of every @tests cell

# One or more tests of the student's code
# The @solution should pass the tests
# The purpose of the tests is to try to catch common errors and
# to give the student a hint on how to resolve these errors

correct_moisturizers = df[df['Label'] == 'Moisturizer']

def test_columns_list():
    assert list(moisturizers_dry.columns) == ['Label', 'Brand', 'Name', 'Price', 'Rank', 'Ingredients', 'Combination', 'Dry', 'Normal', 'Oily', 'Sensitive'], \
    'At least one column name is incorrect or out of order.'

def test_moisturizers():
    assert correct_moisturizers.equals(moisturizers), 'The intermediate moisturizers DataFrame does not contain the data in cosmetics.csv filtered for the label "Moisturizer".'

# def test_moisturizers_dry():
#     correct_moisturizers_dry = correct_moisturizers[correct_moisturizers['Dry'] == 1]
#     correct_moisturizers_dry.reset_index(drop = True)
#     assert correct_moisturizers_dry.equals(moisturizers_dry), 'The moisturizers_dry DataFrame does not contain the data in cosmetics.csv filtered for the label "Moisturizer" then for 1 in the "Dry" column, with the index reset.'

def test_index():
    assert (moisturizers_dry.index == range(0, 190, 1)).all(), \
    'Did you filter the moisturizers DataFrame for 1 in the "Dry" column, then reset the index of the DataFrame? The index should range from 0 to 189.'
```






    3/3 tests passed




## 3. Tokenizing the ingredients
<p>To get to our end goal of comparing ingredients in each product, we first need to do some preprocessing tasks and bookkeeping of the actual words in each product's ingredients list. The first step will be tokenizing the list of ingredients in <code>Ingredients</code> column. After splitting them into tokens, we'll make a binary bag of words. Then we will create a dictionary with the tokens, <code>ingredient_idx</code>, which will have the following format:</p>
<p>{ <strong><em>"ingredient"</em></strong>: index value, … }</p>


```python
# Initialize dictionary, list, and initial index
ingredient_idx = {}
corpus = []
idx = 0

# For loop for tokenization
for i in range(len(moisturizers_dry)):
    ingredients = moisturizers_dry['Ingredients'][i]
    ingredients_lower = ingredients.lower()
    tokens = ingredients_lower.split(', ')
    corpus.append(tokens)
    for ingredient in tokens:
        if ingredient not in ingredient_idx:
            ingredient_idx[ingredient ] = idx
            idx += 1

# Check the result
print("The index for decyl oleate is", ingredient_idx['decyl oleate'])
```

    The index for decyl oleate is 25



```python
%%nose

def test_ingredient_idx_len():
    assert len(ingredient_idx) == 2233, \
    'The length of ingredient_idx should be 2233, but it isn\'t.'

def test_ingredient_idx_content():
    assert [ingredient_idx['paraffin'], ingredient_idx['niacin'], ingredient_idx['water']] == [20, 22, 23], \
    'The items of ingredient_idx are not what we expected. Did you correctly index each token?'

def test_corpus_len():
    assert (len(corpus) == 190), \
    'The length of corpus should be 190, but it isn\'t.'

def test_output_index():
    assert ingredient_idx['decyl oleate'] == 25, \
    'The integer in decyl_oleate_index is not what we expected. Please check if you have correctly input the ingredient.'
```






    4/4 tests passed




## 4. Initializing a document-term matrix (DTM)
<p>The next step is making a document-term matrix (DTM). Here each cosmetic product will correspond to a document, and each chemical composition will correspond to a term. This means we can think of the matrix as a <em>“cosmetic-ingredient”</em> matrix. The size of the matrix should be as the picture shown below.
<img src="https://assets.datacamp.com/production/project_695/img/image_2.PNG" style="width:600px;height:250px;">
To create this matrix, we'll first make an empty matrix filled with zeros. The length of the matrix is the total number of cosmetic products in the data. The width of the matrix is the total number of ingredients. After initializing this empty matrix, we'll fill it in the following tasks. </p>


```python
# Get the number of items and tokens
M = moisturizers_dry.shape[0]
N = len(ingredient_idx)

# Initialize a matrix of zeros
A = np.zeros((M, N))
```


```python
%%nose
# %%nose needs to be included at the beginning of every @tests cell

def test_M_num():
    assert M == 190, 'The value of M is incorrect. It should be 190.'

def test_N_num():
    assert N == 2233, 'The value of N is incorrect. It should be 2233.'

def test_A_zeros():
    assert np.sum(A) == 0, 'The values of A do not all sum to 0 and they should.'

def test_A_shape():
    assert A.shape == (190, 2233), 'The shape of the matrix A is not what we expected. It should be (190, 2233).'
```






    4/4 tests passed




## 5. Creating a counter function
<p>Before we can fill the matrix, let's create a function to count the tokens (i.e., an ingredients list) for each row. Our end goal is to fill the matrix with 1 or 0: if an ingredient is in a cosmetic, the value is 1. If not, it remains 0. The name of this function, <code>oh_encoder</code>, will become clear next.</p>


```python
# Define the oh_encoder function
def oh_encoder(tokens):
    x = np.zeros(N)
    for ingredient in tokens:
        # Get the index for each ingredient
        idx = ingredient_idx[ingredient]
        # Put 1 at the corresponding indices
        x[idx] = 1
    return x
```


```python
%%nose
# %%nose needs to be included at the beginning of every tests cell

# First three values by the correctly defined function
temp = np.asarray(range(2233))
answer = [861, 282, 4077]

def test_oh_encoder():
    submit = [np.dot(oh_encoder(corpus[i]), temp) for i in range(3)]
    assert answer == submit, \
    'The function is not correctly defined. The oh_encoder() function with the input values 1 through 5 should return the following results: 42, 7, 58, 78, 82.'
```






    1/1 tests passed




## 6. The Cosmetic-Ingredient matrix!
<p>Now we'll apply the <code>oh_encoder()</code> functon to the tokens in <code>corpus</code> and set the values at each row of this matrix. So the result will tell us what ingredients each item is composed of. For example, if a cosmetic item contains <em>water, niacin, decyl aleate</em> and <em>sh-polypeptide-1</em>, the outcome of this item will be as follows.
<img src="https://assets.datacamp.com/production/project_695/img/image_3.PNG" style="width:800px;height:400px;">
This is what we called one-hot encoding. By encoding each ingredient in the items, the <em>Cosmetic-Ingredient</em> matrix will be filled with binary values. </p>


```python
# Make a document-term matrix
i = 0
for tokens in corpus:
    A[i, :] = oh_encoder(tokens)
    i += 1
```


```python
%%nose
# %%nose needs to be included at the beginning of every @tests cell

correct_A = np.zeros((M, N))
i = 0
for tokens in corpus:
    correct_A[i, :] = oh_encoder(tokens)
    i += 1

def test_A_matrix():
    assert (correct_A == A).all(), \
    'The contents of A are not what we expected. Please reread the instructions and check the hint if necessary.'
```






    1/1 tests passed




## 7. Dimension reduction with t-SNE
<p>The dimensions of the existing matrix is (190, 2233), which means there are 2233 features in our data. For visualization, we should downsize this into two dimensions. We'll use t-SNE for reducing the dimension of the data here.</p>
<p><strong><a href="https://en.wikipedia.org/wiki/T-distributed_stochastic_neighbor_embedding">T-distributed Stochastic Neighbor Embedding (t-SNE)</a></strong> is a nonlinear dimensionality reduction technique that is well-suited for embedding high-dimensional data for visualization in a low-dimensional space of two or three dimensions. Specifically, this technique can reduce the dimension of data while keeping the similarities between the instances. This enables us to make a plot on the coordinate plane, which can be said as vectorizing. All of these cosmetic items in our data will be vectorized into two-dimensional coordinates, and the distances between the points will indicate the similarities between the items. </p>


```python
# Dimension reduction with t-SNE
model = TSNE(n_components=2, learning_rate=200, random_state=42)
tsne_features = model.fit_transform(A)

# Make X, Y columns
moisturizers_dry['X'] = tsne_features[:, 0]
moisturizers_dry['Y'] = tsne_features[:, 1]
```


```python
%%nose
# %%nose needs to be included at the beginning of every @tests cell

def test_tsne_features_shape():
    assert tsne_features.shape == (190, 2), \
    'The shape of tsne_features is not what we expected. It should be (190, 2).'

#answer = '12.48590'
answer = '-0.42638'
def test_tsne_features_value():
    assert '%.5f' % tsne_features[:3].sum() == answer, \
    'The values of tsne_features are not what we expected. Please check the parameters of the model again.'

def test_X_Y_values():
    assert (tsne_features[:, 0] == moisturizers_dry['X']).all(), 'The values for X in moisturizers_dry are not what we expected. Did you correctly assign the columns of tsne_features?'
    assert (tsne_features[:, 1] == moisturizers_dry['Y']).all(), 'The values for Y in moisturizers_dry are not what we expected. Did you correctly assign the columns of tsne_features?'
```






    3/3 tests passed




## 8. Let's map the items with Bokeh
<p>We are now ready to start creating our plot. With the t-SNE values, we can plot all our items on the coordinate plane. And the coolest part here is that it will also show us the name, the brand, the price and the rank of each item. Let's make a scatter plot using Bokeh and add a hover tool to show that information. Note that we won't display the plot yet as we will make some more additions to it.</p>


```python
from bokeh.io import show, output_notebook, push_notebook
from bokeh.plotting import figure
from bokeh.models import ColumnDataSource, HoverTool
output_notebook()

# Make a source and a scatter plot
source = ColumnDataSource(moisturizers_dry)
plot = figure(x_axis_label = 'T-SNE 1',
              y_axis_label = 'T-SNE 2',
              width = 500, height = 400)
plot.circle(x = 'X',
    y = 'Y',
    source = source,
    size = 10, color = '#FF7373', alpha = .8)
```



    <div class="bk-root">
        <a href="https://bokeh.pydata.org" target="_blank" class="bk-logo bk-logo-small bk-logo-notebook"></a>
        <span id="1109">Loading BokehJS ...</span>
    </div>







<div style="display: table;"><div style="display: table-row;"><div style="display: table-cell;"><b title="bokeh.models.renderers.GlyphRenderer">GlyphRenderer</b>(</div><div style="display: table-cell;">id&nbsp;=&nbsp;'1148', <span id="1151" style="cursor: pointer;">&hellip;)</span></div></div><div class="1150" style="display: none;"><div style="display: table-cell;"></div><div style="display: table-cell;">data_source&nbsp;=&nbsp;ColumnDataSource(id='1110', ...),</div></div><div class="1150" style="display: none;"><div style="display: table-cell;"></div><div style="display: table-cell;">glyph&nbsp;=&nbsp;Circle(id='1146', ...),</div></div><div class="1150" style="display: none;"><div style="display: table-cell;"></div><div style="display: table-cell;">hover_glyph&nbsp;=&nbsp;None,</div></div><div class="1150" style="display: none;"><div style="display: table-cell;"></div><div style="display: table-cell;">js_event_callbacks&nbsp;=&nbsp;{},</div></div><div class="1150" style="display: none;"><div style="display: table-cell;"></div><div style="display: table-cell;">js_property_callbacks&nbsp;=&nbsp;{},</div></div><div class="1150" style="display: none;"><div style="display: table-cell;"></div><div style="display: table-cell;">level&nbsp;=&nbsp;'glyph',</div></div><div class="1150" style="display: none;"><div style="display: table-cell;"></div><div style="display: table-cell;">muted&nbsp;=&nbsp;False,</div></div><div class="1150" style="display: none;"><div style="display: table-cell;"></div><div style="display: table-cell;">muted_glyph&nbsp;=&nbsp;None,</div></div><div class="1150" style="display: none;"><div style="display: table-cell;"></div><div style="display: table-cell;">name&nbsp;=&nbsp;None,</div></div><div class="1150" style="display: none;"><div style="display: table-cell;"></div><div style="display: table-cell;">nonselection_glyph&nbsp;=&nbsp;Circle(id='1147', ...),</div></div><div class="1150" style="display: none;"><div style="display: table-cell;"></div><div style="display: table-cell;">selection_glyph&nbsp;=&nbsp;None,</div></div><div class="1150" style="display: none;"><div style="display: table-cell;"></div><div style="display: table-cell;">subscribed_events&nbsp;=&nbsp;[],</div></div><div class="1150" style="display: none;"><div style="display: table-cell;"></div><div style="display: table-cell;">tags&nbsp;=&nbsp;[],</div></div><div class="1150" style="display: none;"><div style="display: table-cell;"></div><div style="display: table-cell;">view&nbsp;=&nbsp;CDSView(id='1149', ...),</div></div><div class="1150" style="display: none;"><div style="display: table-cell;"></div><div style="display: table-cell;">visible&nbsp;=&nbsp;True,</div></div><div class="1150" style="display: none;"><div style="display: table-cell;"></div><div style="display: table-cell;">x_range_name&nbsp;=&nbsp;'default',</div></div><div class="1150" style="display: none;"><div style="display: table-cell;"></div><div style="display: table-cell;">y_range_name&nbsp;=&nbsp;'default')</div></div></div>
<script>
(function() {
  var expanded = false;
  var ellipsis = document.getElementById("1151");
  ellipsis.addEventListener("click", function() {
    var rows = document.getElementsByClassName("1150");
    for (var i = 0; i < rows.length; i++) {
      var el = rows[i];
      el.style.display = expanded ? "none" : "table-row";
    }
    ellipsis.innerHTML = expanded ? "&hellip;)" : "&lsaquo;&lsaquo;&lsaquo;";
    expanded = !expanded;
  });
})();
</script>





```python
%%nose
# %%nose needs to be included at the beginning of every @tests cell

last_output = _

from bokeh.io import curdoc
curdoc().add_root(plot)

def test_source():
    assert (last_output.data_source.data['Label'] == 'Moisturizer').all() & (last_output.data_source.data['Dry'] == 1).all(), \
    "The ColumnDataSource for plot.circle() should be moisturizers_dry."

def test_x_plot_correct():
    assert curdoc().to_json_string().find('"x":{"field":"X"}') >=0, \
    "The x-argument for plot.circle() should be 'X' and it isn't."

def test_y_plot_correct():
    assert curdoc().to_json_string().find('"y":{"field":"Y"}') >= 0, \
    "The y-argument for plot.circle() should be 'Y' and it isn't."

def test_bokeh_visible():
    assert last_output.visible == True, \
    'A plot was not the last output of the cell.'
```






    4/4 tests passed




## 9. Adding a hover tool
<p>Why don't we add a hover tool? Adding a hover tool allows us to check the information of each item whenever the cursor is directly over a glyph. We'll add tooltips with each product's name, brand, price, and rank (i.e., rating).</p>


```python
# Create a HoverTool object
hover = HoverTool(tooltips = [('Item', '@Name'),
                              ('Brand', '@Brand'),
                              ('Price', '$@Price'),
                              ('Rank', '@Rank')])
plot.add_tools(hover)
```


```python
%%nose
# %%nose needs to be included at the beginning of every @tests cell
import bokeh

from bokeh.io import curdoc
curdoc().add_root(plot)

def test_hover_exists():
    assert type(hover) == bokeh.models.tools.HoverTool, \
    "The variable hover does not contain a HoverlTool object."

correct_hover_tooltips = [('Item', '@Name'),
 ('Brand', '@Brand'),
 ('Price', '$@Price'),
 ('Rank', '@Rank')]

def test_hover_correct():
    assert hover.tooltips == correct_hover_tooltips, \
    "hover is not created correctly. Please reread the instructions and check the hint if necessary."

def test_hover_plot_correct():
    assert curdoc().to_json_string().find('"tooltips":[["Item","@Name"],["Brand","@Brand"],["Price","$@Price"],["Rank","@Rank"]]'), \
    "The hover tool wasn't added to the plot correctly. Please reread the instructions and check the hint if necessary."
```






    3/3 tests passed




## 10. Mapping the cosmetic items
<p>Finally, it's show time! Let's see how the map we've made looks like. Each point on the plot corresponds to the cosmetic items. Then what do the axes mean here? The axes of a t-SNE plot aren't easily interpretable in terms of the original data. Like mentioned above, t-SNE is a visualizing technique to plot high-dimensional data in a low-dimensional space. Therefore, it's not desirable to interpret a t-SNE plot quantitatively.</p>
<p>Instead, what we can get from this map is the distance between the points (which items are close and which are far apart). The closer the distance between the two items is, the more similar the composition they have. Therefore this enables us to compare the items without having any chemistry background.</p>


```python
# Plot the map
show(plot)
```








  <div class="bk-root" id="4f2e4618-1e27-477a-ba21-8d73fd74664e" data-root-id="1111"></div>






```python
%%nose
# %%nose needs to be included at the beginning of every @tests cell

def strip_comment_lines(cell_input):
    """Returns cell input string with comment lines removed."""
    return '\n'.join(line for line in cell_input.splitlines() if not line.startswith('#'))

last_input = strip_comment_lines(In[-2])
last_output = _

def test_command_syntax():
    assert 'show(plot)' in last_input, \
        "Did you call the show() function on the plot variable?"
```






    1/1 tests passed




## 11. Comparing two products
<p>Since there are so many cosmetics and so many ingredients, the plot doesn't have many super obvious patterns that simpler t-SNE plots can have (<a href="https://campus.datacamp.com/courses/unsupervised-learning-in-python/visualization-with-hierarchical-clustering-and-t-sne?ex=10">example</a>). Our plot requires some digging to find insights, but that's okay!</p>
<p>Say we enjoyed a specific product, there's an increased chance we'd enjoy another product that is similar in chemical composition.  Say we enjoyed AmorePacific's <a href="https://sephora.com/product/color-control-cushion-compact-broad-spectrum-spf-50-P378121">Color Control Cushion Compact Broad Spectrum SPF 50+</a>. We could find this product on the plot and see if a similar product(s) exist. And it turns out it does! If we look at the points furthest left on the plot, we see  LANEIGE's <a href="https://sephora.com/product/bb-cushion-hydra-radiance-P420676">BB Cushion Hydra Radiance SPF 50</a> essentially overlaps with the AmorePacific product. By looking at the ingredients, we can visually confirm the compositions of the products are similar (<em>though it is difficult to do, which is why we did this analysis in the first place!</em>), plus LANEIGE's version is $22 cheaper and actually has higher ratings.</p>
<p>It's not perfect, but it's useful. In real life, we can actually use our little ingredient-based recommendation engine help us make educated cosmetic purchase choices.</p>


```python
# Print the ingredients of two similar cosmetics
cosmetic_1 = moisturizers_dry[moisturizers_dry['Name'] == "Color Control Cushion Compact Broad Spectrum SPF 50+"]
cosmetic_2 = moisturizers_dry[moisturizers_dry['Name'] == "BB Cushion Hydra Radiance SPF 50"]

# Display each item's data and ingredients
display(cosmetic_1)
print(cosmetic_1.Ingredients.values)
display(cosmetic_2)
print(cosmetic_2.Ingredients.values)
```


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Label</th>
      <th>Brand</th>
      <th>Name</th>
      <th>Price</th>
      <th>Rank</th>
      <th>Ingredients</th>
      <th>Combination</th>
      <th>Dry</th>
      <th>Normal</th>
      <th>Oily</th>
      <th>Sensitive</th>
      <th>X</th>
      <th>Y</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>45</th>
      <td>Moisturizer</td>
      <td>AMOREPACIFIC</td>
      <td>Color Control Cushion Compact Broad Spectrum S...</td>
      <td>60</td>
      <td>4.0</td>
      <td>Phyllostachis Bambusoides Juice, Cyclopentasil...</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>2.775364</td>
      <td>-0.274434</td>
    </tr>
  </tbody>
</table>
</div>


    ['Phyllostachis Bambusoides Juice, Cyclopentasiloxane, Cyclohexasiloxane, Peg-10 Dimethicone, Phenyl Trimethicone, Butylene Glycol, Butylene Glycol Dicaprylate/Dicaprate, Alcohol, Arbutin, Lauryl Peg-9 Polydimethylsiloxyethyl Dimethicone, Acrylates/Ethylhexyl Acrylate/Dimethicone Methacrylate Copolymer, Polyhydroxystearic Acid, Sodium Chloride, Polymethyl Methacrylate, Aluminium Hydroxide, Stearic Acid, Disteardimonium Hectorite, Triethoxycaprylylsilane, Ethylhexyl Palmitate, Lecithin, Isostearic Acid, Isopropyl Palmitate, Phenoxyethanol, Polyglyceryl-3 Polyricinoleate, Acrylates/Stearyl Acrylate/Dimethicone Methacrylate Copolymer, Dimethicone, Disodium Edta, Trimethylsiloxysilicate, Ethylhexyglycerin, Dimethicone/Vinyl Dimethicone Crosspolymer, Water, Silica, Camellia Japonica Seed Oil, Camillia Sinensis Leaf Extract, Caprylyl Glycol, 1,2-Hexanediol, Fragrance, Titanium Dioxide, Iron Oxides (Ci 77492, Ci 77491, Ci77499).']



<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Label</th>
      <th>Brand</th>
      <th>Name</th>
      <th>Price</th>
      <th>Rank</th>
      <th>Ingredients</th>
      <th>Combination</th>
      <th>Dry</th>
      <th>Normal</th>
      <th>Oily</th>
      <th>Sensitive</th>
      <th>X</th>
      <th>Y</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>55</th>
      <td>Moisturizer</td>
      <td>LANEIGE</td>
      <td>BB Cushion Hydra Radiance SPF 50</td>
      <td>38</td>
      <td>4.3</td>
      <td>Water, Cyclopentasiloxane, Zinc Oxide (CI 7794...</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>2.814905</td>
      <td>-0.277909</td>
    </tr>
  </tbody>
</table>
</div>


    ['Water, Cyclopentasiloxane, Zinc Oxide (CI 77947), Ethylhexyl Methoxycinnamate, PEG-10 Dimethicone, Cyclohexasiloxane, Phenyl Trimethicone, Iron Oxides (CI 77492), Butylene Glycol Dicaprylate/Dicaprate, Niacinamide, Lauryl PEG-9 Polydimethylsiloxyethyl Dimethicone, Acrylates/Ethylhexyl Acrylate/Dimethicone Methacrylate Copolymer, Titanium Dioxide (CI 77891 , Iron Oxides (CI 77491), Butylene Glycol, Sodium Chloride, Iron Oxides (CI 77499), Aluminum Hydroxide, HDI/Trimethylol Hexyllactone Crosspolymer, Stearic Acid, Methyl Methacrylate Crosspolymer, Triethoxycaprylylsilane, Phenoxyethanol, Fragrance, Disteardimonium Hectorite, Caprylyl Glycol, Yeast Extract, Acrylates/Stearyl Acrylate/Dimethicone Methacrylate Copolymer, Dimethicone, Trimethylsiloxysilicate, Polysorbate 80, Disodium EDTA, Hydrogenated Lecithin, Dimethicone/Vinyl Dimethicone Crosspolymer, Mica (CI 77019), Silica, 1,2-Hexanediol, Polypropylsilsesquioxane, Chenopodium Quinoa Seed Extract, Magnesium Sulfate, Calcium Chloride, Camellia Sinensis Leaf Extract, Manganese Sulfate, Zinc Sulfate, Ascorbyl Glucoside.']



```python
%%nose

def test_nothing():
    assert True, "Just run the cell! :)"
```






    1/1 tests passed



