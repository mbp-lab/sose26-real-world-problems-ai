# Class notes — Less is more?  

Congratulations! If you finished the assignment you have now explored ideas from the 
2009 paper "The curse(s) of dimensionality" by Naomi Altman & Martin Krzywinski without even having to read it! In the following class notes, you will see what worked well, some common mistakes and what could improve across submissions. Finally, you will also see additional materials to improve your understanding. 

📌 Note that all Python-generated plots are extracted from the class submissions but are kept anonymous. For future submissions, names can be included if students give their consent in advance! 

## 🟢 Station 1 - Exploring distance in higher dimensions

You started with exploring how distances behave in higher dimensions. Your submissions provided many interesting visualizations. Let's see what went well and where things needed improvement across many of the submissions. 

In most of the submissions, the pair-wise distances were visualized either as line plots or histograms as shown below.

**Figure 1 - Euclidean distance**


<div style="display:flex; gap:10px;">
  <img src="images/euclidean-line.png" width="300"/>
  <img src="images/euclidean-histogram.png" width="300"/>

</div>

**Figure 2 - Cosine distance**

<div style="display:flex; gap:10px;">
  <img src="images/cosine-line.png" width="300"/>
  <img src="images/cosine-histogram.png" width="300"/>

</div>


 ### ✅  What worked well 

The visualizations plotted the steps asked in the assignment and were mostly properly labelled. In fact, some of your visualizations look close to what was published in the influential paper of Naomi Altman & Martin Krzywinski! 

<div style="display:flex; gap:10px;">
  <img src="images/paper-euclidean.png" width="300"/>
  <img src="images/paper-cosine.png" width="300"/>

</div>

```{dropdown} **🤔 Why does the paper use correlations, while we used cosine distance?**

Note that in that paper, they used correlations instead of cosine distance but these two are conceptually related in that they both scale the dot product between two vectors by their lengths. The difference is that correlation first centers the vectors relative to their means, while cosine similarity uses the original vectors directly.

Cosine distance:

$$
d_{\cos}(x,y)=1-\frac{x \cdot y}{\|x\|\|y\|}
$$

Correlation:

$$
\rho_{x,y} = \frac{(x-\bar{x}) \cdot (y-\bar{y})}{\|x-\bar{x}\|\|y-\bar{y}\|}
$$
```

In addition to the visualizations, many submissions reached the following conclusions: 
1) points become farther apart in higher dimensions
2) points become equidistant: the difference between minimum and maximum shrinks
3) cosine distance is less affected than Euclidean distance

These conclusions were **on the right track but incomplete**. Let's look at what was missing across many of your submissions. 


 ### ⚠️  The problem 

Very often, the figures and the statements in the submissions showed a disconnect: the conclusions were correct but they were not stemming directly from the visualizations. For example, 

1) as dimensions increase, the distances between the points also increase (**not specified: for which distance metric?**)
2) the difference between nearest and farthest points gets smaller (**not specified: which exact plot shows that and how**)
3) cosine distance is less affected than Euclidean distance (**not specified: where do we see that? From the typical plots we may conclude the opposite: the distances collapse for cosine**)

For the assignments, having the correct answer is not necessarily the goal. It is important to link insights to evidence and show *how* you arrived at a conclusion. This is an important analytical skill and it will also prompt you to create plots that are guided by your reasoning. Let’s unpack it all next!

 ### 🔗 Establishing the connections
**Absolute Euclidean distance doesn't show the entire picture**

The most obvious thing that Euclidean distance plots (see Figure 1 above) reflected was the following: higher dimensions shift the distance distributions higher: distances increase. For cosine distance, we have to be more nuanced:  we see that the minimum distance increases, while the maximum distance decreases.  This shift in minimum and maximum distances results in a visible decrease of the gap between the two: as dimensions increase everything concentrates around a common value. Interestingly, for Euclidean distance, the gap between min and max distance does not look decisively different for lower vs higher dimensions. They both just increase.  What is going on? 

Euclidean distance measures absolute separation between data points. As dimensionality increases, distances naturally grow because because additional dimensions contribute to the total squared distance. However, absolute distances alone are misleading in high dimensions. What matters is not the raw magnitude of distances, but their relative contrast: whether nearby and distant points remain distinguishable relative to the overall scale of the data. Think of an ant and a human: a few meters are trivial for us but enormous for an ant. Meaningfulness comes from relating distances to the scale of the data, to know what constitutes "close" and "far". The Euclidean distance plots provided (variations of Figure 1) did not directly reveal this phenomenon; they only showed that all distances increased together.

**Why cosine distance reveals contrast**

Cosine distance does something under the hood that Euclidean distance doesn't. It normalizes the vectors (data points) by their lengths. In our assignment, we saw how cosine distances tend to get closer to 1 as dimensionality increases. Since cosine distance is defined as $1 - \cos(\theta)$, this means that cosine similarity ($\cos(\theta)$) approaches 0.  

To understand what this means geometrically, recall that cosine similarity measures how aligned two vectors are. If two vectors point in exactly the same direction, the angle between them is $0^\circ$, and $\cos(0^\circ)=1$. They are maximally similar. If the vectors are perpendicular, the angle between them is $90^\circ$, and $\cos(90^\circ)=0$. In that case, the vectors share no directional alignment: they are orthogonal.  

```{figure} images/cosine.jpg
---
width: 80%
align: center
figclass: nonfloat
---
```
Image Source: https://www.learndatasci.com/glossary/cosine-similarity/


