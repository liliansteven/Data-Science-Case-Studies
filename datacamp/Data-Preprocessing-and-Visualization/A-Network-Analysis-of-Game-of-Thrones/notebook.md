## 1. Winter is Coming. Let's load the dataset ASAP!
<p>If you haven't heard of <em>Game of Thrones</em>, then you must be really good at hiding. Game of Thrones is the hugely popular television series by HBO based on the (also) hugely popular book series <em>A Song of Ice and Fire</em> by George R.R. Martin. In this notebook, we will analyze the co-occurrence network of the characters in the  Game of Thrones books. Here, two characters are considered to co-occur if their names appear in the vicinity of 15 words from one another in the books. </p>
<p><img src="https://assets.datacamp.com/production/project_76/img/got_network.jpeg" style="width: 550px"></p>
<p>This dataset constitutes a network and is given as a text file describing the <em>edges</em> between characters, with some attributes attached to each edge. Let's start by loading in the data for the first book <em>A Game of Thrones</em> and inspect it.</p>

```python
# Importing modules
import pandas as pd

# Reading in datasets/book1.csv
book1 = pd.read_csv('datasets/book1.csv')

# Printing out the head of the dataset
book1.head()
```

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Source</th>
      <th>Target</th>
      <th>Type</th>
      <th>weight</th>
      <th>book</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Addam-Marbrand</td>
      <td>Jaime-Lannister</td>
      <td>Undirected</td>
      <td>3</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Addam-Marbrand</td>
      <td>Tywin-Lannister</td>
      <td>Undirected</td>
      <td>6</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Aegon-I-Targaryen</td>
      <td>Daenerys-Targaryen</td>
      <td>Undirected</td>
      <td>5</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Aegon-I-Targaryen</td>
      <td>Eddard-Stark</td>
      <td>Undirected</td>
      <td>4</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aemon-Targaryen-(Maester-Aemon)</td>
      <td>Alliser-Thorne</td>
      <td>Undirected</td>
      <td>4</td>
      <td>1</td>
    </tr>
  </tbody>
</table>

```python
def test_task1():
    assert len(book1) == 684, \
    'Make sure you have imported the correct book, i.e book1.csv'
```

    1/1 tests passed

## 2. Time for some Network of Thrones
<p>The resulting DataFrame <code>book1</code> has 5 columns: <code>Source</code>, <code>Target</code>, <code>Type</code>, <code>weight</code>, and <code>book</code>. Source and target are the two nodes that are linked by an edge. A network can have directed or undirected edges and in this network all the edges are undirected. The weight attribute of every edge tells us the number of interactions that the characters have had over the book, and the book column tells us the book number.</p>
<p>Once we have the data loaded as a pandas DataFrame, it's time to create a network. We will use <code>networkx</code>, a network analysis library, and create a graph object for the first book.</p>

```python
# Importing modules
import networkx as nx

# Creating an empty graph object
G_book1 = nx.Graph()
```

```python
import networkx as nx

def test_type_of_graph():
    assert isinstance(G_book1, type(nx.Graph())) , \
    'Make sure you have created an object of graph type'
```

    1/1 tests passed

## 3. Populate the network with the DataFrame
<p>Currently, the graph object <code>G_book1</code> is empty. Let's now populate it with the edges from <code>book1</code>. And while we're at it, let's load in the rest of the books too!</p>

```python
# Iterating through the DataFrame to add edges
for i, edge in book1.iterrows():
    G_book1.add_edge(edge['Source'], edge['Target'], weight=edge['weight'])

# Creating a list of networks for all the books
books = [G_book1]
book_fnames = ['datasets/book2.csv', 'datasets/book3.csv', 'datasets/book4.csv', 'datasets/book5.csv']
for book_fname in book_fnames:
    book = pd.read_csv(book_fname)
    G_book = nx.Graph()
    for _, edge in book.iterrows():
        G_book.add_edge(edge['Source'], edge['Target'], weight=edge['weight'])
    books.append(G_book)
```

```python
def test_placeholder():
    assert len(G_book1) == 187, \
    'Make sure that you have iterated through the DataFrame'
```

    1/1 tests passed

