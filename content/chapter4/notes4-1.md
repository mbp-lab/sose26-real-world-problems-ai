#  Model calibration - class notes

## Station 1: What is calibration and why does it matter?

First things first, let's get some definitions and intuitions straight! 

A model is well-calibrated if its predicted probabilities match observed outcomes. For example, among all patients assigned an 80% risk, we would expect about 80% to actually have the disease. But why do we expect that? Why couldn't all people with 80% risk have the disease? Or none? For that let's consider the following questions: 


:::{dropdown}

There is an 80% chance that it will rain tomorrow. What does and doesn't that mean?

It means that among days with similar weather conditions, it will rain on about 80% of those days. It doesn't mean it will rain 80% of the day. 

:::

:::{dropdown}

A doctor tells you: "Based on your test results, you have a 5% chance of having the disease." What does this mean?


A predicted probability is not a statement about what will happen to one individual patient. A patient either has the disease or does not. Instead, the probability describes what should happen across many similar patients. If a model repeatedly assigns an 80% risk to groups of similar patients, then about 80% of those patients should have the disease. If nearly all of them have the disease, the model is underestimating the risk. If only half have the disease, the model is overestimating the risk.

:::


Although we often use percentages to express confidence in everyday language (e.g., "I'm 100% sure this will happen"), in science a probability estimate should correspond to reality. If we repeatedly claim to be 100% confident but are wrong most of the time, then our confidence estimates are poorly calibrated.

The same idea applies to machine learning models. A model may assign an 80% predicted probability (often informally called its confidence), but that does not guarantee the estimate is accurate. Calibration measures whether these predicted probabilities can actually be interpreted as probabilities. In other words, when a model assigns an 80% predicted probability to many similar patients, do about 80% of them actually have the disease? If yes, the model is well calibrated. If not, the model is either overestimating or underestimating the true risk.


---

In your notebook, you were supposed to consider a hypothetical scenario where a hospital uses automatic screening to identify people needing further examination. The model seemed to work sub-optimally and there were doubts that it may not be well calibrated. You were given a few sketches to implement in a quest to identify what's wrong with the model!


:::{dropdown} Plot 1 - Prediction score distribution

The first plot requested you to plot the prediction scores of the undisclosed model. Below are some implementations and some of your insights: 

```{figure} images/histogram.png
---
width: 100%
align: center
figclass: nonfloat
---

Note how some of you took the raw count while others took the percentage. 

```

- "histogram of prediction scores shows that most patients get very low predicted risk and only a smaller group gets very high risk"

- "we can see that prediction scores tend to be extreme, there are two modes close to 0 and 1. The intermediate region is flat, which suggests that nuanced scores are relatively rare."




:::


:::{dropdown} Plot 2 - Predicted vs Observed Risk: One plot many interpretations

Sketch #2 turned out to be a bad idea (at least the way it was sketched). Even my own implementation seemed not ideal ...  So, feel free to skip to the next part or ... follow what is below without putting too much cognitive effort 🍿

```{figure} images/page1.jpg
---
width: 100%
align: center
figclass: nonfloat
---

```

```{figure} images/page2.jpg
---
width: 100%
align: center
figclass: nonfloat
---

```

```{figure} images/page3.jpg
---
width: 100%
align: center
figclass: nonfloat
---

```


:::


:::{dropdown} Plot 3 - Reliability plot

The third sketch asked you to plot a calibration or reliability plot. These plots usually plot observed frequencies vs predicted scores. For that, you were asked to calculate the mean prediction score in each bin and the disease rate for the people assigned to that bin by the model. Below are some of your explanations of what is observed here: 

- "The calibration plot is a key visualization as it compares the predicted risk with observed disease rate. This essentially answers or tries to answer the question: Do predicted probabilities match reality?"

- "Perfect calibration is represented by a linear line. If the model's calibration curve is above the diagonal, this indicates that the actual probabilities are higher than the predicted ones.If the curve is below the diagonal, it means that the predicted risk is more than the actual risk."

```{figure} images/calibration-line.png
---
width: 100%
align: center
figclass: nonfloat
---

```


- "From the calibration curve, the model does not seem very well-calibrated. Especially in the low-risk bins, the actual diseaserate is higher than what the model predicts. So the model is underestimating the risk for some patients."

- "how well the model is calibrated around the decision cutoff really matters for who gets help and who does not."

- "Real-life consequences are, that people that have low risk rates still can have the disease but they are not examined."

- "Also some of the people who dont have it are getting examined, but thats not too bad, in this case better safe than sorry."

- "In case of overestimation, where the model predicts risk scores higher than observed rates [...] it could also put the medical staff and the hospital overloaded when the resources are not widely available."

---
```{figure} images/reliability-bar.png
---
width: 100%
align: center
figclass: nonfloat
---
Note that these two plots are basically showing the same thing: one uses bars, the other a line plot. Having the axes similarly labeled would facilitate the comparison
```
---
```{figure} images/relative-picture.png
---
width: 70%
align: center
figclass: nonfloat
---
An alternative visualization of under- and over-confidence
```

:::


---

