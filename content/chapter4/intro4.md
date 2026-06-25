# Chapter 4 — I want to quantify the certainty of my model

<div style="text-align: right; margin: 2rem 0 1.25rem; line-height: 1.5; font-style: italic;">
<span>“I know that I know nothing”</span><br />
<span style="font-size: 0.75em; font-style: normal;">Socrates</span>
</div>
 

Admitting what one doesn't know is sometimes difficult and not everyone is always as good at it as the famous Greek philosopher. You may have heard of the Dunning-Kruger effect, the phenomenon describing how people overestimate their abilities in domains for which they have less expertise. As expertise grows, confidence generally becomes better calibrated, but outside of one's own area of expertise, this may affect almost everyone, including Nobel laureates (google Nobel disease!). 


```{figure} images/dunning-kruger.png
---
width: 70%
align: center
figclass: nonfloat
---

Image Source : [The Dunning–Kruger Effect: On Being
Ignorant of One’s Own Ignorance](https://www.sciencedirect.com/science/chapter/bookseries/pii/B9780123855220000056)
```



Well, it turns out machine learning models also struggle with overconfidence. You may have noticed this from your own interactions with a large language model: they often sound very certain even when they have no basis for it (I made chatGPT write this). This points to the broader question of model uncertainty: how can we tell whether a model's confidence is actually justified?

**What to expect in this chapter?**

You will start by exploring an important concept in machine learning prediction: calibration. You will learn how to check for calibration, how to improve it and how to ... well, avoid confidently overinterpreting what calibration can achieve. In the second part, you will explore well-known uncertainty quantification methods used for neural networks. 


<details>
<summary><strong> Data for Chapter 4 </strong></summary>

[Rural Cancer Screening (Part 1)](data/rural_screening.csv) 

</details>


<details>
<summary><strong> Part 1 - Model calibration </strong></summary>

A remote rural hospital has implemented an AI-assisted screening program for identifying people with undiagnosed disease. However, after deployment, they notice something isn't quite right. The ML team says the model is not well-calibrated. What does that even mean?


```{figure} images/calibration-image
---
width: 100%
align: center
figclass: nonfloat
---

Image Source: Understanding Model Calibration - A gentle introduction and visual exploration of calibration and the expected calibration error (ECE)
```

In this notebook you will learn what calibration is, why is it important and how to evaluate and improve it. 


[Go to the notebook](notebooks/0-calibration) ⏰ Deadline: Wednesday, July 1, 20:00

[Class notes]()

</details>

<details>
<summary><strong> Part 2 - Coming soon </strong></summary>

[Go to the notebook](notebooks/) ⏰ Deadline: Wednesday, July 8, 20:00

[Class notes]()

</details>

<details>
<summary><strong> 🧶 What else is out there? - Further resources </strong></summary>

</details>

<br> 
