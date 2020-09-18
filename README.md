# Predictors of Heart Failure 

## About the Project

### Goals

My goal for this project is to create a model that will predict heart failure using the clinical data provided. 
Equally important, I would like to identify which of these conditions and attributes are the biggest drivers for heart failure. 
I will deliver the following: acquire.py, prepare.py, model.py, report.ipynb, and predictions.csv

### Background 

From [Kaggle](https://www.kaggle.com/andrewmvd/heart-failure-clinical-data?select=heart_failure_clinical_records_dataset.csv): 

> "Cardiovascular diseases (CVDs) are the number 1 cause of death globally, taking an estimated 17.9 million lives each year, which accounts for 31% of all deaths worlwide.
Heart failure is a common event caused by CVDs and this dataset contains 12 features that can be used to predict mortality by heart failure.  
> Most cardiovascular diseases can be prevented by addressing behavioural risk factors such as tobacco use, unhealthy diet and obesity, physical inactivity and harmful use of alcohol using population-wide strategies.  
> People with cardiovascular disease or who are at high cardiovascular risk (due to the presence of one or more risk factors such as hypertension, diabetes, hyperlipidaemia or already established disease) need early detection and management wherein a machine learning model can be of great help."

### Acknowledgements

If you use this dataset in your research, please credit the authors  

> Davide Chicco, Giuseppe Jurman: *Machine learning can predict survival of patients with heart failure from serum creatinine and ejection fraction alone.* BMC Medical Informatics and Decision Making 20, 16 (2020). [link](https://doi.org/10.1186/s12911-020-1023-5)

> License: CC BY 4.0

___________________

## Data Dictionary

**age:** Age of the patient

**anemia:** Decrease of red blood cells or hemoglobin (boolean)

**creatinine_phosphokinase:** Level of the CPK enzyme in the blood (mcg/L)  

**diabetes:** If the patient has diabetes (boolean)  

**ejection_fraction:** Percentage of blood leaving the heart at each contraction (percentage)  

**high_blood_pressure:** If the patient has hypertension (boolean)  

**platelets:** Platelets in the blood (kiloplatelets/mL)

**serum_creatinine:** Level of serum creatinine in the blood (mg/dL)

**serum_sodium:** Level of serum sodium in the blood (mEq/L)

**sex:** Female or male (binary). I'm not certain, but my guess is that female = 0 and male = 1, based on the order of female & male listed in the dictionary.  

**smoking:** If the patient smokes or not (boolean)

**time:** Follow-up period (days)

**death_event:** If the patient deceased during the follow-up period (boolean)

______________

## Initial Hypotheses & Thoughts

### Thoughts

- We could add a new feature that counts the number of risk factors. 

- Should I turn the continuous variables into booleans, with a cutoff that represents increase in risk?   


### Hypotheses  

Those who do not survive have a higher number of risk factors than those who do. 

> $H_{0}: \mu(age_{death}) = \mu(age_{survival})$  
> $H_{a}: \mu(age_{death}) > \mu(age_{survival})$

Those who do not survive are older, on average, than those who do. 

> $H_{0}: \mu(age_{death}) = \mu(age_{survival})$  
> $H_{a}: \mu(age_{death}) > \mu(age_{survival})$

Those who do not survive have a higher ejection fraction, or percentage of blood leaving the heart at each contraction, on average, than those who do survive. 

> $H_{0}: \mu(EF_{death}) = \mu(EF_{survival})$  
> $H_{a}: \mu(EF_{death}) > \mu(EF_{survival})$

Those who do not survive have a significantly different levels of the creatinine phosphokinase enzyme in their blood, on average, than those who do survive. 

> $H_{0}: \mu(CPK_{death}) = \mu(CPK_{survival})$   
> $H_{a}: \mu(CPK_{death}) \ne \mu(CPK_{survival})$  

Those who do not survive have a significantly different count of plateles in their blood, on average, than those who do survive. 

> $H_{0}: \mu(platelets_{death}) = \mu(platelets_{survival})$  
> $H_{a}: \mu(platelets_{death}) \ne \mu(platelets_{survival})$

Those who do not survive have a significantly different level of serum sodium in their blood, on average, than those who do survive. 

> $H_{0}: \mu(serumNA_{death}) = \mu(serumNA_{survival})$  
> $H_{a}: \mu(serumNA_{death}) \ne \mu(serumNA_{survival})$

Those who do not survive have a significantly different level of serum creatinine in their blood, on average, than those who do survive. 

> $H_{0}: \mu(serumCreat_{death}) = \mu(serumCreat_{survival})$  
> $H_{a}: \mu(serumCreat_{death}) \ne \mu(serumCreat_{survival})$

The proportion anemic patients who die from heart failure is significantly different that of non-anemic patients.  

> $H_{0}: P(death_{anemia}) = P(death_{noAnemia})$  
> $H_{a}: P(death_{anemia}) \ne P(death_{noAnemia})$  

The proportion diabetic patients who die from heart failure is significantly different that of non-diabetic patients.  

> $H_{0}: P(death_{diabetes}) = P(death_{noDiabetes})$  
> $H_{a}: P(death_{diabetes}) \ne P(death_{noDiabetes})$

The proportion smoking patients who die from heart failure is significantly different that of non-smoking patients.  

> $H_{0}: P(death_{smoking}) = P(survival_{noSmoking})$  
> $H_{a}: P(death_{smoking}) \ne P(survival_{noSmoking})$

The proportion patients with high blood pressure who die from heart failure is significantly different that of patients without high blood pressure.  

> $H_{0}: P(death_{highBP}) = P(survival_{noHighBP})$  
> $H_{a}: P(death_{highBP}) \ne P(survival_{noHighBP})$

The proportion male patients who die from heart failure is significantly different that of female patients.  

> $H_{0}: P(death_{male}) = P(death_{female})$  
> $H_{a}: P(death_{male}) \ne P(death_{female})$

_________________

### Project Plan: Breaking it Down

**acquire.py**

acquire data from csv gathered from kaggle.com

**prepare.py**

- address missing data
- address outliers
- create `risk_factor_count`: I'm not sure which variables to include in that until I do the testing on my hypotheses, but in the meantime, I will use HighBP, Smoking, Diabetes, & Anemia)
- split into train, validate, test

**explore**  

- plot correlation matrix of all variables
- test each hypothesis
- are there cutoffs I should use to label each continuous feature as increased risk? Plot the continuous variables using a swarmplot or boxplot with death_event, and also observe the outcomes of the t-tests.  

**model**  

- try different algorithms: decision tree, logistic regression, random forest, knn, svm  
- which features are most influential? 
- evaluate on train
- select top 3 +/- models to evaluate on validate
- select top model  
- create a model.py that pulls all the parts together. 
- run model on test to verify. 

**conclusion**  

- summarize findings  
- make recommendations   
- next steps  
- how to run with new data.  

____________

### How to Reproduce

1. Download data from [Kaggle](https://www.kaggle.com/andrewmvd/heart-failure-clinical-data?select=heart_failure_clinical_records_dataset.csv) into your working directory. (You must be logged in to your Kaggle account.)

2. Install acquire.py, prepare.py and model.py into your working directory.  

3. Run the jupyter notebook.  

