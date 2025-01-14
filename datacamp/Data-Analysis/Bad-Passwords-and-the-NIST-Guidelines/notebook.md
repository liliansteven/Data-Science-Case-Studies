
## 1. The NIST Special Publication 800-63B
<p>If you – 50 years ago – needed to come up with a secret password you were probably part of a secret espionage organization or (more likely) you were pretending to be a spy when playing as a kid. Today, many of us are forced to come up with new passwords <em>all the time</em> when signing into sites and apps. As a password <em>inventeur</em> it is your responsibility to come up with good, hard-to-crack passwords. But it is also in the interest of sites and apps to make sure that you use good passwords. The problem is that it's really hard to define what makes a good password. However, <em>the National Institute of Standards and Technology</em> (NIST) knows what the second best thing is: To make sure you're at least not using a <em>bad</em> password. </p>
<p>In this notebook, we will go through the rules in <a href="https://pages.nist.gov/800-63-3/sp800-63b.html">NIST Special Publication 800-63B</a> which details what checks a <em>verifier</em> (what the NIST calls a second party responsible for storing and verifying passwords) should perform to make sure users don't pick bad passwords. We will go through the passwords of users from a fictional company and use Python to flag the users with bad passwords. But us being able to do this already means the fictional company is breaking one of the rules of 800-63B:</p>
<blockquote>
  <p>Verifiers SHALL store memorized secrets in a form that is resistant to offline attacks. Memorized secrets SHALL be salted and hashed using a suitable one-way key derivation function.</p>
</blockquote>
<p>That is, never save users' passwords in plaintext, always encrypt the passwords! Keeping this in mind for the next time we're building a password management system, let's load in the data.</p>
<p><em>Warning: The list of passwords and the fictional user database both contain <strong>real</strong> passwords leaked from <strong>real</strong> websites. These passwords have not been filtered in any way and include words that are explicit, derogatory and offensive.</em></p>

```python
# Importing the pandas module
import pandas as pd

# Loading in datasets/users.csv
users = pd.read_csv('datasets/users.csv')

# Printing out how many users we've got
print(users.shape[0])

# Taking a look at the 12 first users
users.head()
```

    982

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>user_name</th>
      <th>password</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>vance.jennings</td>
      <td>joobheco</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>consuelo.eaton</td>
      <td>0869347314</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>mitchel.perkins</td>
      <td>fabypotter</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>odessa.vaughan</td>
      <td>aharney88</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>araceli.wilder</td>
      <td>acecdn3000</td>
    </tr>
  </tbody>
</table>

```python
import pandas as pd

def test_users_read_in_correctly():
    correct_users = pd.read_csv("datasets/users.csv")
    assert correct_users.equals(users), \
    '`users` should contain the data in "datasets/users.csv".'
```

    1/1 tests passed

## 2. Passwords should not be too short
<p>If we take a look at the first 12 users above we already see some bad passwords. But let's not get ahead of ourselves and start flagging passwords <em>manually</em>. What is the first thing we should check according to the NIST Special Publication 800-63B?</p>
<blockquote>
  <p>Verifiers SHALL require subscriber-chosen memorized secrets to be at least 8 characters in length.</p>
</blockquote>
<p>Ok, so the passwords of our users shouldn't be too short. Let's start by checking that!</p>

```python
# Calculating the lengths of users' passwords
users['length'] = users['password'].str.len()

# Flagging the users with too short passwords
users['too_short'] = users['length'] < 8

# Counting and printing the number of users with too short passwords
print(users['too_short'].sum())

# Taking a look at the 12 first rows
users.head()
```

    376

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>user_name</th>
      <th>password</th>
      <th>length</th>
      <th>too_short</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>vance.jennings</td>
      <td>joobheco</td>
      <td>8</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>consuelo.eaton</td>
      <td>0869347314</td>
      <td>10</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>mitchel.perkins</td>
      <td>fabypotter</td>
      <td>10</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>odessa.vaughan</td>
      <td>aharney88</td>
      <td>9</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>araceli.wilder</td>
      <td>acecdn3000</td>
      <td>10</td>
      <td>False</td>
    </tr>
  </tbody>
</table>

```python
def test_length_sum_correct():
    assert (users['password'].str.len() < 8).sum() == users['too_short'].sum(), \
    "users['too_short'] should be a True/False column where all rows with passwords < 8 are True."
```

    1/1 tests passed

## 3.  Common passwords people use
<p>Already this simple rule flagged a couple of offenders among the first 12 users. Next up in Special Publication 800-63B is the rule that</p>
<blockquote>
  <p>Verifiers SHALL compare the prospective secrets against a list that contains values known to be commonly-used, expected, or compromised.</p>
  <ul>
  <li>Passwords obtained from previous breach corpuses.</li>
  <li>Dictionary words.</li>
  <li>Repetitive or sequential characters (e.g. ‘aaaaaa’, ‘1234abcd’).</li>
  <li>Context-specific words, such as the name of the service, the username, and derivatives thereof.</li>
  </ul>
