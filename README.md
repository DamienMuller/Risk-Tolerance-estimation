# From a subjective to a (more) objective approach to assessing investment risk tolerance
<br> 

## TLDR
---
- Objective: Predict proportion of risky assets in portfolio using investor characteristics to approximate client risk tolerance.
- Decision Tree shows highest accuracy score on both raw and transformed data sets to predict risky portfolio share.
- High accuracy of over 99% shows that demographic and financial variables are useful to predict portfolio risk distribution of investors. 
- Risk tolerance then relies on more objective characteristics (demographics and financial situation) which might be advisable to consider in suitability assessments. 

## Project objective
---
The objective of this project is to propose a more objective way to assess investment risk tolerance that is less prone to human biases (e.g. overestimate risk willingness). The approach consists in using regression algorithms that learn the relationship between investor characteristics and the portfolio proportion invested in risky assets. Accordingly, the resulting asset allocation is less dependent on the investor's preferences and relies more on what is adopted by the majority of similar market participants.  

## Rationale
---
In investment management, financial advisors rely on risk-assessment questionnaires that are filled out by clients to identify their risk profile as well as the corresponding investment vehicles that may be selected. However, research has identified several shortcomings when it comes to such questionnaires. In fact, risk tolerance tests show inconsistencies over time, meaning that one individual's risk score changes over a short period of time (Grable, 2020). Second, there are also inconsistencies in test scores among risk-assessment questionnaires, which makes the choice of the retained score highly subjective (Yook & Everett, 2003). Last, individuals tend to overestimate their risk appetite, which leads to a riskier investment portfolio than appropriate (Lucarelli, et al., 2015). It is therefore of interest to find a more objective method to assist investment managers in the asset allocation process. 

## Project overview
---

| | |
|-|-|
|**Predictive problem**| Regression analysis |
|**Data**| Input and output variables retrieved from the US Survey of Consumer Finances conducted by the Federal Reserve in 2019. The dataset contains 28496 observations of investor characteristics and related portfolio compositions. |
|**Output variable**| $\mbox{Risk Tolerance} = \frac{\mbox{Value of risky investments}}{\mbox{Value of risky investments + risk-low investments}}$ <br><br> Risky investment = Stocks + corporate bonds + foreign bonds <br> Risk-low investments = Transaction accounts (checking + saving) + Certificates of deposit + US government bonds | 
|**Input variables**| Demographic variables <br><br> *AGE = Age of respondent* <br> *EDCL = Latest diploma received* <br> *MARRIED = Martial status* <br> *OCCAT1 = Employment status* <br><br> Financial variables <br><br> *INCOME = Yearly income (in $)* <br> *Invest_goal = Investment goal* <br> *NET WORTH = Assets - Liabilities* <br> *LIQ = Holdings in transaction accounts* <br> *CDS = Certificates of deposit investments* <br> *GOVTBND = US government bond holdings* <br> *EQUITY = Stocks and mutual fund investment values* | 
|**Data split**| Training set (80%): Perform cross-validation and select best model. <br> Validation set (20%): Verify consistency of best predictor. |
|**Learning process**| Models are trained and tested with 10-fold cross validation. |
|**Model evaluation**| Average R-squared|
|**Algorithms**| Linear regression <br> Lasso regression <br> Elastic net regularization <br> KNN <br> Decision Tree <br> Support Vector Machine |
|**Model variations**| <ol> <li> Baseline: Only necessary data transformations (one-hot encoding). <li> Data transformation: Standardize numerical variables and reduce skewness (Yeo-Johnson transform).|
|**Final model**| The combination of machine learning algorithm and data transform that provides the highest prediction accuracy in the training set while ensuring consistency in the test set will be selected.|
<br>
    
## Results
---




| | |R-squared | % Performance Change |
|---|---|:---:|:---:|
|**Linear regression**| Baseline | 0.19 | 
| | Transform | 0.95 | <font color="green">400%|
|**Lasso regression**| Baseline | 0.06 | 
| | Transform | 0.72 | <font color="green">1100%|
|**Elastic net**| Baseline | 0.10 | 
| | Transform | 0.68 | <font color="green">580%|
|**KNN**| Baseline | 0.87 | 
| | Transform | 0.93 |  <font color="green">6.9%|
|**Decision Tree**| Baseline | <font color="green">0.997 | 
| | Transform | <font color="green">0.997 | 0% |
|**SVM**| Baseline | 0.21 | 
| | Transform | <font color="green">0.989 | <font color="green">371%|
<br>

## Key Findings
---

<ul>
    <li> As shown by exploratory analysis, there is no strong linear relationship between input and output variables in raw dataset. Thus, decision tree largely outperformed linear models. 
    <li> All models benefit from data transformation, except for decision tree (expected as invariant to data scale and distribution). 
    <li> Decision tree remains best predictor after data transformation, but SVM and linear regression become competitive predictors. 
    <li> Decision tree performance confirmed by validation set (0.998% accuracy).
    <li> High accuracy scores show that demographic and financial investor characteristics are useful to predict portfolio risk distribution. Risk tolerance would then primarily rely on the overall market (similar investors with similar risk appetite).  
