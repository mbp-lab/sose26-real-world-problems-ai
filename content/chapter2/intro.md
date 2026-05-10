# Chapter 2 — I want my model to be robust


<div style="text-align: right; margin: 2rem 0 1.25rem; line-height: 1.5; font-style: italic;">
<span>“It is difficult to predict, especially the future.”</span><br />
<span style="font-size: 0.75em; font-style: normal;">Attributed to various sources</span>
</div>


Humans may not be perfect at recognizing every kind of animal, but we know a panda when we see one. Deep neural networks, however, can be surprisingly confused. It has been shown that adding tiny noise that is invisible to humans can cause advanced models to misclassify a panda as a gibbon with over 99% confidence [[1]]( 	
https://doi.org/10.48550/arXiv.1412.6572). This is not an isolated example: funky glasses could fool face-recognition systems into mistaking one person for another [[2]](https://dl.acm.org/doi/10.1145/2976749.2978392). In some cases, even changing a single pixel has been enough to change a model's prediction [[3]](https://doi.org/10.48550/arXiv.1710.08864). 


```{figure} images/adversarial-examples
---
width: 100%
align: center
figclass: nonfloat
---
```



These examples expose a fundamental question in machine learning: robustness. Robustness refers to "the capacity of a model to sustain stable predictive performance in the face of variations and changes in the input data" [[4]](https://doi.org/10.48550/arXiv.2404.00897). This is a crucial point toward deploying ML applications in the real world. 


**What to expect in this chapter?**

You will start by exploring adversarial attacks in tabular data, a type of data that has received relatively less attention in the adversarial machine learning literature. You will then explore a notebook related to generalizability.

<details>
<summary><strong> Data for Chapter 2 </strong></summary>


[German Credit Risk dataset](data/german_credit_data.csv) 


</details>


<details>
<summary><strong> Part 1 - Adversarial attacks on tabular data </strong></summary>

While adversarial attacks on images are well-established and often hard to detect with the naked eye, tabular data is more complicated because its features are heterogeneous, constrained by relationships between the features and perturbations are often noticeable.

![Image](images/adversarial-tabular)

**Image source**: Investigating imperceptibility of adversarial attacks on tabular data: An empirical analysis

In the following notebook, you can perform an example adversarial attack on tabular data and learn quantitative imperceptibility metrics for describing such attacks.

[Go to the notebook](notebooks/0-adversarial) ⏰ Deadline: Wednesday, May 20, 20:00

Class notes (will be available after deadline)

</details>

<details>
<summary><strong> Part 2 - Coming soon </strong></summary>

[Go to the notebook](notebooks/1-generalization) ⏰ Deadline: Wednesday, May 27, 20:00

Class notes (will be available after deadline)

</details>

<details>
<summary><strong> 🧶 What else is out there? - Further resources </strong></summary>

</details>

<br> 




