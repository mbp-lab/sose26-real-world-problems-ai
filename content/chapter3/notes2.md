# Mitigating algorithmic bias - class notes


In the last notebook, you had the chance to explore different bias mitigation algorithms for the COMPAS scenario introduced in the first part of this chapter. You took the role of a data analyst to simplify the given plots and suggest a clean and concise story of - did we manage to make the algorithm more fair? 

# 1) The story so far: how do we want to achieve fairness?

In the first notebook of this chapter, you found out that the COMPAS predictions were particularly problematic with respect to false positives (higher for the African-American group) and false negatives (higher for the Caucasian group). To mitigate this disparity, the second notebook suggested using equalized odds difference as a fairness metric. This metric corresponds to [Judge 4 discussed in class](https://mbp-lab.github.io/sose26-real-world-problems-ai/notes1-1/) and tries to minimize both types of error. Equalized odds difference measures the largest difference in either the **true positive rate (TPR)** or the **false positive rate (FPR)** between demographic groups:

EO Diff = max(TPR difference, FPR difference)

:::{dropdown} 🤔 Wait a minute! Wasn't EO supposed to be about false negatives and false positives? Why is TPR in the equation?

Yes! In our scenario, equalized odds was introduced as a fairness metric that accounts for both types of classification error: false positives and false negatives. In many textbooks and research papers, however, equalized odds is instead defined in terms of the true positive rate (TPR) and the false positive rate (FPR).

This is simply a difference in how the metric is expressed, since the **false negative rate (FNR)** is the complement of the true positive rate:
[
\text{FNR} = 1 - \text{TPR}.
]
As a result, requiring equal false negative rates across groups is mathematically equivalent to requiring equal true positive rates across groups.

:::

--- 

# 2) Some technicalities of bias mitigation methods

There are many methods for achieving fairness in the machine learning literature—so many, in fact, that they have been described as a ["zoo of fairness metrics"](https://arxiv.org/abs/2106.00467). This is hardly surprising, given what we saw with our "judges" from the last session: there is no single way to define fairness.

Broadly, most traditional fairness methods fall into one of three categories: pre-processing, where you modify the data before training; in-processing, where you incorporate fairness directly into the learning algorithm; and post-processing, where you adjust the model's predictions after training. You had the chance to try one method from each category!

:::{dropdown} Reminder of the mitigation methods used

| Stage | What Changes? | Method |
|-------|---------------|---------|
| **Pre-processing** | **Data representation** | **[CorrelationRemover](https://fairlearn.org/main/api_reference/generated/fairlearn.preprocessing.CorrelationRemover.html)** transforms the data before training by reducing linear correlations between the features and the sensitive attribute. Intuitively, it adjusts feature values so that variables such as `priors_count` reveal less information about a person's race, while attempting to retain as much predictive information as possible. |
| **In-processing** | **Model training** | **[ExponentiatedGradient](https://fairlearn.org/main/api_reference/generated/fairlearn.reductions.ExponentiatedGradient.html)** incorporates fairness into the learning objective. Unlike standard gradient-based training, which searches for one best model, it maintains and reweights multiple candidate models, favoring those with a better accuracy–fairness trade-off under **[Equalized Odds](https://fairlearn.org/main/api_reference/generated/fairlearn.reductions.EqualizedOdds.html)**. |
| **Post-processing** | **Decision rule** | **[ThresholdOptimizer](https://fairlearn.org/main/api_reference/generated/fairlearn.postprocessing.ThresholdOptimizer.html)** leaves the trained model unchanged and adjusts the thresholds used to convert risk scores into binary predictions. Intuitively, it can be understood as selecting different operating points along group-specific ROC curves to better satisfy **[Equalized Odds](https://fairlearn.org/main/api_reference/generated/fairlearn.reductions.EqualizedOdds.html)**. |

:::


:::{dropdown} The benefits and drawbacks of each type of method

Here are some points based on the section *4.4 Which Mechanism to Use?* in the [review paper of Pessach and Shmueli, 2022](https://dl.acm.org/doi/10.1145/3494672): 

- *Pre-processing methods* - can be used with any type of ML algorithm because they modify the input. The drawback is that it may harm the explainability of the results as the features may be modified in unpredictable ways. 

- *In-processing methods* - Nice because they integrate the fairness-accuracy tradeoff directly into the model constraints. However, they are coupled with the machine learning algorithm itself. 

- *Post-processing methods* - again, can be used with any type of ML algorithm. The drawback is the late stage in the learning process that can lead to inferior results. Post-processing mechanisms may be particularly good at removing disparate impact but they may lead to higher individual unfairness in the sense that two similar *individuals* may be treated differently by the algorithm in pursuit of making the *groups* metrics more similar. 


```{figure} images/group_vs_individual.png

---
width: 50%
align: center
figclass: nonfloat
---

```


:::
---

# 3) Getting insights from a sea of visualizations

Your task in this notebook was to inspect a bunch of visualizations on the fairness mitigation methods and come up with a more concise representation of the results. For that you were invited to first think what information you want to find out before looking at the plots. Most of you were interested in the following questions: 

- Which algorithm does the best job in bias mitigation?
- Does fairness come at the cost of accuracy?

Below you can see some of your suggestions and the resulting plots with the actual data!


:::{dropdown} Your suggestions for results cleanup!


**Transparent visualizations of model mistakes**

Some of you wanted to have a transparent picture of the false alarms and false negatives and how they differ between the two racial groups. The following suggestions don't use the equalized odds difference but prefer showing the error rates directly. This has the advantage that it's easy to see when things are equal: the closer the two bars are to zero and to each other, the better! 


```{figure} images/suggestion1.png
---
width: 100%
align: center
figclass: nonfloat
---

```
---

**Accuracy vs bias tradeoff - nice but requires some cognitive effort**

Some other suggestions wanted to visualize how bias mitigation methods may affect model fairness. These suggestions offered a direct comparison of the different approaches regarding model accuracy and bias. One conceptual wrinkle here is that for the x-axis, lower values are associated with higher fairness. Typically, that requires more mental steps to process. 

```{figure} images/suggestion2.png
---
width: 100%
align: center
figclass: nonfloat
---

```

Another suggestion is also focusing on both accuracy and equalized odds difference but this time using bars instead of a scatter plot. Here, fairness and accuracy metrics of different methods are subtracted from the baseline. Here, too, a conceptual issue is that positive values mean two different things for the two metrics: for accuracy that would mean mitigation methods are doing better, while for equalized odds difference, a positive value means more difference = more bias.  

```{figure} images/suggestion3.png

---
width: 50%
align: center
figclass: nonfloat
---

```
**Same principles - less mental steps**

These final visualizations try to fix the conceptual wrinkles and simply "flip" the fairness value. Instead of taking the equalized odds difference (EOD), we can use 1-EOD, such that higher values now mean more fairness. This liberty will help a reader process the information faster. 

----

```{figure} images/suggestion4.png

---
width: 50%
align: center
figclass: nonfloat
---

```




:::


:::{dropdown} What else you'd like to know and your recommendations

- intersectional analysis of race and sex
- multi-class fairness: how fair is the algorithm for the other racial groups
- which exact features lead to the bias?

:::



----



