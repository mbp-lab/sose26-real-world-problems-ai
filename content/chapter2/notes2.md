# Class notes — Valid Validation


#### Hindsight is always 20/20  - setting the stage

In Greek mythology, two titan brothers, Prometheus and Epimetheus, represented foresight and hindsight, respectively. When the gods tasked them with distributing abilities among living creatures, Epimetheus acted first, giving animals claws, fur, speed, wings et cetera. It took a moment for him to realize nothing was left for humans. Prometheus then intervened, stealing fire from the gods and gifting it to humanity as a means to survive and progress. The story of Epimetheus, the Greek "god of afterthought", captures the very human experience of understanding problems once mistakes have been made, mistakes that seem obvious in hindsight. 

Across the stations of the last notebook, you were to investigate and reflect on aspects of machine learning that may seem obvious today, but were not always as widely recognized or understood. Many of these ideas are now built directly into modern libraries, workflows and teaching materials, which can make them feel intuitive in hindsight (a nod to Epimetheus). The goal in the exercises was not to immediately get the right answer, but to think through the problems in the way some past researchers and practitioners may have when these methods were still being uncovered and understood. 
 
--- 

### 🟢 Station 1 - In Folds We Trust*...
<div style="text-align: right;">

**or do we?*  

</div>


In the first station of the notebook, you were first introduced to a standard definition of k-fold validation, highlighting its economical nature when data is scarce. This was paired with the graph on the right, showing model accuracy higher for k-fold than for the holdout set. You were asked to reason why this discrepancy arose. Many of you argued along the following lines: *"with only 100 samples, the holdout test set is relatively small, so the performance estimate can become unstable and heavily dependent on the specific train-test split, "a single hold out split may give a weak or unlucky result" , "some test folds might be harder, while others might be easier. Thus mixing in easier folds raises the average validation accuracy compared to a hard-only test set"*. 

```{figure} images/caution-k-fold-vs-holdout1.png
---
width: 100%
align: center
figclass: nonfloat
---
```


Your arguments made complete sense. However, there was one little detail. Now that you are done with the exercise, let's let the cat out of the bag. This framing was intentionally designed to (mis)lead to a “better method, better accuracy” mindset. In this particular example, the holdout estimate was actually closer to the truth ... what you weren't told was that the model was trained on Gaussian noise. So, random chance is all one should get, yet k-fold shows higher performance, even though not dramatic. While a large discrepancy between the two methods would likely have raised immediate suspicion in a classroom of masters students, the difference here was subtle enough to be misleading. So why was this deceptive example introduced?



**First, let's take a step back - k-fold is not necessarily bad.** Quite the opposite, it is a very helpful technique. You did give very good reasons why it would be better in a small data scenario. Hence, **the lesson is not that k-fold cross-validation is a bad method**, far from it. Rather, it shows how easy it is to place too much trust in a result without carefully considering how the method is being used. By the end of Station 2, you will learn why k-fold gave "higher accuracy" and what mistake I had (deliberately) introduced. We will reconcile with k-fold validation but first let's have a look at a finding from the literature!  

--- 

### 🟢🟢 Station 2 - Autism classification accuracy.

A paper from 2019 called "Machine learning algorithm validation with a limited sample size" summarized the reported classification accuracy values for 55 studies on autism detection. The studies varied in the number of participants included. Before seeing the data from this paper, you were asked to write down what relationship you would expect between sample size and accuracy. An overwhelming majority of you guessed that large datasets should result in higher accuracies. That's absolutely the correct intuition based on how one would expect machine learning models to behave. 

```{dropdown}

Valid reasons why you thought large datasets would have higher accuracies

- "with increase in sample data, there is the possibility that the model trains on more examples and likely to learn realistic patterns compared to less data"

- "I would expect studies with larger sample sizes to generally perform better, since the underlying model has more data to train on." 


```

But, lo and behold! The data revealed something quite different from what we expected. Instead of accuracy improving with larger sample sizes, the relationship was actually negative: smaller studies tended to report higher accuracies. In some cases, the reported performance was suspiciously high, enough to set off alarm bells for many master's students with a background in computer science. 

