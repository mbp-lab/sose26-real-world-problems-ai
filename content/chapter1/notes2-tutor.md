# Class notes — Representation learning




## 🟢 Station 1 - Know thy data!

In the first station of this assignment, you were asked to covert text into numerical representations to train a classifier to distinguish between news articles in different topics. The two methods for getting numerical representations that you were asked to use were bag of words and tf-idf, two classical methods from natural language processing.



```{figure} images/bow-tf-idf.png
---
width: 80%
align: center
figclass: nonfloat
---
Image Source: https://web.stanford.edu/~jurafsky/slp3/

```


```{dropdown} **Bag of words vs tf-idf**

As reported in your exercises, both methods resulted in a similar number of features. Those features correspond to the number of unique words (or terms) across the available documents (vocabulary size). What makes them different is how these words are treated. For the Bag of Words approach, it's simply the frequency of each word, while TF-IDF takes into account not only how often each word appears in a document but also how important or distinctive that word is across the entire collection of documents. That is calculated by multiplying two values: how often a word appears in a specific document and how rare that word is across all documents in the dataset. Common words carry less discriminatory information, while more distinctive words can help differentiate documents. In William Shakespeare's works, words such as “Romeo” or “Juliet” would likely receive a higher TF-IDF score because they are strongly associated with a specific play, whereas very common words appearing across many texts would receive lower scores.


```{figure} images/nasa
---
width: 80%
align: center
figclass: nonfloat
---


```


```{dropdown} **What do these results tell us?**

For most of you, the model was trained on 5991 features. However, there were some numbers that were diverging (5000,5650,5736). Check your code - what could have caused this. 

Think about one more scenario: the number of features is 8125. What do you think has likely happened? 

```

## 🟢🟢 Station 2: Place your bets!


You were asked to guess how each of the following scenarios would perform: BoW and TF-IDF paired with wither no dimensionality reduction, PCA and PCA reduced to 2 features only. 


What most of you agreed on was that BoW would perform better than TF-IDF because it considers how unique words are to documents rather than their absolute frequency. You also agreed that 2D PCA would likely lose a lot of information. Where opinions diverged was no dimensionality reduction vs PCA. What was your reasoning? 

```{figure} images/tab
---
width: 80%
align: center
figclass: nonfloat
---

```

```{dropdown} **When is PCA helpful?**


```

```{dropdown} **How to select the number of PCA features?**

```{figure} images/PCA-selection
---
width: 80%
align: center
figclass: nonfloat
---

```
```{dropdown} **What is the maximum number of features PCA can return?**

As mentioned in the paper "Use and Misuse of PCA for Measuring Well-Being", "the idea of PCA is simple: reduce the dimensionality of a dataset, while preserving as much ‘variability’ as possible. This translates into finding new variables that are linear functions of the original ones, that successively maximize variance and that are uncorrelated with each other. Finding such new variables reduces to solving an eigenvalue/eigenvector problem, and the results depend on the dataset, rather than being pre-defined basis functions. Because the new variables are defined by the dataset at hand, and not a priori, PCA can be considered an adaptive data analysis tool."

PCA depends on the data and its covariance matrix, so it cannot create more principal components than the number of samples or the number of features (whichever is smaller). Therefore, the x-axis in the plots never goes beyond that limit.

```{figure} images/PCA-selection
---
width: 80%
align: center
figclass: nonfloat
---

```
```{dropdown} **Examples of t-sne visualizations**

```{figure} images/tsne3
---
width: 80%
align: center
figclass: nonfloat
---

```{figure} images/tsne2
---
width: 80%
align: center
figclass: nonfloat
---
```


## 🟢🟢🟢 Station 3: Test your assumptions!


```{dropdown} **How did the models actually perform?**

```{figure} images/bow-tfidf-results.png
---
width: 80%
align: center
figclass: nonfloat
---


```

## 🟢🟢🟢🟢 Station 4: What kind of sorcery is this?

```{dropdown} **Embeddings**


```{figure} images/embeddings-tsne2
---
width: 80%
align: center
figclass: nonfloat
---

```{figure} images/embeddings-results
---
width: 80%
align: center
figclass: nonfloat
---


```

