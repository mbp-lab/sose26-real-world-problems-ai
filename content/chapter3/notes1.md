# Diagnosing algorithmic bias - class notes

In the last exercise, you were asked to explore a dataset associated with COMPAS, an algorithm predicting recidivism rate. This approach has caused a lot of [controversy](https://www.propublica.org/article/how-we-analyzed-the-compas-recidivism-algorithm) for being unfair to specific groups and you got a chance to get hands-on experience in it! In the following, we'll try to contextualize the insights from the notebook into the broader discussion of algorithmic fairness. 


## Simulated "judges" with different notions of fairness

The concept of fairness in itself is complicated. There are many definitions and metrics and it can be a bit challenging to keep a track of everything. So, to make our lives easier,  let's imagine different "judge personas" who each have a different notion of fairness. 

Note that this is done for the purposes of navigating the literature, not necessarily implying any legal approaches or definitions which would be outside of the scope of this class. 


--- 

```{figure} images/judge1.png
---
width: 100%
align: center
figclass: nonfloat
---

```
The first "judge" we meet cares about the accuracy of an algorithm. Our judge is not very oblivious to justice and is informed about the fact that models may perform differently for different groups. Hence, their view is also a bit nuanced: they do demand that different groups should have similar accuracies. 


:::{dropdown} Responses to Judge №1

Well, we actually had a look at the model performance for the different groups and the ROC-curves and the AUCs look similar for the both groups. 

```{figure} images/roc-with-race
---
width: 100%
align: center
figclass: nonfloat

```
However, you had a few words of caution:

- "The model performs similarly for both groups AUC around 0.73, which looks fair at first glance. But AUC only tells us how good the model is at ranking people it doesn't tell us who gets wrongly accused or wrongly cleared."

- "what I would more interested in, will be about how many false negative and false positive decisions are made" 

:::

--- 



```{figure} images/judge2.png
---
width: 100%
align: center
figclass: nonfloat
---

```
Judge №2 wants to avoid any kind of **disparate treatment**. This is a legal term referring to direct discrimination based on characteristics, such as race, gender, sexual orientation, religion, disability and similar. These are often referred to as protected characteristics. Nowadays, it is illegal in many contexts to make decisions explicitly based on such characteristics. 

:::{dropdown}
Responses to Judge №2

**Disparate treatment and disparate impact**

While the judge is very much aware of disparate impact, they  seem to forget about **disparate impact**. This is a form of indirect discrimination - even when protected characteristics are not used explicitly, different groups may still experience different outcomes due to historical inequalities, societal factors or patterns in the data that reflect historical and socioeconomic biases. 

**So, is it fairness or ignorance?**

Disparate impact expressed by practices that disadvantage one group over another may lead to features that indirectly "betray" group identity, even when race, gender or other protected attributes are removed from the model. In such cases, "fairness through unawareness" may lead to ignorance rather than to fairness. In the words of one of your colleagues, *"hiding the ‘race’ column is equivalent to putting a blindfold on the model once it has already seen the room"*. In fact, removing race completely from the model did not change the performance at all for our model. 

**What could be the reason that the removal of the race feature didn't change anything?**

We cannot give a definite answer without further information but we can make educated guesses based on our features and what we know about the policing system. Our small dataset has features, such as the number of prior offenses, how severe the charges were as well as sex and age of the offenders. For example, the number of prior offenses can be high, if people often get arrested for minor crimes due to racial profiling, or simply happening to leave in an area where crime is higher due to socioeconomic factors. So, if a model learns that number of prior offenses is important for predicting re-offending probability and if one group is more likely to be arrested for minor transgressions or due to systemic biases, this group will be automatically disadvantaged. 

```{figure} images/roc-with&without-race
---
width: 100%
align: center
figclass: nonfloat
---
```


:::

----

```{figure} images/judge3.png
---
width: 100%
align: center
figclass: nonfloat
---

```

Judge №3 is very concerned about avoiding future crimes. They really want to maximize the rate of identifying reoffenders to make their city a much safer place to leave. They don't care if a crime is committed by a white or a black person, all they care about is equal opportunity to identify either! 


:::{dropdown} Responses to Judge №3

Okay, one good thing about this judge is that they do go beyond the simple accuracy metric. They also seem to be aware of the confusion matrix, mentioning technical terms like "true positive rate". At the moment we have the following situation regarding the true positive and false negative rates:

```{figure} images/true-positives-false-negatives.png
---
width: 50%
align: center
figclass: nonfloat
---
Blue: African-American group, Orange: Caucasian group
```


In fact, true positives and false negatives are related and sum up to 1 as true positives reflect identifying actual reoffenders, while false negatives reflect letting actual reoffenders slide.

Some of you resonated with the judge, considering the false negatives very important for this application:

- "But I will be more worried about the FN as this will cause the harm to someone else as well and there will be more then one life effected by this decision".

- "the model is unfair to white crime-victims"

This point of view seeks fairness for future victims by trying to prevent crime. People initially emphasizing false negatives equally or even more than false positives were in the minority in the submissions. But would you side more on this judge, if the stakes were perceived as much, much higher? Say terrorism that can affect many people at once? This leads to  a more in-depth philosophical, ethical and legal discussion which is unfortunately beyond the scope of this class but worth thinking about as such discussions are often part of the public discourse. 

**More natural uses of this notion of fairness**

The emphasis on true positives may or may not be the most relatable in this application but you can think about other cases, where positive predictions are associated with resources and opportunities. For example, for a loan application or college admission, maximizing true positives would be desirable and false positives less consequential than in this application. That's why this metric is also called equal opportunity metric. 

:::

----

```{figure} images/judge4.png
---
width: 100%
align: center
figclass: nonfloat
---
```
Judge №4 has a slightly different stance - they acknowledge that no procedure is perfect, mistakes happen. But when they do happen, no group should be disproportionately affected by them. 


:::{dropdown} Responses to Judge №4

This judge seems to be even more nuanced as they consider different types of decision outcomes. First, let's have a recap based on the confusion matrix. Here, the mistakes of the model can be seen for false negatives (reoffenders not identified) and false positives (somebody wrongly flagged). 


```{figure} images/confusion-matrix.png
---
width: 50%
align: center
figclass: nonfloat
---
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

Now that our emphasis is on both types of mistakes, we can see that African-Americans have higher rates of false positives, e.g. being wrongfully flagged (unfair as they are stigmatized and suffer real consequences), while Caucasian group has larger chance of not being identified (unfair to their potential victims). The fairness notion of Judge №4 would try to make sure the rates are similar for both groups for both types of errors!

:::

---

```{figure} images/judge5.png
---
width: 100%
align: center
figclass: nonfloat
---
```
There is also another judge who thinks that fairness can only achieved if the model predicts recidivism at equal rates for each group, regardless of the true base rate!

:::{dropdown} Responses to Judge №5

Let's be honest, the point of view of this judge is hard to understand in the recidivism setting. Why should we expect the same rate between different groups without considering what the actual recidivism rates are? If one group genuinely reoffends more often, shouldn't the algorithm reflect that?

This is exactly why Judge №5 often feels out of place in this context. However, the judge plays an important role in reminding us that historical patterns are not always patterns we want algorithms to perpetuate.

Consider representational bias in text. Historically, women were more often associated with caregiving roles and men with leadership roles. A model trained on historical data may faithfully reproduce those patterns. Judge №5 asks a different question: should algorithms merely reflect the world as it was or should they help us move toward the world we want? In such settings, enforcing demographic parity or similar notions of representation may be a way to counteract and correct historical biases rather than reinforce them.

:::

---

## Bias in - bias out?

Now, let's leave our judges behind and actually check how the algorithm predictions compare to the actual recidivism rate of the groups. 

What we notice is that the recidivism rate is actually high for the African-American group. The algorithm seems to also predict this quite well. However, we see that for the Caucasian group, the predictions are far below the actual rate. This means that the existing gap between the two demographic groups (solid blue bar vs solid orange bar) not only get reflected by the algorithm but also get amplified (dashed blue bar vs dashed orange bar)! So it's not just bias in - bias out but bias in - more bias out!

```{figure} images/bias-amplified.png
---
width: 50%
align: center
figclass: nonfloat
---
Blue: African-American group, Orange: Caucasian group
```
---

## A broader discussion - what else do we want to "teach our judges"?

Further points from your submissions

- **The notion of race**: 
"since the false positive rate is higher for the ‘Caucasian race’than for the ‘African-American race’ as the true positive rate increases. Writing it this wayfeels very wrong, since there is effectively no such thing as a “race,” and any theoryof race is simply racist."

- **The general accuracy of the model**: "the performance of the model is only decent, better than a random-guessing baseline, but not stellar", "Even with the ethical disaster that these numbers imply pushed to the side, aren't these rates like really bad? If I had come up with a model performing like this in another class, I'm not sure if I would've passed."

- **Deployment bias**: Note that when discussing the negative consequences of false positives, you mentioned different scenarios from being arrested to facing a harsher sentence, being denied bail, et cetera. While these answers worked for the sake of the exercise, it is very important to be careful here! Remember, all that the model is predicting is a recidivism rate! That doesn't translate into things like sentence harshness because the sentence is given for a particular crime not for the entire character of a person. This disconnect between what an algorithm is trained for and what it may be used for is known as deployment bias that should be avoided! 

----

## Technicalities

:::{dropdown} Fairness definitions verbatim from a paper

Below is an extract from the paper ["A Survey on Bias and Fairness in Machine Learning"](https://dl.acm.org/doi/10.1145/3457607) by Mehrabi et al. 2021 for your reference: 

```{figure} images/fairness-technicalities.png
---
width: 100%
align: center
figclass: nonfloat
---
```

:::
---