As you can see this pattern cannot be explained simply by the method used or the data type. Some of you hypothesized that publication year might have an effect, with earlier studies having less data and suffering from selection bias, e.g. only studies with high enough accuracies would make it to publication. As we see, there is not really any pattern here. 


```{figure} images/various-confounders.png
---
width: 100%
align: center
figclass: nonfloat
---

```


```{dropdown}

A few cautionary words regarding linear fits

Several of you had versions of the left plot in your submissions, where a line was fitted to an obviously non linear set of data!  This was often paired with Pearson's correlation coefficient, despite Pearson being designed to quantify linear association. A better choice here is Spearman's rank correlation coefficient, which captures monotonic relationships without assuming linearity. Alternatively, if you are particularly committed to Pearson's classical method, you can log-transform the data (as shown on the right) to make it more suitable to Pearson's analysis.


```{figure} images/linear-log-sample-size.png
---
width: 80%
align: center
figclass: nonfloat
---

```

You gave many interesting reasons of why this curious pattern of negative relationship would arise. The reasons varied from data representativeness (maybe smaller studies have better quality), to mistakes in ML workflow and overfitting, to factors beyond ML pipeline, such as smaller studies having more experts in the loop. 

```{dropdown}

Reasons you gave for the negative relationship - extracts from submissions

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
certain accuracy level, which can't be done on a big scale"


```

The actual reason of higher accuracies may vary from study to study. [One study](https://www.sciencedirect.com/science/article/pii/S2666389925000339) boiled it down to overfitting and publication bias for neuroimaging-based classification models.  But there was one thing that stood out in 2019 paper from which your data was taken... And that is how k-fold validation was defined: 

*"First, a well-defined model is developed by normalizing data, selecting features, tuning parameters and/or performing other development steps. Then a portion of data is separated for validation leaving the rest to train a model and predict the classes on the left-out validation data. This process is repeated several times, by leaving out a different portion of the data for validation until all the data is used. The model’s performance is then calculated as a mean of classification performances, in each of the validation folds".* 


Well, that's exactly what I did for Station 1 and it's wrong!!! I (deliberately) performed feature selection and parameter tuning *before* splitting the data into training and validation folds. And this is a form of data leakage! The authors *did* criticize this "standard" way of doing k-fold cross-validation. But the concerning thing is that the way they described it was not the correct way of doing k-fold cross-validation when feature selection and hyperparameter tuning are involved! Let's unpack what k-folds do and don't do by going back to the drawing board! 


--- 




### 🟢🟢🟢 Station 3 - Cross-validation revisited

In Station 3, you were asked to re-arrange and reuse the components of this scrambled image to illustrate a good ML workflow. Before discussing your sketches, let's have a look at what is the story so far. 

- We want to get the most out of (small) data - cross validation helps
- We really don't want to rely on "lucky" splits - folds and repetitions help
- We want to choose a good model - trying out different hyper-parameters with different splits help



```{figure} images/scrambled-validation.png
---
width: 80%
align: center
figclass: nonfloat
---


```

Okay, let's use three examples to guide us through this scrambled mess! 

**Feature selection and hyper parameter tuning shouldn't touch the validation data**

First things first - it should be clear by now that feature selection and parameter tuning should not be done on both training and validation sets. It should be done exclusively on the training set! Let's see how easy it may be to miss this even if you know about it! 

In the figure below, the author is very careful. They explicitly mention that data normalization should only be performed on the training set, which cleanly separates the training data from the test data. This is very good. However, if normalization is applied to the entire training set *before* entering the k-fold cross-validation loop, the normalization parameters will be computed using observations that later appear in the validation folds. This introduces information leakage from the validation folds into the training folds. To avoid this, normalization should be performed separately within each cross-validation iteration, using only the corresponding training fold and then applying the resulting parameters to the validation fold. 

```{figure} images/k-fold-leakage.png

---
width: 80%
align: center
figclass: nonfloat
---


```

```{dropdown}

Check out a visual example for normalization leakage here!

One may think data leakage due to normalization may be minimal. This may be true in some cases but not always; so having a clean pipeline remains crucial! Check out the example below for a drastic example of the "average face". 

