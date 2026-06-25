# Mitigating algorithmic bias - class notes


In the last notebook, you had the chance to explore different bias mitigation algorithms for the COMPAS scenario introduced in the first part of this chapter. You took the role of a data analyst to simplify the given plots and suggest a clean and concise story of - did we manage to make the algorithm more fair? 

**The story so far**



:::{dropdown} Reminder of the used methods

| Stage | What Changes? | Method |
|-------|---------------|---------|
| **Pre-processing** | **Data representation** | **[CorrelationRemover](https://fairlearn.org/main/api_reference/generated/fairlearn.preprocessing.CorrelationRemover.html)** transforms the data before training by reducing linear correlations between the features and the sensitive attribute. Intuitively, it adjusts feature values so that variables such as `priors_count` reveal less information about a person's race, while attempting to retain as much predictive information as possible. |
| **In-processing** | **Model training** | **[ExponentiatedGradient](https://fairlearn.org/main/api_reference/generated/fairlearn.reductions.ExponentiatedGradient.html)** incorporates fairness into the learning objective. Unlike standard gradient-based training, which searches for one best model, it maintains and reweights multiple candidate models, favoring those with a better accuracy–fairness trade-off under **[Equalized Odds](https://fairlearn.org/main/api_reference/generated/fairlearn.reductions.EqualizedOdds.html)**. |
| **Post-processing** | **Decision rule** | **[ThresholdOptimizer](https://fairlearn.org/main/api_reference/generated/fairlearn.postprocessing.ThresholdOptimizer.html)** leaves the trained model unchanged and adjusts the thresholds used to convert risk scores into binary predictions. Intuitively, it can be understood as selecting different operating points along group-specific ROC curves to better satisfy **[Equalized Odds](https://fairlearn.org/main/api_reference/generated/fairlearn.reductions.EqualizedOdds.html)**. |

:::


:::{dropdown} The benefits and drawbacks of each type of method

Here are some points based on the review paper: 

- *Pre-processing methods* - can be used with any type of ML algorithm because they modify the input. The drawback is that it may harm the explainability of the results as the features may be modified in unpredictable ways. 

- *Post-processing methods* - again, can be used with any type of ML algorithm. The drawback is the late stage in the learning process that can lead to inferior results. Post-processing mechanisms may be particularly good at removing disparate impact but they may lead to higher individual unfairness in the sense that two similar *individuals* may be treated differently by the algorithm in pursuit of making the *groups* metrics more similar. 

- *In-processing methods* - Nice because they integrate the fairness-accuracy tradeoff directly into the model constraints. However, they are coupled with the machine learning algorithm itself. 


```{figure} images/group_vs_individual.png

---
width: 50%
align: center
figclass: nonfloat
---

```


:::
---

:::{dropdown} Your suggestions for results cleanup!

**What you wanted to find out (before looking at the plots)**

- Which algorithm does the best job in bias mitigation?
- Does fairness come at the cost of accuracy?

**You suggested - I implemented!**

```{figure} images/bars1.png
---
width: 50%
align: center
figclass: nonfloat
---

```

```{figure} images/bars2.png
---
width: 50%
align: center
figclass: nonfloat
---

```

```{figure} images/error_rate_gaps.png
---
width: 50%
align: center
figclass: nonfloat
---


```{figure} images/bars_equalized_odds_difference.png
---
width: 50%
align: center
figclass: nonfloat
---




```{figure} images/accuracy-vs-fairness1
---
width: 50%
align: center
figclass: nonfloat
---

```


```{figure} images/accuracy_vs_equalized_odds.png

---
width: 50%
align: center
figclass: nonfloat
---

```


**Main takeaways**


**What else you'd like to know and your recommendations**

- intersectional analysis of race and sex
- multi-class fairness: how fair is the algorithm for the other racial groups
- which exact features lead to the bias?


:::


:::{dropdown} Individual vs group fairness

- The impossibility of fairness: remember our judges! 

:::



:::{dropdown} Let's have another look at the sources of bias now! 


:::

----



