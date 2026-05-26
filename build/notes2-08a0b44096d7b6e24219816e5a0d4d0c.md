# Class notes — Representation learning




## 🟢 Station 1 - Know thy data!

In the first station of the assignment, you were asked to covert text into numerical representations to train a classifier to distinguish between news articles in different topics. The two methods for getting numerical representations that you were asked to use were bag of words (BoW) and TF-IDF, two classical methods from natural language processing.



```{figure} images/bow-tf-idf.png
---
width: 80%
align: center
figclass: nonfloat
---
Image Source: https://web.stanford.edu/~jurafsky/slp3/

```


As reported in your exercises, both methods resulted in a similar number of features. Those features correspond to the number of unique words (or terms) across the available documents (vocabulary size). What makes them different is how these words are treated. For the Bag of Words approach, it's simply the frequency of each word, while TF-IDF takes into account not only how often each word appears in a document but also how important or distinctive that word is across the entire collection of documents. That is calculated by multiplying two values: how often a word appears in a specific document and how rare that word is across all documents in the dataset. Common words carry less discriminatory information, while more distinctive words can help differentiate documents. In William Shakespeare's works, words such as “Romeo” or “Juliet” would likely receive a higher TF-IDF score because they are strongly associated with a specific play, whereas very common words appearing across many texts would receive lower scores.




```{dropdown} **What do these numbers tell us? - Puzzle 1 inspired by your submissions**

The training data provided to you contained 5991 unique words, resulting in 5991 features for the numerical representations of BoW and TF-IDF. Now think of a case where the number of features that the model was trained on was instead 8125 but the training data was not modified in any way and the exact same function was used to transform text into numbers. What do you think has likely happened? Think carefully about which data the vectorizer may have been fit on. 

```{dropdown} Answer

In the described scenario, both the training and test data was used to create feature representations. However, this is a case of data leakage as the statistics of the test data creeps into the training. Hence, the correct option was to fit the representations to the training data only.

``` # Python example
X_train_vec = vectorizer.fit_transform(X_train) # fit AND transform
X_test_vec = vectorizer.transform(X_test) # only transform based on the fit on the training data
```

```{dropdown} **What do these numbers tell us? - Puzzle 2 inspired by your submissions**

In the description of BoW and TF-IDF, it was mentioned that TF-IDF assigns higher scores to words that are unique to fewer documents. However, in the results shown below, the word "the" got higher score than "nasa" despite being present in more documents. Why do you think that happens?

```{figure} images/nasa
---
width: 80%
align: center
figclass: nonfloat
---


```{dropdown} Answer

While the frequency of a word across different documents is important for the TF-IDF representations, the term frequency itself is part of the equation. In the presented example, the word "the" appears 91 times in one document, accounting for around 7% of the word's occurrence across hundreds of documents. This happens to be a particularly long news entry, pointing to the need to also account for the length of documents

```


--- 


## 🟢🟢 Station 2: Place your bets!


You were asked to guess how each of the following scenarios would perform: BoW and TF-IDF paired with wither no dimensionality reduction, PCA and PCA reduced to 2 features only. 


What most of you agreed on was that BoW would perform better than TF-IDF because it considers how unique words are to documents rather than their absolute frequency. You also agreed that 2D PCA would likely lose a lot of information. Where opinions diverged was no dimensionality reduction vs PCA. The reasoning in favor of PCA was that it can help remove redundancy and make it more efficient to learn from correlated features. The reasoning against it was that we will use valuable information that a logistic regressor would be able to handle comfortably. In fact, both arguments are valid. The decision of whether to apply dimensionality reduction, and which method and number of components to use, should be treated as a hyperparameter choice. The optimal configuration depends on the dataset properties and the model and can be determined empirically. For example, standard PCA is often less suitable for sparse data, and tree-based models frequently benefit less from PCA than linear models do.

```{figure} images/tab.jpg
---
width: 80%
align: center
figclass: nonfloat
---

```

```{dropdown} **When is PCA helpful?**


```

```{dropdown} **How to select the number of PCA features?**

PCA is often used for visualization by projecting data onto the first two principal components, allowing us to inspect the structure of the data in 2D. However, restricting the representations to only two dimensions is usually too limiting for model training. 

To determine an appropriate number of PCA features, a common heuristic is to retain enough components to explain a certain percentage of the variance, such as 90%. While this approach helps preserve most of the relevant information, it does not indicate whether the chosen dimensionality is actually optimal for the given dataset. 

A more informative approach is to plot the cumulative explained variance against the number of principal components. If the curve exhibits a clear elbow, this suggests that adding more components beyond that point yields only small addition to the captured variance. This can help identify a more efficient trade-off between dimensionality reduction and information retention. 

In the figure below, the BoW representations show a pronounced elbow. However, this does not necessarily imply that they will perform better with fewer features. PCA identifies directions of maximum variance in the data but it is agnostic to which features are actually predictive for the task at hand. 


```{figure} images/PCA-selection
---
width: 80%
align: center
figclass: nonfloat
---

```{dropdown} **What is the maximum number of features PCA can return?**

PCA depends on the data and its covariance matrix, so it cannot create more principal components than the number of samples or the number of features (whichever is smaller). Therefore, the x-axis in the plots never goes beyond that limit. Even if you have thousands of features (over 5000 in our case), the maximum number of possible PCA-reduced features would be the sample size (200 in the assignment). 

```
```{dropdown} **Examples of t-SNE visualizations**

Below you can see t-SNE visualizations for the different scenarios. Many of you were unsure how to interpret them and for good reason. At this stage, there is no clearly discernible pattern and depending on the hyperparameters or random initialization, t-SNE can produce visualizations that appear more or less structured. 

Since no stable or meaningful separation emerges consistently, there is likely no strong low-dimensional structure to interpret in this case. More generally, t-SNE plots should be interpreted with caution, as apparent clusters or patterns may sometimes be artifacts of the embedding process rather than genuine structure in the data.

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
--- 

## 🟢🟢🟢 Stations 3 - 4 Testing model performance

Here is the image that emerged from model evaluation. Most of you got values similar to the ones in the figure. At least the results pattern should be consistent and the numerical differences may arise from the number of PCA components used or model choices, such as whether or not you applied regularization. 

```{figure} images/text-classification-performance.png

---
width: 80%
align: center
figclass: nonfloat
---
```

Your intuitions were correct: TF-IDF is more informative than BoW. We also empirically observe that PCA has relatively little impact in our specific scenario. Compressing the data into 2D is detrimental but interestingly, 2D PCA still performs reasonably well when paired with dense, informative representations from the sentence transformer. This approach is clearly superior - lo and behold, we can now achieve a relatively high performance with as few as two features! This can be important in cases where you face computational limitations. This is the power of transfer learning! Representations from pre-trained models help tap into knowledge acquired during large-scale pretraining, resulting in highly informative feature representations.  

In our case of text classification, the representations of the sentence transformer also had lower dimensionality, reducing the number of features required for our small dataset. In general, such scenario may help mitigate the curse of dimensionality observed in the previous notebook. 



```{figure} images/embeddings-tsne.png

---
width: 80%
align: center
figclass: nonfloat
---
```
---- 

