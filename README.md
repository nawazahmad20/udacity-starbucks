# Starbucks Capstone Challenge
Project in Data Scientist Nanodegree of Udacity

### Table of Contents

1. [Domain Background](#domain_background)
2. [Problem Statement](#problem_statement)
3. [Datasets and Inputs](#inputs)
4. [Solution Statement / Project Design](#solution)
5. [Benchmark Model](#benchmark)
6. [Evaluation Metrics](#evaluation)

## Domain Background <a name="domain_background"></a>

In general terms, the problem is to boost the sales of a company by providing offers to the customers. There are multiple answers that have to be answered using data science to fully understand the impact of the offers on the sale. Some of them are listed below:-
1.	Identify whether to provide offer to a customer- This is relevant because if you provide offer to customers who were anyways going to purchase the product, we would end up decreasing the overall profit margin. On the other hand, if we miss out on targeting the customers that would have purchased had we given them the offer, we would miss out on sales and in long term may end up losing customers as well to a rival brands.
2.	Identify which offer is to suitable to which customer- Once we are sure that an offer is to be given to a customer, we must find out which offer is better suitable or eye catching to a customer. As it is well known that BOGO and 50% discount, although having same monetary value can sometimes have different impact on sales. 
3.	Identify the overall impact of the offers – It is very necessary to calculate the actual impact of the offers on the sales and in turn identify whether giving offers make sense to the business. In order to calculate the actual boost in sales, we should not only look at the sales for the weeks where the offer was active, but we should also have a look at the subsequent weeks to understand the stocking and competitor effect. This may not be relevant to the Starbucks problem we are solving, but can have serious implications for other similar problems

## Problem Statement <a name="problem_statement"></a>
After having a look at the Starbucks dataset, it is not very clear if the offers were given as a reward to loyal customers or to reengage customers who have gone dormant. I am assuming it is latter instead of the former, as this can change the way problem is to be approached. As mentioned above there can be multiple use cases built out of this particular dataset, however, I would like to focus on the first use case mentioned above. The objective is to analyze customer demographic and transactional data to find out if the customer made purchase because of the offer or he was anyways going to purchase the items. This in turn will help us decide whether to give offer to a customer. 

## Datasets and Inputs <a name="inputs"></a>

The notebook available here showcases work related to the above questions.  

This data set is a simplified version of the real Starbucks app because the underlying simulator only has one product whereas Starbucks actually sells dozens of products.

The data is contained in three files:
- `portfolio.json` - containing offer ids and meta data about each offer (duration, type, etc.)
- `profile.json` - demographic data for each customer
- `transcript.json` - records for transactions, offers received, offers viewed, and offers completed

Here is the schema and explanation of each variable in the files:

`portfolio.json`
- id (string) - offer id
- offer_type (string) - the type of offer ie BOGO, discount, informational
- difficulty (int) - the minimum required to spend to complete an offer
- reward (int) - the reward is given for completing an offer
- duration (int) - time for the offer to be open, in days
- channels (list of strings)

`profile.json`
- age (int) - age of the customer
- became_member_on (int) - the date when customer created an app account
- gender (str) - gender of the customer (note some entries contain 'O' for other rather than M or F)
- id (str) - customer id
- income (float) - customer's income

`transcript.json`
- event (str) - record description (ie transaction, offer received, offer viewed, etc.)
- person (str) - customer id
- time (int) - time in hours since the start of the test. The data begins at time t=0
- value - (dict of strings) - either an offer id or transaction amount depending on the record


## Solution Statement / Project Design<a name="solution"></a>

TIn order to find out if the customer:-
1.	We are going to focus only on the customers that were provided with offer and also availed the offer. 
2.	The customers who availed the offer but didn’t viewed the offer would be considered as the customers to whom offer should not have been given. This is because their purchasing behavior was not influenced by the offer. 
3.	The customers who availed the offer and also viewed the offer would be considered as the customers to whom offer should have been given. Note that I am assuming here that the reason of transaction for these customers is offer and they would not have made the purchase had the offer not given. 
4.	For each of the customers, demographic information is directly available. We would have to process the transaction data to get the information related to whether the offer availed was viewed or not. We would also make features like amount of transaction done in past week/2weeks, no. of time transaction done etc. The transactional data is available only for month and not sure how much information we will be able to extract out of this. 
5.	We will build a classification model to predict whether the customer belongs to category “no offer to be given” or category “offer to be given”. Also in order to do the prediction, we will use transaction data of at least 1 week back. The reason to set up the problem in this way is so that can we get some insights based on the transactional data of the customer along with demographic data to predict that given customer does a transaction, whether it would be because of the offer or he would anyways make the transaction. This will help us identify the customers to whom offer should be given. And since we are using transaction data of at least one week back, we can appropriately tag whether to give offer to the customers for the next week. 

## Benchmark Model<a name="benchmark"></a>
- 

## Evaluation Metrics<a name="evaluation"></a>
We will split the dataset in train and test set, and evaluate the performance of the model on test set. We will use accuracy, auc-roc and precision and recall scores to evaluate the performance of the model. Precision and recall scores are particularly important as it will give us an idea as to how many customers who deserve the offer but were not 
