## 1. Darwin's bibliography
<p><img src="https://assets.datacamp.com/production/project_607/img/CharlesDarwin.jpg" alt="Charles Darwin" width="300px"></p>
<p>Charles Darwin is one of the few universal figures of science. His most renowned work is without a doubt his "<em>On the Origin of Species</em>" published in 1859 which introduced the concept of natural selection. But Darwin wrote many other books on a wide range of topics, including geology, plants or his personal life. In this notebook, we will automatically detect how closely related his books are to each other.</p>
<p>To this purpose, we will develop the bases of <strong>a content-based book recommendation system</strong>, which will determine which books are close to each other based on how similar the discussed topics are. The methods we will use are commonly used in text- or documents-heavy industries such as legal, tech or customer support to perform some common task such as text classification or handling search engine queries.</p>
<p>Let's take a look at the books we'll use in our recommendation system.</p>

```python
# Import library
import glob

# The books files are contained in this folder
folder = "datasets/"

# List all the .txt files and sort them alphabetically
files = glob.glob(folder + "*.txt")

files.sort()
```

```python
# This needs to be included at the beginning of every @tests cell.

# One or more tests of the students code.
# The @solution should pass the tests.
# The purpose of the tests is to try to catch common errors and to
# give the student a hint on how to resolve these errors.

def test_files_type():
    assert isinstance(files, list), \
    'The files variable should be a list.'

def test_glob_len():
    assert len(files) == 20, \
    'The files variable should contain 20 elements. Make sure you only selected files ending by .txt.'

def test_is_files_list_sorted():
    assert all(files[i] <= files[i+1] for i in range(len(files)-1)), \
    'The files list should be sorted by using the .sort() method.'
```

    3/3 tests passed

## 2. Load the contents of each book into Python
<p>As a first step, we need to load the content of these books into Python and do some basic pre-processing to facilitate the downstream analyses. We call such a collection of texts <strong>a corpus</strong>. We will also store the titles for these books for future reference and print their respective length to get a gauge for their contents.</p>

```python
# Import libraries
import re, os

# Initialize the object that will contain the texts and titles
txts = []
titles = []

for n in files:
    # Open each file
    f = open(n, encoding='utf-8-sig')
    # Remove all non-alpha-numeric characters
    data = re.sub('[\W_]+', ' ', f.read())
    # Store the texts and titles of the books in two separate lists
    titles.append(os.path.basename(n).replace('.txt', ''))
    txts.append(data)

# Print the length, in characters, of each book
[len(t) for t in txts]
```

    [123231,
     496068,
     1776539,
     617088,
     913713,
     624232,
     335920,
     523021,
     797401,
     901406,
     1047518,
     1010643,
     767492,
     1660866,
     298319,
     916267,
     1093567,
     1043499,
     341447,
     1149574]

```python
# This needs to be included at the beginning of every @tests cell.
import _io

# For some reasons, the index isn't the same between my local notebook and the DataCamp version.
# Therefore, I can not hardcode the value and have to generate it here.

def test_txts_titles_len():
    assert len(txts) == 20 & len(titles) == 20, \
    'The txts and titles variable should contain 20 elements.'


def test_f_type():
    assert isinstance(f, _io.TextIOWrapper), \
    'The f variable should be of type _io.TextIOWrapper and be generated with the open() function.'

def test_file_encoding():
    assert f.encoding == 'utf-8-sig', \
    'Make sure you open the text file encoded as utf-8-sig.'

def test_txt_in_title():
    assert all([".txt" not in title for title in titles]), \
    'The titles contained in the titles variable should not contain the .txt string. Use the .replace() method to remove them.'

def test_folder_in_title():
    assert all([folder not in title for title in titles]), \
    'The titles contained in the titles variable should not contain the name of the folder (' + str(folder) + '). Use the os.path.basename() function to remove them.'


def test_alphanumeric_in_txt():
    assert not sum([len(i) for i in [re.findall('^[\w-]+$', t) for t in txts]]), \
    'The elements of the txts variable should not contain non-alphanumeric characters.'
```

    6/6 tests passed

## 3. Find "On the Origin of Species"
<p>For the next parts of this analysis, we will often check the results returned by our method for a given book. For consistency, we will refer to Darwin's most famous book: "<em>On the Origin of Species</em>." Let's find to which index this book is associated.</p>

```python
# Browse the list containing all the titles
for i in range(len(titles)):
    # Store the index if the title is "OriginofSpecies"
    if titles[i] == 'OriginofSpecies':
        ori = i
        break

# Print the stored index
ori
```

    15

```python
# This needs to be included at the beginning of every @tests cell.

# For some reasons, the index isn't the same between my local notebook and the DataCamp version.
# Therefore, I can not hardcode the value and have to generate it here.

for i in range(len(titles)):
    # Store the index if the title is "OriginofSpecies"
    if(titles[i]=="OriginofSpecies"):
        ori_test = i


def test_ori_existence():
    assert 'ori' in globals(), \
    'Make sure you created a variable called ori.'

def test_ori_type():
    assert type(ori) == int, \
    'The ori variable should be of type integer.'

def test_ori_value():
    assert ori == ori_test, \
    'The ori variable does not contain the correct index number.'
```

    3/3 tests passed

## 4. Tokenize the corpus
<p>As a next step, we need to transform the corpus into a format that is easier to deal with for the downstream analyses. We will tokenize our corpus, i.e., transform each text into a list of the individual words (called tokens) it is made of. To check the output of our process, we will print the first 20 tokens of "<em>On the Origin of Species</em>".</p>

```python
# Define a list of stop words
stoplist = set('for a of the and to in to be which some is at that we i who whom show via may my our might as well'.split())

# Convert the text to lower case
txts_lower_case = [txt.lower() for txt in txts]

# Transform the text into tokens
txts_split = [txt.split() for txt in txts_lower_case]

# Remove tokens which are part of the list of stop words
texts = [[word for word in txt if word not in stoplist] for txt in txts_split]

# Print the first 20 tokens for the "On the Origin of Species" book
texts[ori][: 20]
```

    ['on',
     'origin',
     'species',
     'but',
     'with',
     'regard',
     'material',
     'world',
     'can',
     'least',
     'go',
     'so',
     'far',
     'this',
     'can',
     'perceive',
     'events',
     'are',
     'brought',
     'about']

```python
# This needs to be included at the beginning of every @tests cell.

# One or more tests of the students code.
# The @solution should pass the tests.
# The purpose of the tests is to try to catch common errors and to
# give the student a hint on how to resolve these errors.
stoplist = set('for a of the and to in to be which some is at that we i who whom show via may my our might as well'.split())

def intersection(lst1, lst2):
    lst3 = [value for value in lst1 if value in lst2]
    return lst3

## Variables existence

def test_var_texts_existence():
    assert 'texts' in globals(), \
    'The results should be stored in a variable called texts.'

def test_var_lowercase_existence():
    assert 'txts_lower_case' in globals(), \
    'The variable txts_lower_case should exist.'

def test_var_split_existence():
    assert 'txts_split' in globals(), \
    'The variable txts_split should exist.'

## Variables type and length
def test_var_texts_type():
    assert isinstance(txts, list), \
    'The texts variable should be a list.'

def test_var_texts_lowercase_type():
    assert isinstance(txts_lower_case, list), \
    'The txts_lower_case variable should be a list.'

def test_var_texts_split_type():
    assert isinstance(txts_split, list), \
    'The txts_split variable should be a list.'

## Variables length
def test_var_texts_len():
    assert len(texts) == 20, \
    'The texts list should contain 20 elements.'

def test_var_texts_lowercase_len():
    assert len(txts_lower_case) == 20, \
    'The txts_lower_case list should contain 20 elements.'

def test_var_texts_split_len():
    assert len(txts_split) == 20, \
    'The txts_split list should contain 20 elements.'

## Variable content

def test_lower_case():
    assert all([t.islower() for t in txts_lower_case]), \
    'The texts in the txts_lower_case list should all be in lower case.'

def test_split_list():
    assert all([isinstance(t, list) for t in txts_split]), \
    'Each element of the txts_split list should be a list'


def test_stopwords():
    assert not sum([len(i) for i in [intersection(t, stoplist) for t in texts]]), \
    'You should remove stop words from the final token sets contained in the texts variable.'
```

    12/12 tests passed

## 5. Stemming of the tokenized corpus
<p>If you have read <em>On the Origin of Species</em>, you will have noticed that Charles Darwin can use different words to refer to a similar concept. For example, the concept of selection can be described by words such as <em>selection</em>, <em>selective</em>, <em>select</em> or <em>selects</em>. This will dilute the weight given to this concept in the book and potentially bias the results of the analysis.</p>
<p>To solve this issue, it is a common practice to use a <strong>stemming process</strong>, which will group together the inflected forms of a word so they can be analysed as a single item: <strong>the stem</strong>. In our <em>On the Origin of Species</em> example, the words related to the concept of selection would be gathered under the <em>select</em> stem.</p>
<p>As we are analysing 20 full books, the stemming algorithm can take several minutes to run and, in order to make the process faster, we will directly load the final results from a pickle file and review the method used to generate it.</p>

```python
import pickle

# Load the stemmed tokens list from the pregenerated pickle file
texts_stem = pickle.load(open('datasets/texts_stem.p', 'rb'))

# Print the 20 first stemmed tokens from the "On the Origin of Species" book
texts_stem[ori][: 20]
```

    ['on',
     'origin',
     'speci',
     'but',
     'with',
     'regard',
     'materi',
     'world',
     'can',
     'least',
     'go',
     'so',
     'far',
     'thi',
     'can',
     'perceiv',
     'event',
     'are',
     'brought',
     'about']

```python
# This needs to be included at the beginning of every @tests cell.

# One or more tests of the students code.
# The @solution should pass the tests.
# The purpose of the tests is to try to catch common errors and to
# give the student a hint on how to resolve these errors.

def test_var_existence():
    assert 'texts_stem'in globals(), \
    'The content of the pickle file should be loaded into a variable named texts_stem.'

def test_var_type():
    assert isinstance(texts_stem, list), \
    'The texts_stem variable should be a list.'

def test_var_len():
    assert len(texts_stem) == 20, \
    'The texts_stem list should contain 20 elements.'
```

    3/3 tests passed

## 6. Building a bag-of-words model
<p>Now that we have transformed the texts into stemmed tokens, we need to build models that will be useable by downstream algorithms.</p>
<p>First, we need to will create a universe of all words contained in our corpus of Charles Darwin's books, which we call <em>a dictionary</em>. Then, using the stemmed tokens and the dictionary, we will create <strong>bag-of-words models</strong> (BoW) of each of our texts. The BoW models will represent our books as a list of all uniques tokens they contain associated with their respective number of occurrences. </p>
<p>To better understand the structure of such a model, we will print the five first elements of one of the "<em>On the Origin of Species</em>" BoW model.</p>