## 4. The most important character in Game of Thrones
<p>Is it Jon Snow, Tyrion, Daenerys, or someone else? Let's see! Network science offers us many different metrics to measure the importance of a node in a network. Note that there is no "correct" way of calculating the most important node in a network, every metric has a different meaning.</p>
<p>First, let's measure the importance of a node in a network by looking at the number of neighbors it has, that is, the number of nodes it is connected to. For example, an influential account on Twitter, where the follower-followee relationship forms the network, is an account which has a high number of followers. This measure of importance is called <em>degree centrality</em>.</p>
<p>Using this measure, let's extract the top ten important characters from the first book (<code>book[0]</code>) and the fifth book (<code>book[4]</code>).</p>

```python
# Calculating the degree centrality of book 1
deg_cen_book1 = nx.degree_centrality(books[0])

# Calculating the degree centrality of book 5
deg_cen_book5 = nx.degree_centrality(books[4])

# Sorting the dictionaries according to their degree centrality and storing the top 10
sorted_deg_cen_book1 = sorted(deg_cen_book1.items(), key=lambda x: x[1], reverse=True)[0:10]

# Sorting the dictionaries according to their degree centrality and storing the top 10
sorted_deg_cen_book5 = sorted(deg_cen_book5.items(), key=lambda x: x[1], reverse=True)[0:10]

# Printing out the top 10 of book1 and book5
print(sorted_deg_cen_book1)
print(sorted_deg_cen_book5)
```

    [('Eddard-Stark', 0.3548387096774194), ('Robert-Baratheon', 0.2688172043010753), ('Tyrion-Lannister', 0.24731182795698928), ('Catelyn-Stark', 0.23118279569892475), ('Jon-Snow', 0.19892473118279572), ('Robb-Stark', 0.18817204301075272), ('Sansa-Stark', 0.18817204301075272), ('Bran-Stark', 0.17204301075268819), ('Cersei-Lannister', 0.16129032258064518), ('Joffrey-Baratheon', 0.16129032258064518)]
    [('Jon-Snow', 0.1962025316455696), ('Daenerys-Targaryen', 0.18354430379746836), ('Stannis-Baratheon', 0.14873417721518986), ('Tyrion-Lannister', 0.10443037974683544), ('Theon-Greyjoy', 0.10443037974683544), ('Cersei-Lannister', 0.08860759493670886), ('Barristan-Selmy', 0.07911392405063292), ('Hizdahr-zo-Loraq', 0.06962025316455696), ('Asha-Greyjoy', 0.056962025316455694), ('Melisandre', 0.05379746835443038)]

```python
def test_task4():
    assert sorted_deg_cen_book1[0][0] == 'Eddard-Stark', \
    'Make sure you have sorted the degree centrality dictionary in the correct order'
```

    1/1 tests passed

## 5. The evolution of character importance
<p>According to degree centrality, the most important character in the first book is Eddard Stark but he is not even in the top 10 of the fifth book. The importance of characters changes over the course of five books because, you know, stuff happens… ;)</p>
<p>Let's look at the evolution of degree centrality of a couple of characters like Eddard Stark, Jon Snow, and Tyrion, which showed up in the top 10 of degree centrality in the first book.</p>

```python
%matplotlib inline

# Creating a list of degree centrality of all the books
evol = [nx.degree_centrality(book) for book in books]

# Creating a DataFrame from the list of degree centralities in all the books
degree_evol_df = pd.DataFrame.from_records(evol)

# Plotting the degree centrality evolution of Eddard-Stark, Tyrion-Lannister and Jon-Snow
degree_evol_df[['Eddard-Stark', 'Tyrion-Lannister', 'Jon-Snow']].plot();
```

![png](images/output_13_0.png)

```python
def test_task5():
    assert degree_evol_df.shape == (5, 796), \
    'Check the construction of the DataFrame degree_evol_df'
```

    1/1 tests passed

