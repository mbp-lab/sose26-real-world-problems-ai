#  Model uncertainty - class notes



:::{dropdown} Short recap: types of uncertainty


:::



#### Station 1: How do two models compare on the same data?

You were asked to compare the two models in terms of their accuracy and calibration. Your results showed that they had similar accuracy and the calibration was somewhat better for the MLP model. You then compared decisions from two models and identified cases where they agreed vs disagreed. Many of you used a scatter plot showing the prediction scores from the two models. You can see that they don't perfectly agree in terms of the prediction scores (points aren't on the diagonal) and the orange points show where the two models also disagree in classification, i.e. when a threshold of 0.5 is applied to the prediction scores to make a binary decision. 

```{figure} images/compare-predictions2.png
---
width: 50%
align: center
figclass: non-float
---
```

The next plots show more detailed exploration. What's interesting is that when the two models disagree, each of them is correct half of the time: so neither model is systematically more correct than the other. 

```{figure} images/compare-predictions1.png
---
width: 100%
align: center
figclass: non-float
---
```



:::{dropdown} Examples from submissions where concepts were reused

Although you were not explicitly asked for it in this submission, some of you re-used the visualizations and metrics from the last assignment! That's very nice and shows that you are transferring your knowledge out of the context you learned!

```{figure} images/calibration-plots-reused

---
width: 70%
align: center
figclass: non-float
---

```

```{figure} images/prediction-plots-reused

---
width: 70%
align: center
figclass: non-float
---

```

:::


--- 


#### Station 2: Model uncertainty: why calibration is not enough?

Up to now, we saw that models can have similar accuracy but different calibration scores. So, again, the story so far:

- **Accuracy** in a classification task measures how often the model correctly predicts the class.

- **Calibration** characterizes whether a model’s predicted probabilities make sense as probabilities.

A model can have high accuracy but be poorly miscalibrated. For example, if the model gives somebody a risk score of 60% even though their actual risk score is 80% in both cases, the value would exceed a decision threshold of 50% --> accuracy wouldn't change. 

So far so good. But in the last station saw that two models often disagree. What to make of that? This points to another important concept: uncertainty. There are different ways of defining uncertainty, but a helpful way for you to remember is asking: would a model always make the same decision for a given data point? 

There are two types of uncertainty: epistemic and aleatoric. Epistemic uncertainty (on the right in the figure below) characterizes lack of knowledge, either because of the model itself or because of lack of data. This type of uncertainty can be mitigated with a better model or collecting more data. By contrast, aleatoric uncertainty (on the left in the figure below), arises due to the randomness present in the data itself (alea in Latin means a game of dice, so it indicates the element of chance)!

```{figure} images/uncertainty-types.png

---
width: 70%
align: center
figclass: non-float
---
Image source: [Aleatoric and epistemic uncertainty in machine learning: an introduction to concepts and methods](https://link.springer.com/article/10.1007/s10994-021-05946-3)
```


In your assignment, you used MC dropout to get a measure of uncertainty for your data. This concept relies on the concept of dropout used for regularization: in a neural network, such as MLP, you have different forward passes, in which you randomly switch off some neurons. Then you repeat this process so that the network avoids relying on specific pathways only. A standard rule for dropout for regularization is to only use the neuron switching during training and use the full network for the inference. However, Monte Carlo (MC) dropout keeps the dropout active during inference (test) time. By performing multiple forward passes, the model produces a set of predictions rather than a single prediction. The variability across these predictions can then be used to estimate the model's predictive uncertainty. 

```{figure} images/dropout-MC.png
---
width: 70%
align: center
figclass: non-float
---
```


You used the predictions from 50 estimations aka 50 different forward passes to derive uncertainty based on the standard deviation of these prediction scores. You can see that in our scenario, the uncertainty was higher for the middle range of the prediction scores which also happen to be areas where the two classes overlap a lot. In this case, the aleatoric uncertainty is high as this overlap is intrinsic to the scenario and cannot be mitigated simply by collecting more data. 


```{figure} images/uncertainty-scatter2
---
width: 70%
align: center
figclass: non-float
---
```

:::{dropdown} Sometimes a cigar is just a cigar 
When asked to describe the relationship between the prediction scores and uncertainty, many of you interpreted "relationship" as the need to come up with a quantitative measure, such as a correlation. 
* Good news: none of you fitted a line to an obviously non-linear dataset
* But you still reported correlation coefficients!
* Some were more careful but... was it really needed?

Sometimes a cigar is just a cigar is a saying attributed to Sigmund Freud and it's often colloquially used for scenarios where things are simpler than one assumes - in this case, there was no need of fitting any model, you could have just described the scatter plots qualitatively. 

```{figure} images/fitted-curves.png
---
width: 70%
align: center
figclass: non-float
---
```

:::



#### Station 3: Model uncertainty and data coverage

In the final station, you simulated a scenario of "“We want the AI to only make predictions when it is likely to be reliable; otherwise, pass the decision to a human!”. For that you simulated a system that only provides a prediction if the uncertainty score is below a threshold; otherwise the decision would be referred to a human specialist. Your task was to examine what fraction of patients would rely on an automated decision (algorithm coverage) for different values of the threshold. As you can see in the image below, having automated decisions only when the uncertainty is very low (the left part of the curves), results on very high accuracy. However, the coverage is also very low, meaning that most decisions would need to be referred to a human specialist. This shows that for sensitive cases, such as in healthcare, where high decision confidence is needed, a ML model with high accuracy or good calibration may not be enough. Uncertainty considerations may make even a highly accurate model impractical. 


```{figure} images/referral-results.png

---
width: 70%
align: center
figclass: non-float
---
```