```python
# Load the functions allowing to create and use dictionaries
from gensim import corpora

# Create a dictionary from the stemmed tokens
dictionary = corpora.Dictionary(texts_stem)

# Create a bag-of-words model for each book, using the previously generated dictionary
bows = [dictionary.doc2bow(txt) for txt in texts_stem]

# Print the first five elements of the On the Origin of species' BoW model
bows[ori][: 5]
```

    [(0, 11), (5, 51), (6, 1), (8, 2), (21, 1)]

```python
# This needs to be included at the beginning of every @tests cell.

# One or more tests of the students code.
# The @solution should pass the tests.
# The purpose of the tests is to try to catch common errors and to
# give the student a hint on how to resolve these errors.
import gensim.corpora.dictionary
from gensim import corpora

dictionary_test = corpora.Dictionary(texts_stem)
bows_test = [dictionary.doc2bow(text) for text in texts_stem]
bows_len =[len(b) for b in bows]
bows_test_len =[len(b) for b in bows_test]

## Dictionary variable
def test_dictionary_type():
    assert isinstance(dictionary, gensim.corpora.dictionary.Dictionary), \
    'The dictionary should be created using the corpora.Dictionary() function and the resulting object should be of type "gensim.corpora.dictionary.Dictionary".'

def test_dictionary_len():
    assert len(dictionary) == len(dictionary_test), \
    'The dictionary should contain ' +  str(len(dictionary_test)) + ' tokens. Make sure you generated the dictionary from the texts_stem object.'

## bows variable

def test_bows_type():
    assert isinstance(bows, list), \
    'The bows variable should be a list.'

def test_bows_list_len():
    assert bows_len == bows_test_len, \
    'The lengths of the bows are not those expected. Make sure you generated them using the texts_stem object.'

def test_bows_len():
    assert len(bows) == 20, \
    'The bows object should have 20 elements, one model per text.'

def test_bows_content_type():
    assert all([isinstance(b, list) for b in bows]), \
    'Each elements in the bows list should be a list.'
```

    6/6 tests passed

## 7. The most common words of a given book
<p>The results returned by the bag-of-words model is certainly easy to use for a computer but hard to interpret for a human. It is not straightforward to understand which stemmed tokens are present in a given book from Charles Darwin, and how many occurrences we can find.</p>
<p>In order to better understand how the model has been generated and visualize its content, we will transform it into a DataFrame and display the 10 most common stems for the book "<em>On the Origin of Species</em>".</p>

```python
# Import pandas to create and manipulate DataFrames
import pandas as pd

# Convert the BoW model for "On the Origin of Species" into a DataFrame
df_bow_origin = pd.DataFrame(bows[ori])
# Add the column names to the DataFrame
df_bow_origin.columns = ['index', 'occurrences']

# Add a column containing the token corresponding to the dictionary index
df_bow_origin['token'] = df_bow_origin['index'].apply(lambda x: dictionary[x])

# Sort the DataFrame by descending number of occurrences and print the first 10 values
df_bow_origin = df_bow_origin.sort_values('occurrences', ascending=False)
df_bow_origin.head(10)
```

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>index</th>
      <th>occurrences</th>
      <th>token</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>748</th>
      <td>1168</td>
      <td>2023</td>
      <td>have</td>
    </tr>
    <tr>
      <th>1119</th>
      <td>1736</td>
      <td>1558</td>
      <td>on</td>
    </tr>
    <tr>
      <th>1489</th>
      <td>2288</td>
      <td>1543</td>
      <td>speci</td>
    </tr>
    <tr>
      <th>892</th>
      <td>1366</td>
      <td>1480</td>
      <td>it</td>
    </tr>
    <tr>
      <th>239</th>
      <td>393</td>
      <td>1362</td>
      <td>by</td>
    </tr>
    <tr>
      <th>1128</th>
      <td>1747</td>
      <td>1201</td>
      <td>or</td>
    </tr>
    <tr>
      <th>125</th>
      <td>218</td>
      <td>1140</td>
      <td>are</td>
    </tr>
    <tr>
      <th>665</th>
      <td>1043</td>
      <td>1137</td>
      <td>from</td>
    </tr>
    <tr>
      <th>1774</th>
      <td>2703</td>
      <td>1000</td>
      <td>with</td>
    </tr>
    <tr>
      <th>1609</th>
      <td>2452</td>
      <td>962</td>
      <td>thi</td>
    </tr>
  </tbody>
</table>

```python
# This needs to be included at the beginning of every @tests cell.

# One or more tests of the students code.
# The @solution should pass the tests.
# The purpose of the tests is to try to catch common errors and to
# give the student a hint on how to resolve these errors.

import pandas.core.frame

# Hardcoded numbers might not hold once on Datacamp's servers.
# Hence the values are recomputed here.

df_bow_origin_test = pd.DataFrame(bows[ori])
n_rows_test = df_bow_origin_test.shape[0]

#### Tests

def test_df_type():
    assert isinstance(df_bow_origin, pandas.core.frame.DataFrame), \
    'The df_bow_origin variable should be a pandas DataFrame of type pandas.core.frame.DataFrame.'

def test_df_dim1():
    assert df_bow_origin.shape[1] == 3, \
    'The df_bow_origin DataFrame should have 3 columns.'

def test_df_dim2():
    assert df_bow_origin.shape[0] == n_rows_test, \
    'The df_bow_origin DataFrame should have ' + str(n_rows_test) + ' rows.'

def test_df_columns():
    assert all(df_bow_origin.columns == list(["index", "occurrences", "token"])), \
    'The columns of the df_bow_origin DataFrame should be named "index", "occurrences" and "token".'
```

    4/4 tests passed

## 8. Build a tf-idf model
<p>If it wasn't for the presence of the stem "<em>speci</em>", we would have a hard time to guess this BoW model comes from the <em>On the Origin of Species</em> book. The most recurring words are, apart from few exceptions, very common and unlikely to carry any information peculiar to the given book. We need to use an additional step in order to determine which tokens are the most specific to a book.</p>
<p>To do so, we will use a <strong>tf-idf model</strong> (term frequency–inverse document frequency). This model defines the importance of each word depending on how frequent it is in this text and how infrequent it is in all the other documents. As a result, a high tf-idf score for a word will indicate that this word is specific to this text.</p>
<p>After computing those scores, we will print the 10 words most specific to the "<em>On the Origin of Species</em>" book (i.e., the 10 words with the highest tf-idf score).</p>

