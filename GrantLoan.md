# Grant Loan

## Overview
The objective of Grant Loan API is to approve loan and answer various queries regarding the loan application.

![alt text](https://github.com/iSPIRT/OCEN/blob/master/Sequence-Diagram/GrantLoan.PNG "Grant Loan")

## /v3/loan/grantLoanRequest
Requests the lender to grant the loan with given loan application id

### Request Body

|Fields           |Type |Origin|comments|mandatory?|
|---------------- |:---:|:----:|:-------|---------:|
|metadata         |Object|LSP||Y|
|requestId        |String|LSP||Y|
|loanApplicationId|String|LSP|This was sent to the lender through **createLoanApplicationsRequest**|Y|





---
## /v3/loan/grantLoanResponse
![alt text](https://github.com/EzyReach/api-doc/blob/loan-api/grantLoanResponse.PNG "grantLoanResponse Request Body")

```
{
  "metadate": {
    "version": "1.0",
    "timestamp": "2018-12-06T11:39:57.153Z",
    "traceId": "e8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
    "orgId": "FIU123"
  },
  "response": {
    "error": "0"
  },
  "requestId": "e8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
  "loanId": "e8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
  "loanStatus": "GRANTED",
  "terms": {},
  "disbursement": {},
  "repayment": {},
  "actionRequired": [],
  "rejectionDetails": []
}
```

### Request Body

|Fields          |Type |Origin|comments|mandatory?|
|----------------|:---:|:----:|:-------|---------:|
|metadata        |Object|LSP||Y|
|response        |Object|Lender||Y|
|requestId       |String|LSP||Y|
|loanId          |String|LSP||Y|
|loanStatus      |String-enum|Lender|GRANTED, REJECTED, DEFAULTED, COMPLETED, ACTION_REQUIRED|Y|
|terms           |Object||schema: LoanTerms|Y|
|repayment       |Object|Lender|schema: ChosenRepayment|Y|
|disbursement    |Object|...|schema: ChosenDisbursement
|rejectionDetails|List|Lender|FRAUD, DOC_IRREGULARITIES, LOW_CREDIT_SCORE, OTHERS|N|


#### LoanTerms (schema of terms)
```
"terms": {
    "requestedAmount": "50000.00",
    "description": null,
    "currency": "INR",
    "sanctionedAmount": "50000.00",
    "interestType": "FIXED",
    "interestRate": "12",
    "interestAmount": "6000.00",
    "totalAmount": "56000.00",
    "tenure": {
      "duration": "3",
      "unit": "MONTH"
    },
    "legalAgreement": {
      "type": "TEXT",
      "data": "<Base64 Encoded Data>"
    },
    "documents": [],
    "charges": {}
  }
```
|Fields          |Type  |Origin|comments|mandatory?|
|----------------|:----:|:----:|:-------|---------:|
|requestedAmount |float |||Y|
|description     |String|||N|
|currency        |String|||Y|
|sanctionedAmount|float |||N|
|interestType    |String-enum||FIXED, FLOATING|N|
|interestRate    |float|||N|
|interestAmount  |float|||N|
|totalAmount     |float|||N|
|tenure          |Object|||N|
|legalAgreement  |Object|||N|
|documents       |List|||N|
|charges         |Object|||N|
|url             |String|||N|
|extensibleData  |String|||N|

##### LoanTenure
|Field   |Type  |Origin|comments|mandatory?|
|--------|:----:|:----:|:-------|---------:|
|duration|int|||Y|
|unit    |String-enum||DAY, MONTH, YEAR|Y|

##### LegalAgreement
|Fields |Type  |Origin|comments|mandatory?|
|-------|:----:|:----:|:-------|---------:|
|type   |String-enum||TEXT, URL|Y|
|data   |String||Base64 Encoded Data|Y|

##### Charges
```
"charges": {
      "prepayment": {
        "chargeType": "RATE_BASED",
        "data": {
          "rate": "6",
          "amount": null,
          "description": "Description of charge calculation",
          "url": null,
          "applicableParameter": "TOTAL_LOAN_AMOUNT"
        },
        "url": null,
        "extensibleData": null
      },
      "bounce": {
        "chargeType": "FIXED_AMOUNT",
        "data": {
          "rate": null,
          "amount": "3000.00",
          "description": "Description of charge calculation",
          "url": null,
          "applicableParameter": null
        },
        "url": null,
        "extensibleData": null
      },
      "latePayment": {
        "chargeType": "FIXED_AMOUNT",
        "data": {
          "rate": null,
          "amount": "3000.00",
          "description": "Description of charge calculation",
          "url": null,
          "applicableParameter": null
        },
        "url": null,
        "extensibleData": null
      },
      "processing": {
        "chargeType": "FIXED_AMOUNT",
        "data": {
          "rate": null,
          "amount": "3000.00",
          "description": "Description of charge calculation",
          "url": null,
          "applicableParameter": null
        },
        "url": null,
        "extensibleData": null
      }
    }
```
|Field      |Type  |Origin|comments|mandatory?|
|-----------|:----:|:----:|:-------|---------:|
|payment    |Object|||N|
|bounce     |Object|||N|
|latePayment|Object|||N|
|processing |Object|||N|

###### ChargeDetails
|Field         |Type  |Origin|comments|mandatory?|
|--------------|:----:|:----:|:-------|---------:|
|chargeType    |String-enum||FIXED_AMOUNT, RATE_BASED|Y|
|data          |String||schema: ChargeData|Y|
|description   |String|||N|
|url           |String|||N|
|extensibleData|String|||N|

###### ChargeData
|Field              |Type  |Origin|comments|mandatory?|
|-------------------|:----:|:----:|:-------|---------:|
|rate               |float|||N|
|amount             |float|||N|
|description        |String|||N|
|url                |String|||N|
|applicableParameter|String-enum||TOTAL_LOAN_AMOUNT, OUTSTANDING_PAYABLE_AMOUNT, EMI, PREPAYMENT_PRINCIPAL|N|


##### Document
|Fields          |Type |Origin|comments|mandatory?|
|------          |:---:|:----:|:-------|---------:|
|format          |String-enum|User|DOC, IMAGE, CSV, JSON, XML|Y|
|refernece       |String|User||Y|
|source          |String-enum|User||AA, FIP, FIU, FSR, USER, GSTN|Y|
|sourceIdentifier|String|User|example: GSTN|Y|
|type            |String-enum||GSTN_B2B_INVOICE, GSTN_PROFILE, PAN, AADHAAR, DRIVING_LICENSE, PASSPORT, OTHER|Y|
|isDataInline    |boolean|User||Y|
|data            |String|LSP||Base64 encoded String|Y|

#### ChosenRepayment
```
"repayment": {
    "plan": {
      "id": "a8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
      "title": null,
      "shortDescription": null,
      "description": null,
      "paymentUrl": null,
      "automatic": false,
      "scheduleType": "ONE_TIME",
      "payNowAllowed": false,
      "editPlanAllowed": null,
      "changeMethodAllowed": false,
      "frequency": null,
      "noOfInstallments": "1",
      "tenure": null,
      "principal": "9000.00",
      "interestAmount": "1000.00",
      "penalty": "0.00",
      "startDate": null,
      "totalAmount": "10000.00",
      "status": "ACTIVE",
      "url": null,
      "extensibleData": null
    },
    "method": {
      "id": "e8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
      "description": null,
      "type": null,
      "isActive": null,
      "data": null,
      "status": "ACTIVE",
      "url": null,
      "extensibleData": null
    }
  }
```
|Fields          |Type |Origin|comments|mandatory?|
|----------------|:---:|:----:|:-------|---------:|
|plan            |Object||schema: PaymentPlan|Y|


##### PaymentPlan
|Fields             |Type |Origin|comments|mandatory?|
|-------------------|:---:|:----:|:-------|---------:|
|id                 |String|||Y|
|automatic          |boolean|||Y|
|scheduleType       |String-enum||ONE_TIME, RECURRING, AS_PRESENTED|Y|
|noOfInstallments   |int|||Y|
|totalAmount        |float|||Y|
|title              |String|||N|
|shortDescription   |String|||N|
|description        |String|||N|
|paymentUrl         |String|||N|
|payNotAllowed      |boolean|||N|
|editPlanAllpwed    |boolean|||N|
|changeMethodAllowed|boolean|||N|
|frequency          |String-enum||WEEKLY, MONTHLY, QUARTERLY, HALF_YEARLY, YEARLY|N|
|tenure             |Object|||N|
|principal          |float|||N|
|interestAmount     |float|||N|
|penalty            |float|||N|
|startDate          |DateTime|||N|
|status             |String-enum||ACTIVE, INACTIVE, PENDING_AUTH|N|
|url                |String|||N|
|extensibleData     |String|||N|

#### ChosenDisbursement
```
"disbursement": {
    "plan": {
      "id": "hb8c6822bd4bbb4eb1b9e1b4996fbff8acb",
      "title": null,
      "shortDescription": null,
      "description": null,
      "paymentUrl": null,
      "automatic": false,
      "payNowAllowed": null,
      "editPlanAllowed": null,
      "changeMethodAllowed": null,
      "scheduleType": "ONE_TIME",
      "frequency": null,
      "noOfInstallments": "1",
      "tenure": null,
      "principal": null,
      "interestAmount": null,
      "penalty": null,
      "startDate": null,
      "totalAmount": "10000.00",
      "status": "ACTIVE",
      "url": null,
      "extensibleData": null
    },
    "accountDetails": {}
  }
```
|Fields          |Type |Origin|comments|mandatory?|
|----------------|:---:|:----:|:-------|---------:|
|plans           |List<Object> ||schema: paymentPlan|Y|
|accountDetails  |List<Object> |||Y|


##### AccountDetails
```
"accountDetails": {
      "id": null,
      "description": null,
      "status": null,
      "accountDataType": "ACCOUNT",
      "data": {
        "accountType": "CURRENT",
        "accountIFSC": null,
        "accountNumber": null,
        "vpa": null,
        "maskedAccountNumber": "XXXXXXXXX9090"
      },
      "url": null,
      "extensibleData": null
    }
```
|Fields         |Type |Origin|comments|mandatory?|
|---------------|:---:|:----:|:-------|---------:|
|id             |String|||N|
|description    |String|||N|
|status         |String-enum||ACTIVE, INACTIVE|N|
|accountDataType|String-enum||ACCOUNT, VPA|Y|
|data           |Object||schema: AccountDetailsData|Y|
|url            |String|||N|
|extensibleData |String|||N|

###### AccountDetailsData (schema of data)
|Fields             |Type |Origin|comments|mandatory?|
|-------------------|:---:|:----:|:-------|---------:|
|accountType        |String-enum||SAVINGS, CURRENT, OVERDRAFT|N|
|accountIFSC        |String|||N|
|accountNumber      |String|||N|
|vpa                |String||virtual payment address|N|
|maskedAccountNumber|String||eg. XXXXXXXXX9090|N|


#### RejectionDetail
|Fields        |Type |Origin|comments|mandatory?|
|--------------|:---:|:----:|:-------|---------:|
|reason        |String-enum|Lender|FRAUD, DOC_IRREGULARITIES, LOW_CREDIT_SCORE, OTHERS|Y|
|description   |String|Lender|eg. Credit score below 600|Y|
|url           |String|Lender||N|
|extensibleData|String|Lender||N|


#### ActionRequired
|Fields     |Type |Origin|comments|mandatory?|
|-----------|:---:|:----:|:-------|---------:|
|actionType |String-enum|Lender|ADDDOCUMENT, RESUBMITDOCUMENT, OTHER|Y|
|description|String|Lender|eg. DL number not visible|Y|
|reference  |Object|Lender||N|


##### Reference
|Field |Type |Origin|comments|mandatory?|
|------|:---:|:----:|:-------|---------:|
|object|String|||Y|
|value |String|||Y|


---
## /v3/loan/loanSummaryRequest
Requests the lender to fetch the summary of a loan with given loan id

### Request Body
|Fields          |Type |Origin|comments|mandatory?|
|----------------|:---:|:----:|:-------|---------:|
|metadata        |Object|LSP||Y|
|loanId          |String|LSP||Y|
|requestId       |String|LSP||Y|





---
## /v3/loan/loanSummaryResponse
Fetches the summary of a loan with given loan id

```
{
  "metadata": {
    "version": "1.0",
    "timestamp": "2018-12-06T11:39:57.153Z",
    "traceId": "e8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
    "orgId": "LSP123"
  },
  "response": {
    "error": "0"
  },
  "requestId": "e8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
  "loanId": "e8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
  "loanStatus": "GRANTED",
  "createdDate": "2019-12-30T13:55:00Z",
  "startDate": "2019-12-30T00:00:00Z",
  "endDate": "2020-03-01T00:00:00Z",
  "summary": {}
}
```
### Request Body

|Fields          |Type |Origin|comments|mandatory?|
|----------------|:---:|:----:|:-------|---------:|
|metadata        |Object|LSP||Y|
|response        |Object|Lender||Y|
|requestId       |String|LSP||Y|
|loanId          |String|LSP||Y|
|loanStatus      |String-enum|Lender|GRANTED, DEFAULTED, COMPLETED, OVERDUE|Y|
|createDate      |DateTime|||Y|
|startDate       |DateTime|||Y|
|endDate         |String|LSP||Y|
|summary         |Object|||Y|


#### Summary
```
"summary": {
    "nextRepayment": {},
    "currentRepayment": {},
    "principalPaid": "10000.00",
    "interestPaid": "100.00",
    "penaltyPaid": "10.00",
    "principalPending": "10000.00",
    "interestPending": "100.00",
    "amountDisbursed": "1000.00",
    "amountRepaid": "1000.00",
    "tenure": {
      "duration": "3",
      "unit": "MONTH"
    },
    "description": "short description for the loan"
  }
```
|Fields          |Type |Origin|comments|mandatory?|
|----------------|:---:|:----:|:-------|---------:|
|nextPayment     |Object||schema: Payment|Y|
|currentPayment  |Object||schema: Payment|Y|
|principalPaid   |float|||Y|
|interestPaid    |float|||Y|
|penaltyPaid     |float|||Y|
|principalPending|float|||Y|
|interestPending |float|||Y|
|amountDisbursed |float|||Y|
|amountRepaid    |float|||Y|
|tenure          |Object||schema: LoanTenure|Y|
|description     |String|||Y|

##### Payment (schema for nextPayment and currentPayment)
```
"currentRepayment": {
      "id": "ws4c6822bd4bbb4eb1b9e1b4996fbff8wed",
      "description": null,
      "status": "SUCCESS",
      "useSavedPaymentOption": null,
      "paymentMethodType": null,
      "paymentUrl": null,
      "txnRefNo": null,
      "url": null,
      "extensibleData": null,
      "totalAmount": "5000.00",
      "principal": "4000.00",
      "interestAmount": "1000.00",
      "penalty": "0.00",
      "fee": "0.00",
      "date": "2020-10-10",
      "installmentNumber": "1"
    }
```
|Fields               |Type |Origin|comments|mandatory?|
|---------------------|:---:|:----:|:-------|---------:|
|id                   |String|||Y|
|description          |String|||N|
|date                 |DateTime|||N|
|principal            |float|||N|
|interestAmount       |float|||N|
|fee                  |float|||N|
|penalty              |float|||N|
|totalAmount          |float|||N|
|intallmentAmount     |float|||N|
|status               |String-enum||SUCCESS, FAILURE, PENDING_AUTH|N|
|useSavedPaymentOption|boolean|||N|
|paymentMethodType    |String-enum||EMANDATE_UPI, NETBANKING, UPI, ENACH, DEBIT_CARD|N|
|paymentUrl           |String|||N|
|txnRefNo             |String|||N|
|url                  |String|||N|
|extensibleData       |String|||N|


##### LoanTenure
|Field   |Type  |Origin|comments|mandatory?|
|--------|:----:|:----:|:-------|---------:|
|duration|int|||Y|
|unit    |String-enum||DAY, MONTH, YEAR|Y|

---
## /v3/loan/getLoanRequest
Requests the lender to fetch the details of loan with given loan id

### Request Body
|Fields          |Type |Origin|comments|mandatory?|
|----------------|:---:|:----:|:-------|---------:|
|metadata        |Object|LSP|||
|loanId          |String|LSP|||
|requestId       |String|LSP|||






---
## /v3/loan/getLoanResponse
Fetches the details of loan with given loan id

### Request Body
|Fields          |Type |Origin|comments|mandatory?|
|----------------|:---:|:----:|:-------|---------:|
|metadata        |Object|LSP||Y|
|response        |Object|Lender||Y|
|requestId       |String|LSP||Y|
|loanId          |String|||Y|
|loanStatus      |String-enum||GRANTED, DEFAULTED, COMPLETED, OVERDUE|Y|
|createDate      |DateTime|||Y|
|startDate       |DateTime|||Y|
|endDate         |String|LSP||Y|
|type            |String-enum||CASHFLOW, PERSONAL, HOME, VEHICLE, BUSINESS|Y|
|lender          |Object|||Y|
|collateral      |List|||Y|
|guarantors      |List|||Y|
|applicants      |List|||Y|
|terms           |Object|||Y|
|disbursement    |Object|||Y|
|repayment       |Object|||Y|





---
## /v3/loan/loanStatementRequest
Requests the lender to fetch transactions for given loan between given dates

### Request Body

|Fields          |Type |Origin|comments|mandatory?|
|----------------|:---:|:----:|:-------|---------:|
|metadata        |Object|LSP||Y|
|loanId          |String|||Y|
|requestId       |String|LSP||Y|
|startDate       |DateTime|LSP||N|
|endDate         |DateTime|LSP||N|




---
## /v3/loan/loanStatementResponse
Fetches the transactions for given loan

### Request Body

|Fields          |Type |Origin|comments|mandatory?|
|----------------|:---:|:----:|:-------|---------:|
|metadata        |Object|LSP||Y|
|loanId          |String|LSP||N|
|requestId       |String|LSP||Y|
|response        |Object|Lender||Y|
|accountStatement|Object|Lender|schema: Transaction|Y|

#### Transaction (Schema for accountStatement)

```
"accountStatement": {
    "date": "2020-03-01T00:00:00Z",
    "narration": "Repayment of Loan no : xxxxxxx9090",
    "txnRefNo": "004618602124",
    "amount": "50000.00",
    "type": "DEPOSIT",
    "closingBalance": "50000.00",
    "url": null,
    "extensibleData": null
  }
 ```

|Fields          |Type |Origin|comments|mandatory?|
|----------------|:---:|:----:|:-------|---------:|
|date            |DateTime|||Y|
|narration       |String||Details of the transaction|Y|
|txnRefNo        |String|||Y|
|amount          |float|||Y|
|type            |String-enum||DEPOSIT,WITHDRAWAL|Y|
|closingBalance  |float|||Y|
|url             |String|||N|
|extensibleData  |String|||N|


---
## /v3/loan/listLoansRequest
Requests the lender to fetch all loans raised for the given borrower between given dates

### Request Body
|Fields          |Type |Origin|comments|mandatory?|
|----------------|:---:|:----:|:-------|---------:|
|metadata        |Object|LSP||Y|
|borrower        |Object|LSP||Y|
|requestId       |String|LSP||Y|
|collateral      |Object|LSP||N|
|startDate       |DateTime|LSP||N|
|endDate         |DateTime|LSP||N|




---
## /v3/loan/listLoansResponse
Fetches the list of all loans on for the given borrower

### Request Body

|Fields          |Type |Origin|comments|mandatory?|
|----------------|:---:|:----:|:-------|---------:|
|metadata        |Object|LSP||Y|
|response        |Object|Lender||Y|
|requestId       |String|LSP||Y|
|loans           |List|Lender|Schema: loanDetail|Y|

### loanDetail
|Fields          |Type |Origin|comments|mandatory?|
|----------------|:---:|:----:|:-------|---------:|
|loanId          |String|||Y|
|terms           |Object||schema: LoanTerms|Y|