# Heart-Health-Prediction
Using Public Dataset to predict chance of heart disease.

The goal of this project was to dissect the UCI Health dataset on heart health. It contains 14 different values and a target for whether or not the patient has heart disease. As someone with a family history of heart disease, this is a dataset which peaked my interest.

It's not extremely clear what each of the variables represent, so I will explain them here:

1. age: how old the patient is
2. sex: 1 for male and 0 for female
3. cp: Chest pain type
	1 - typical angina
	2 - atypical angina
	3 - non-anginas pain
	4 - asymptomatic
4. trestbps: resting blood pressure (mmHg)
5. chol: cholesterol in mg/dl
6. fbs: fasting blood sugar:

	'> 120 = 1'
	
	'< 120 = 0'
7. restecg: resting electrocardiographic results 
	- Value 0: normal 
	- Value 1: having ST-T wave abnormality (T wave inversions and/or ST elevation or depression of > 0.05 mV) 
	- Value 2: showing probable or definite left ventricular hypertrophy by Estes' criteria 
8. thalach: maximum heart rate achieved
9. exang: exercise induced angia (1 for yes, 0 for no)
10. oldpeak: ST depression induced by exercise relative to rest
	- ST depression is relative to your heart rate and can be viewed with a T wave graph measuring heart beat
11. slope: Another metric used by analyzing the T wave graph
	- Can be upward (2), flat (1), or downward sloping(0)
12. ca: number of major vessels (0-3) colored by fluoroscopy
13. thal: 
	- 3 = normal
	- 6 = fixed defect
	- 7 = reversible defect
14. target: 1 for no heart disease, 0 for heart disease.

After I defined all the variables, I did a few tests to check for relationships between the target and predictors individually. This is where my initial bar graphs come in. I can separate the groups based on the value of the predictor variable, and see if there is a change based on the target. For example, if the predictor was not significant, there should be a similar amount of people in the target and non target group for that predictor variable.

I start by checking the amount of people in each target group. We have slightly more people who are healthy than unhealthy. Additionally, it's important to note that the healthy patients information was gathered when they were admitted to the hospital for suspicion of a heart problem. This means that we definitely did not have a random sample, but prediction of the average person should still give us an accurate result. 

I first saw that exercise angia has a big difference in outcome for those who did and didn't have that symptom. If the patient did have exercise angia, they were very likely to have heart disease.

I saw conflicting results with the variable 'ca'. I initially thought that as patients had more vessels colored by fluoroscopy, they would be more likely to have heart disease. This is true for all except one value, when there are two colored vessels.

It can also be noted that females have a much lower chance of heart disease than males.

Now that I have a general idea of what variables might be significant, I can conduct a hypothesis and create a linear regression. Based on what I saw above, I guessed the most significant variables will be  exang, thal, sex, and age.

I then moved onto creating my first logistic regression. I first inputted all 13 predictor variables into the same logit function and saw the results. My hypothesis was close, as I guessed 3 of the 4 most significant variables correctly. I guessed that 'thal' would be significant, but it came in 5th with 'thalach' being the 4th most significant variable. Nonetheless, I recreated my logit function with the 4 most significant variables and compared the two.

The full model has significantly higher prediction power. This means that I removed some variables I should not have. My next model will be all of the predictor variables that are significant at the 5% level (p < .05).

This model now meets both general requirements I was looking for. Each predictor variable is significant, and I didn't lose too much prediction power from the full model. If I wanted to go further here, I could do diagnostic analysis and continue to test different submodels.

My next step was to test how accurate this logistic regression was on the original data. From the code below, it turned out to be 79% accurate at predicting the test set. I wanted to compare this to a Random Forest and Support Vector Machine before concluding that this is a good model.

The random forest (similar to decision tree) method came in at 78% accuracy, a bit worse than the logistic regression. The SVM had a 81% accuracy. The confusion matrix shows that each method was only off by a couple of observations from one another.

Support Vector Machine: 81% accuracy

Logistic Regression: 79% accuracy

Random Forest: 78% accuracy

It seems that these results help confirm the words of many Data Scientists: chances are a simple model will get the job done just fine. 