```python
# Load the gensim functions that will allow us to generate tf-idf models
from gensim.models import TfidfModel

# Generate the tf-idf model
model = TfidfModel(bows)

# Print the model for "On the Origin of Species"
model[bows[ori]]
```

    [(8, 0.00020383224047642202),
     (21, 0.0005716037746542094),
     (23, 0.0017118699041370883),
     (27, 0.0006458270601429994),
     (28, 0.0025678048562056324),
     (31, 0.0008559349520685442),
     (35, 0.00101497410751472),
     (36, 0.00101497410751472),
     (51, 0.000886740665721021),
     (54, 0.00202994821502944),
     (56, 0.0023757190244598344),
     (57, 0.00010191612023821101),
     (63, 0.0027544680933525786),
     (64, 0.000509580601191055),
     (66, 0.00020383224047642202),
     (67, 0.0023757190244598344),
     (68, 0.00202994821502944),
     (75, 0.0013772340466762893),
     (76, 0.0004433703328605105),
     (78, 0.004171843479607349),
     (80, 0.0020859217398036746),
     (83, 0.00857405661981314),
     (84, 0.000509580601191055),
     (88, 0.002445986885717064),
     (89, 0.0033632319678609636),
     (90, 0.000886740665721021),
     (91, 0.0016747506839411234),
     (94, 0.000886740665721021),
     (95, 0.0004433703328605105),
     (96, 0.003546962662884084),
     (97, 0.0016306579238113761),
     (102, 0.037686478293143394),
     (104, 0.000917245082143899),
     (106, 0.001417375386254771),
     (108, 0.0035434384656369273),
     (109, 0.005299638252386972),
     (111, 0.0022421546452406423),
     (114, 0.0015287418035731652),
     (123, 0.0509769226270304),
     (125, 0.009580115302391834),
     (126, 0.004171843479607349),
     (127, 0.001417375386254771),
     (137, 0.020026648174904797),
     (139, 0.007749924721715993),
     (141, 0.00101916120238211),
     (143, 0.004751438048919669),
     (144, 0.0047597336465067894),
     (154, 0.0010467191774632021),
     (156, 0.013962508472634907),
     (165, 0.006781184131501494),
     (167, 0.000611496721429266),
     (172, 0.021771758891234606),
     (176, 0.0033632319678609636),
     (178, 0.0031035923300235736),
     (186, 0.009274366941677202),
     (188, 0.0016747506839411234),
     (192, 0.006257765219411025),
     (196, 0.0038749623608579963),
     (197, 0.0013772340466762893),
     (198, 0.000886740665721021),
     (204, 0.0042521261587643135),
     (207, 0.0022603947105004976),
     (212, 0.001324909563096743),
     (214, 0.020395035311583484),
     (215, 0.021720943436859957),
     (219, 0.0019374811804289981),
     (220, 0.004396220545345449),
     (221, 0.0054618131386103995),
     (222, 0.0018206043795367997),
     (223, 0.0007086876931273855),
     (224, 0.007703414568616897),
     (226, 0.0030574836071463303),
     (230, 0.005135609712411265),
     (231, 0.0027544680933525786),
     (235, 0.002445986885717064),
     (236, 0.0012916541202859988),
     (237, 0.0020934383549264042),
     (241, 0.0029308136968969663),
     (242, 0.0015865778821689297),
     (243, 0.008263404280057736),
     (245, 0.004520789421000995),
     (246, 0.003465148088099174),
     (247, 0.001732574044049587),
     (249, 0.0018840945194337638),
     (251, 0.008343686959214698),
     (252, 0.0030449223225441605),
     (253, 0.0006458270601429994),
     (261, 0.001324909563096743),
     (269, 0.0006458270601429994),
     (271, 0.0008373753419705617),
     (276, 0.009921627703783398),
     (278, 0.0034296226479252566),
     (280, 0.0021260630793821567),
     (283, 0.02138147122013851),
     (285, 0.001417375386254771),
     (287, 0.0013301109985815313),
     (288, 0.006886170233381447),
     (290, 0.0035434384656369273),
     (291, 0.0018206043795367997),
     (296, 0.009839160268154101),
     (298, 0.042694255446964965),
     (300, 0.0016747506839411234),
     (301, 0.000611496721429266),
     (302, 0.0042521261587643135),
     (303, 0.004171843479607349),
     (304, 0.0020859217398036746),
     (311, 0.0016306579238113761),
     (313, 0.007086876931273855),
     (323, 0.0047597336465067894),
     (325, 0.021606217490500734),
     (327, 0.001732574044049587),
     (329, 0.01790404260679176),
     (335, 0.0004433703328605105),
     (336, 0.0023922081541910096),
     (338, 0.0020859217398036746),
     (339, 0.001417375386254771),
     (344, 0.001417375386254771),
     (345, 0.011527628654373272),
     (346, 0.00020383224047642202),
     (348, 0.0006280315064779214),
     (349, 0.0006458270601429994),
     (351, 0.0036412087590735995),
     (354, 0.007980665991489189),
     (356, 0.0018840945194337638),
     (358, 0.013772340466762893),
     (359, 0.0022603947105004976),
     (362, 0.00101497410751472),
     (367, 0.0023922081541910096),
     (369, 0.19772097392783367),
     (370, 0.043694505108883196),
     (371, 0.000509580601191055),
     (372, 0.0023922081541910096),
     (373, 0.0016306579238113761),
     (374, 0.001732574044049587),
     (375, 0.001936406284526009),
     (376, 0.006489658900271853),
     (377, 0.0030449223225441605),
     (380, 0.0016145676503574987),
     (387, 0.0007086876931273855),
     (388, 0.0042521261587643135),
     (389, 0.0005716037746542094),
     (391, 0.0023922081541910096),
     (400, 0.00202994821502944),
     (406, 0.013772340466762893),
     (407, 0.0005716037746542094),
     (409, 0.0035588452033748874),
     (411, 0.0007086876931273855),
     (412, 0.004751438048919669),
     (418, 0.0027544680933525786),
     (421, 0.0027544680933525786),
     (424, 0.007538884401734597),
     (425, 0.00811979286011776),
     (426, 0.0032291353007149973),
     (429, 0.000886740665721021),
     (431, 0.000886740665721021),
     (432, 0.010149741075147201),
     (433, 0.0016306579238113761),
     (434, 0.00405989643005888),
     (436, 0.0021260630793821567),
     (442, 0.009212940010656012),
     (446, 0.004171843479607349),
     (448, 0.021562415055741965),
     (449, 0.03291890683694216),
     (450, 0.0035434384656369273),
     (453, 0.0011210773226203211),
     (454, 0.00405989643005888),
     (456, 0.011301973552502492),
     (457, 0.0020859217398036746),
     (458, 0.0003229135300714997),
     (463, 0.01790404260679176),
     (464, 0.0027544680933525786),
     (465, 0.0008559349520685442),
     (468, 0.00202994821502944),
     (470, 0.0018206043795367997),
     (478, 0.010923626277220799),
     (482, 0.0344479258546676),
     (484, 0.013772340466762893),
     (486, 0.0020859217398036746),
     (489, 0.0054618131386103995),
     (490, 0.022603947105004983),
     (491, 0.00405989643005888),
     (493, 0.0007086876931273855),
     (497, 0.012839024281028162),
     (498, 0.0035434384656369273),
     (502, 0.00637818923814647),
     (505, 0.011970998987233783),
     (507, 0.0009687405902144991),
     (514, 0.0025121260259116855),
     (520, 0.004280477050004863),
     (524, 0.0020859217398036746),
     (526, 0.005716037746542095),
     (527, 0.0027544680933525786),
     (529, 0.006318799454769082),
     (531, 0.003546962662884084),
     (532, 0.012791353704852355),
     (534, 0.005320443994326125),
     (536, 0.0014268256833349542),
     (541, 0.0011432075493084189),
     (543, 0.01110604517518251),
     (544, 0.0031401575323896065),
     (546, 0.0017148113239626283),
     (551, 0.004784416308382019),
     (552, 0.0031731557643378595),
     (558, 0.0023922081541910096),
     (559, 0.00020383224047642202),
     (561, 0.0022421546452406423),
     (562, 0.005197722132148762),
     (563, 0.006908346571257135),
     (564, 0.0011432075493084189),
     (565, 0.00405989643005888),
     (566, 0.0013772340466762893),
     (569, 0.04034670029030646),
     (573, 0.010630315396910783),
     (576, 0.0025121260259116855),
     (578, 0.0028580188732710474),
     (579, 0.003159399727384541),
     (582, 0.0035434384656369273),
     (586, 0.003563578536689751),
     (590, 0.0017118699041370883),
     (592, 0.0010467191774632021),
     (593, 0.0018206043795367997),
     (594, 0.015898914757160917),
     (596, 0.0015865778821689297),
     (598, 0.0023922081541910096),
     (600, 0.01251553043882205),
     (601, 0.00202994821502944),
     (604, 0.05582357591330961),
     (605, 0.00637818923814647),
     (606, 0.0005716037746542094),
     (616, 0.0010467191774632021),
     (619, 0.00710481875260304),
     (620, 0.024945049756828264),
     (626, 0.0013772340466762893),
     (628, 0.00041868767098528084),
     (629, 0.004197875890929496),
     (633, 0.0013301109985815313),
     (635, 0.004960813851891699),
     (636, 0.005991544664479809),
     (641, 0.006346311528675719),
     (646, 0.0027544680933525786),
     (649, 0.005763814327186636),
     (652, 0.000917245082143899),
     (653, 0.0011432075493084189),
     (654, 0.0023757190244598344),
     (655, 0.0016747506839411234),
     (657, 0.0030449223225441605),
     (658, 0.007104097661572994),
     (660, 0.005144433971887885),
     (662, 0.003563578536689751),
     (663, 0.0011878595122299172),
     (665, 0.00101497410751472),
     (666, 0.006395676852426178),
     (667, 0.01623958572023552),
     (668, 0.005669501545019084),
     (670, 0.011723254787587865),
     (674, 0.002445986885717064),
     (675, 0.0450089246309177),
     (676, 0.061655829302082535),
     (678, 0.00040766448095284403),
     (679, 0.005144433971887885),
     (681, 0.0007134128416674771),
     (682, 0.0015865778821689297),
     (685, 0.0020859217398036746),
     (686, 0.0006458270601429994),
     (693, 0.0035670642083373855),
     (698, 0.0022864150986168378),
     (705, 0.0034237398082741766),
     (712, 0.0017118699041370883),
     (713, 0.0013772340466762893),
     (720, 0.0029308136968969663),
     (722, 0.005074870537573601),
     (726, 0.01771719232818464),
     (727, 0.004396220545345449),
     (728, 0.0031731557643378595),
     (729, 0.006089844645088321),
     (730, 0.01028886794377577),
     (731, 0.0017148113239626283),
     (740, 0.008357121859533303),
     (741, 0.0066990027357644935),
     (743, 0.006930296176198348),
     (744, 0.01033323296228799),
     (745, 0.006257765219411025),
     (748, 0.017254559827750243),
     (750, 0.07127157073379503),
     (752, 0.1459896647842414),
     (753, 0.06980942681543291),
     (758, 0.004197875890929496),
     (769, 0.0017118699041370883),
     (770, 0.0010467191774632021),
     (771, 0.0007134128416674771),
     (776, 0.00020934383549264042),
     (783, 0.006346311528675719),
     (784, 0.004171843479607349),
     (785, 0.002834750772509542),
     (786, 0.004171843479607349),
     (787, 0.006930296176198348),
     (788, 0.002955567486908119),
     (789, 0.003546962662884084),
     (793, 0.014208195323145987),
     (797, 0.004197875890929496),
     (798, 0.024359378580353284),
     (803, 0.010149741075147201),
     (805, 0.0034237398082741766),
     (806, 0.02571547930590961),
     (810, 0.0011878595122299172),
     (811, 0.006886170233381447),
     (815, 0.0018840945194337638),
     (816, 0.0012560630129558428),
     (817, 0.0015865778821689297),
     (819, 0.0026602219971630626),
     (820, 0.006458270601429995),
     (821, 0.006207184660047147),
     (822, 0.0688958517093352),
     (825, 0.0003229135300714997),
     (830, 0.001222993442858532),
     (831, 0.003552048830786497),
     (832, 0.02256933073236843),
     (833, 0.01097906002243099),
     (834, 0.0017118699041370883),
     (838, 0.001936406284526009),
     (839, 0.0016306579238113761),
     (842, 0.0013772340466762893),
     (848, 0.006886170233381447),
     (849, 0.0011432075493084189),
     (851, 0.0020859217398036746),
     (857, 0.0005716037746542094),
     (859, 0.008343686959214698),
     (861, 0.0018840945194337638),
     (862, 0.001732574044049587),
     (866, 0.004433703328605105),
     (867, 0.004784416308382019),
     (870, 0.0003229135300714997),
     (873, 0.01886292456358891),
     (875, 0.0009687405902144991),
     (878, 0.00202994821502944),
     (879, 0.005489530011215495),
     (881, 0.0007086876931273855),
     (883, 0.0008153289619056881),
     (885, 0.0023922081541910096),
     (887, 0.001732574044049587),
     (891, 0.0006458270601429994),
     (892, 0.0013772340466762893),
     (894, 0.002445986885717064),
     (897, 0.005991544664479809),
     (898, 0.0011432075493084189),
     (903, 0.0011878595122299172),
     (905, 0.0025678048562056324),
     (909, 0.002649819126193486),
     (910, 0.005508936186705157),
     (917, 0.05877026247301295),
     (919, 0.0017118699041370883),
     (921, 0.0011210773226203211),
     (924, 0.0054015543726251836),
     (925, 0.004784416308382019),
     (929, 0.013718490591701027),
     (931, 0.00101497410751472),
     (935, 0.0026602219971630626),
     (936, 0.0025121260259116855),
     (937, 0.0009687405902144991),
     (939, 0.0016306579238113761),
     (944, 0.000886740665721021),
     (945, 0.00710481875260304),
     (948, 0.0023757190244598344),
     (951, 0.012692623057351438),
     (952, 0.006089844645088321),
     (953, 0.005074870537573601),
     (956, 0.010149741075147201),
     (957, 0.0012560630129558428),
     (958, 0.0008559349520685442),
     (962, 0.0011432075493084189),
     (966, 0.12753430785821307),
     (967, 0.047703783053191846),
     (971, 0.0019374811804289981),
     (973, 0.000509580601191055),
     (975, 0.00040766448095284403),
     (976, 0.00203832240476422),
     (980, 0.009502876097839338),
     (981, 0.016526808560115472),
     (982, 0.00101497410751472),
     (985, 0.03886905667648624),
     (988, 0.004382393170243073),
     (992, 0.0014268256833349542),
     (994, 0.007932889410844648),
     (995, 0.021725146310165012),
     (996, 0.011527628654373272),
     (997, 0.0022603947105004976),
     (998, 0.03014551231094022),
     (999, 0.009519467293013579),
     (1000, 0.00010191612023821101),
     (1004, 0.0011878595122299172),
     (1007, 0.011339003090038168),
     (1009, 0.004520789421000995),
     (1010, 0.0034296226479252566),
     (1012, 0.013194663397691361),
     (1013, 0.006089844645088321),
     (1016, 0.018752566123830826),
     (1018, 0.005911134973816238),
     (1019, 0.00020383224047642202),
     (1020, 0.0007134128416674771),
     (1022, 0.0022864150986168378),
     (1023, 0.0012916541202859988),
     (1024, 0.055986327757063456),
     (1026, 0.0017148113239626283),
     (1029, 0.00710481875260304),
     (1030, 0.0030449223225441605),
     (1031, 0.000611496721429266),
     (1037, 0.0007086876931273855),
     (1039, 0.0005716037746542094),
     (1042, 0.01110604517518251),
     (1045, 0.02000613211289733),
     (1048, 0.007703414568616897),
     (1050, 0.0015865778821689297),
     (1053, 0.006859245295850513),
     (1060, 0.002445986885717064),
     (1061, 0.019686503897576514),
     (1062, 0.004279674760342721),
     (1065, 0.009640638326734025),
     (1067, 0.0023757190244598344),
     (1068, 0.00931077699007072),
     (1077, 0.0011878595122299172),
     (1082, 0.004131702140028868),
     (1083, 0.06973566050781355),
     (1085, 0.01623958572023552),
     (1086, 0.0250310608776441),
     (1087, 0.001417375386254771),
     (1088, 0.0005716037746542094),
     (1089, 0.00968740590214499),
     (1092, 0.11889753916880946),
     (1093, 0.01110604517518251),
     (1094, 0.0013772340466762893),
     (1095, 0.0018206043795367997),
     (1096, 0.0045728301972336755),
     (1098, 0.0006458270601429994),
     (1103, 0.0031731557643378595),
     (1106, 0.0047597336465067894),
     (1107, 0.0022603947105004976),
     (1108, 0.009593515278639267),
     (1109, 0.0018206043795367997),
     (1110, 0.005489530011215495),
     (1112, 0.001773481331442042),
     (1115, 0.02203574474682063),
     (1117, 0.0022603947105004976),
     (1118, 0.004877073661465615),
     (1119, 0.0036412087590735995),
     (1120, 0.010149741075147201),
     (1122, 0.010690735610069255),
     (1123, 0.0031731557643378595),
     (1124, 0.0003229135300714997),
     (1125, 0.0020934383549264042),
     (1132, 0.0006280315064779214),
     (1135, 0.0031731557643378595),
     (1136, 0.0020859217398036746),
     (1142, 0.001222993442858532),
     (1145, 0.000611496721429266),
     (1146, 0.00101497410751472),
     (1148, 0.001324909563096743),
     (1154, 0.0015865778821689297),
     (1158, 0.0020859217398036746),
     (1161, 0.0015865778821689297),
     (1167, 0.005508936186705157),
     (1169, 0.001417375386254771),
     (1173, 0.001773481331442042),
     (1174, 0.0031401575323896065),
     (1175, 0.0009687405902144991),
     (1176, 0.0005716037746542094),
     (1177, 0.0023922081541910096),
     (1179, 0.02203574474682063),
     (1180, 0.0008373753419705617),
     (1182, 0.0015865778821689297),
     (1185, 0.00020934383549264042),
     (1186, 0.0027544680933525786),
     (1187, 0.001417375386254771),
     (1192, 0.006908346571257135),
     (1193, 0.00710481875260304),
     (1196, 0.003197838426213089),
     (1198, 0.0273207687812881),
     (1200, 0.0009687405902144991),
     (1208, 0.0034296226479252566),
     (1209, 0.0016306579238113761),
     (1210, 0.0022603947105004976),
     (1212, 0.00405989643005888),
     (1214, 0.0036412087590735995),
     (1218, 0.00020934383549264042),
     (1223, 0.018291320788934702),
     (1224, 0.006257765219411025),
     (1225, 0.006395676852426178),
     (1227, 0.0013772340466762893),
     (1228, 0.004520789421000995),
     (1229, 0.005233595887316011),
     (1230, 0.0021402385250024313),
     (1232, 0.00831501658560942),
     (1234, 0.004171843479607349),
     (1236, 0.030149182634514715),
     (1239, 0.0006280315064779214),
     (1240, 0.0016306579238113761),
     (1241, 0.000509580601191055),
     (1245, 0.004279674760342721),
     (1246, 0.0013772340466762893),
     (1247, 0.0028580188732710474),
     (1248, 0.02138147122013851),
     (1249, 0.0007086876931273855),
     (1251, 0.008263404280057736),
     (1254, 0.009103021897684),
     (1255, 0.12827247245605677),
     (1257, 0.0027544680933525786),
     (1258, 0.004001226422579465),
     (1259, 0.016687373918429397),
     (1260, 0.0016306579238113761),
     (1261, 0.0023922081541910096),
     (1264, 0.006489658900271853),
     (1267, 0.0018840945194337638),
     (1270, 0.0054618131386103995),
     (1272, 0.0008559349520685442),
     (1273, 0.0016306579238113761),
     (1275, 0.004382393170243073),
     (1278, 0.0016306579238113761),
     (1281, 0.10809521561292246),
     (1283, 0.005716037746542095),
     (1284, 0.0015865778821689297),
     (1285, 0.0022864150986168378),
     (1286, 0.0012560630129558428),
     (1290, 0.0042521261587643135),
     (1292, 0.00020383224047642202),
     (1293, 0.01116471518266192),
     (1294, 0.0018206043795367997),
     (1296, 0.000886740665721021),
     (1297, 0.0033495013678822468),
     (1300, 0.0006458270601429994),
     (1301, 0.005144433971887885),
     (1302, 0.005508936186705157),
     (1305, 0.00101497410751472),
     (1307, 0.006781184131501494),
     (1310, 0.0015287418035731652),
     (1311, 0.005442939722808651),
     (1314, 0.023338791534550322),
     (1315, 0.11339003090038167),
     (1317, 0.006280315064779213),
     (1319, 0.01116471518266192),
     (1320, 0.002751735246431697),
     (1322, 0.0011432075493084189),
     (1323, 0.041978758909294964),
     (1324, 0.010923626277220799),
     (1325, 0.001732574044049587),
     (1326, 0.00020934383549264042),
     (1327, 0.00020383224047642202),
     (1328, 0.0035588452033748874),
     (1331, 0.0022168516643025524),
     (1333, 0.09545783036725297),
     (1334, 0.0005716037746542094),
     (1335, 0.0031731557643378595),
     (1336, 0.0015865778821689297),
     (1337, 0.001222993442858532),
     (1338, 0.0021260630793821567),
     (1339, 0.0005716037746542094),
     (1340, 0.0017118699041370883),
     (1342, 0.07023893638049075),
     (1346, 0.013772340466762893),
     (1347, 0.0022603947105004976),
     (1349, 0.005991544664479809),
     (1351, 0.0012560630129558428),
     (1355, 0.0025121260259116855),
     (1356, 0.000611496721429266),
     (1359, 0.0030449223225441605),
     (1360, 0.0014654068484484832),
     (1363, 0.04312483011148393),
     (1364, 0.01323945473293149),
     (1379, 0.0022864150986168378),
     (1380, 0.0006280315064779214),
     (1381, 0.000886740665721021),
     (1390, 0.008504252317528627),
     (1393, 0.0006458270601429994),
     (1396, 0.00800245284515893),
     (1402, 0.0007086876931273855),
     (1406, 0.0020859217398036746),
     (1407, 0.0084240363243497),
     (1410, 0.0011432075493084189),
     (1411, 0.0032291353007149973),
     (1414, 0.001417375386254771),
     (1416, 0.0023757190244598344),
     (1418, 0.001222993442858532),
     (1423, 0.005320443994326125),
     (1425, 0.0022864150986168378),
     (1426, 0.0025678048562056324),
     (1428, 0.026796010943057974),
     (1430, 0.02341297879349692),
     (1433, 0.006287641521196303),
     (1439, 0.0027544680933525786),
     (1441, 0.0036412087590735995),
     (1442, 0.0023922081541910096),
     (1443, 0.0013772340466762893),
     (1445, 0.038426710078508466),
     (1449, 0.0031731557643378595),
     (1450, 0.0008373753419705617),
     (1451, 0.0008559349520685442),
     (1457, 0.0054015543726251836),
     (1464, 0.004877073661465615),
     (1465, 0.0017148113239626283),
     (1471, 0.031288248913130784),
     (1476, 0.003197838426213089),
     (1478, 0.0025678048562056324),
     (1480, 0.000917245082143899),
     (1482, 0.006257765219411025),
     (1488, 0.0011432075493084189),
     (1489, 0.005166616481143995),
     (1492, 0.007176624462573028),
     (1493, 0.0010467191774632021),
     (1497, 0.006886170233381447),
     (1500, 0.000509580601191055),
     (1502, 0.005074870537573601),
     (1503, 0.002751735246431697),
     (1506, 0.02482211360998778),
     (1520, 0.0027214698614043257),
     (1523, 0.016526808560115472),
     (1524, 0.0729948323921207),
     (1525, 0.004171843479607349),
     (1530, 0.0023757190244598344),
     (1532, 0.0036412087590735995),
     (1533, 0.0023757190244598344),
     (1534, 0.0021260630793821567),
     (1535, 0.0008373753419705617),
     (1536, 0.024095381566331106),
     (1540, 0.0013772340466762893),
     (1541, 0.00857405661981314),
     (1542, 0.0014268256833349542),
     (1543, 0.00931077699007072),
     (1544, 0.0032291353007149973),
     (1546, 0.009568832616764038),
     (1548, 0.006395676852426178),
     (1554, 0.017817892683448758),
     (1557, 0.0013772340466762893),
     (1559, 0.001732574044049587),
     (1561, 0.005911134973816238),
     (1566, 0.004960813851891699),
     (1568, 0.013772340466762893),
     (1572, 0.0015865778821689297),
     (1576, 0.0016306579238113761),
     (1577, 0.00020383224047642202),
     (1578, 0.000611496721429266),
     (1581, 0.012414369320094295),
     (1583, 0.0047597336465067894),
     (1587, 0.0017148113239626283),
     (1588, 0.0013772340466762893),
     (1589, 0.004171843479607349),
     (1590, 0.0020859217398036746),
     (1598, 0.00040766448095284403),
     (1601, 0.0022168516643025524),
     (1605, 0.0023757190244598344),
     (1607, 0.0034296226479252566),
     (1609, 0.004784416308382019),
     (1613, 0.005716037746542095),
     (1616, 0.008263404280057736),
     (1619, 0.0008559349520685442),
     (1624, 0.005135609712411265),
     (1625, 0.017254559827750243),
     (1627, 0.0011432075493084189),
     (1628, 0.040583868000448865),
     (1629, 0.002445986885717064),
     (1635, 0.007703414568616897),
     (1636, 0.003563578536689751),
     (1637, 0.013772340466762893),
     (1640, 0.009103021897684),
     (1642, 0.0035434384656369273),
     (1643, 0.0034296226479252566),
     (1644, 0.0020859217398036746),
     (1646, 0.006257765219411025),
     (1647, 0.0014268256833349542),
     (1648, 0.005991544664479809),
     (1649, 0.000509580601191055),
     (1650, 0.0012560630129558428),
     (1655, 0.0032613158476227522),
     (1657, 0.00998777978334468),
     (1661, 0.0016747506839411234),
     (1665, 0.002751735246431697),
     (1666, 0.0015287418035731652),
     (1667, 0.0012916541202859988),
     (1668, 0.004751438048919669),
     (1670, 0.03715424535252361),
     (1677, 0.0015287418035731652),
     (1680, 0.00101916120238211),
     (1684, 0.008263404280057736),
     (1686, 0.0014654068484484832),
     (1692, 0.0008153289619056881),
     (1695, 0.0012916541202859988),
     (1696, 0.012179689290176642),
     (1701, 0.005135609712411265),
     (1705, 0.0031035923300235736),
     (1708, 0.0035588452033748874),
     (1710, 0.001222993442858532),
     (1712, 0.000305748360714633),
     (1715, 0.0011878595122299172),
     (1716, 0.001732574044049587),
     (1719, 0.0003229135300714997),
     (1722, 0.0027544680933525786),
     (1727, 0.0011432075493084189),
     (1728, 0.10571949658846262),
     (1735, 0.00202994821502944),
     (1743, 0.0020934383549264042),
     (1744, 0.0009687405902144991),
     (1752, 0.026602219971630627),
     (1754, 0.007282417518147199),
     (1759, 0.008263404280057736),
     (1761, 0.0031401575323896065),
     (1762, 0.0008373753419705617),
     (1763, 0.0059392975611495865),
     (1766, 0.0014654068484484832),
     (1768, 0.007176624462573028),
     (1770, 0.0023757190244598344),
     (1772, 0.01626276408930234),
     (1774, 0.0031731557643378595),
     (1775, 0.0054618131386103995),
     (1778, 0.006859245295850513),
     (1779, 0.007282417518147199),
     (1780, 0.0010467191774632021),
     (1781, 0.002834750772509542),
     (1782, 0.004960813851891699),
     (1784, 0.0027544680933525786),
     (1785, 0.006395676852426178),
     (1793, 0.0020859217398036746),
     (1794, 0.0008559349520685442),
     (1797, 0.01883056894550797),
     (1798, 0.02109663688930968),
     (1799, 0.0047597336465067894),
     (1806, 0.002955567486908119),
     (1808, 0.006346311528675719),
     (1813, 0.0004433703328605105),
     (1815, 0.0013772340466762893),
     (1816, 0.0013772340466762893),
     (1820, 0.0023757190244598344),
     (1823, 0.008559349520685442),
     (1825, 0.0054618131386103995),
     (1832, 0.0011210773226203211),
     (1833, 0.0031035923300235736),
     (1834, 0.0008373753419705617),
     (1835, 0.0007086876931273855),
     (1838, 0.0005716037746542094),
     (1840, 0.0006280315064779214),
     (1841, 0.0015865778821689297),
     (1846, 0.006886170233381447),
     (1847, 0.005144433971887885),
     (1848, 0.009640638326734025),
     (1849, 0.00101916120238211),
     (1850, 0.005508936186705157),
     (1851, 0.009415284472753985),
     (1853, 0.017118699041370884),
     (1854, 0.0017118699041370883),
     (1857, 0.004382393170243073),
     (1858, 0.0029062217706434974),
     (1859, 0.04178560929766652),
     (1860, 0.003552048830786497),
     (1862, 0.00710481875260304),
     (1864, 0.0021260630793821567),
     (1866, 0.004131702140028868),
     (1869, 0.006346311528675719),
     (1876, 0.00020934383549264042),
     (1878, 0.07361040587789479),
     (1881, 0.020026648174904797),
     (1884, 0.006089844645088321),
     (1885, 0.00857405661981314),
     (1898, 0.005812443541286995),
     (1899, 0.0027544680933525786),
     (1904, 0.005508936186705157),
     (1905, 0.005135609712411265),
     (1906, 0.0008559349520685442),
     (1907, 0.0006458270601429994),
     (1908, 0.00040766448095284403),
     (1909, 0.0034237398082741766),
     (1910, 0.0027544680933525786),
     (1915, 0.0023922081541910096),
     (1916, 0.0013301109985815313),
     (1922, 0.01251553043882205),
     (1923, 0.0031731557643378595),
     (1926, 0.0025678048562056324),
     (1933, 0.001834490164287798),
     (1934, 0.000305748360714633),
     (1935, 0.007703414568616897),
     (1938, 0.006207184660047147),
     (1940, 0.006847479616548353),
     (1941, 0.0033495013678822468),
     (1942, 0.00010191612023821101),
     (1944, 0.0011878595122299172),
     (1945, 0.0012560630129558428),
     (1948, 0.0005716037746542094),
     (1949, 0.00499388989167234),
     (1951, 0.010690735610069255),
     (1952, 0.0023757190244598344),
     (1953, 0.0027544680933525786),
     (1958, 0.004784416308382019),
     (1959, 0.00020934383549264042),
     (1964, 0.007282417518147199),
     (1965, 0.00101497410751472),
     (1966, 0.01097906002243099),
     (1967, 0.00499388989167234),
     (1968, 0.005135609712411265),
     (1974, 0.01417375386254771),
     (1979, 0.0021260630793821567),
     (1980, 0.004279674760342721),
     (1981, 0.00203832240476422),
     (1982, 0.0013772340466762893),
     (1985, 0.015865778821689297),
     (1986, 0.061627316548935177),
     (1990, 0.011961040770955049),
     (1991, 0.0003229135300714997),
     (1993, 0.02065851070014434),
     (1994, 0.009134766967632482),
     (1997, 0.0025833082405719975),
     (2000, 0.0025121260259116855),
     (2001, 0.0007134128416674771),
     (2002, 0.001732574044049587),
     (2003, 0.00101497410751472),
     (2007, 0.0016306579238113761),
     (2010, 0.003977532874360168),
     (2012, 0.013607349307021628),
     (2013, 0.0013301109985815313),
     (2014, 0.0011210773226203211),
     (2018, 0.001417375386254771),
     (2020, 0.0016306579238113761),
     (2021, 0.0017118699041370883),
     (2022, 0.008255205739295092),
     (2023, 0.0005716037746542094),
     (2026, 0.00481490821633073),
     (2030, 0.0005716037746542094),
     (2031, 0.0018206043795367997),
     (2032, 0.0020859217398036746),
     (2037, 0.0005716037746542094),
     (2039, 0.008583097255198258),
     (2044, 0.0059392975611495865),
     (2045, 0.0010467191774632021),
     (2049, 0.0035434384656369273),
     (2051, 0.0008153289619056881),
     (2053, 0.003563578536689751),
     (2054, 0.000886740665721021),
     (2055, 0.001732574044049587),
     (2065, 0.001834490164287798),
     (2066, 0.0005716037746542094),
     (2067, 0.009921627703783398),
     (2068, 0.0018206043795367997),
     (2069, 0.0005716037746542094),
     (2073, 0.004751438048919669),
     (2074, 0.00101497410751472),
     (2076, 0.0031035923300235736),
     (2078, 0.0015865778821689297),
     (2082, 0.0011878595122299172),
     (2083, 0.0014654068484484832),
     (2084, 0.0011432075493084189),
     (2086, 0.0054618131386103995),
     (2087, 0.011304567116602583),
     (2088, 0.0003229135300714997),
     (2089, 0.000917245082143899),
     (2090, 0.003197838426213089),
     (2095, 0.0013772340466762893),
     (2096, 0.000886740665721021),
     (2102, 0.0027544680933525786),
     (2108, 0.004171843479607349),
     (2110, 0.0008559349520685442),
     (2111, 0.000917245082143899),
     (2114, 0.007086876931273855),
     (2116, 0.0023757190244598344),
     (2117, 0.004131702140028868),
     (2118, 0.02065851070014434),
     (2119, 0.004843702951072495),
     (2125, 0.0011878595122299172),
     (2127, 0.0023922081541910096),
     (2128, 0.0059392975611495865),
     (2133, 0.001417375386254771),
     (2134, 0.0038749623608579963),
     (2135, 0.0020859217398036746),
     (2136, 0.007932889410844648),
     (2138, 0.0021260630793821567),
     (2144, 0.039395450668722964),
     (2145, 0.001417375386254771),
     (2148, 0.0022421546452406423),
     (2152, 0.002302782190419045),
     (2154, 0.0014268256833349542),
     (2155, 0.0054618131386103995),
     (2156, 0.04131702140028868),
     (2158, 0.07758980825058934),
     (2159, 0.024359378580353284),
     (2162, 0.014290094366355236),
     (2164, 0.3274137142248521),
     (2165, 0.007537295658628679),
     (2169, 0.002547903005955275),
     (2170, 0.0012916541202859988),
     (2172, 0.00202994821502944),
     (2176, 0.006089844645088321),
     (2180, 0.0029308136968969663),
     (2183, 0.0026602219971630626),
     (2186, 0.02858018873271047),
     (2187, 0.04536455245963284),
     (2195, 0.013718490591701027),
     (2197, 0.02837570130307267),
     (2200, 0.0007086876931273855),
     (2202, 0.0013772340466762893),
     (2206, 0.01657650946497207),
     (2208, 0.00101497410751472),
     (2210, 0.026167446886849497),
     (2222, 0.0018206043795367997),
     (2223, 0.0018206043795367997),
     (2226, 0.0021402385250024313),
     (2227, 0.00202994821502944),
     (2229, 0.0054618131386103995),
     (2232, 0.00010191612023821101),
     (2233, 0.002445986885717064),
     (2234, 0.006346311528675719),
     (2235, 0.0047597336465067894),
     (2237, 0.00041868767098528084),
     (2238, 0.00020383224047642202),
     (2240, 0.0012916541202859988),
     (2241, 0.009640638326734025),
     (2242, 0.002834750772509542),
     (2244, 0.07437063852051962),
     (2249, 0.000886740665721021),
     (2250, 0.0022168516643025524),
     (2255, 0.005716037746542095),
     (2258, 0.0023922081541910096),
     (2264, 0.000305748360714633),
     (2266, 0.0020859217398036746),
     (2267, 0.00460556438083809),
     (2272, 0.004131702140028868),
     (2273, 0.004171843479607349),
     (2274, 0.002751735246431697),
     (2277, 0.0021260630793821567),
     (2279, 0.0023922081541910096),
     (2280, 0.005166616481143995),
     (2281, 0.0008373753419705617),
     (2282, 0.001732574044049587),
     (2284, 0.01306645463452909),
     (2285, 0.0023757190244598344),
     (2289, 0.006420715575007294),
     (2290, 0.005299638252386972),
     (2292, 0.004279674760342721),
     (2294, 0.0015865778821689297),
     (2296, 0.0015865778821689297),
     (2297, 0.00041868767098528084),
     (2300, 0.004001226422579465),
     (2302, 0.009103021897684),
     (2303, 0.00203832240476422),
     (2305, 0.005508936186705157),
     (2309, 0.01420963750520608),
     (2311, 0.008263404280057736),
     (2313, 0.0074308490705047225),
     (2315, 0.000886740665721021),
     (2317, 0.0022421546452406423),
     (2319, 0.0022864150986168378),
     (2320, 0.0031035923300235736),
     (2322, 0.0039903329957445945),
     (2325, 0.14818621969714912),
     (2328, 0.00101497410751472),
     (2330, 0.04287028309906571),
     (2332, 0.0020934383549264042),
     (2335, 0.004001226422579465),
     (2336, 0.01116471518266192),
     (2337, 0.0031731557643378595),
     (2339, 0.0030574836071463303),
     (2340, 0.03718531926025981),
     (2342, 0.0014654068484484832),
     (2343, 0.0025678048562056324),
     (2344, 0.0014654068484484832),
     (2346, 0.004960813851891699),
     (2349, 0.0034237398082741766),
     (2352, 0.0013301109985815313),
     (2353, 0.0009687405902144991),
     (2357, 0.06874270623335639),
     (2359, 0.0015865778821689297),
     (2361, 0.002649819126193486),
     (2363, 0.0006458270601429994),
     (2364, 0.007439876777389404),
     (2368, 0.027404300902897444),
     (2369, 0.0042521261587643135),
     (2370, 0.0013772340466762893),
     (2375, 0.007980665991489189),
     (2376, 0.003159399727384541),
     (2377, 0.0030574836071463303),
     (2378, 0.00857405661981314),
     (2381, 0.00202994821502944),
     (2382, 0.0016747506839411234),
     (2383, 0.000886740665721021),
     (2385, 0.0006458270601429994),
     (2387, 0.0003229135300714997),
     (2389, 0.0042521261587643135),
     (2392, 0.0006280315064779214),
     (2393, 0.00203832240476422),
     (2396, 0.006257765219411025),
     (2399, 0.011084258321512764),
     (2401, 0.00101497410751472),
     (2408, 0.016538163003918593),
     (2409, 0.019005752195678675),
     (2417, 0.0007086876931273855),
     (2418, 0.004131702140028868),
     (2419, 0.0013772340466762893),
     (2420, 0.0013301109985815313),
     (2421, 0.01064088798865225),
     (2422, 0.014187850651536335),
     (2423, 0.0019374811804289981),
     (2431, 0.0005716037746542094),
     (2432, 0.003159399727384541),
     (2433, 0.00010191612023821101),
     (2434, 0.0020934383549264042),
     (2444, 0.0005716037746542094),
     (2446, 0.02909879313347702),
     (2449, 0.0047597336465067894),
     ...]

