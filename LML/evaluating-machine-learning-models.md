## machine learning jargon
- deep learning
- the kernel trick
- regularization
- overfitting
- semi-supervised learning
- cross-validation
## outset question
- How can I measure success for this project?
- How would I know when I’ve succeeded?

## machine learning workflow
- prototype---model selection  
- deployed model
- offline & online evaluation

## why is it so complicated?
### difference between off/online evaluation
- offline  </br>
    >accuracy ; precision-recall
- online <br/>
    >business metrics: LTV
    
### distribution drift
- historical and live data
- assume:  the distribution of data stays the same over time

## evaluation metrics
### classification metrics
- accuracy <br/>
    > measures how often the classifier makes the correct prediction.
    > correct answers for class 0 and class 1 are treated equally
- confusion matrix
- log-loss
- auc <br/>
    > The ROC curve shows the sensitivity of the classifier by plotting the rate of true positives to the rate of false positives. In other words, it shows you how many correct positive classifications can be gained as you allow for more and more false positives
    there are many popular variations of the idea of ROC curves：
    The marketing analytics community uses lift and gain charts. 
    The medical modeling community often looks at odds ratios.
    The statistics community examines sensitivity and specificity
  
### ranking metrics
- precision-recall (also popular for classification tasks)
- f1
- NDCG

### regression metrics
- RMSE ( sensitive to large outliers)

### offline evaluation mechanisms
- prototype: select right model to fit the data
- hold-out validation, also as known: k-fold cross-validation