Thus, in high dimensions, random vectors in high-dimensional spaces tend to become nearly orthogonal. Their directions become increasingly unrelated, which means the data points become less similar. So, in simple words, once we account for the scale (normalizing by magnitude) with the cosine distance, we can reveal visually how the distances concentrate, the gap between minimum and maximum shrinks. This loss of contrast is what the curse of dimensionality is about! Close and far "lose their meaning". 

**How to directly compare distance metrics**


We can in fact also adjust the visualization of the Euclidean distances to make this loss of contrast clear. The assignment didn't specify how to assess the "separation between the closest and farthest points". That was on purpose to make you think how to define separation. If ratio, rather than the absolute difference between minimum and maximum distances is used, an interesting pattern emerges: as dimensionality increases, the ratio between the closest and farthest distances approaches one.  It becomes harder to distinguish between nearby and distant points for many random data models. Intuitively, points become like isolated dots scattered in a vast space, where everything is far apart and differences become less meaningful. Different metrics may have been affected at different rates but no distance metric truly escapes the curse of dimensionality. 


```{figure} images/line-relative-complete.png
---
width: 80%
align: center
figclass: nonfloat
---
```



<details>

<summary><strong> Implications for machine learning </strong></summary>

When we speak of the dimensionality of a dataset, we are typically referring to the number of features or variables used to describe each data point. In machine learning, this has important implications: as dimensionality increases, models often require more data to generalize well. Think of k-nearest neighbors: it relies on distance-based comparisons between points but in high dimensional spaces, distances become less informative, making it harder to distinguish "friend from foe". Same issues arise for clustering methods replying on distance estimations!

**Visualization of neighborhood in relation to space**


```{figure} images/Hastie-cube.png
---
width: 60%
align: center
figclass: nonfloat
---
Figure from "The Elements of Statistical Learning", Hastie et al. 2017
```


**Blind spots due to small data**

```{figure} images/blind-spot-visualization.png
---
width: 70%
align: center
figclass: nonfloat
---
Figure from "The Elements of Statistical Learning", Hastie et al. 2017
```


</details>

</details>

</details>



## 🟢🟢 Station 2

In Station 2, you were asked to repeat the calculation of distances in different dimensions but this time simulating two classes with varying degrees of overlap. 

To manipulate the overlap between the two classes, most of you rightfully manipulated the means of the Gaussian distributions. 

When looking at *absolute* Euclidean distances, the separation between classes tends to increase with dimensionality. This is because distances accumulate across dimensions, so even small differences in the underlying distributions (such as a slight mean shift in the high-overlap case) add up. But we need to be careful! 


```{figure} images/overlap-line.png

---
width: 70%
align: center
figclass: nonfloat
---

```

```{figure} images/overlap-histogram.png

---
width: 70%
align: center
figclass: nonfloat
---

```

While more dimensions may increase absolute inter-class distances, intra-class distances often increase as well. As a result, larger raw distances do not necessarily imply improved class separability. As observed in Station 1, high-dimensional spaces tend to reduce the contrast between near and far points relative to the scale of the space. Below is an example from a submission that used relative distances. As you can see, higher distances did not necessarily lead to a better separation once the scale of the space was taken into account:


<div style="display:flex; gap:10px;">
  <img src="images/euclidean-distance-separation" width="300"/>
  <img src="images/cosine-distance-separation" width="300"/>

</div>


<details>

<summary><strong> Important distinction: adding dimensions vs transformations </strong></summary>

Note that there is an important difference between simply adding more dimensions and transforming the data into a more informative feature representation. For example, transforming Cartesian coordinates into a radial feature (distance from the center) can make the classes below linearly separable.

<div style="display:flex; gap:10px;">
  <img src="images/svm1.png" width="300"/>
  <img src="images/svm2.png" width="300"/>

</div>


</details>

</details>




## 🟢🟢🟢 Station 3

In Station 3, you simulated a scenario where you would add more and more features to your model, while there was only one feature actually affecting your variable. As most of you noticed, with more features (higher dimensions in the sense of dataset), irrelevant features started having larger coefficients (so more relevance for the model decision), while the coefficient for the true variable decreased. One of you even pushed the number of features further to 10000 showing how the true predictor becomes indistinguishable from noise.

<div style="display:flex; gap:10px;">
  <img src="images/all-noise" width="200"/>
  <img src="images/interpolation2.png" width="200"/>
  <img src="images/interpolation1.png" width="200"/>


</div>


</details>

</details>


The line plots show the effect in a particularly interesting way: do you notice the bump around 100? That is the interpolation threshold, where the number of features is exactly the same as the number of samples, leading to a case where the model can perfectly fit the training data. In this setting, the model can memorize the data and becomes highly unstable, fitting noise instead of signal, causing coefficients to fluctuate wildly and inflate for irrelevant features. While not strictly the same, this effect is eerily similar to the phenomenon of [double descent](https://en.wikipedia.org/wiki/Double_descent). 


Finally, many of you rightfully noticed that the increase of irrelevant feature coefficients can be tamed by regularization. By adding a penalty on large coefficients (e.g. L2 regularization), the model becomes discouraged from assigning large weights to irrelevant features.



## 🐘 Optional Bonus Station 

The bonus station introduced “von Neumann’s elephant”, referring to the famous quote: “With four parameters I can fit an elephant, and with five I can make him wiggle his trunk.” One of you actually managed to fit a curve to the elephant in the classroom using multiple Fourier terms!

This nicely concludes the topic of “Less is More?” by reminding us that increasing complexity can make our tools powerful but, under the wrong circumstances, eventually ridiculous.

![Image](images/elephant-solved.png)

