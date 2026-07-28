# Class notes — Adversarial attacks on tabular data

#### A short taxonomy of adversarial attacks 
Adversarial attacks aim to manipulate a model's output while remaining imperceptible or minimally noticeable. There are several ways to classify these attacks. In terms of adversary's influence, attacks may evasion attacks, when an adversary modifies input data to mislead an already trained model (test-time attack). Poisoning attacks, on the other hand, occur during training, when manipulation is introduced into the training data to influence the model's behavior (training-time attack). 

Adversarial attacks can also be classified according to the adversary's knowledge of the model. In a white-box attack, the adversary has access to information, such as the model architecture or parameters. In a black-box attack, the adversary has limited or no knowledge of the model's internal structure. 

In addition, an attack may be bounded or unbounded. A bounded attack restricts the magnitude of the perturbation according to a predefined constraint, such as a maximum distance between the original and the modified inputs. An unbounded attack does not impose such limits. 

Finally, an adversary may conduct either an untargeted or a targeted attack. In an untargeted attack, the goal is simply to cause the model to produce any incorrect prediction, while the targeted attack aims to force the model into a specific prediction. 

```{figure} images/adversarial-taxonomy
---
width: 80%
align: center
figclass: nonfloat
---

Image source: "TabAttackBench: A Benchmark for Adversarial Attacks  on Tabular Data", He et al. 2025
```


#### Boundary attack for tabular data

In the assignment, you worked with a breast cancer dataset and applied a Boundary Attack to generate adversarial examples. A Boundary attack is a black-box attack method that changes the original input to make the model misclassify it. Once an adversarial example is created, the algorithm performs a random walk, reducing the distance to the original input while remaining in the adversarial region, i.e. preserving the incorrect prediction. 

```{figure} images/boundary-intuition
---
width: 50%
align: center
figclass: nonfloat
---

Image source: "Decision-Based Adversarial Attacks: Reliable Attacks Against Black-Box Machine Learning Models", Brendel et al. 2018

```


#### **Imperceptibility metrics - your examples vs literature**

Once the adversarial attack was implemented, your main task was to implement so-called imperceptibility metrics. These metrics aim to quantify how easy adversarial attacks would be to detect based on how much they have changed the original input. 

Below, you can see the imperceptibility metrics, your implementations and suggestions from the literature based on the paper [Investigating Imperceptibility of Adversarial Attacks on
Tabular Data: An Empirical Analysis](https://arxiv.org/abs/2407.11463). 

---
**Proximity** - how much do the adversarial examples differ from the original sample?


:::{dropdown} Your examples


```{figure} images/proximity3
---
width: 80%
align: center
figclass: nonfloat

```

```{figure} images/proximity5
---
width: 80%
align: center
figclass: nonfloat

```
:::
:::{dropdown}Literature

```{figure} images/proximity-lit
---
width: 80%
align: center
figclass: nonfloat

```

:::

---
**Sparsity** - how many features were changed to achieve adversarial examples?
:::{dropdown} Your examples

```{figure} images/sparsity0
---
width: 80%
align: center
figclass: nonfloat

```

```{figure} images/sparsity1
---
width: 80%
align: center
figclass: nonfloat

```



```{figure} images/sparsity2
---
width: 80%
align: center
figclass: nonfloat

```
:::

:::{dropdown} Literature

```{figure} images/sparsity-lit
---
width: 80%
align: center
figclass: nonfloat

```
:::

----

**Deviation** - how representative are the adversarial examples of the original dataset distribution?

:::{dropdown}Your examples

```{figure} images/deviation0
---
width: 80%
align: center
figclass: nonfloat

```

```{figure} images/deviation1
---
width: 80%
align: center
figclass: nonfloat

```

```{figure} images/deviation2
---
width: 80%
align: center
figclass: nonfloat

```
:::

:::{dropdown}Literature

```{figure} images/deviation-lit
---
width: 80%
align: center
figclass: nonfloat

```
----
:::

**Feature interdependency - do the adversarial perturbations maintain meaningful relationships between features?**

:::{dropdown} Your examples

```{figure} images/feature-correlations0
---
width: 80%
align: center
figclass: nonfloat

```

```{figure} images/feature-correlations3
---
width: 80%
align: center
figclass: nonfloat

```

```{figure} images/feature-correlations1
---
width: 80%
align: center
figclass: nonfloat

```

```{figure} images/feature-correlations2
---
width: 80%
align: center
figclass: nonfloat

```
:::

---- 

#### Adversarial training for defense 🛡️
In the final part of the assignment, you explored adversarial training as a defense mechanism. The idea behind adversarial training is that the model is exposed to adversarial examples during training so that it learns to become more robust against attacks.


On the left of the figure below, you can see that when that the original model is very susceptible to adversarial attacks (the line at one on the extreme left). When we evaluate the same attack after adversarial retraining (compare to the blue box in the middle of the graph), the attack success rate decreases. However, when we now generate a new attack against the retrained model, we again see high success rate (the orange bar in the middle). Interestingly, even when using a completely different model, such as the TabPFN on the right, we see that although the adversarial samples were not generated against this model specifically (above zero success rate on the right side). 

This phenomenon, known as transferability, demonstrates that adversarial examples can often generalize across different model architectures. Hence, while adversarial training increases a model's robustness against previously known attacks, it does not completely eliminate its vulnerability.

```{figure} images/adversarial-transfer.png
---
width: 80%
align: center
figclass: nonfloat

```