</blockquote>
<p>We're going to check these in order and start with <em>Passwords obtained from previous breach corpuses</em>, that is, websites where hackers have leaked all the users' passwords. As many websites don't follow the NIST guidelines and encrypt passwords there now exist large lists of the most popular passwords. Let's start by loading in the 10,000 most common passwords which I've taken from <a href="https://github.com/danielmiessler/SecLists/tree/master/Passwords">here</a>.</p>

```python
# Reading in the top 10000 passwords
common_passwords = pd.read_csv('datasets/10_million_password_list_top_10000.txt',
                              header=None,
                              squeeze=True)

# Taking a look at the top 20
common_passwords[:20]
```

    0        123456
    1      password
    2      12345678
    3        qwerty
    4     123456789
    5         12345
    6          1234
    7        111111
    8       1234567
    9        dragon
    10       123123
    11     baseball
    12       abc123
    13     football
    14       monkey
    15      letmein
    16       696969
    17       shadow
    18       master
    19       666666
    Name: 0, dtype: object

```python
def test_common_passwords_correct():
    correct_common_passwords = pd.read_csv("datasets/10_million_password_list_top_10000.txt",
                                           header=None, squeeze=True)
    assert correct_common_passwords.equals(common_passwords), \
    'datasets/10_million_password_list_top_10000.txt should be read as a Series and put into common_passwords.'
```

    1/1 tests passed

## 4.  Passwords should not be common passwords
<p>The list of passwords was ordered, with the most common passwords first, and so we shouldn't be surprised to see passwords like <code>123456</code> and <code>qwerty</code> above. As hackers also have access to this list of common passwords, it's important that none of our users use these passwords!</p>
<p>Let's flag all the passwords in our user database that are among the top 10,000 used passwords.</p>

```python
# Flagging the users with passwords that are common passwords
users['common_password'] = users['password'].isin(common_passwords)

# Counting and printing the number of users using common passwords
print(users['common_password'].sum())

# Taking a look at the 12 first rows
users.head()
```

    129

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>user_name</th>
      <th>password</th>
      <th>length</th>
      <th>too_short</th>
      <th>common_password</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>vance.jennings</td>
      <td>joobheco</td>
      <td>8</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>consuelo.eaton</td>
      <td>0869347314</td>
      <td>10</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>mitchel.perkins</td>
      <td>fabypotter</td>
      <td>10</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>odessa.vaughan</td>
      <td>aharney88</td>
      <td>9</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>araceli.wilder</td>
      <td>acecdn3000</td>
      <td>10</td>
      <td>False</td>
      <td>False</td>
    </tr>
  </tbody>
</table>

```python
def test_example():
    assert users['password'].isin(common_passwords).sum() == users['common_password'].sum(), \
    "users['common_password'] should be True for each row with a password that is also in common_passwords."
```

    1/1 tests passed

## 5. Passwords should not be common words
<p>Ay ay ay! It turns out many of our users use common passwords, and of the first 12 users there are already two. However, as most common passwords also tend to be short, they were already flagged as being too short. What is the next thing we should check?</p>
<blockquote>
  <p>Verifiers SHALL compare the prospective secrets against a list that contains […] dictionary words.</p>
</blockquote>
<p>This follows the same logic as before: It is easy for hackers to check users' passwords against common English words and therefore common English words make bad passwords. Let's check our users' passwords against the top 10,000 English words from <a href="https://github.com/first20hours/google-10000-english">Google's Trillion Word Corpus</a>.</p>

```python
# Reading in a list of the 10000 most common words
words = pd.read_csv('datasets/google-10000-english.txt',
                   header=None,
                   squeeze=True)

# Flagging the users with passwords that are common words
users['common_word'] = users['password'].str.lower().isin(words)

# Counting and printing the number of users using common words as passwords
print(users['common_word'].sum())

# Taking a look at the 12 first rows
users.head()
```

    137

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>user_name</th>
      <th>password</th>
      <th>length</th>
      <th>too_short</th>
      <th>common_password</th>
      <th>common_word</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>vance.jennings</td>
      <td>joobheco</td>
      <td>8</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>consuelo.eaton</td>
      <td>0869347314</td>
      <td>10</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>mitchel.perkins</td>
      <td>fabypotter</td>
      <td>10</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>odessa.vaughan</td>
      <td>aharney88</td>
      <td>9</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>araceli.wilder</td>
      <td>acecdn3000</td>
      <td>10</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
  </tbody>
