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
