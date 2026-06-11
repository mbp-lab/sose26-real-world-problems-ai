# What is fairness?


<details>
<summary><strong> Fairness matters (obviously) </strong></summary>

Humans care deeply about fairness, to the extent that they will often sacrifice their own gain to reject unfair behavior. In the famous Ultimatum Game, one person decides how to split a sum of money (e.g., €100), while the other can either accept the offer or reject it, leaving both with nothing. It may or may not surprise you that people often reject offers they consider unfair, such as a 95–5 split, even though accepting the offer would leave them better off financially. Fairness, it seems, matters more than maximizing reward.

 
![Image](images/ultimatum-game)

Image Source: A review of neuroeconomic gameplay in psychiatric disorders, Robson et al., 2019


More amusingly, it has been shown that even primates have a sense of fairness. If they get unequal rewards for equal effort, they ... react unfavorably. 

[Watch the video on how monkeys react to unfairness](https://www.youtube.com/watch?v=meiU6TxysCg)

</details>



<details>
<summary><strong> Examples of unfair AI </strong></summary>


</details>

<details>
<summary><strong> Some useful concepts to think about algorithmic fairness </strong></summary>

While machine learning systems can exhibit many different forms of bias, it is often most useful to classify them according to the harms they produce. A common distinction is between allocative harms and representational harms.

**Allocative harms** occur when resources, opportunities, or services are unfairly distributed, resulting in certain individuals or groups being denied access to benefits such as jobs, healthcare or education. For example, a biased hiring algorithm may systematically disadvantage qualified applicants from particular demographic groups.

**Representational harms**, by contrast, arise when systems reinforce, perpetuate, or amplify negative stereotypes about individuals or social groups. Language models, recommendation systems, or image-generation models may encode societal biases and reproduce harmful associations, even when no direct allocation of resources is involved. 


It is also important to consider the entire machine learning pipeline when assessing potential harms, as bias can be introduced at multiple stages. Evaluating fairness requires not only examining technical aspects of the system but also understanding the social contexts in which it operates.

```{figure} images/bias-sources
---
width: 100%
align: center
figclass: nonfloat
---

Image Source : [A Framework for Understanding Sources of Harm throughout
the Machine Learning Life Cycle, Suresh and Guttag 2021 ](https://arxiv.org/pdf/1901.10002)
```


</details>