```python
# This needs to be included at the beginning of every @tests cell.

import gensim.models.tfidfmodel


def test_model_type():
    assert isinstance(model, gensim.models.tfidfmodel.TfidfModel), \
    'The tf-idf model should be created using the TfidfModel() function and the model variable should be of type "gensim.models.tfidfmodel.TfidfModel".'
```

    1/1 tests passed

## 9. The results of the tf-idf model
<p>Once again, the format of those results is hard to interpret for a human. Therefore, we will transform it into a more readable version and display the 10 most specific words for the "<em>On the Origin of Species</em>" book.</p>

```python
# Convert the tf-idf model for "On the Origin of Species" into a DataFrame
df_tfidf = pd.DataFrame(model[bows[ori]])

# Name the columns of the DataFrame id and score
df_tfidf.columns = ['id', 'score']

# Add the tokens corresponding to the numerical indices for better readability
df_tfidf['token'] = df_tfidf['id'].apply(lambda x: dictionary[x])

# Sort the DataFrame by descending tf-idf score and print the first 10 rows.
df_tfidf = df_tfidf.sort_values('score', ascending=False)
df_tfidf.head(10)
```

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>score</th>
      <th>token</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>878</th>
      <td>2164</td>
      <td>0.327414</td>
      <td>select</td>
    </tr>
    <tr>
      <th>3106</th>
      <td>10108</td>
      <td>0.203908</td>
      <td>pigeon</td>
    </tr>
    <tr>
      <th>128</th>
      <td>369</td>
      <td>0.197721</td>
      <td>breed</td>
    </tr>
    <tr>
      <th>2988</th>
      <td>9396</td>
      <td>0.167496</td>
      <td>migrat</td>
    </tr>
    <tr>
      <th>945</th>
      <td>2325</td>
      <td>0.148186</td>
      <td>steril</td>
    </tr>
    <tr>
      <th>284</th>
      <td>752</td>
      <td>0.145990</td>
      <td>domest</td>
    </tr>
    <tr>
      <th>503</th>
      <td>1255</td>
      <td>0.128272</td>
      <td>hybrid</td>
    </tr>
    <tr>
      <th>370</th>
      <td>966</td>
      <td>0.127534</td>
      <td>fertil</td>
    </tr>
    <tr>
      <th>3889</th>
      <td>16210</td>
      <td>0.124392</td>
      <td>rtner</td>
    </tr>
    <tr>
      <th>3540</th>
      <td>12715</td>
      <td>0.121197</td>
      <td>naturalis</td>
    </tr>
  </tbody>
