# AWS Cost Estimation

For first year, the target is 50 Loan Applications per day, ie. 1500 applications/month and onboarding 750 clients. The following calculations are based on this assumption.

>Note: The following rates are for Asia Pacific (Mumbai) region. Rates may differ for other regions. 

|AWS Tech Stack   |Rate                                          |Estimated Usage                 |Estimated Cost|
|-----------------|:---------------------------------------------|:-------------------------------|-------------:|
|RDS (PostgreSQL) |$0.262 per GB-month for multi Zone SSD storage|||
|SNS              |First 1 million request free, $ 0.5/million req, req size=64kb, SMS cost: $0.00278 per SMS||Nil|    
|SQS              |First 1 million request free, $ 0.5/million req, req size=64kb||Nil|
|S3               |$0.025/GB for first 50 TB/month|||
|AWS Managed Encryption Keys|$0.03 per 10,000 requests|||
|EC2              |$20.59 for reserved t3.medium instance/month|||
|AWS Cognito      |$0.015/Active User|||
|API Gateway      |$1.05/million req for first 300 million req, req size=512kb||$0.0004/month|
|EKS              |$0.10 per hour for each Amazon EKS|||
|AWS WAF - ALB    ||||
|AWS Cloud Front  ||||
|AWS Lambda       ||||

## 1. EC2
Price for EC2 instances varies a lot depending upon the type of instance.
There are following types of instances available:

* On-Demand: No long term commitment needed

* Spot Instances:

* Savings Plan:

* Reserved Instances: t3.medium (vCPU: 2, Memory: 4GiB)

* Dedicated hosts:




## 2. RDS (PostgreSQL)
There are following kinds of RDS storage available and every kind has option of single or multi AZ deployment:

* On-Demand DB instances: They are used for applications with no long term commitments.

* Reserved instaces: The price depends on the type of instance. 
For Multi zone db.t3.large (Memory: 8 GiB, vCPU: 2) reserved for 1 year, the cost is $0.329 per Hour, ie $237 per Month.
For Multi zone db.r6g.8xlarge (Memory: 256 GiB, vCPU: 32) reserved for 1 year, the cost is $5.5966  per Hour, ie $4030 per Month.

* Database Storage: For general purpose Multi AZ SSD storage, the price is $0.262 per GB-month.

* Backup Storage: Backup storage is the storage associated with your automated database backups. Backup storage is billed at $0.095 per GiB-month




## 3. API Gateway
It takes 32 API requests for one happy user journey (from Sign Up to loan disbursement).

The sizes of a few request payload have been checked as follows
```
obj = {
	"orgId": "LSP123"
};

const size = new TextEncoder().encode(JSON.stringify(obj)).length;
const kiloBytes = size / 1024;

console.log(kiloBytes);
```
CreateLoanApplicationRequest size = 4kb, GeneraateOfferResponse size = 2kb, SetRepaymentPlanResponse size = 0.7kb

Assuming the average request sizes to be 8kb, one user journey would effectively be 32×8/512 = 0.5 request

Assuming 1500 loan applications per month, the estimated cost is 0.5 req × 750 / 1,000,000 × $1.05 = $0.0004/month



## 4. Amazon Cognito:
Pricing is based on monthly active users (MAU).
For users who sign in through SAML or OIDC federation, the price for MAUs above the 50 MAU free tier is $0.015/MAU. First 50 MAUs are free.
There
There are additional charges for Advanced Security Features.



## 5. AWS Key Management Service (KMS):
API request to the AWS Key Management Service is as follows:
* First 20,000 req/month - Free
* $0.03 per 10,000 requests

Key Storage price: $1/month for each custom master key (CMK)