</table>

```python
def test_words_correct():
    correct_words = pd.read_csv("datasets/google-10000-english.txt",
                    header=None, squeeze=True)
    assert correct_words.equals(words), \
    'datasets/google-10000-english.txt should be read in as a Series and put into words.'

def test_common_words_correct():
    assert users['password'].str.lower().isin(words).sum() == users['common_word'].sum() , \
    "users['common_word'] should be True for each row with a password that is also in words."
```

    2/2 tests passed

## 6. Passwords should not be your name
<p>It turns out many of our passwords were common English words too! Next up on the NIST list:</p>
<blockquote>
  <p>Verifiers SHALL compare the prospective secrets against a list that contains […] context-specific words, such as the name of the service, the username, and derivatives thereof.</p>
</blockquote>
<p>Ok, so there are many things we could check here. One thing to notice is that our users' usernames consist of their first names and last names separated by a dot. For now, let's just flag passwords that are the same as either a user's first or last name.</p>

```python
# Extracting first and last names into their own columns
users['first_name'] = users['user_name'].str.extract(r'(\w+$)', expand = False)
users['last_name'] = users['user_name'].str.extract(r'(^\w+)', expand = False)

# Flagging the users with passwords that matches their names
users['uses_name'] = (users['password'] == users['first_name']) | (users['password'] == users['last_name'])
# Counting and printing the number of users using names as passwords
print(users['uses_name'].sum())

# Taking a look at the 12 first rows
users.head()
```

    50

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>user_name</th>
      <th>password</th>
      <th>length</th>
      <th>too_short</th>
      <th>common_password</th>
      <th>common_word</th>
      <th>first_name</th>
      <th>last_name</th>
      <th>uses_name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>vance.jennings</td>
      <td>joobheco</td>
      <td>8</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>jennings</td>
      <td>vance</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>consuelo.eaton</td>
      <td>0869347314</td>
      <td>10</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>eaton</td>
      <td>consuelo</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>mitchel.perkins</td>
      <td>fabypotter</td>
      <td>10</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>perkins</td>
      <td>mitchel</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>odessa.vaughan</td>
      <td>aharney88</td>
      <td>9</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>vaughan</td>
      <td>odessa</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>araceli.wilder</td>
      <td>acecdn3000</td>
      <td>10</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>wilder</td>
      <td>araceli</td>
      <td>False</td>
    </tr>
  </tbody>
</table>

```python
def test_not_same_as_name():
    correct_first_name = users['user_name'].str.extract(r'(^\w+)', expand = False)
    correct_last_name = users['user_name'].str.extract(r'(\w+$)', expand = False)

    # Flagging the users with passwords that matches their names
    correct_uses_name = (
        (users['password'].str.lower() == users['first_name']) |
        (users['password'].str.lower() == users['last_name']))

    assert correct_uses_name.sum() == users['uses_name'].sum(), \
    "users['uses_name'] should be True for each row with a password which is also the first or last name."
```

    1/1 tests passed

