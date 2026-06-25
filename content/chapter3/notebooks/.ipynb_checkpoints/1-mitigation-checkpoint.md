# Fairness mitigation - assignment


# What is this task about?

In the tutorial so far, you have primarily worked with notebooks containing coding exercises and short reflections. This time, we will switch gears and focus on a more conceptual task that nevertheless resembles challenges encountered in real-world data science projects.

Several of you mentioned that you find it difficult to create effective visualizations or to communicate insights in a concise manner. In this assignment, you will combine a fairness audit of the COMPAS system that you explored in the last session with the role of a data analyst and communicator. Your goal is not only to understand the results of different fairness mitigation strategies, but also to determine which findings matter most, how they can be communicated more clearly and how complex information can be distilled into an easier-to-digest story! 

🚀 Time to get started! 

---
#### 🟢 Station 1 - Getting to know different types of fairness mitigation methods

Let's first consider a hypothetical scenario. 

Following the debate around COMPAS, two independent parties are hired to improve the system: a machine learning team and a fairness auditor. After lengthy discussions about what fairness should mean in this context, they agree to evaluate fairness using **Equalized Odds Difference (EO Diff)**. Intuitively, this metric measures the largest difference in either the **true positive rate (TPR)** or the **false positive rate (FPR)** between demographic groups:

EO Diff = max(TPR difference, FPR difference)

The machine learning team explores different ways to achieve this goal, each targeting a different stage of the prediction pipeline: before training (pre-processing), during training (in-processing), or after predictions have been made (post-processing).


| Stage | What Changes? | Method |
|-------|---------------|---------|
| **Pre-processing** | **Data representation** | **[CorrelationRemover](https://fairlearn.org/main/api_reference/generated/fairlearn.preprocessing.CorrelationRemover.html)** transforms the data before training by reducing linear correlations between the features and the sensitive attribute. Intuitively, it adjusts feature values so that variables such as `priors_count` reveal less information about a person's race, while attempting to retain as much predictive information as possible. |
| **In-processing** | **Model training** | **[ExponentiatedGradient](https://fairlearn.org/main/api_reference/generated/fairlearn.reductions.ExponentiatedGradient.html)** incorporates fairness into the learning objective. Unlike standard gradient-based training, which searches for one best model, it maintains and reweights multiple candidate models, favoring those with a better accuracy–fairness trade-off under **[Equalized Odds](https://fairlearn.org/main/api_reference/generated/fairlearn.reductions.EqualizedOdds.html)**. |
| **Post-processing** | **Decision rule** | **[ThresholdOptimizer](https://fairlearn.org/main/api_reference/generated/fairlearn.postprocessing.ThresholdOptimizer.html)** leaves the trained model unchanged and adjusts the thresholds used to convert risk scores into binary predictions. Intuitively, it can be understood as selecting different operating points along group-specific ROC curves to better satisfy **[Equalized Odds](https://fairlearn.org/main/api_reference/generated/fairlearn.reductions.EqualizedOdds.html)**. |

---
#### 🟢🟢 Station 2 - Exploring all the different plots

Now imagine that you are an independent reviewer that need to make sense of what each of the mitigation methods achieved. You are handed over a file with a lot of figures and tables. This is not ideal because effectively you are flooded with information but it's very difficult to quickly obtain insights. For now have a look at the items handed over to you as shown below!!

:::{dropdown} Results

```{figure} ../images/audit-file/bars_accuracy.png
---
width: 100%
align: center
figclass: nonfloat
---
```
```{figure} ../images/audit-file/bars_false_alarms.png
---
width: 100%
align: center
figclass: nonfloat
---
```
```{figure} ../images/audit-file/bars_false_negatives.png
---
width: 100%
align: center
figclass: nonfloat
---
```
```{figure} ../images/audit-file/bars_true_negatives.png
---
width: 100%
align: center
figclass: nonfloat
---
```
```{figure} ../images/audit-file/confusion_matrices_by_race.png
---
width: 100%
align: center
figclass: nonfloat
---
```

```{figure} ../images/audit-file/confusion_matrices_overall.png
---
width: 100%
align: center
figclass: nonfloat
---
```

```{figure} ../images/audit-file/diff_true_negatives.png
---
width: 100%
align: center
figclass: nonfloat
---
```

```{figure} ../images/audit-file/roc_all_mitigation_models.png
---
width: 100%
align: center
figclass: nonfloat
---
```

```{figure} ../images/audit-file/table_performance.png
---
width: 100%
align: center
figclass: nonfloat
---
```



:::


---
#### 🟢🟢 🟢 Station 3 - Your task - Get insights from the data!

As we established, the machine learning team has handed you a large collection of plots and tables. While all of them contain useful information, the overall result is overwhelming and difficult to interpret. A good analyst does not simply create more visualizations but they also decide which information matters, how it should be presented and what story it tells.

Your task is therefore not only to analyze the results, but also to improve how they are communicated.

1) Before you even start: what questions to you want to answer in this setting? Think of what you know about COMPAS already, about the fairness mitigation approaches from Station 1 and the data at hand!
2) Then start by identifying the least interesting plots! Which elements are redundant or add little value?
3) Extract the key findings (insights) from the remaining visualizations. Focus on comparisons, trade-offs and relationships rather than individual numbers.
4) Think critically about information density. Which plots could be merged? Which metrics could be summarized differently?
5) Think of one or more alternative visualizations that would help communicate the results more effectively. Provide **hand-drawn examples** of plots you would like to see implemented! Based on the numbers at hand, depict what you expect to see!
6) Imagine that you need to brief a decision maker who only has one minute available. What are the three most important insights they should take away from the results?

**What should the submission look like?**

Submit a simple pdf file that includes 

- Your short insights from the data (see point 6!)  

- Images of the **hand-drawn sketches** of plots you would like to see implemented that would make the provided data easier to navigate! (See point 5)

- A short statement recommending one of the approaches (or none) and steps you would further want to be implemented! 

