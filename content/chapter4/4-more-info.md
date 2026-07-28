# Chapter 4— I want to quantify the uncertainty of my model

```{figure} images/summary4

---
width: 70%
align: center
figclass: nonfloat
---

```
#### In a nutshell: what I hope you'll remember


- **Accuracy** in a classification task measures how often the model correctly predicts the class. 
- **Calibration** characterizes whether a model's predicted probabilities make sense as probabilities. In other words, do they match the observed frequencies of outcomes? For example, among all patients assigned an 80% risk, we would expect about 80% to actually have the disease. Calibration is important whenever predicted probabilities are used for decision-making, e.g. in a medical scenario, rather than only the predicted class. Note that a model can achieve high accuracy while still being poorly calibrated.


- **Uncertainty** characterizes how certain the model is about its predictions. For example, would the model make the same decision if it were trained again with a different random initialization? Or would a different model trained on the same data agree with its prediction? Uncertainty can arise from aleatoric aspects caused by inherent noise or ambiguity in the data or due to epistemic factors reflecting limited knowledge. The epistemic uncertainty can often be reduced by collecting more data or having a better model, the aleatoric can't. 

- **Dropout** is a regularization technique while MC dropout is a method for estimating predictive uncertainty. They differ by whether dropout is used only during training or also during inference. 


#### What we didn't cover: things to explore

- [A Survey on Uncertainty Quantification Methods for Deep Learning](https://arxiv.org/abs/2302.13425)
- [Aleatoric and epistemic uncertainty in machine learning: an introduction to concepts and methods](https://link.springer.com/article/10.1007/s10994-021-05946-3)
- [Understanding model calibration - a gentle introduction and visual exploration of calibration and the expected calibration error (ECE)](https://arxiv.org/abs/2501.19047)


- Can one measure and disentangle epistemic and aleatoric uncertainty practically?
- What methods of uncertainty estimation are combined with which models?
- Can we benchmark uncertainty estimation?
- How to best communicate model uncertainty and use it in decision-making?
- Why isn't everybody doing uncertainty quantification and report calibration? Shouldn't it be more famous? 

