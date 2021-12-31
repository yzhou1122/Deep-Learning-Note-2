
# Gradient Checks

 ## 1. Use centered formula

 Use dual side check for numerical gradient : 
 $$df(x)\,/\,dx = \frac{f(x+h)- f(x-h)}{ 2h}$$ 
 where h is commonly set to 1e-5.

 ## 2. Use relative error for the comparison

 Concrectly, let $\,f'_n$ and $\,f'_a$ denote numerical gradient and analytic gradient, respectively. 
 Use a "ratio" check : 
 $$\frac{\| f'_a - f'_n \| }{max \,( \|f'_a\| \mathrm{,} \|f'_n\| )}$$

 if error \> 1e-2, usually means gradient is wrong.
 1e-2 - 1e-4 : unconfortable.
 1e-4 : Ok for objectives wih kinks. Too high for objectives without kinks ( e.g. tanh, softmax).
 1e-7 : happy.

 The deeper the network , the higher the relative errors will be.

 ## 3. Use double precision

 ## 4. Stick around active range of floating point.

 if some reason or cases driving your gradient very small ( e.g. normalize loss over batch, when gradients per datapoint are very small, 

 which leads to even smaller ( divided by n ),

 you should scale up temporarilly the loss function by a constant to make sure a nicer range where floats are more dense.

 ## 5. Kinks in the objective.

 kinks refer to non-differentiable part. (e.g. ReLU, when x \< 0, analytic gradient should be zero. However, numberic gradient may be non-zero when $\,f(x+h)$ cross over the kink. Use $max\,(x,y)$ when evaluating $\,f(x+h)$ and then $\,f(x-h)$, if winner changes, then it shows that a kink was crossed.

 Another way to solve it is to use only few datapoints.

 ## 6. Gradcheck in a period of "burn in" time

 Do not do gradcheck on the first iteration, and not on single point but in a period.
```
def 
 ## 7. Turn off regularization, drop out, 
 ## and augmentation when checking
 The "regularization loss overwhelm the data loss", thereby masking incorrect grad implementation.

 ## 8. Check only few dimensions
 .

---



# Deep-Learning-Note-2

# Setting up your Goal
  '''
  continue..
  '''
  ## 1.2 satisficing metrics (e.g. running time <100ms ) v.s optimizing goals ( no limit, once satisficing goal satisfied)
    if one metric doesnt fit...
  ## 1.3 train/dev/test distributions
  
    1. try let your dev and test be with same distribution
	2. Size: 98%/1%/1% 
	  a. test set be big enough to give high confidence in the overall performance of your system. (e.g. 1W~10W)
	3. if you do well on dev/test , but not on your application, change metric and dev/test set

  ## 1.4. beyong human performance and the limit of performance : bayes optimal
        the avoidable bias = gap b/w bayes optimal and model training error
  		understand human performance:
		  usually, human-level error as a proxy for bayes error: 
		  case                -I-       -II-       -III-
		  human error         0.5%       0.5%       0.5%? 
		  training error      5%         1%         0.7%
		  dev error           6%         5%         0.8%
		  see problem as     bias     variance       ?
		  
		  *but as you approach bayes optimal, you have to be more careful since you dont know how far from it 
	
	## 1.5. Whem ML surpasses human , current tools which could help you direction become limited.
	
	
	## 1.6. to wrap up, given 2 assumptions of supervised learning 
	      a. have low avoidable bias --> training fit well
		  b. have low acceptable variance -->training performance generalize well
		  
		  if diff(human error, training error) > diff(training error, dev error):
		  	focus on bias reduction:
				bigger model, train longer,better optimization, nn architecture, search hyper-para
		  else:
		    focus on variance reduction:
				bigger data set, regularization , nn architecture, search hyper-para
				
	
# ML strategy - week 2
## 2.1 error analysis
       analyze badcase one by one, find the class or type that improves the model most.
## 2.2 clean up incorrect label data 
   	   a. DL algorithms are quiet robust to random errors in the training set
	   b. but not robust to systematic errors 
	   
	   count incorrect labels in misclassified ones to check is it worthful to correct them?
	   
	   to correct labels:
	    1. "apply" same process to dev and test sets to ensure same distribution
		2. 	"consider" both the algorithm got right and got wrong (not apply because once 98% vs 2%, the 98% may be very costly)
		3. and "notice" that train and dev/test may now come from slightly different distribution.
		
## 2.3 build you first system very quickly,then iterate 
