# Class notes — Valid Validation

<div style="text-align: right;">

*"Hindsight is always 20/20"*  
— Billy Wilder, American Screenwriter

</div>

#### Setting the stage

In Greek mythology, two twin titans, Prometheus and Epimetheus, represented foresight and hindsight, respectively. When the gods tasked them with distributing abilities among living creatures, Epimetheus acted first, giving animals claws, fur, speed, wings et cetera. It took a moment for him to realize, nothing was left for humans. Prometheus then intervened, stealing fire from the gods and gifting it to humanity as a means to survive and progress. The story of Epimetheus, the God of Afterthought, captures the very human experience of understanding problems once mistakes have been made, mistakes that seem obvious in hindsight. 

Across the three stations of this notebook, you were to investigate and reflect on aspects of machine learning that may seem obvious today, but were not always widely recognized or understood. Many of these ideas are now built directly into modern libraries, workflows and teaching materials, which can make them feel intuitive in hindsight (a nod to Epimetheus). The goal in the exercises was not to immediately get the right answer, but to think through the problems in the way researchers once had to when these issues were still being uncovered and understood. 



### 🟢🟢 Station 2 - Autism classification accuracy.

```{dropdown}

Reasons why you thought large datasets would have higher accuracies

- "with increase in sample data, there is the possibility that the model trains on more examples and likely to learn realistic patterns compared to less data"

- "I would expect studies with larger sample sizes to generally perform better, since the
underlying model has more data to train on." 




```


```{dropdown}

Reasons why you thought small datasets would have higher accuracies

- "Given our context (autism classification, small sample sizes, 55 studies), I expect a nega-
tive correlation. Studies with very small sample sizes, as discussed in the paper ”Illusory
generalizability of clinical prediction models”, have shown to be more likely to demon-
strate illusory high accuracies"


```


```{dropdown}

Figures from your submissions



```{figure} images/linear-log-sample-size.png
---
width: 80%
align: center
figclass: nonfloat
---


```{figure} images/various-confounders.png
---
width: 80%
align: center
figclass: nonfloat
---

```


```{dropdown}

Figures from the literature



```{figure} images/sample-size-linear
---
width: 80%
align: center
figclass: nonfloat
---

```




```{dropdown}

Epimetheus 

**Representativeness of the data**

- "larger datasets likely show less accuracy due to the possibility of having more diverse participants or variations in features and expression" 

- "merging datasets from different studies"


- "bigger datasets might have features that are less accurate because they
ask more general or even "easier/simpler" questions to get more people to fill a questionnaire."


**Mistakes in ML workflow and overfitting**

- "some model accuracies can definitely be explained by insufficient knowledge in ML methodology. The very high accuracies suggest that the ML Researchers at some point had data / information leakage while training"

- "When you train a complex classifier on high-dimensional data (like brain scans) but only give it few patients, the model doesn't learn generalizable signs of autism. It just memorizes the specific noise of those few specific people. "



**Factors beyond ML pipeline**

- "here might be a publication bias that affects small studies stronger: Weak performance results are less publishable, so good results might be overrepresented"


- "Smaller studies might be done with experts directly in the loop and are therefore more accurate in their datapoints. "

- "Maybe special diagnostic tools such as brain scans or similar could be needed to reach a
certain accuracy level, which cant be done on a big scale"


```


### 🟢 Station 1 - In Folds We Trust*...


```{dropdown}

Reasons why hold-out may be worse than 10-fold cross validation

- "With only 100 samples, the holdout test set is relatively small, so the performance estimate can become unstable and heavily dependent on the specific train-test split."

- "A single hold out split may give a weak or unlucky result" 


- Some test folds might be harder, while others might be easier. Thus mixing in easier folds raises the average validation accuracy compared to a hard-only test set.


```



```{dropdown}

So, here is the thing... 

- "If you only used a single holdout split to evaluate your model, you would conclude that your Support Vector Machine (SVM) is performing no better than a coin flip for this binary classification problem"





```



```{dropdown}

There were signs ... 

- Notably, the first SVM even underperformed a random guessing of the class label, which
leads me to believe that there might be something fishy with the way the data was sampled
or split, because the classifier seems to have actively learned "wrong" things

- Average accuracy - what does it mean for the holdout case? 


```



```{dropdown}

The WHY?

- Well, the confirmation bias
- Well, the expectation bias
- Well, the optimism bias
- People did it wrong (because of oversimplified graphs?)


```



### 🟢🟢🟢 Station 3 - Apparently I forgot to give this station a title ... 

```{figure} images/scrambled-validation.png
---
width: 80%
align: center
figclass: nonfloat
---


```


```{dropdown}

Figures from your submissions



```{figure} images/maik-cv
---
width: 80%
align: center
figclass: nonfloat
---


```{figure} images/bernd-cv
---
width: 80%
align: center
figclass: nonfloat
---

```{figure} images/anton-cv
---
width: 80%
align: center
figclass: nonfloat
---


```

```{dropdown}

The story so far ... 

- We want to get the most out of (small) data - cross validation helps
- We really don't want to rely on "lucky" splits - folds and repetitions help
- We want to choose a good model - trying out different hyper-parameters with different splits help
- How about test performance though? Why is suddenly one single number enough to evaluate the model? What about the lucky split again?
- Long story short - we need a distribution of performance metrics; not one value! 
- Meet nested cross-validation!

```



### 🟢🟢🟢🟢 Station 4 - Data leakage can be subtle 

```{dropdown}

What was the data leakage in Station 4?

```



### What should you look out for?


```{figure} images/leakage
---
width: 80%
align: center
figclass: nonfloat
---


```




