# Chapter 3 — I want my model to be fair


<div style="text-align: right; margin: 2rem 0 1.25rem; line-height: 1.5; font-style: italic;">
<span>“The real problem of humanity is the following: we have paleolithic emotions, medieval institutions and godlike technology.”</span><br />
<span style="font-size: 0.75em; font-style: normal;">Edward O. Wilson, American biologist </span>
</div>



Fairness is something humans seem to care about from an early age. Even animals have been observed [rejecting unequal rewards](https://www.nature.com/articles/nature01963) when they see others receiving better treatment for the same effort. While far from perfect, humanity has made significant progress toward fair treatment of individuals through developments, such as the abolition of slavery, advances in  gender equality and human rights in general. 

```{figure} images/ai-fairness
---
width: 70%
align: center
figclass: nonfloat
---

Image Source : [Jan Teichmann](https://medium.com/data-science/bias-and-algorithmic-fairness-10f0805edc2b)
```


In a future, where algorithms are likely to be increasingly involved in decisions about hiring, healthcare and other aspects of our lives, they should also be held to the standard of fairness. Imagine being rejected for a job because the algorithm was trained on past hiring decisions that favored other demographic. Or receiving a less accurate medical recommendation because the system had been trained on relatively few patients similar to you. People care not only whether an AI system is accurate on average but also whether its decisions are fair. Yet defining and measuring fairness is not an easy task. 


**What to expect in this chapter?**

In the next notebooks, you will explore different metrics for assessing algorithmic fairness, methods for mitigating algorithmic bias, and the difficult trade-offs that arise when defining what it means for an AI system to be fair.

<details>
<summary><strong> Warm up - What is fairness? </strong></summary>

In this activity, we will briefly the concept of fairness - from its roots in biology to the modern challenges in Artificial Intelligence. 

```{figure} images/lady-justice.jpg
---
width: 40%
align: center
figclass: nonfloat
---
```


[Go to activity](fairness)


</details>

<details>
<summary><strong> Data for Chapter 3 </strong></summary>

[Compass dataset (Part 1, Station 1)](data/compas_clean.csv) 


</details>


<details>
<summary><strong>  Part 1 - Diagnosing algorithmic bias </strong></summary>

In this notebook you will perform a fairness audit by identifying bias from the famous COMPAS algorithm that was used to predict whether people will reoffend after a crime. You can probably already guess that there is some sort of bias going on. The exercise will be a warm-up to better understand the more complex-sounding fairness metrics from the literature that will be presented in the tutorial session. 

![Image](images/propublica)


[Go to the notebook](notebooks/0-compas.ipynb) ⏰ Deadline: Wednesday, June 17, 20:00

[Class notes]()


</details>


<details>
<summary><strong> Part 2 - Mitigating algorithmic bias </strong></summary>

Coming soon

[Go to the notebook](notebooks/) ⏰ Deadline: Wednesday, June 24, 20:00

[Class notes]()


</details>

<details>
<summary><strong> 🧶 What else is out there? - Further resources</strong></summary>

</details>

<br> 


