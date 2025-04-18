# Final
Final Capstone submission


# Initial framing and deviation
From the initial framing of the problem to report out a food complaint, the analysis is modified to determine if the complaint received qualifies for a recall and what category of recall does the reason for re-call fall into.

Why the question is important :  Primarily the Food Manufacturing industry takes significant time and resources to determine whether the complaint classifies as a recall and what kind of class it belongs, to determine the urgency of the recall process. One of the plots from de codetermines the lag in number of days since a complaint was filed and a classification was determined because of the heavily human interfered process. The ML initiative is to create a model to identify if the event/complaint qualifies for a recall and which class of recall it belongs to.

Recalls are actions taken by a firm to remove a product from the market. Recalls may be conducted on a firm's own initiative, by FDA request, or by FDA order under statutory authority.
Class I recall: a situation in which there is a reasonable probability that the use of or exposure to a violative product will cause serious adverse health consequences or death.
Class II recall: a situation in which use of or exposure to a violative product may cause temporary or medically reversible adverse health consequences or where the probability of serious adverse health consequences is remote.
Class III recall: a situation in which use of or exposure to a violative product is not likely to cause adverse health consequences.

# Dataset and Initial analysis

The dataset used for generating the model is directly downloaded files in JSON format from the FDA complaints and recalls database. The focus was primarily on the reason for recall field, where some of the key words for recall for grouped to evaluate the type of recalls at large. But mostly this would be a classical NLP based multi-classification model. And for that reason, Naïve Bayes model was chosen as the base line model.

 # Baseline Model output – Naïve Bayes

Accuracy: 0.815033161385409
             		 precision    	recall 	 f1-score   	support
     Class I       	0.86     		 0.82      0.83      	2401
    Class II       	0.78      	0.88      0.83      	2718
   Class III       	0.86     		 0.23      0.36      	 309

    accuracy                           		0.82      	5428
   macro avg       0.83      	0.64      0.67     	 5428
weighted avg       0.82      	0.82      0.81      	5428
 
After the initial evaluation of the base line model which showed a decent accuracy, we used multiple regression and classification models, focused just on the column ‘reason for recall’ as the only feature for NLP modeling. The output for each model is as below

# Logistic Regression 
Accuracy: 0.8848563006632277
Best Parameters for Logistic Regression: {'C': 10}
              		precision    recall  		f1-score   	support
   Class I      	 0.88      	0.90      	0.89     	 	2401
    Class II       	0.89      	0.89      	0.89     	 	2718
   Class III       	0.86     		 0.71      	0.78      	309

    accuracy                           		0.88      5428
   macro avg       0.88      0.83      	0.85      5428
weighted avg       0.88      0.88      	0.88      5428

 
# Random Forest 
Accuracy: 0.909174649963154
Best Parameters for Random Forest: {'max_depth': None, 'n_estimators': 100}
             		 precision    	recall 	 	f1-score   	support
     Class I       		0.92      0.92      	0.92      	2401
    Class II      		 0.90      0.93      	0.91      	2718
   Class III      		 0.94      0.67      	0.78       	309
    	accuracy                          	 0.91      5428
macro avg       0.92      0.84      0.87      5428
weighted avg       0.91      0.91      0.91      5428
 
# Support Vector Machine 
Accuracy: 0.9119380987472365
Best Parameters for SVM: {'C': 10, 'kernel': 'rbf'}
              			precision    recall  	f1-score   	support
     Class I       		0.92      	0.93      0.92      	2401
    Class II      		 0.91      	0.92      0.91      	2718
   Class III       		0.92     		 0.71      0.80       	309
    accuracy                           		0.91      5428
   macro avg       	0.91      0.85      0.88      5428
weighted avg      	 0.91      0.91      0.91      5428

  
	 Model	                  Accuracy
	Naive Bayes	              0.833456
	Logistic Regression	      0.884856
  Random Forest            	0.909175
	SVM	                       0.911938

# Evaluation Metrics Interpretation

The two evaluation metrices: accuracy and the classification report (which includes precision, recall, F1-score, and support).  
For each class, precision is the proportion of correctly predicted positive observations to the total predicted positive observations.  A high precision means that when the model predicts a class, it is likely to be correct.
For each class, recall is the proportion of correctly predicted positive observations to the all observations in actual class. A high recall means that the model is good at identifying all positive instances of a given class. The F1-score is the harmonic mean of precision and recall.  It provides a balanced measure that considers both false positives and false negatives.  It's particularly useful when the classes are imbalanced.
While accuracy gives an overall picture, the classification report provides a more granular analysis of the model's performance for each class. This is crucial because the classes might be imbalanced (different numbers of Class I, II, and III recalls).  Accuracy alone could be misleading if one class significantly outnumbers others.  The classification report helps identify if the model is performing well for all classes or if it's biased towards certain classes, particularly important for recall which is how well it finds all of a specific class of recalls.  In this food recall context, correctly identifying all Class I recalls (most serious) is critical even if the model makes a few more errors on less severe recalls. A  low recall and F1 Score for Class III due to lesser data.

After evaluating all the models, Support Vector Model  is having an higher accuracy and precision across all classifications, closely followed by Random Forest. Boosting Random Forest model did not help as the accuracy reduced drastically. Boosting SVM was costing high GPU usage and was not able produce any outputs with the existing GPU capacity. (Code is provided for the same).

# Final recommendation is to rely on SVM with the below mentioned accuracy and parameters.
# Accuracy: 0.9119380987472365
# Best Parameters for SVM: {'C': 10, 'kernel': 'rbf'}