</table>

```python
# This needs to be included at the beginning of every @tests cell.

# One or more tests of the students code.
# The @solution should pass the tests.
# The purpose of the tests is to try to catch common errors and to
# give the student a hint on how to resolve these errors.

import pandas.core.frame

### Recomputing object to avoid hard-coded values
df_tfidf_test = pd.DataFrame(model[bows[ori]])
n_rows_test_tfidf = df_tfidf_test.shape[0]

def test_df_type():
    assert isinstance(df_tfidf, pandas.core.frame.DataFrame), \
    'The df_tfidf variable should contain a pandas DataFrame of type pandas.core.frame.DataFrame.'

def test_df_dim1():
    assert df_tfidf.shape[1] == 3, \
    'The df_bow_origin DataFrame should have 3 columns.'

def test_df_dim2():
    assert df_tfidf.shape[0] == n_rows_test_tfidf, \
    'The df_bow_origin DataFrame should have ' + str(n_rows_test_tfidf) + ' rows.'

def test_df_columns():
    assert all(df_tfidf.columns == list(["id", "score", "token"])), \
    'The columns of the df_bow_origin DataFrame should be named "id", "score" and "token".'
```

    4/4 tests passed

## 10. Compute distance between texts
<p>The results of the tf-idf algorithm now return stemmed tokens which are specific to each book. We can, for example, see that topics such as selection, breeding or domestication are defining "<em>On the Origin of Species</em>" (and yes, in this book, Charles Darwin talks quite a lot about pigeons too). Now that we have a model associating tokens to how specific they are to each book, we can measure how related to books are between each other.</p>
<p>To this purpose, we will use a measure of similarity called <strong>cosine similarity</strong> and we will visualize the results as a distance matrix, i.e., a matrix showing all pairwise distances between Darwin's books.</p>

