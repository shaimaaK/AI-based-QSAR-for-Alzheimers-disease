# AI-based-QSAR-for-Alzheimers-disease
AI-based Quantitative structure Activity relationship study for Alzheimer's disease project is implemented as part of the Data Mining Course in my Masters degree in AI.
The projects analysis the Quantitative structure Activity relationship of the Amyloid beta A4 protein and the Alzheimer's disease where the activity of the protein is
predicted as pIC50 standard value.

## Table of Content
- [Implementation Remarks](#implementation-remarks)
- [Table of Contents](#table-of-contents)
- [Libraries Used](#libraries-used)
- [Preprocessing Steps](#preprocessing-steps)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Machine Learning Regression Problem](#machine-learning-regression-problem)
  * [Try Majority of Regression models using LazyRegressor](#try-majority-of-regression-models-using-lazyRegressor)
  * [Evaluate four regression models and optimized best model](#evaluate-four-regression-models-and-optimized-best-model)

## Implementation Remarks
This project is implmented on Google Colab, hence all additional packages to installed are documented and installed using shell commands in the [colab project](https://colab.research.google.com/drive/1UWrWKShhioxFjCvmLoFM8qMjxZ5lJMIO?usp=sharing). The dataset is fetched from [ChEMBL](https://www.ebi.ac.uk/chembl/) in 2021 using the `ChEMBL webresource client API` which is regularly updated
hence an image of the dataset is saved for reference.

### Libraries Used
**Data Retrieval API** 
* [ChEMBL webresource client](https://github.com/chembl/chembl_webresource_client) </ul>

**Data Manipulation**
* [Pandas](https://github.com/pandas-dev/pandas)
* [Numpy](https://github.com/numpy/numpy)</ul>

**Data Visualization**
* [Seaborn](https://github.com/mwaskom/seaborn)
* [Matplotlib](https://github.com/matplotlib/matplotlib)</ul>

**Protein Descriptors Computations**
* [RDKit](https://github.com/rdkit/rdkit)
* [PaDEL](https://github.com/dataprofessor/bioinformatics)</ul>


### Preprocessing Steps
**Step 1:** Access the ChEMBL database and filter data, to exctract the data for Alzheimers disease where protein studies is Amyloid beta A4 protein.
<br>**Step 2:** Handling missing , duplicated, and null data
<br>**Step 3:** simply the  simplified molecular input line-entry system (SMILE) notation e.g. disconnections in SMILEs notation
<br>**Step 4:** Transforming attribute types according to the attribute nature
<br>**Step 5:** Discretization of bio-activity to 3 levels: active, intermediate, inactive according to the standard value then eliminate intermediate level rows to focus on active/inactive instances
<br>**Step 6:** Normalize IC50 value by computing pIC50 (negative logarithmic of IC50)
<br>**Step 7:** Generate Padel discriptor using [githuh project](https://github.com/dataprofessor/bioinformatics), from SMILES notation 
<br>**Step 8:** Drop identifier attribute
<br>**Step 9:** Dimension reduction using VarianceThreshold method
<br>**Step 10:** split the data to training and testing with spliting ratio 67% and 33%

### Exploratory Data Analysis
![Alt text](image link)

### Machine Learning Regression Problem
The problem at hand is a regression problem as the input to the regression model is the PaDEL descriptor that represents the footprint/descriptor of a molecule and try to predict the bio-activity value in pIC50 continuous-domain value hence the problem name Quantitative structure Activity relationship(QSAR). First the LazyRegressor library is used to norrow down the top four perfroming regression model then these models are compared to elect the best performing regression model which is further optimized by tuning the hyperparameter values.

#### Try Majority of Regression models using LazyRegressor
The LazyRegressor library runs 40 regression models including Support Vector Machine(SVM), Random Forest (RF), Adaboost regressor, decision tree regressor,and many more. The performance of the regressor models are evaluated according to the R-squared value , Root Mean Square Error (RMSE), and computation time.

#### Evaluate four regression models and optimized best model
The following models are selected four models for regression
1. Random Forest with 80 estimators
2. Gradient Boost with 80 estimators
3. Support Vector Machine with Radial Basis Function (rbf) kernal
4. K Nearest Neighbor with k=10</ul>

where the performance is evaluated according to:
1. Mean Absolute Error (MAE)
2. R squared
3. Computation time</ul>

According to table below the most promising regression is **random forest** thus the followig parameters are optimized in oder to optimize the performance of the model:
- n_estimators = \[100, 300, 500, 800, 1200\]
- max_depth = \[5, 8, 15, 25, 30\] </ul>

In addition Cross Validation is used to accurately evaluate the model's performance with cv = 3
<br>
| **Model**                      	| **R2 Score**     	| **MAE**         	| **Execution Time** 	|
|--------------------------------	|------------------	|-----------------	|--------------------	|
| **Random Forest**              	|    <br>0.7045    	|    <br>0.549    	|    <br>0.0091      	|
| **Gradient Boosted Regressor** 	|    <br>0.692     	|    <br>0.61     	|    <br>0.0015      	|
| **K Nearest Neighbor**         	|    <br>0.68      	|    <br>0.61     	|    <br>0.0016      	|
| **Support Vector Machine**     	|    <br>0.708     	|    <br>0.61     	|    <br>0.0018      	|
| **Optimized Random Forest**    	|    <br>0.928     	|    <br>0.29     	|    <br>0.0702      	|
