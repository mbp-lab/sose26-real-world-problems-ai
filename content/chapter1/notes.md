# Class notes — Less is more?  

Congratulations! If you finished the assignment you have now explored the insights from the 
2009 paper "The curse(s) of dimensionality" by Naomi Altman & Martin Krzywinski without even reading it!

You started with exploring how distances behave in higher dimensions. What you would have observed is that pairwise comparisons become less informative as the number of dimensions grows. Specifically, it becomes harder to distinguish between nearby and distant points. Intuitively, points become like isolated dots scattered in a vast space, where everything is far apart and differences become less meaningful. Different metrics may have been affected at different rates but no distance metric can truly escape the curse of dimensionality. To fill the space, often exponentially more data points would be required. 

<details>
<summary><strong> Gallery of your figures from class </strong></summary>
</details>


<details>
<summary><strong> Fig.2 from Altman and Krzywinski, 2009 </strong></summary>


```{figure} images/Fig1-curses-of-dimensionality.png
---
width: 80%
align: center
figclass: nonfloat
---
```
</details>


When we speak of the dimensionality of a dataset, we are referring to the number of features or variables used to describe each data point. In machine learning, this has important implications: as dimensionality increases, models often require more data to generalize well. Think of k-nearest neighbors: it relies on distance-based comparisons between points but in high dimensional spaces, distances become less informative, making it harder to distinguish "friend from foe". 

<details>
<summary><strong> Visualization of neighborhood in relation to space  </strong></summary>


```{figure} images/Hastie-cube.png
---
width: 60%
align: center
figclass: nonfloat
---
Figure from "The Elements of Statistical Learning", Hastie et al. 2017
```
</details>


<details>
<summary><strong> Blind spots due to small data  </strong></summary>


```{figure} images/blind-spot-visualization.png
---
width: 70%
align: center
figclass: nonfloat
---
Figure from "The Elements of Statistical Learning", Hastie et al. 2017
```
</details>


In Station 2, you explored a hypothetical scenario in clinical application. 