## Station 2: Model re-calibration

In this station we tried to set the record straight and improve the model calibration. As we didn't have access to the model to retrain it, post-hoc calibration is all we could do! 

:::{dropdown} Reminder of the re-calibration methods used

**Temperature Scaling**: intuitively, it turns the model's confidence up or down by a fixed amount for all predictions. This is done by adjusting the predicted risks by first expressing them on the log-odds (logit) scale, where the logit is defined as $\text{logit}(p) = \log\left(\frac{p}{1-p}\right)$. These log-odds are then divided by a single parameter called the temperature $T$ and transformed back into probabilities. A temperature above 1 makes predictions less extreme, while a temperature below 1 makes them more extreme. The temperature is learned from the calibration set by finding the value that best matches predicted risks to observed disease rates.

**Isotonic Regression**: intuitively, it applies a second machine learning model to transform the original risk scores into better-calibrated probabilities. It fits a regression model that learns how predicted risks relate to observed disease rates. This relationship is constrained to be isotonic, meaning that regression preserves the ordering of the predictions. In Python, this can be implemented with `sklearn.isotonic.IsotonicRegression`. Note that we are training a new model, so we'll need a training or calibration sample and a validation (some call it test) sample!
:::


:::{dropdown} Re-calibration results

Below you can see the results for the baseline model and the two re-calibration scenarios. While the re-calibrated models do not perfectly map the diagonal, they certainly come closer. In the words of one of your colleagues, "both methods pull the predictions much closer to the diagonal line in the calibration curve. The original model had predictions all over the place, way off in the low bin and underestimating in some high bins."

```{figure} images/re-calibration-comparison

---
width: 70%
align: center
figclass: nonfloat
---
```
---

This plot shows how the prediction scores change after re-calibration and how many people actually have the disease in each bin. Note that the distributions now get more spread out instead of being concentrated at the extremes. Having the same scale for the y-axis would have made it easier to spot the differences. 

```{figure} images/predictions_recalibrated

---
width: 70%
align: center
figclass: non-float
---
```

---
The plot below shows the predicted score distributions. Note how fixing the scale across the three plots makes the comparison easy. 

```{figure} images/prediction-scores-recalibrated

---
width: 70%
align: center
figclass: non-float
---
```

---
This other plot also illustrates how many people with the disease fall into each bin of the prediction scores. 

```{figure} images/recalibration-numbers

---
width: 70%
align: center
figclass: non-float
---
```



---

As one summarizing metric for calibration, we used the Brier score as it is used in clinical contexts for binary outcomes. The Brier score is calculated based on how much prediction scores differ from ground truth for each data point: 
$BS(p, y) = \frac{1}{n} \sum_{i=1}^{n} (p_i - y_i)^2$

Note that this is different from the estimated calibration error (ECE) which is based on the weighted difference between the predicted scores and observed outcomes *per bin* instead of each data point.  Check out [this Medium post](https://towardsdatascience.com/model-calibration-explained-a-visual-guide-with-code-examples-for-beginners-55f368bafe72/) for a visual explanation!

```{figure} images/recalibrated-table

---
width: 70%
align: center
figclass: non-float
---
```


:::




---

## Station 3: Visualizing "confidence"

In the final station, you were asked to visualize the dataset as a scatter plot and color each data point based on the predicted risk. For now, we informally treated the prediction score as confidence. However, this is a mental shortcut to think about the probabilities and the word "confidence" should not be interpreted too literally, as calibration is not the only concept relevant for uncertainty as you'll see in the next notebook. 

As you can see, calibration helps to smooth out the sharp divide between the data points that were originally assigned probabilities on the extremes of the scale (green vs red). For the re-calibrated model on the right, we can see how the probabilities are now more distributed, there are more points with predicted risk covering the middle parts of the scale. 

Note however, that from this plot we don't have information how these probabilities relate to the ground truth, hence we cannot speak of calibration: we can simply show that the prediction scores are now more distributed.  

```{figure} images/heatmap

---
width: 70%
align: center
figclass: non-float
---
```

The next plot added the ground truth with the help of markers. While the scatter plots are messier than the reliability plots or using Brier scores to summarize calibration, this can be a helpful visual example to get a quick idea. For example, note how the number of yellow dots, i.e., people getting the highest predicted risk, has decreased from left (original model) to the right (re-calibrated model). And all of the yellow dots are now patients who do actually have the disease. This helps us identify cases with the highest risk and compare to the ground truth. Consider a medical intervention with high stakes, such as amputation - we would like to have the highest probability only for people who actually are at highest risk, as a mistake would literally cost an arm and a leg. 

This plot also helps us see that the two classes overlap quite a bit. The regions of the scatter plot where the classes meet are regions of high aleatoric uncertainty, i.e. uncertainty that stems from the structure of the data itself and cannot be simply solved by collecting more data (epistemic uncertainty). 

While the scatterplots are not easy to summarize, they can be a great means for initial exploration, getting intuitions and sharing insights with less technical audiences. 

```{figure} images/heatmap1

---
width: 70%
align: center
figclass: non-float
---
```



