#  Model uncertainty - class notes


:::{dropdown} Short recap: types of uncertainty


:::



## Station 1: Comparing two models

Accuracy vs calibration: what's the difference? --> somebody's gotta sketch it out! 

:::{dropdown} Short recap: accuracy vs calibration

1) What do we see regarding calibration?

```{figure} images/calibration-plots-reused

---
width: 70%
align: center
figclass: non-float
---

```

```{figure} images/prediction-plots-reused

---
width: 70%
align: center
figclass: non-float
---

```

:::


:::{dropdown} Do the models agree? What's the morale here? 


```{figure} images/compare-predictions.png

---
width: 50%
align: center
figclass: non-float
---
```

```{figure} images/compare-predictions1.png

---
width: 100%
align: center
figclass: non-float
---
```

```{figure} images/compare-predictions2.png

---
width: 100%
align: center
figclass: non-float
---
```



- **Some people reported different disagreement scores: I wonder if some of you only checked the predictions on what was dubbed as validation data? (Devarshi: 87 vs 56, Sanskriti: 25 vs 24)**

:::




## Station 2: Model uncertainty: why calibration is not enough?


:::{dropdown} Somebody's got to explain the MC dropout! 

```{figure} images/team-chat.png

---
width: 70%
align: center
figclass: non-float
---
```

:::

:::{dropdown} What we observed

* What are the axes?
* What do we see?
* What surprised you?

```{figure} images/uncertainty-scatter1
---
width: 70%
align: center
figclass: non-float
---
```

```{figure} images/uncertainty-scatter2
---
width: 70%
align: center
figclass: non-float
---
```


```{figure} images/compare-predictions2.png

---
width: 100%
align: center
figclass: non-float
---
```


```{figure} images/correlation-prevalence

---
width: 70%
align: center
figclass: non-float
---
```

:::

:::{dropdown} Sometimes a cigar is just a cigar 
* Good news: none of you fitted a line to an obviously non-linear dataset
* But you still reported correlation coefficients!
* Some were more careful but... was it really needed?

```{figure} images/fitted-curves.png
---
width: 70%
align: center
figclass: non-float
---
```

:::





## Station 3: Model uncertainty and data coverage


:::{dropdown} Refer or not refer that is the question

```{figure} images/referral

---
width: 70%
align: center
figclass: non-float
---
```


```{figure} images/coverage-uncertainty

---
width: 70%
align: center
figclass: non-float
---
```


:::

:::{dropdown} What else may be important?

Why may even low uncertainty not be enough?

- Imagine a case where the disease is heterogeneous: some cases are easy to classify because they present with clear symptoms but it's a less deadly form, while other cases have ... .  


:::


