# Dataset

## 1. Business Problem
- Thera Bank ran a campaign last year, where the manager aim to convert liability customers to personal loan cusstomers wwhile retaining them as depositors. 
- The campaing ressulted in a 9% conversion rate. This motivated Retail Marketing Department to come up with a better target marketing to increase the success ratio. 
As a DS, the goal is to build a model that will help the marketing department to pinpoint potential clients who have higher probability of purchasing the loan. 

## 2. Dataset Overview
- The data set consists of 5.000 rows & 14 columns, identified by the following questions: 


## 3. Features
- ID: Customer ID
- Age: Customer’s age in completed years
Experience: #years of professional experience
Income: Annual income of the customer (in thousand dollars)
ZIP Code: Home Address ZIP code.
Family: the Family size of the customer
CCAvg: Average spending on credit cards per month (in thousand dollars)
Education: Education Level. 1: Undergrad; 2: Graduate;3: Advanced/Professional
Mortgage: Value of house mortgage if any. (in thousand dollars)
Personal_Loan: Did this customer accept the personal loan offered in the last campaign?
Securities_Account: Does the customer have securities account with the bank?
CD_Account: Does the customer have a certificate of deposit (CD) account with the bank?
Online: Do customers use internet banking facilities?
CreditCard: Does the customer use a credit card issued by any other Bank (excluding All life Bank)?


## 4. Target Variable
Target Varriable here is Personal_Loan, with 2 classes: 
- 0: Customer does not accept the loan. (N) 
- 1: Client accept the loan. (Y) 

## 5. Questions I Need to Understand
As the output is assessed by catergorical oucome (Y/N), it identified the given problem as a binary classification matter. Potentially relevant features include Income, Education, CCAvg, Family, Mortgage, Age, and account-related variables. Their relationships with loan acceptance will be explored during EDA.
