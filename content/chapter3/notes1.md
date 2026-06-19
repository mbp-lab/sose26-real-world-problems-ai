# Diagnosing algorithmic bias - class notes

In the last exercise, you were asked to explore a dataset associated with COMPAS, an algorithm predicting recidivism rate. This approach has caused a lot of controversy for being unfair to specific groups and you got a chance to get hands-on experience in it! In the following, we'll try to contextualize the insights from the notebook into the broader discussion of algorithmic fairness. 

The concept of fairness in itself is complicated. There are many definitions and metrics and it can be a bit challenging to keep a track of everything. So, to make our lives easier,  let's imagine different "judge personas" who each have a different notion of fairness. 

Note that this is done for the purposes of navigating the literature, not necessarily implying any legal approaches or definitions which would be outside of the scope of this class. 


## Simulated "judges" with different notions of fairness

The first "judge" we meet cares about the accuracy of an algorithm. Our judge is not very oblivious to justice and is informed about the fact that models may perform differently for different groups. Hence, their view is also a bit nuanced: they do demand that different groups should have similar accuracies. 

```{figure} images/judge1.png
---
width: 100%
align: center
figclass: nonfloat
---

```


```{dropdown}

Responses to Judge №1


```{figure} images/roc-with-race

---
width: 100%
align: center
figclass: nonfloat

---

- "The model performs similarly for both groups AUC around 0.73, which looks fair at first glance. But AUC only tells us how good the model is at ranking people it doesn't tell us who gets wrongly accused or wrongly cleared."

- "what I would more interested in, will be about how many false negative and false positive decisions are made" 

```

--- 



```{figure} images/judge2.png
---
width: 100%
align: center
figclass: nonfloat
---

```


```{dropdown}

Responses to Judge №2

**Disparate treatment and disparate impact**


There are some attributes that have historically been associated with discrimination and unequal treatment. These include characteristics such as race, gender, sexual orientation, religion, and disability. In fairness and anti-discrimination law, these are often referred to as protected characteristics.

Today, it is illegal in many contexts to make decisions explicitly based on such characteristics. This form of direct discrimination is known as **disparate treatment**. However, even when protected characteristics are not used explicitly, different groups may still experience different outcomes due to historical inequalities, societal factors or patterns in the data that reflect historical and socioeconomic biases. This form of indirect discrimination is known as **disparate impact**.

**Fairness or ignorance?**


Disparate impact expressed by practices that disadvantage one group over another may lead to features that indirectly "betray" group identity, even when race, gender or other protected attributes are removed from the model. In such cases, "fairness through unawareness" may lead to ignorance rather than to fairness. In the words of one of your colleagues, *"hiding the ‘race’ column is equivalent to putting a blindfold on the model once it has already seen the room"*. In fact, removing race completely from the model did not change the performance at all for our model. 

**What could be the reason that the removal of the race feature didn't change anything?**

We cannot give a definite answer without further information but we can make educated guesses based on our features and what we know about the policing system. Our small dataset has features, such as the number of prior offenses, how severe the charges were as well as sex and age of the offenders. For example, the number of prior offenses can be high, if people often get arrested for minor crimes due to racial profiling, or more "innocently" happening to leave in an area where crime is higher due to socioeconomic factors. So, if a model learns that number of prior offenses is important for predicting re-offending probability and if one group is more likely to be arrested for minor transgressions or due to systemic biases, this group will be automatically disadvantaged. 

```{figure} images/roc-with&without-race
---
width: 100%
align: center
figclass: nonfloat
---



```

----

```{figure} images/judge3.png
---
width: 100%
align: center
figclass: nonfloat
---

```


:::{dropdown} Responses to Judge №3

Okay, one good thing about this judge is that they do go beyond the simple accuracy metric. They also seem to be aware of the confusion matrix. But why are they focusing only on one value? Why true positives? In our application of recidivism prediction, this would mean an emphasis on identifying people who would re-offend and making sure we do so equally well for the different groups. At the moment we have the following situation:

```{figure} images/true-positives.png
---
width: 30%
align: center
figclass: nonfloat
---
Blue: African-American group, Orange: Caucasian group
```

If you can't follow the judgement of this judge, let's consider a broader picture depicting both the true positive rate and the false negative rate. In fact, they are related and sum up to 1 as true positives reflect identifying actual reoffenders, while false negatives reflect letting actual reoffenders slide.

```{figure} images/true-positives-false-negatives.png
---
width: 50%
align: center
figclass: nonfloat
---
Blue: African-American group, Orange: Caucasian group
```

You may not have cared initially for the true positive rate alone but at least some of you considered the false negatives very important for this application:

- "But I will be more worried about the FN as this will cause the harm to someone else as well and there will be more then one life effected by this decision".

- "the model is unfair to white crime-victims"

People initially emphasizing false negatives equally or even more than false positives were in the minority in the submissions. But they do have a point that would lead to a more in-depth philosophical, ethical and legal discussion which is unfortunately beyond the scope of this class. In the context of this task, we are aware of the historical bias and it's easy to (rightfully) care about false positives and how they affect individuals. But how would this reasoning hold if the stakes were perceived much, much higher? Say terrorism that can affect many people at once? It is at least something to think about!

**More natural uses of this notion of fairness**

The emphasis on true positives may be less relatable in this application but if you think about other cases, where positive predictions are associated with resources and opportunities, things change. For example, for a loan application or college admission, maximizing true positives would be desirable and false positives less consequential than in this application. 

:::

----

```{figure} images/judge4.png
---
width: 100%
align: center
figclass: nonfloat
---
```

:::{dropdown} Responses to Judge №4

This judge seems to be even more nuanced as they consider different types of decision outcomes. First, let's have a recap based on the confusion matrix.

```{figure} images/confusion-matrix.png
---
width: 50%
align: center
figclass: nonfloat
---
Blue: African-American group, Orange: Caucasian group
```

Okay, now we have arrived to a point where we consider both types of errors, an approach called equalized odds. Sometimes this is worded a bit differently but the gist is the same. Now, let's finally see the entire performance of our model and what it tells us about these odds!

```{figure} images/overall-performance.png
---
width: 100%
align: center
figclass: nonfloat
---
Blue: African-American group, Orange: Caucasian group
```

:::


## Bias in - bias out?



```{figure} images/bias-amplified.png
---
width: 50%
align: center
figclass: nonfloat
---
Blue: African-American group, Orange: Caucasian group
```

## A broader discussion - what else do we want to "teach our judges"?

:::{dropdown} Further points from your submissions

- The notion of race: 
"since the false positive rate is higher for the ‘Caucasian race’than for the ‘African-American race’ as the true positive rate increases. Writing it this wayfeels very wrong, since there is effectively no such thing as a “race,” and any theoryof race is simply racist."

- The general accuracy:

"the performance of the model is only decent, better than a random-guessing baseline, but not stellar"

- Deployment bias: 

- Odds

- Thresholds


:::


----

```{figure} images/judge5.png
---
width: 100%
align: center
figclass: nonfloat
---
```

---


