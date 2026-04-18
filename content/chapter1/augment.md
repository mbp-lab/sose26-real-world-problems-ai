# Tutor guide — Less is more?  

- The exercises are designed to walk them through the   2009 paper "The curse(s) of dimensionality" by Naomi Altman & Martin Krzywinski without reading it!

- The instructions are deliberately not too detailed to allow room for interpretation, decision making and consequently, different results with common mistakes

- The former point has been tested by prompting AI to do the exercise as described. It gives a bunch of plots but not necessarily in an intelligent way to get to an interesting result. 

- The test showed that the students may likely just plot all distances on the same plot - masking the effect relative to scale. Similarly, the separation between min and max distances may be measured by mere subtraction which would ignore the scale of the space. 

- Asking them to plot max/min may lead to an aha-moment when all distances (although at different rates) tend to go to 1 with higher dimensions. 


# Questions to guide the session

- You were asked to sample points from a standard normal distribution. Which of this is a standard normal distribution?
- How would you do it in Python? Which function did you use?
- At first, you were asked to simply  visualize pairwise distances between points as dimensions increase. What distance metric did you choose for that? 
- What happened when the dimensions increased? 
- Who saw a pattern that looked like this. 
- Who saw something like this. 
- What did you pick for separation? 
- Choice of the distance metric.  