```python
# Load the library allowing similarity computations
from gensim import similarities

# Compute the similarity matrix (pairwise distance between all texts)
sims = similarities.MatrixSimilarity(model[bows])

# Transform the resulting list into a dataframe
sim_df = pd.DataFrame(list(sims))

# Add the titles of the books as columns and index of the dataframe
sim_df.columns = titles
sim_df.index = titles

# Print the resulting matrix
sim_df
```

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Autobiography</th>
      <th>CoralReefs</th>
      <th>DescentofMan</th>
      <th>DifferentFormsofFlowers</th>
      <th>EffectsCrossSelfFertilization</th>
      <th>ExpressionofEmotionManAnimals</th>
      <th>FormationVegetableMould</th>
      <th>FoundationsOriginofSpecies</th>
      <th>GeologicalObservationsSouthAmerica</th>
      <th>InsectivorousPlants</th>
      <th>LifeandLettersVol1</th>
      <th>LifeandLettersVol2</th>
      <th>MonographCirripedia</th>
      <th>MonographCirripediaVol2</th>
      <th>MovementClimbingPlants</th>
      <th>OriginofSpecies</th>
      <th>PowerMovementPlants</th>
      <th>VariationPlantsAnimalsDomestication</th>
      <th>VolcanicIslands</th>
      <th>VoyageBeagle</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Autobiography</th>
      <td>1.000000</td>
      <td>0.049467</td>
      <td>0.080428</td>
      <td>0.066482</td>
      <td>0.077184</td>
      <td>0.088723</td>
      <td>0.040678</td>
      <td>0.059271</td>
      <td>0.030562</td>
      <td>0.014878</td>
      <td>0.396709</td>
      <td>0.217129</td>
      <td>0.005686</td>
      <td>0.008483</td>
      <td>0.022856</td>
      <td>0.099991</td>
      <td>0.016247</td>
      <td>0.049018</td>
      <td>0.038556</td>
      <td>0.183507</td>
    </tr>
    <tr>
      <th>CoralReefs</th>
      <td>0.049467</td>
      <td>1.000000</td>
      <td>0.009480</td>
      <td>0.001952</td>
      <td>0.001923</td>
      <td>0.004999</td>
      <td>0.029432</td>
      <td>0.022096</td>
      <td>0.061027</td>
      <td>0.002276</td>
      <td>0.030965</td>
      <td>0.017558</td>
      <td>0.006324</td>
      <td>0.010579</td>
      <td>0.001518</td>
      <td>0.039089</td>
      <td>0.002707</td>
      <td>0.011586</td>
      <td>0.057514</td>
      <td>0.267749</td>
    </tr>
    <tr>
      <th>DescentofMan</th>
      <td>0.080428</td>
      <td>0.009480</td>
      <td>1.000000</td>
      <td>0.072761</td>
      <td>0.029968</td>
      <td>0.148670</td>
      <td>0.027055</td>
      <td>0.135775</td>
      <td>0.009698</td>
      <td>0.009404</td>
      <td>0.059684</td>
      <td>0.080314</td>
      <td>0.053506</td>
      <td>0.043275</td>
      <td>0.005146</td>
      <td>0.267554</td>
      <td>0.011357</td>
      <td>0.232841</td>
      <td>0.007882</td>
      <td>0.123917</td>
    </tr>
    <tr>
      <th>DifferentFormsofFlowers</th>
      <td>0.066482</td>
      <td>0.001952</td>
      <td>0.072761</td>
      <td>1.000000</td>
      <td>0.391834</td>
      <td>0.006474</td>
      <td>0.010585</td>
      <td>0.040104</td>
      <td>0.002846</td>
      <td>0.007502</td>
      <td>0.015933</td>
      <td>0.046523</td>
      <td>0.009405</td>
      <td>0.005484</td>
      <td>0.008151</td>
      <td>0.128909</td>
      <td>0.018964</td>
      <td>0.050023</td>
      <td>0.002611</td>
      <td>0.013124</td>
    </tr>
    <tr>
      <th>EffectsCrossSelfFertilization</th>
      <td>0.077184</td>
      <td>0.001923</td>
      <td>0.029968</td>
      <td>0.391834</td>
      <td>1.000000</td>
      <td>0.006844</td>
      <td>0.032262</td>
      <td>0.040288</td>
      <td>0.002246</td>
      <td>0.006777</td>
      <td>0.019504</td>
      <td>0.046504</td>
      <td>0.003212</td>
      <td>0.002962</td>
      <td>0.014932</td>
      <td>0.146441</td>
      <td>0.039770</td>
      <td>0.055132</td>
      <td>0.002178</td>
      <td>0.017140</td>
    </tr>
    <tr>
      <th>ExpressionofEmotionManAnimals</th>
      <td>0.088723</td>
      <td>0.004999</td>
      <td>0.148670</td>
      <td>0.006474</td>
      <td>0.006844</td>
      <td>1.000000</td>
      <td>0.020985</td>
      <td>0.047202</td>
      <td>0.005217</td>
      <td>0.011475</td>
      <td>0.064873</td>
      <td>0.048886</td>
      <td>0.016825</td>
      <td>0.029897</td>
      <td>0.005913</td>
      <td>0.062979</td>
      <td>0.011317</td>
      <td>0.083847</td>
      <td>0.005561</td>
      <td>0.098961</td>
    </tr>
    <tr>
      <th>FormationVegetableMould</th>
      <td>0.040678</td>
      <td>0.029432</td>
      <td>0.027055</td>
      <td>0.010585</td>
      <td>0.032262</td>
      <td>0.020985</td>
      <td>1.000000</td>
      <td>0.021470</td>
      <td>0.067989</td>
      <td>0.035589</td>
      <td>0.027916</td>
      <td>0.023620</td>
      <td>0.019866</td>
      <td>0.023984</td>
      <td>0.038820</td>
      <td>0.049258</td>
      <td>0.040182</td>
      <td>0.033147</td>
      <td>0.059407</td>
      <td>0.097908</td>
    </tr>
    <tr>
      <th>FoundationsOriginofSpecies</th>
      <td>0.059271</td>
      <td>0.022096</td>
      <td>0.135775</td>
      <td>0.040104</td>
      <td>0.040288</td>
      <td>0.047202</td>
      <td>0.021470</td>
      <td>1.000000</td>
      <td>0.028028</td>
      <td>0.006023</td>
      <td>0.057820</td>
      <td>0.054782</td>
      <td>0.007618</td>
      <td>0.010883</td>
      <td>0.003973</td>
      <td>0.322405</td>
      <td>0.008788</td>
      <td>0.194533</td>
      <td>0.017590</td>
      <td>0.089132</td>
    </tr>
    <tr>
      <th>GeologicalObservationsSouthAmerica</th>
      <td>0.030562</td>
      <td>0.061027</td>
      <td>0.009698</td>
      <td>0.002846</td>
      <td>0.002246</td>
      <td>0.005217</td>
      <td>0.067989</td>
      <td>0.028028</td>
      <td>1.000000</td>
      <td>0.006879</td>
      <td>0.028551</td>
      <td>0.012104</td>
      <td>0.009687</td>
      <td>0.024738</td>
      <td>0.002043</td>
      <td>0.058046</td>
      <td>0.003491</td>
      <td>0.014389</td>
      <td>0.373249</td>
      <td>0.260141</td>
    </tr>
    <tr>
      <th>InsectivorousPlants</th>
      <td>0.014878</td>
      <td>0.002276</td>
      <td>0.009404</td>
      <td>0.007502</td>
      <td>0.006777</td>
      <td>0.011475</td>
      <td>0.035589</td>
      <td>0.006023</td>
      <td>0.006879</td>
      <td>1.000000</td>
      <td>0.005967</td>
      <td>0.016518</td>
      <td>0.019214</td>
      <td>0.020023</td>
      <td>0.249814</td>
      <td>0.014961</td>
      <td>0.023056</td>
      <td>0.010522</td>
      <td>0.008544</td>
      <td>0.014776</td>
    </tr>
    <tr>
      <th>LifeandLettersVol1</th>
      <td>0.396709</td>
      <td>0.030965</td>
      <td>0.059684</td>
      <td>0.015933</td>
      <td>0.019504</td>
      <td>0.064873</td>
      <td>0.027916</td>
      <td>0.057820</td>
      <td>0.028551</td>
      <td>0.005967</td>
      <td>1.000000</td>
      <td>0.885828</td>
      <td>0.005752</td>
      <td>0.012772</td>
      <td>0.005388</td>
      <td>0.097457</td>
      <td>0.009505</td>
      <td>0.055259</td>
      <td>0.026374</td>
      <td>0.171708</td>
    </tr>
    <tr>
      <th>LifeandLettersVol2</th>
      <td>0.217129</td>
      <td>0.017558</td>
      <td>0.080314</td>
      <td>0.046523</td>
      <td>0.046504</td>
      <td>0.048886</td>
      <td>0.023620</td>
      <td>0.054782</td>
      <td>0.012104</td>
      <td>0.016518</td>
      <td>0.885828</td>
      <td>1.000000</td>
      <td>0.004967</td>
      <td>0.010843</td>
      <td>0.017565</td>
      <td>0.096955</td>
      <td>0.012099</td>
      <td>0.050764</td>
      <td>0.011806</td>
      <td>0.089947</td>
    </tr>
    <tr>
      <th>MonographCirripedia</th>
      <td>0.005686</td>
      <td>0.006324</td>
      <td>0.053506</td>
      <td>0.009405</td>
      <td>0.003212</td>
      <td>0.016825</td>
      <td>0.019866</td>
      <td>0.007618</td>
      <td>0.009687</td>
      <td>0.019214</td>
      <td>0.005752</td>
      <td>0.004967</td>
      <td>1.000000</td>
      <td>0.522273</td>
      <td>0.012441</td>
      <td>0.029902</td>
      <td>0.018694</td>
      <td>0.023460</td>
      <td>0.010754</td>
      <td>0.014342</td>
    </tr>
    <tr>
      <th>MonographCirripediaVol2</th>
      <td>0.008483</td>
      <td>0.010579</td>
      <td>0.043275</td>
      <td>0.005484</td>
      <td>0.002962</td>
      <td>0.029897</td>
      <td>0.023984</td>
      <td>0.010883</td>
      <td>0.024738</td>
      <td>0.020023</td>
      <td>0.012772</td>
      <td>0.010843</td>
      <td>0.522273</td>
      <td>1.000000</td>
      <td>0.006802</td>
      <td>0.036755</td>
      <td>0.022376</td>
      <td>0.030669</td>
      <td>0.017952</td>
      <td>0.025047</td>
    </tr>
    <tr>
      <th>MovementClimbingPlants</th>
      <td>0.022856</td>
      <td>0.001518</td>
      <td>0.005146</td>
      <td>0.008151</td>
      <td>0.014932</td>
      <td>0.005913</td>
      <td>0.038820</td>
      <td>0.003973</td>
      <td>0.002043</td>
      <td>0.249814</td>
      <td>0.005388</td>
      <td>0.017565</td>
      <td>0.012441</td>
      <td>0.006802</td>
      <td>1.000000</td>
      <td>0.008802</td>
      <td>0.104966</td>
      <td>0.011530</td>
      <td>0.002832</td>
      <td>0.012282</td>
    </tr>
    <tr>
      <th>OriginofSpecies</th>
      <td>0.099991</td>
      <td>0.039089</td>
      <td>0.267554</td>
      <td>0.128909</td>
      <td>0.146441</td>
      <td>0.062979</td>
      <td>0.049258</td>
      <td>0.322405</td>
      <td>0.058046</td>
      <td>0.014961</td>
      <td>0.097457</td>
      <td>0.096955</td>
      <td>0.029902</td>
      <td>0.036755</td>
      <td>0.008802</td>
      <td>1.000000</td>
      <td>0.018266</td>
      <td>0.405333</td>
      <td>0.036014</td>
      <td>0.164661</td>
    </tr>
    <tr>
      <th>PowerMovementPlants</th>
      <td>0.016247</td>
      <td>0.002707</td>
      <td>0.011357</td>
      <td>0.018964</td>
      <td>0.039770</td>
      <td>0.011317</td>
      <td>0.040182</td>
      <td>0.008788</td>
      <td>0.003491</td>
      <td>0.023056</td>
      <td>0.009505</td>
      <td>0.012099</td>
      <td>0.018694</td>
      <td>0.022376</td>
      <td>0.104966</td>
      <td>0.018266</td>
      <td>1.000000</td>
      <td>0.020589</td>
      <td>0.003819</td>
      <td>0.024149</td>
    </tr>
    <tr>
      <th>VariationPlantsAnimalsDomestication</th>
      <td>0.049018</td>
      <td>0.011586</td>
      <td>0.232841</td>
      <td>0.050023</td>
      <td>0.055132</td>
      <td>0.083847</td>
      <td>0.033147</td>
      <td>0.194533</td>
      <td>0.014389</td>
      <td>0.010522</td>
      <td>0.055259</td>
      <td>0.050764</td>
      <td>0.023460</td>
      <td>0.030669</td>
      <td>0.011530</td>
      <td>0.405333</td>
      <td>0.020589</td>
      <td>1.000000</td>
      <td>0.012620</td>
      <td>0.114134</td>
    </tr>
    <tr>
      <th>VolcanicIslands</th>
      <td>0.038556</td>
      <td>0.057514</td>
      <td>0.007882</td>
      <td>0.002611</td>
      <td>0.002178</td>
      <td>0.005561</td>
      <td>0.059407</td>
      <td>0.017590</td>
      <td>0.373249</td>
      <td>0.008544</td>
      <td>0.026374</td>
      <td>0.011806</td>
      <td>0.010754</td>
      <td>0.017952</td>
      <td>0.002832</td>
      <td>0.036014</td>
      <td>0.003819</td>
      <td>0.012620</td>
      <td>1.000000</td>
      <td>0.138323</td>
    </tr>
    <tr>
      <th>VoyageBeagle</th>
      <td>0.183507</td>
      <td>0.267749</td>
      <td>0.123917</td>
      <td>0.013124</td>
      <td>0.017140</td>
      <td>0.098961</td>
      <td>0.097908</td>
      <td>0.089132</td>
      <td>0.260141</td>
      <td>0.014776</td>
      <td>0.171708</td>
      <td>0.089947</td>
      <td>0.014342</td>
      <td>0.025047</td>
      <td>0.012282</td>
      <td>0.164661</td>
      <td>0.024149</td>
      <td>0.114134</td>
      <td>0.138323</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>

