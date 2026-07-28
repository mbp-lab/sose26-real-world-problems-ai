# Chapter 2 — I want my model to be robust

```{figure} images/summary2

---
width: 70%
align: center
figclass: nonfloat
---

```

#### In a nutshell: what I hope you'll remember

- **Adversarial attacks** work by the principle of adding small perturbations that fool the model.
There are a bunch of metrics for assessing their properties, such as how feasible they are, how close the adversarial samples are to the original, how sparse they are, meaning how many features need to be changed. Adversarial training can make models robust against the attacks but it may not be the final answer as the model may remain vulnerable to further types of attacks. 

- **Data leakage** can happen at many stages of the ML pipeline, always keep an eye for it.  For example, keep an eye on how you standardize, normalize your data, how you select your features, to which data you apply PCA! All of these should always be fit to the training data, not validation or test, as the model otherwise will be exposed to data leakage!

- **Nested cross-validation** is computationally expensive but recommended for small data as it allows you to get not one test error but several, helping to obtain a more reliable estimate of model generalization. 

- **Research skill**: pen-and-paper scribbling has underestimated power! When grappling with complex concepts, sketch out your thought process, revise and redraw your ideas, do battle with the paper and emerge with triumphant clarity!


#### What we didn't cover: things to explore

**The broader field of ML robustness**
- Chapter 3 - Machine learning robustness: a primer [](https://www.sciencedirect.com/science/chapter/edited-volume/abs/pii/B9780443237614000122)

**Adversarial attacks**
- When can adversarial examples be helpful? - Check this paper shared by one of your colleagues on [Adversarial T-Shirt! Evading Person Detectors in a Physical World](https://dl.acm.org/doi/10.1007/978-3-030-58558-7_39)

- Adversarial examples in the physical world [](https://arxiv.org/abs/1607.02533) - these things aren't just theoretical. 

- More methods to protect models against adversarial attacks [](https://link.springer.com/article/10.1007/s10462-025-11147-4) 

- What are common ways of adversarial training and what challenges and solutions do they have?

**Validation**
- Cross-Validation Visualized: A Narrative Guide to Advanced Methods [](https://www.mdpi.com/2504-4990/6/2/65)
- The impact of K selection in K‑fold cross-validation on bias and variance in supervised learning models [](https://www.nature.com/articles/s41598-026-37247-x)

**Data leakage**
- Leakage and the reproducibility crisis in machine-learning-based science [](https://www.sciencedirect.com/science/article/pii/S2666389923001599)
- Don’t push the button! Exploring data leakage risks in machine learning and transfer learning [](https://link.springer.com/article/10.1007/s10462-025-11326-3)
- Guiding questions to avoid data leakage in biological machine learning applications [](https://www.nature.com/articles/s41592-024-02362-y)