## 7. Passwords should not be repetitive
<p>Milford Hubbard (user number 12 above), what where you thinking!? Ok, so the last thing we are going to check is a bit tricky:</p>
<blockquote>
  <p>Verifiers SHALL compare the prospective secrets [so that they don't contain] repetitive or sequential characters (e.g. ‘aaaaaa’, ‘1234abcd’).</p>
</blockquote>
<p>This is tricky to check because what is <em>repetitive</em> is hard to define. Is <code>11111</code> repetitive? Yes! Is <code>12345</code> repetitive? Well, kind of. Is <code>13579</code> repetitive? Maybe not..? To check for <em>repetitiveness</em> can be arbitrarily complex, but here we're only going to do something simple. We're going to flag all passwords that contain 4 or more repeated characters.</p>

```python
### Flagging the users with passwords with >= 4 repeats
users['too_many_repeats'] = users['password'].str.contains(r'(.)\1\1\1')

# Taking a look at the users with too many repeats
users[users['too_many_repeats']]
```

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>user_name</th>
      <th>password</th>
      <th>length</th>
      <th>too_short</th>
      <th>common_password</th>
      <th>common_word</th>
      <th>first_name</th>
      <th>last_name</th>
      <th>uses_name</th>
      <th>too_many_repeats</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>146</th>
      <td>147</td>
      <td>patti.dixon</td>
      <td>555555</td>
      <td>6</td>
      <td>True</td>
      <td>True</td>
      <td>False</td>
      <td>dixon</td>
      <td>patti</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>572</th>
      <td>573</td>
      <td>cornelia.bradley</td>
      <td>555555</td>
      <td>6</td>
      <td>True</td>
      <td>True</td>
      <td>False</td>
      <td>bradley</td>
      <td>cornelia</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>644</th>
      <td>645</td>
      <td>essie.lopez</td>
      <td>11111</td>
      <td>5</td>
      <td>True</td>
      <td>True</td>
      <td>False</td>
      <td>lopez</td>
      <td>essie</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>798</th>
      <td>799</td>
      <td>charley.key</td>
      <td>888888</td>
      <td>6</td>
      <td>True</td>
      <td>True</td>
      <td>False</td>
      <td>key</td>
      <td>charley</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>807</th>
      <td>808</td>
      <td>thurman.osborne</td>
      <td>rinnnng0</td>
      <td>8</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>osborne</td>
      <td>thurman</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>941</th>
      <td>942</td>
      <td>mitch.ferguson</td>
      <td>aaaaaa</td>
      <td>6</td>
      <td>True</td>
      <td>True</td>
      <td>False</td>
      <td>ferguson</td>
      <td>mitch</td>
      <td>False</td>
      <td>True</td>
    </tr>
  </tbody>
</table>

```python
def test_too_many_repeats():
    assert users['password'].str.contains(r'(.)\1\1\1').sum() == users['too_many_repeats'].sum(), \
    "users['too_many_repeats'] should be True for each row with a password with 4 or more repeats."
```

    1/1 tests passed

## 8. All together now!
<p>Now we have implemented all the basic tests for bad passwords suggested by NIST Special Publication 800-63B! What's left is just to flag all bad passwords and maybe to send these users an e-mail that strongly suggests they change their password.</p>

```python
# Flagging all passwords that are bad
users['bad_password'] = (users['too_short']) | (users['common_password']) | (users['common_word']) | (users['uses_name']) | (users['too_many_repeats'])

# Counting and printing the number of bad passwords
print(users['bad_password'].sum())

# Looking at the first 25 bad passwords
users[users['bad_password']]['password'][:25]
```

    424

    5       5278049
    6        master
    7        murphy
    8       lwsves2
    11      hubbard
    13       310356
    15      oZ4k0QE
    16      chelsea
    17      zvc1939
    18       nickgd
    21     cocacola
    22      woodard
    25        AJ9Da
    26       ewokzs
    28      YyGjz8E
    30         reid
    34      jOYZBs8
    38      wwewwf1
    43       225377
    45       NdZ7E6
    47        CQB3Z
    48        diffo
    51    123456789
    52      y8uM7D6
    56      mikeloo
    Name: password, dtype: object

```python
def test_all_nist_rules():
    correct_bad_password = (
        users['too_short'] |
        users['common_password'] |
        users['common_word'] |
        users['uses_name'] |
        users['too_many_repeats'] )
    assert correct_bad_password.sum() == users['bad_password'].sum(), \
    "All rows with passwords that should be flagged as bad should have users['bad_password'] set to True."
```

    1/1 tests passed

## 9. Otherwise, the password should be up to the user
<p>In this notebook, we've implemented the password checks recommended by the NIST Special Publication 800-63B. It's certainly possible to better implement these checks, for example, by using a longer list of common passwords. Also note that the NIST checks in no way guarantee that a chosen password is good, just that it's not obviously bad.</p>
<p>Apart from the checks we've implemented above the NIST is also clear with what password rules should <em>not</em> be imposed:</p>
<blockquote>
  <p>Verifiers SHOULD NOT impose other composition rules (e.g., requiring mixtures of different character types or prohibiting consecutively repeated characters) for memorized secrets. Verifiers SHOULD NOT require memorized secrets to be changed arbitrarily (e.g., periodically).</p>
</blockquote>
<p>So the next time a website or app tells you to "include both a number, symbol and an upper and lower case character in your password" you should send them a copy of <a href="https://pages.nist.gov/800-63-3/sp800-63b.html">NIST Special Publication 800-63B</a>.</p>

```python
# Enter a password that passes the NIST requirements
# PLEASE DO NOT USE AN EXISTING PASSWORD HERE
new_password = "jsdfhjshf43knjd23jn23d2kjb"
```

```python
def test_not_bad_password():
    temp_new_password = pd.Series(new_password)
    temp_common_passwords = pd.read_csv("datasets/10_million_password_list_top_10000.txt",
                                   header=None, squeeze=True)
    temp_words = pd.read_csv("datasets/google-10000-english.txt",
                        header=None, squeeze=True)

    is_bad = (
        (temp_new_password.str.len() < 8) |
        (temp_new_password.isin(temp_common_passwords)) |
        (temp_new_password.str.lower().isin(temp_words)) |
        (temp_new_password.str.contains(r'(.)\1\1\1'))
    ).all()
    assert not is_bad, \
    'This password does not fulfill the NIST requirements.'
```

    1/1 tests passed
