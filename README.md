# predictive-medicare
Modeling on a public-use Medicare dataset to attempt to predict several chronic health outcomes: diabetes, depression, and high-cost.

Medicare is the United States’ national social health insurance program for older adults. Medicare
serves approximately 50 million Americans, the majority of which are 65 and older (some younger
individuals with disabilities are also served).
Machine learning can be applied in healthcare to identify patients at risk for specific health outcomes.
We analyzed a publicuse
Medicare dataset to attempt predictive modeling for several outcomes:
diabetes, depression, and highcost.
We selected diabetes due to its widespread prevalence in the
United States (much of it undiagnosed) , and the significant economic toll it takes 1 on our healthcare
system2. We chose depression because its cooccurrence
with physical health conditions has been well
documented3, and we wanted to see if we could predict its occurrence based on physical and
demographic features in our dataset. We sought to predict highcost
individuals because we believe a
predictive algorithm for the costliest patients would be useful to insurance companies wishing to curb
expenditures via preventive programs. We also initially attempted predictive models for death and
endstage
renal disease, although we abandoned these efforts for reasons we will address in a following
section.
Our hypothesis was that we could use machine learning models to effectively predict diabetes,
depression, and highcost
patient outcomes.

## Data Storage and PreProcessing
We loaded the dataset into a PostgreSQL database, and served it to Jupyter notebooks via ODBC
connection. Initial preprocessing
was performed on the fly while loading in the data, by way of SQL
query. A death indicator was constructed by checking for patients with a listed death date in 2009 or
2010, so that 2008 data could be used predictively. We derived an age field from the listed date of birth,
and we aggregated cost fields into subtotals
for inpatient, outpatient, carrier claims, and total costs.

## Methods: Predictive Models Used
We ran four predictive models on our data. First, we constructed a naive Bayes classifier mixed model to
accommodate both discrete and continuous inputs, adapting code provided in class; we used a training
set to construct a probability distribution to apply against a test set. Next, we ran our data through a
linear support vector machine (SVM) using sklearn, using a validation set to identify an optimal C value.
We then applied a neural network classifier against our training and test set, using code furnished by the
course instructor. We additionally ran a random forest model, using sklearn. Finally, we constructed a
simple heuristic model from scratch.
To simplify evaluation of our various models, we created a module called evaluate.py to output a set of
standarized set of evaluation results. Specifically, this function calculates outputs the following: true
positives, false positives, true negatives, false negatives, accuracy, sensitivity/recall, specificity, precision,
and F1 score. Additionally, for reference, it also outputs the true rate of the outcome of interest in the
sample. Values we paid close attention to are sensitivity out
of all patients with diabetes, how many
did the classifier classify correctly and
precision out
of the individuals whom the model predicted
diabetes, how many were classified correctly.

## Data treatment before running the models
Before applying the features into the models, we created dummy data for the demographic data and
rescaled the medical expense data through whitening for
both the linear support vector machine and
the random forest classifier. In addition, we sampled 10% of the entire dataset to enable the SVM
workable in our personal computers where computing resource is not enough to deal with all data.
Before running the Random Forest Classifier, we also converted the continuous data coverage,
inpatient, outpatient and carrier costs into binary variables by splitting the data at the median values.
In testing our models, we employed a 67%/33% training/test split.
