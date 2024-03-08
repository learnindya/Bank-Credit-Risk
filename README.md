# Bank-Credit-Risk
Determine credit risk category of bank customers: Good or Bad.

## Problem
You are hired as a data scientist intern in a project from a lending company. You are asked to build a model that can predict credit risk using a dataset from the company which comprises list of credits that are accepted and rejected.

## Goal
Determine credit risk category of bank customers.
0: Good risk
1: Bad risk

## Defining Label
The label can be defined from column 'loan_status'.
We define a "bad" borrower as a member that meets one of the following 'loan_status': 
- Charged Off
- Late (31-120 days)
- Default
- Does not meet the credit policy. Status:Charged Off

## Data Pre-processing
### Drop columns

More than 70% missing values: mths_since_last_record, mths_since_last_major_derog, annual_inc_joint, dti_joint, verification_status_joint, open_acc_6m, open_il_6m, open_il_12m, open_il_24m, mths_since_rcnt_il, total_bal_il, il_util, open_rv_12m, open_rv_24m, max_bal_bc, all_util, inq_fi, total_cu_tl, inq_last_12m, mths_since_last_delinq.

Identifiers: Unnamed: 0, member id, url, title, desc, zip_code, emp_title, addr_state, and policy_code.

Drop sub_grad as it is similar as the grade column.

Drop dti_joint because it is similar to dti.

Drop out_prncp_inv because it is similar to out_prncp.

Drop total_pymnt_inv because it is similar to total_pymnt.

Drop funded_amnt_inv because it is similar to funded_amnt

Drop features that contain information about the outcome: next_pymnt, recoveries.

Drop application_type because only 1 unique value.

Columns that are not relevant to predicting bad borrowers: collection_recovery_fee, pymnt_plan (there is no description for this column)

### emp_length
Change to numerical data type.

### term
Change to numerical data type.

### Handle missing values
- impute emp_length with 0
- impute 'earliest_cr_line' with mode
- impute 'last_pymnt_d'  with mode
- impute 'last_credit_pull_d' with mode
- impute 'annual_inc' with median
- impute 'delinq_2yrs' with 0
- impute 'inq_last_6mths' with 0
- impute 'open_acc' with 0
- impute 'pub_rec' with 0
- impute 'revol_util' with 0
- impute 'total_acc' with 0
- impute 'collections_12_mths_ex_med' with 0
- impute 'acc_now_delinq' with 0
- impute 'tot_coll_amt' with 0
- impute 'tot_cur_bal' with 0
- impute 'total_rev_hi_lim' with 0

### Convert date to duration
- change data type 'issue_d' from object to datetime then to duration
- change data type 'earliest_cr_line' from object to datetime then to duration
- change data type 'last_pymnt_d' from object to datetime then to duration
- change data type 'last_credit_pull_d' from object to datetime then to duration

## Feature Selection
- Check correlation
- Drop 'installment', 'total_rec_prncp', 'last_pymnt_d', 'revol_bal' due to multicollinearity

## Feature Encoding
- Purpose
- Grade
- Home_ownership
- Verification_status
- List_status

## Imbalance Resampling
- SMOTE

## Result
LogisticRegression()
AUC (Train): 0.9855
AUC (Test): 0.9714
KS (Train): 0.9004
KS (Test): 0.8474

DecisionTreeClassifier()
AUC (Train): 1.0000
AUC (Test): 0.9309
KS (Train): 1.0000
KS (Test): 0.8618

RandomForestClassifier()
AUC (Train): 1.0000
AUC (Test): 0.9814
KS (Train): 1.0000
KS (Test): 0.8750

## Summary
The best fit model uses Random Forest algorithm and results in AUC = 0.98 dan KS = 0.87.