```python
import gensim.similarities.docsim
import pandas.core.frame
import pandas.core.indexes.base

def test_sims_type():
    assert isinstance(sims, gensim.similarities.docsim.MatrixSimilarity), \
    'The sims variable should be created using the similarities.MatrixSimilarity() function and be of type gensim.similarities.docsim.MatrixSimilarity.'

def test_sim_df_type():
    assert isinstance(sim_df, pandas.core.frame.DataFrame), \
    'The sim_df variable should be a pandas DataFrame of type pandas.core.frame.DataFrame.'

def test_df_dims():
    assert sim_df.shape[0] == 20 and sim_df.shape[1] == 20 , \
    'The sim_df DataFrame should have 20 rows and 20 columns.'

def test_df_columns():
    assert all(sim_df.columns == titles), \
    'The columns of the sim_df DataFrame should be the titles of the books (contained in the titles variable).'

# This test isn't working properly and is redundant with the following one. Hence, it is disabled.
#def test_df_index_type():
#    assert isinstance(sim_df.index, pandas.core.indexes.base.Index), \
#    'The index of the sim_df DataFrame should be of type pandas.core.indexes.base.Index. Make sure the index contains the titles of the books, and not numbers.'

def test_df_index_content():
    assert  list(sim_df.index) == titles , \
    'The index of the sim_df DataFrame should contain the titles of the books, contained in the titles variable. For example, use: sim_df.index = titles.'
```

   5/5 tests passed

