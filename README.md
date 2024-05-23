# ICPU-Final-Project

This is a reproducable tool suitable for conducting linguistic analysis on a large text file. In the process of developing this tool it was catered specifically to a study of the language being used in discussion of the organic food sector. This repository contains the raw data used for this research, as well as the code used to analyse three different data sets of a respective 'positive' 'negative' or 'neutral' sentiment.

Below is a flow chart to visualise the key processes involved in using this tool, followed by a general step-by-step breakdown of how each of these steps is achieved within the code.
![github diagram drawio](https://github.com/elviehatescoding/ICPU-Final-Project/assets/169135173/f98ae1ab-6922-4774-83a9-dac7bb9a9bef)



involved setting up code for which a text file was then fed in, the case lowered, stop words and punctuation removed, and the words lemmatised. Lemmatisation is a data alteration process essential for many Natural Language Processing tasks (Müller et al., 2015). Word forms are reduced to their “lemmata”; simple form. For example, lemmatisation would cause the following transformations:

A lemmatization tool available in the NLTK python toolbox was implemented, and those missed by the tool were sorted through manually. 
The text file was then split into words, and each word identified as an individual data unit. A frequency count for each word was then produced, and the most common 50 words displayed. From there, a graph was plotted to represent this data. To create a meaningful and legible graph, data was plotted from the 4th most frequently used word onwards, so as not to include ‘organic’, ‘farm’ and ‘food’ which dominated significantly in the positive, negative and neutral data sets.