```{figure} images/standardization-leakage
---
width: 80%
align: center
figclass: nonfloat
---

Image source: Don’t push the button! Exploring data leakage risks in machine learning and transfer learning, Apicella et al., 2025

```

**k-fold is great and all but it is still optimistic for evaluation**

The next figure carefully mentions that the feature selection and parameter tuning should be done only on the training folds. So far so good! It also shows nicely that the average performance across folds helps with model selection as the model with the lowest average error may be the better one. Again, good. The author also rightly mentions that the model selection is overfitted to the validation set. That is correct as well. While each validation fold is treated independently of the training ones, it is still part of the bigger picture, providing error estimates to help model selection. So the average error here is more optimistic and biased than it would be on completely independent data. What would be an even better approach?

```{figure} images/optimistic-cv
---
width: 80%
align: center
figclass: nonfloat
---
```

**We had one test error, yes. But how about a second one? And a third?**

Remember how the idea of a lucky split didn't quite sit right with us in Station 1, especially for small data? That's why we started with the whole k-fold thing! We have come far now and learned how to do k-fold cross-validation correctly. But there is still one issue remaining. What about the test data? It's well established that you should never touch the test data except for final evaluation. But aren't we again relying on a lucky split there? What if the train/test split is an unlucky one? With very large datasets, this doesn't really matter, and holdout validation is fine. But many applications we consider don't have that luxury.

So, what we can do instead is have multiple test estimates using a method called nested cross-validation. It is computationally costly, so it is most commonly used when data is limited and reliable performance estimates are important. What you can do is have two loops instead of one. In each iteration of the outer loop, one fold is held out as the test fold, while the remaining folds are used for model selection. Within the inner loop, you then proceed with the regular k-fold validation for model selection. Afterward, you use the fold that was set aside at the beginning of the outer iteration to obtain an independent estimate of performance. You do this as many times as you have outer folds. This helps you obtain a distribution of test errors rather than relying on a single estimate. And each time, the training and test data are kept at a safe distance from each other.


```{figure} images/nested-cv
---
width: 80%
align: center
figclass: nonfloat
---


```

**When to use holdout, when k-fold, when nested cross-validation?**

Here are a few rules from a scikit-learn [video](https://www.youtube.com/watch?v=DuDtXtKNpZs&t=1127s):

- small data - always* use nested cross-validation (e.g. medical data with less than 2000 patients) *always may be strong as computationally this may not always be feasible

- medium data - nested cross-validation if you can afford it, otherwise k-fold (e.g. 100k rows and 1000 features)

- big data - single training/validation/test split (e.g. ImageNet)



----


### 🟢🟢🟢🟢 Station 4 - Data leakage can be subtle 

Okay, we are almost done! But there is one more nuance we considered in the class. Data leakage doesn't necessarily creep in from the ML workflow itself. Even if you have the perfect setup and validation strategy, it doesn't guarantee clean data. Data may contain duplicates or illegitimate features. In the constructed scenario of the exercise, you had to "predict" diabetes. But one of the features was ... continuous glucose monitoring. This is an illegitimate feature because it's a proxy of the target variable - a person would typically have a device for managing glucose if they were already diagnosed with diabetes. And this was not just a hypothetical brain teaser. A similar scenario with hypertension has well been published! 

Below you can find examples of different data leakage scenarios, from simple ones, such as no test-train split, to duplicates, illegitimate features, temporal leakage (in time series data: neighboring points are related), non-independent data points in train-test (data from same or related participants) et cetera! Note that each row here presents a meta-study summarizing many other studies. As you see, data leakage is more common than one would like. 



```{figure} images/leakage
---
width: 80%
align: center
figclass: nonfloat
---

Image source: Leakage and the reproducibility crisis in machine-learning-based science, Kapoor and Narayanan 2023, Patterns

```

---

### Final words

After this brief excursion into revisiting, understanding, and even repeating the mistakes of the past, let's leave Epimetheus behind for this particular problem and move on with Prometheus, armed with the foresight needed to detect and prevent data leakage and validation issues before they arise.