## 6. What's up with Stannis Baratheon?
<p>We can see that the importance of Eddard Stark dies off as the book series progresses. With Jon Snow, there is a drop in the fourth book but a sudden rise in the fifth book.</p>
<p>Now let's look at various other measures like <em>betweenness centrality</em> and <em>PageRank</em> to find important characters in our Game of Thrones character co-occurrence network and see if we can uncover some more interesting facts about this network. Let's plot the evolution of betweenness centrality of this network over the five books. We will take the evolution of the top four characters of every book and plot it.</p>

```python
# Creating a list of betweenness centrality of all the books just like we did for degree centrality
evol = [nx.betweenness_centrality(book, weight='weight') for book in books]

# Making a DataFrame from the list
betweenness_evol_df = pd.DataFrame.from_records(evol).fillna(0)

# Finding the top 4 characters in every book
set_of_char = set()
for i in range(5):
    set_of_char |= set(list(betweenness_evol_df.T[i].sort_values(ascending=False)[0:4].index))
list_of_char = list(set_of_char)

# Plotting the evolution of the top characters
betweenness_evol_df[list_of_char].plot(figsize=(13, 7));
```

![png](images/output_16_0.png)

```python
def test_task6():
    assert betweenness_evol_df.shape == (5, 796), \
    'Check the construction of the DataFrame betweenness_evol_df'
```

    1/1 tests passed

## 7. What does Google PageRank tell us about GoT?
<p>We see a peculiar rise in the importance of Stannis Baratheon over the books. In the fifth book, he is significantly more important than other characters in the network, even though he is the third most important character according to degree centrality.</p>
<p>PageRank was the initial way Google ranked web pages. It evaluates the inlinks and outlinks of webpages in the world wide web, which is, essentially, a directed network. Let's look at the importance of characters in the Game of Thrones network according to PageRank. </p>

```python
# Creating a list of pagerank of all the characters in all the books
evol = [nx.pagerank(book, weight='weight') for book in books]

# Making a DataFrame from the list
pagerank_evol_df = pd.DataFrame.from_records(evol)

# Finding the top 4 characters in every book
set_of_char = set()
for i in range(5):
    set_of_char |= set(list(pagerank_evol_df.T[i].sort_values(ascending=False)[0:4].index))
list_of_char = list(set_of_char)

# Plotting the top characters
pagerank_evol_df[list_of_char].plot(figsize=(13, 7));
```

![png](images/output_19_0.png)

```python
def test_task7():
    assert pagerank_evol_df.shape == (5, 796), \
    'Check the construction of the DataFrame pagerank_evol_df'
```

    1/1 tests passed

## 8. Correlation between different measures
<p>Stannis, Jon Snow, and Daenerys are the most important characters in the fifth book according to PageRank. Eddard Stark follows a similar curve but for degree centrality and betweenness centrality: He is important in the first book but dies into oblivion over the book series.</p>
<p>We have seen three different measures to calculate the importance of a node in a network, and all of them tells us something about the characters and their importance in the co-occurrence network. We see some names pop up in all three measures so maybe there is a strong correlation between them?</p>
<p>Let's look at the correlation between PageRank, betweenness centrality and degree centrality for the fifth book using Pearson correlation.</p>

