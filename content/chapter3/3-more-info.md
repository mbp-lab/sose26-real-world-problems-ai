# Chapter 3 — I want my model to be fair

```{figure} images/summary3

---
width: 70%
align: center
figclass: nonfloat
---

```

#### In a nutshell: what I hope you'll remember


- **Algorithmic bias** can stem from different sources: historical bias, representation bias, deployment bias, et cetera! It's important to keep an eye for it beyond simple performance metrics of a model. As there are different applications with different stakes, fairness metrics should also be chosen appropriately (remember our different judges!). 

- **The path to fairness is not easy** - simply removing sensitive attributes doesn't automatically lead to a fair model. Also, if differences exist between groups in reality, it doesn't mean that it's fair for the algorithm to reflect those differences. Real-life differences may stem from real life biases, which we shouldn't propagate. In addition, algorithms not only reflect existing biases but amplify them: bias in - more bias out. 

- **Bias mitigation** can employ different methods targeting different stages of the ML pipeline: some methods work at pre-processing level, other in-processing by including a fairness metric as learning objective or post-processing, trying to make predictions less biased after training. This distinction between in-, pre- and post is generally important because it also occurs for methods, such as re-calibration or xAI, which we didn't cover in detail. 

- **Research skill**: when trying to understand figures, you can do two things: 1) carefully study everything in the figure and ask yourself if you understand every element on the figure (e.g. what the legend means, what the axes represent, whether you can imagine what the underlying data and metrics are). This is very helpful when you know little about the topic and are trying to learn. 2) ask yourself what you want to find out before exploring the figure/ think about what you'd expect to see given what you already know about the problem. Then, check if the figure answers your questions. This is helpful when you are trying to critically evaluate somebody else's work or your own work say from a few days ago!

- **Research skill**: extracting information from a sea of visualizations is important. It's difficult to be concise, informative and clear but it's a goal to strive for. Once it becomes clear to you what questions you want to answer and what information to convey, it will become easier to know how to present insights. In addition, take inspirations from other fields to learn elements of visualizations that may not be present in your field. 


#### What we didn't cover: things to explore

- [A Survey on Bias and Fairness in Machine Learning](https://dl.acm.org/doi/10.1145/3457607) - very nice resource to look up things

- [A Clarification of the Nuances in the Fairness Metrics Landscape](https://www.nature.com/articles/s41598-022-07939-1)

- **The distinction between group vs individual fairness** - We already saw how different "judges" prioritize different things for achieving fairness. One additional concern is also group vs individual fairness as it may not be possible to achieve both, to the extent that some people have spoken of the [impossibility of fairness](https://arxiv.org/abs/1609.07236)!

- **Our discussions were limited to binary classification and one sensitive attribute** - We only talked about fairness metrics in binary classification. What happens in multi-class scenarios? How about regression? How about intersectional analysis, such as that of race and sex?

- **Calibration for fairness** - some people also consider calibration as fairness indicator. We didn't explore that. 




