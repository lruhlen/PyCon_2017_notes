# Snakes on a hyperplane: Python machine learning in production
Speaker: Jessica Lundin

## Different populations in training vs. production
Benchmark your model's performance.  It should be worse in production.  If it's better, that's a red flag that something might be broken.

Unknown production distribution: you don't know if your production user population is significantly different from what you tested the model on.

Ways to handle this:
+ retrain with non-linear algorithms ("pull out a bigger hammer")
+ feature engineering to linearize features
  	  + You generally want the simplest model that gives higher accuracy.  Linear methods, while less shiny, are generally better: more performant, easier to understand.
+ techniques for suspected distribution differences b/w preprod adn prod:
  + visualization (histograms, pair plots)
  + clustering
  + Kullback-Leibler (KL) divergence <-- NOTE TO SELF: LOOK THIS UP

## Unbalanced problems
(Where one class vastly outnumbers the other)

It's hard to characterize rare events: the model may fit to say "everything is just the majority class".

+ Precision: the sum of true positives over all predicted positives
+ Recall: <didn't catch>

Ways to handle this:
+ random over-sampling with replacement <--supervised
+ importance weighting <-- supervised
+ boosting <-- supervised
+ Treat it as an anomaly detection problem (one-class SVM) <-- unsupervised approach

## Hyperplanes
Transform your input data into a higher dimensional space (the 'kernel trick' in SVM)

## Practical tips

### LOGGING!
+ timestamp + instance ids
+ model run time
+ model results, performance metrics
+ model convergence errors

### Auditing
+ Manual process of digging into logs and data to resolve unexpected behavior

## ML resources
+ Caffe
+ The elements of statistical learning (free book) by Hastie, Tibshirani, Friedman, http://statweb.stanford.edu/~tibs/ElemStatLearn/
