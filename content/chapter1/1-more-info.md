# Chapter 1 — I have only small data

```{figure} images/summary1

---
width: 70%
align: center
figclass: nonfloat
---

```

#### In a nutshell: what I hope you'll remember

- **The curse of dimensionality** can become a problem when you have little data and many features. But note, it does not arise simply because the distances between data points increase in higher dimensions. The real issue is that *relative distances* collapse: data points become almost equidistant, so the distinction of far and close loses its meaning. As a result, similarity becomes less informative, making it harder for algorithms that rely on distances to learn effectively. 


- **Noisy features**: Having many features in the data can also be counterproductive if the features are noisy. They may make regression coefficients inflated but the issue can be improved with regularization. 


- **Transfer learning** can improve model performance by providing informative, dense feature representations from data: instead of training from scratch with limited data you take advantage from knowledge learned from bigger datasets. However, be careful that data used for pre-training is representative of your data. 


- **Research skills**: When communicating insights using numbers or plots, make it clear how the evidence supports your conclusions.


#### What we didn't cover: things to explore

[A recent paper on ML with small and limited data](https://link.springer.com/article/10.1186/s40537-025-01346-9)

:::{dropdown} Check out a screenshot from the paper
```{figure} images/further-review1

---
width: 70%
align: center
figclass: nonfloat
---

```
:::

- What are the traditional methods to mitigate the curse of dimensionality?
- **Something to think about**: is the curse of dimensionality really an issue for modern models, such as deep neural networks, transformers or LLMs? 