```python
# Creating a list of pagerank, betweenness centrality, degree centrality
# of all the characters in the fifth book.
measures = [nx.pagerank(books[4]),
            nx.betweenness_centrality(books[4], weight='weight'),
            nx.degree_centrality(books[4])]

# Creating the correlation DataFrame
cor = pd.DataFrame.from_records(measures)

# Calculating the correlation
cor.corr().T
```

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Aegon-I-Targaryen</th>
      <th>Daenerys-Targaryen</th>
      <th>Aegon-Targaryen-(son-of-Rhaegar)</th>
      <th>Elia-Martell</th>
      <th>Franklyn-Flowers</th>
      <th>Haldon</th>
      <th>Harry-Strickland</th>
      <th>Jon-Connington</th>
      <th>Lemore</th>
      <th>Rhaegar-Targaryen</th>
      <th>...</th>
      <th>Tysha</th>
      <th>Shrouded-Lord</th>
      <th>Theomore</th>
      <th>William-Foxglove</th>
      <th>Walder-Frey-(son-of-Jammos)</th>
      <th>Wex-Pyke</th>
      <th>Willow-Witch-eye</th>
      <th>Thistle</th>
      <th>Wylis-Manderly</th>
      <th>Wulfe</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Aegon-I-Targaryen</th>
      <td>1.000000</td>
      <td>-0.018377</td>
      <td>0.278893</td>
      <td>0.675768</td>
      <td>0.647014</td>
      <td>0.918495</td>
      <td>0.999852</td>
      <td>0.836828</td>
      <td>0.995226</td>
      <td>0.753194</td>
      <td>...</td>
      <td>0.312087</td>
      <td>0.999997</td>
      <td>-0.578654</td>
      <td>1.000000</td>
      <td>0.997255</td>
      <td>1.000000</td>
      <td>0.999742</td>
      <td>0.923316</td>
      <td>0.999994</td>
      <td>0.999190</td>
    </tr>
    <tr>
      <th>Daenerys-Targaryen</th>
      <td>-0.018377</td>
      <td>1.000000</td>
      <td>0.955035</td>
      <td>0.724571</td>
      <td>0.750459</td>
      <td>0.378486</td>
      <td>-0.035547</td>
      <td>0.531994</td>
      <td>0.079287</td>
      <td>0.643845</td>
      <td>...</td>
      <td>0.944158</td>
      <td>-0.020834</td>
      <td>0.826070</td>
      <td>-0.019232</td>
      <td>-0.092358</td>
      <td>-0.018104</td>
      <td>-0.041092</td>
      <td>-0.400943</td>
      <td>-0.021945</td>
      <td>-0.058597</td>
    </tr>
    <tr>
      <th>Aegon-Targaryen-(son-of-Rhaegar)</th>
      <td>0.278893</td>
      <td>0.955035</td>
      <td>1.000000</td>
      <td>0.896334</td>
      <td>0.912672</td>
      <td>0.635904</td>
      <td>0.262358</td>
      <td>0.759128</td>
      <td>0.371282</td>
      <td>0.841758</td>
      <td>...</td>
      <td>0.999396</td>
      <td>0.276532</td>
      <td>0.621831</td>
      <td>0.278072</td>
      <td>0.207021</td>
      <td>0.279155</td>
      <td>0.256999</td>
      <td>-0.111296</td>
      <td>0.275465</td>
      <td>0.240022</td>
    </tr>
    <tr>
      <th>Elia-Martell</th>
      <td>0.675768</td>
      <td>0.724571</td>
      <td>0.896334</td>
      <td>1.000000</td>
      <td>0.999265</td>
      <td>0.912169</td>
      <td>0.663009</td>
      <td>0.969047</td>
      <td>0.744480</td>
      <td>0.993857</td>
      <td>...</td>
      <td>0.911196</td>
      <td>0.673955</td>
      <td>0.210135</td>
      <td>0.675138</td>
      <td>0.619335</td>
      <td>0.675970</td>
      <td>0.658844</td>
      <td>0.340867</td>
      <td>0.673134</td>
      <td>0.645559</td>
    </tr>
    <tr>
      <th>Franklyn-Flowers</th>
      <td>0.647014</td>
      <td>0.750459</td>
      <td>0.912672</td>
      <td>0.999265</td>
      <td>1.000000</td>
      <td>0.895787</td>
      <td>0.633823</td>
      <td>0.958870</td>
      <td>0.718338</td>
      <td>0.988884</td>
      <td>...</td>
      <td>0.926320</td>
      <td>0.645138</td>
      <td>0.247460</td>
      <td>0.646362</td>
      <td>0.588781</td>
      <td>0.647222</td>
      <td>0.629521</td>
      <td>0.304576</td>
      <td>0.644289</td>
      <td>0.615806</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>Wex-Pyke</th>
      <td>1.000000</td>
      <td>-0.018104</td>
      <td>0.279155</td>
      <td>0.675970</td>
      <td>0.647222</td>
      <td>0.918603</td>
      <td>0.999848</td>
      <td>0.836978</td>
      <td>0.995253</td>
      <td>0.753374</td>
      <td>...</td>
      <td>0.312347</td>
      <td>0.999996</td>
      <td>-0.578431</td>
      <td>0.999999</td>
      <td>0.997235</td>
      <td>1.000000</td>
      <td>0.999736</td>
      <td>0.923211</td>
      <td>0.999993</td>
      <td>0.999179</td>
    </tr>
    <tr>
      <th>Willow-Witch-eye</th>
      <td>0.999742</td>
      <td>-0.041092</td>
      <td>0.256999</td>
      <td>0.658844</td>
      <td>0.629521</td>
      <td>0.909273</td>
      <td>0.999985</td>
      <td>0.824172</td>
      <td>0.992752</td>
      <td>0.738053</td>
      <td>...</td>
      <td>0.290418</td>
      <td>0.999795</td>
      <td>-0.597037</td>
      <td>0.999761</td>
      <td>0.998680</td>
      <td>0.999736</td>
      <td>1.000000</td>
      <td>0.931805</td>
      <td>0.999817</td>
      <td>0.999846</td>
    </tr>
    <tr>
      <th>Thistle</th>
      <td>0.923316</td>
      <td>-0.400943</td>
      <td>-0.111296</td>
      <td>0.340867</td>
      <td>0.304576</td>
      <td>0.696200</td>
      <td>0.929776</td>
      <td>0.562409</td>
      <td>0.881429</td>
      <td>0.442816</td>
      <td>...</td>
      <td>-0.076704</td>
      <td>0.924257</td>
      <td>-0.847493</td>
      <td>0.923644</td>
      <td>0.949218</td>
      <td>0.923211</td>
      <td>0.931805</td>
      <td>1.000000</td>
      <td>0.924681</td>
      <td>0.938023</td>
    </tr>
    <tr>
      <th>Wylis-Manderly</th>
      <td>0.999994</td>
      <td>-0.021945</td>
      <td>0.275465</td>
      <td>0.673134</td>
      <td>0.644289</td>
      <td>0.917078</td>
      <td>0.999907</td>
      <td>0.834870</td>
      <td>0.994872</td>
      <td>0.750843</td>
      <td>...</td>
      <td>0.308695</td>
      <td>0.999999</td>
      <td>-0.581560</td>
      <td>0.999996</td>
      <td>0.997513</td>
      <td>0.999993</td>
      <td>0.999817</td>
      <td>0.924681</td>
      <td>1.000000</td>
      <td>0.999327</td>
    </tr>
    <tr>
      <th>Wulfe</th>
      <td>0.999190</td>
      <td>-0.058597</td>
      <td>0.240022</td>
      <td>0.645559</td>
      <td>0.615806</td>
      <td>0.901838</td>
      <td>0.999734</td>
      <td>0.814120</td>
      <td>0.990493</td>
      <td>0.726114</td>
      <td>...</td>
      <td>0.273603</td>
      <td>0.999286</td>
      <td>-0.611005</td>
      <td>0.999224</td>
      <td>0.999427</td>
      <td>0.999179</td>
      <td>0.999846</td>
      <td>0.938023</td>
      <td>0.999327</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>
<p>317 rows × 317 columns</p>

```python
def test_task8():
    assert len(cor) == 3, \
    'Make sure you have calculated the correlation correctly'
```

    1/1 tests passed

## 9. Conclusion
<p>We see a high correlation between these three measures for our character co-occurrence network.</p>
<p>So we've been looking at different ways to find the important characters in the Game of Thrones co-occurrence network. According to degree centrality, Eddard Stark is the most important character initially in the books. But who is/are the most important character(s) in the fifth book according to these three measures? </p>

```python
# Finding the most important character in the fifth book,
# according to degree centrality, betweenness centrality and pagerank.
p_rank, b_cent, d_cent = cor.idxmax(axis=1)

# Printing out the top character accoding to the three measures
print(p_rank)
print(b_cent)
print(d_cent)
```

    Jon-Snow
    Stannis-Baratheon
    Jon-Snow

```python
def test_task9():
    assert p_rank == 'Jon-Snow', \
    'Nope, wrong answer. Make sure you have found the max using the correct axis'
```

    1/1 tests passed
