# Chapter 5 — I need to explain my model

```{figure} images/summary5

---
width: 70%
align: center
figclass: nonfloat
---

```

#### What I hope you'll remember

- **Different applications may call for different methods**: There are different xAI methods that focus on providing explanations focusing on features, examples and counterfactuals. Even if you may be technically be able to implement all for your model, different explanations may be helpful in different scenarios (remember: medical diagnosis, loan approval, job applications)
 
- **Keeping users in mind**:  xAI methods are only useful if they can be understood and correctly interpreted
by users.

- **Research skills**: when extracting information from sources like videos, pay attention to what is the best level currently for you. You may need to focus on pieces of knowledge that have long shelf-life (e.g. concepts, ways of thinking about things), such as ideas that age well and transfer between domains. Remember how Shapley values were developed in a game theory context and counterfactuals are inspired by cognitive science. On the other hand, you may also need things with immediate relevance, such as what is a good library that is state-of-the art (DICE example in one of the videos). 
 

#### Some additional resources

- [Explanation in Artificial Intelligence:  Insights from the Social Sciences](https://www.sciencedirect.com/science/article/pii/S0004370218305988) - a highly influential paper

- [Explainable AI for Audio and Visual Affective Computing: A Scoping Review](https://ieeexplore.ieee.org/abstract/document/10766406) - A review paper on xAI from our lab


#### Your open questions after the chapter

- How does SHAP work for image data? How are the features defined exactly?
- How can SHAP be used for human-centric explanations?
- What is more often used in real-world applications: SHAP or counterfactuals?
- How exactly does SHAP remove features. The video mentioned replacing it by random features but how dependent are these on the specific dataset?
- Does the approximation affect the quality of SHAP explanations compared to actual permutations?
- What happens if the features are highly correlated?
- How precisely can SHAP answer questions like "feature i is only useful if feature j is also in the subset", if at all?
- Which SHAP visualization is helpful for which question?


- How do counterfactuals work for neural networks?
- How do counterfactuals work for image or video data?
- How can more diversity be forced for counterfactuals?
- Okay, we learned that counterfactuals are similar to adversarial examples. What exactly is the difference though? The intent?
- If a model is bad, how useful are the explanations at all?

