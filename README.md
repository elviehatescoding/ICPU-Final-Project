# Linguistic Analyisis Code

This is a reproducable tool suitable for conducting linguistic analysis on a large text file. In the process of developing this tool it was catered specifically to a study of the language being used in discussion of the organic food sector. This repository contains the raw data used for this research, as well as the code used to analyse three different data sets of a respective 'positive' 'negative' or 'neutral' sentiment.

Below is a flow chart to visualise the key processes involved in this tool, followed by a general step-by-step breakdown of how each of these steps is achieved within the code.

![github diagram drawio](https://github.com/elviehatescoding/ICPU-Final-Project/assets/169135173/f98ae1ab-6922-4774-83a9-dac7bb9a9bef)

## 1. Import Appropriate Tools

```
import numpy as np
import matplotlib.pyplot as plt
import pandas as pd
from collections import Counter
import string
import nltk
nltk.download('wordnet')
from nltk.stem import WordNetLemmatizer
```

## 2. Read in Text File
```
filename = 'all positive files.txt'
f = open(filename,encoding = "utf-8")
data = f.read()
```
## 3. Prepare Data
### a. Case
```
datalower = data.lower()
```
### b. Punctuation
```
# Function to remove punctuation
def remove_punctuation(text):
    return text.translate(str.maketrans('', '', string.punctuation))
text_no_punctuation = remove_punctuation(datalower)
```
### c. Split Data
```
words = text_no_punctuation.split()
```
### d. Stop Words
```
#defining stop word and punctuation function

# Basic list of stop words. Consider expanding this list based on your needs.
stop_words = set([
    "i", "me", "my", "myself", "we", "our", "ours", "ourselves", "you", "your", 
    "yours", "yourself", "yourselves", "he", "him", "his", "himself", "she", 
    "her", "hers", "herself", "it", "its", "itself", "they", "them", "their", 
    "theirs", "themselves", "what", "which", "who", "whom", "this", "that", 
    "these", "those", "am", "is", "are", "was", "were", "be", "been", "being", 
    "have", "has", "had", "having", "do", "does", "did", "doing", "a", "an", 
    "the", "and", "but", "if", "or", "because", "as", "until", "while", "of", 
    "at", "by", "for", "with", "about", "against", "between", "into", "through", 
    "during", "before", "after", "above", "below", "to", "from", "up", "down", 
    "in", "out", "on", "off", "over", "under", "again", "further", "then", 
    "once", "here", "there", "when", "where", "why", "how", "all", "any", 
    "both", "each", "few", "more", "most", "other", "some", "such", "no", 
    "nor", "not", "only", "own", "same", "so", "than", "too", "very", "s", "t", 
    "can", "will", "just", "don", "should", "now", "and", "And", "1", "i'm", 
    "im", "us", "–", "said", "also"
])

words_no_stop_words = remove_stop_words(words)
```
### e. Lemmatisation
```
lemmatizer = WordNetLemmatizer()
lemmatized_words = [lemmatizer.lemmatize(word) for word in words_no_stop_words]
```
#### i. Manual Revision
why did we do this
```
def lemmatize_word(word):
    lemmatizer = WordNetLemmatizer()
    return lemmatizer.lemmatize(word)

def replace_farm_words(words):
    replacements = {"farming": "farm", "farmer": "farm", "farms": "farm", "farmers": "farm"}
    return [replacements.get(lemmatize_word(word), word) for word in words]

# Example list of words
word_list = lemmatized_words

# Replace farm-related words
modified_list = replace_farm_words(word_list)
```
## 4. Word Counter
```
words_count = Counter()
for word in modified_list:
    words_count.update({word,1})
```
## 5. Top 50
```
most_common_words = words_count.most_common(51)
```
reason it is 51 and not 50
## 6. Plot

```
x, y = zip(*most_common_words)
plt.bar(x[1:],y[1:])
plt.xticks(rotation=90, fontsize=8)
plt.xlabel('Word')
plt.ylabel('Number of Usages')
plt.title('Most Common Words Used In Positive Media on Organic Produce')
plt.show()
```

involved setting up code for which a text file was then fed in, the case lowered, stop words and punctuation removed, and the words lemmatised. Lemmatisation is a data alteration process essential for many Natural Language Processing tasks (Müller et al., 2015). Word forms are reduced to their “lemmata”; simple form. For example, lemmatisation would cause the following transformations:

A lemmatization tool available in the NLTK python toolbox was implemented, and those missed by the tool were sorted through manually. 
The text file was then split into words, and each word identified as an individual data unit. A frequency count for each word was then produced, and the most common 50 words displayed. From there, a graph was plotted to represent this data. To create a meaningful and legible graph, data was plotted from the 4th most frequently used word onwards, so as not to include ‘organic’, ‘farm’ and ‘food’ which dominated significantly in the positive, negative and neutral data sets.