## 11. The book most similar to "On the Origin of Species"
<p>We now have a matrix containing all the similarity measures between any pair of books from Charles Darwin! We can now use this matrix to quickly extract the information we need, i.e., the distance between one book and one or several others. </p>
<p>As a first step, we will display which books are the most similar to "<em>On the Origin of Species</em>," more specifically we will produce a bar chart showing all books ranked by how similar they are to Darwin's landmark work.</p>

```python
# This is needed to display plots in a notebook
%matplotlib inline

# Import libraries
import matplotlib.pyplot as plt

# Select the column corresponding to "On the Origin of Species" and
v = sim_df['OriginofSpecies']

# Sort by ascending scores
v_sorted = v.sort_values()

# Plot this data has a horizontal bar plot
v_sorted.plot.barh(x='lab', y='val', rot=0).plot()

# Modify the axes labels and plot title for a better readability
plt.xlabel("Score")
plt.ylabel("Book")
plt.title("Similarity")
```

    <matplotlib.text.Text at 0x7fd87278aef0>

![png](images/output_31_1.png)

```python
# This needs to be included at the beginning of every @tests cell.

# One or more tests of the students code.
# The @solution should pass the tests.
# The purpose of the tests is to try to catch common errors and to
# give the student a hint on how to resolve these errors.

import pandas.core.series

v_sorted_list = list(v_sorted) # We collapse this into a list to avoid issues if indices are wrong

## Variable types
def test_v_type():
    assert isinstance(v, pandas.core.series.Series), \
    'The v variable should be a series of type pandas.core.series.Series.'

def test_v_sorted_type():
    assert isinstance(v_sorted, pandas.core.series.Series), \
    'The v_sorted variable should be a series of type pandas.core.series.Series.'

## Variable lengths
def test_v_len():
    assert len(v) == 20, \
    'The v series should be of length 20.'

def test_v_sorted_len():
    assert len(v_sorted) == 20, \
    'The v_sorted series should be of length 20.'

## Is the series sorted?
def test_is_series_sorted():
    assert all(v_sorted_list[i] <= v_sorted_list[i+1] for i in range(len(v_sorted_list)-1)), \
    'The v_sorted series should be sorted by ascending scores.'
```

    5/5 tests passed

## 12. Which books have similar content?
<p>This turns out to be extremely useful if we want to determine a given book's most similar work. For example, we have just seen that if you enjoyed "<em>On the Origin of Species</em>," you can read books discussing similar concepts such as "<em>The Variation of Animals and Plants under Domestication</em>" or "<em>The Descent of Man, and Selection in Relation to Sex</em>." If you are familiar with Darwin's work, these suggestions will likely seem natural to you. Indeed, <em>On the Origin of Species</em> has a whole chapter about domestication and <em>The Descent of Man, and Selection in Relation to Sex</em> applies the theory of natural selection to human evolution. Hence, the results make sense.</p>
<p>However, we now want to have a better understanding of the big picture and see how Darwin's books are generally related to each other (in terms of topics discussed). To this purpose, we will represent the whole similarity matrix as a dendrogram, which is a standard tool to display such data. <strong>This last approach will display all the information about book similarities at once.</strong> For example, we can find a book's closest relative but, also, we can visualize which groups of books have similar topics (e.g., the cluster about Charles Darwin personal life with his autobiography and letters). If you are familiar with Darwin's bibliography, the results should not surprise you too much, which indicates the method gives good results. Otherwise, next time you read one of the author's book, you will know which other books to read next in order to learn more about the topics it addressed.</p>


```python
# Import libraries
from scipy.cluster import hierarchy

# Compute the clusters from the similarity matrix,
# using the Ward variance minimization algorithm
Z = hierarchy.linkage(sims, 'ward')

# Display this result as a horizontal dendrogram
hierarchy.dendrogram(Z, leaf_font_size=8, labels=sim_df.index, orientation='left')
```

    {'icoord': [[15.0, 15.0, 25.0, 25.0],
      [5.0, 5.0, 20.0, 20.0],
      [55.0, 55.0, 65.0, 65.0],
      [45.0, 45.0, 60.0, 60.0],
      [35.0, 35.0, 52.5, 52.5],
      [75.0, 75.0, 85.0, 85.0],
      [95.0, 95.0, 105.0, 105.0],
      [115.0, 115.0, 125.0, 125.0],
      [100.0, 100.0, 120.0, 120.0],
      [135.0, 135.0, 145.0, 145.0],
      [155.0, 155.0, 165.0, 165.0],
      [185.0, 185.0, 195.0, 195.0],
      [175.0, 175.0, 190.0, 190.0],
      [160.0, 160.0, 182.5, 182.5],
      [140.0, 140.0, 171.25, 171.25],
      [110.0, 110.0, 155.625, 155.625],
      [80.0, 80.0, 132.8125, 132.8125],
      [43.75, 43.75, 106.40625, 106.40625],
      [12.5, 12.5, 75.078125, 75.078125]],
     'dcoord': [[0.0, 0.2614022284757893, 0.2614022284757893, 0.0],
      [0.0, 1.3236890048907108, 1.3236890048907108, 0.2614022284757893],
      [0.0, 0.8674413968985818, 0.8674413968985818, 0.0],
      [0.0, 1.1416963762963117, 1.1416963762963117, 0.8674413968985818],
      [0.0, 1.1971846842906972, 1.1971846842906972, 1.1416963762963117],
      [0.0, 0.6763229592290168, 0.6763229592290168, 0.0],
      [0.0, 0.8951415948353619, 0.8951415948353619, 0.0],
      [0.0, 1.1046849530861735, 1.1046849530861735, 0.0],
      [0.8951415948353619,
       1.528753257879734,
       1.528753257879734,
       1.1046849530861735],
      [0.0, 0.8619942648514105, 0.8619942648514105, 0.0],
      [0.0, 1.0643246586447814, 1.0643246586447814, 0.0],
      [0.0, 1.3650120145801365, 1.3650120145801365, 0.0],
      [0.0, 1.4204909376669876, 1.4204909376669876, 1.3650120145801365],
      [1.0643246586447814,
       1.5488870372890475,
       1.5488870372890475,
       1.4204909376669876],
      [0.8619942648514105,
       1.8572464487515041,
       1.8572464487515041,
       1.5488870372890475],
      [1.528753257879734,
       1.9985744662795528,
       1.9985744662795528,
       1.8572464487515041],
      [0.6763229592290168,
       2.085712452282797,
       2.085712452282797,
       1.9985744662795528],
      [1.1971846842906972,
       2.1421800100995623,
       2.1421800100995623,
       2.085712452282797],
      [1.3236890048907108,
       2.54823657155394,
       2.54823657155394,
       2.1421800100995623]],
     'ivl': ['Autobiography',
      'LifeandLettersVol1',
      'LifeandLettersVol2',
      'DescentofMan',
      'FoundationsOriginofSpecies',
      'OriginofSpecies',
      'VariationPlantsAnimalsDomestication',
      'MonographCirripedia',
      'MonographCirripediaVol2',
      'GeologicalObservationsSouthAmerica',
      'VolcanicIslands',
      'CoralReefs',
      'VoyageBeagle',
      'DifferentFormsofFlowers',
      'EffectsCrossSelfFertilization',
      'InsectivorousPlants',
      'MovementClimbingPlants',
      'ExpressionofEmotionManAnimals',
      'FormationVegetableMould',
      'PowerMovementPlants'],
     'leaves': [0,
      10,
      11,
      2,
      7,
      15,
      17,
      12,
      13,
      8,
      18,
      1,
      19,
      3,
      4,
      9,
      14,
      5,
      6,
      16],
     'color_list': ['g',
      'g',
      'r',
      'r',
      'r',
      'c',
      'm',
      'm',
      'm',
      'y',
      'k',
      'k',
      'k',
      'k',
      'b',
      'b',
      'b',
      'b',
      'b']}

![png](images/output_34_1.png)

```python
import numpy

def test_Z_type():
    assert isinstance(Z, numpy.ndarray), \
    'The Z variable should be generated by the hierarchy.linkage() function and of type numpy.ndarray.'
```

    1/1 tests passed
