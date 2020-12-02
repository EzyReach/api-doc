# Grant Loan

## Overview
The objective of Grant Loan API is to approve loan and answer various queries regarding the loan application.

![alt text](https://github.com/iSPIRT/OCEN/blob/master/Sequence-Diagram/GrantLoan.PNG "Grant Loan")

## /v3/loan/grantLoanRequest

### Request Body

|Fields           |Type |Origin|comments|mandatory?|
|---------------- |:---:|:----:|:-------|---------:|
|metadata         |Object|LSP||Y|
|requestId        |String|LSP||Y|
|loanApplicationId|String|LSP|This was sent to the lender through **createLoanApplicationsRequest**|Y|





---
## /v3/loan/grantLoanResponse

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
|repayment       |Object|Lender||Y|
|disbursement    |Object|...||Y|
|actionRequired  |List|Lender||N|
|rejectionDetails|List|Lender||N|


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
  }
```
|Fields          |Type |Origin|comments|mandatory?|
|----------------|:---:|:----:|:-------|---------:|
|requestedAmount |float|||Y|
|description     |String|||N|
|currency        |String|||Y|
|sanctionedAmount|float|||N|
|interestType    |String-enum|||N|
|interestRate    |float|||N|
|interestAmount  |float|||N|
|totalAmount     |float|||N|
|tenure          |Object|||N|
|legalAgreement  |Object|||N|
|documents       |List|||N|
|charges         |Object|||N|
|url             |String|||N|
|extensibleData  |String|||N|



#### repayment
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

#### disbursement
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
  }
```
|Fields          |Type |Origin|comments|mandatory?|
|----------------|:---:|:----:|:-------|---------:|
|plans           |List ||schema: paymentPlan|Y|
|accountDetails  |List |||Y|


##### accountDetails
|Fields         |Type |Origin|comments|mandatory?|
|---------------|:---:|:----:|:-------|---------:|
|id             |String|||N|
|description    |String|||N|
|status         |String-enum||ACTIVE, INACTIVE|N|
|accountDataType|String-enum||ACCOUNT, VPA|N|
|data           |Object||schema: AccountDetailsData|Y|
|url            |String|||N|
|extensibleData |String|||N|

###### AccountDetailsData (schema of data)
|Fields             |Type |Origin|comments|mandatory?|
|-------------------|:---:|:----:|:-------|---------:|
|accountType        |String-enum||SAVINGS, CURRENT, OVERDRAFT|N|
|accountIFSC        |String|||N|
|accountNumber      |String|||N|
|vpa                |String|||N|
|maskedAccountNumber|String||eg. XXXXXXXXX9090|N|


---
## /v3/loan/loanSummaryRequest
### Request Body

|Fields          |Type |Origin|comments|mandatory?|
|----------------|:---:|:----:|:-------|---------:|
|metadata        |Object|LSP|||
|loanId          |String|LSP|||
|requestId       |String|LSP|||





---
## /v3/loan/loanSummaryResponse

### Request Body

|Fields          |Type |Origin|comments|mandatory?|
|----------------|:---:|:----:|:-------|---------:|
|metadata        |Object|LSP|||
|response        |Object|Lender|||
|requestId       |String|LSP|||
|loanId          |String||||
|loanStatus      |String-enum||||
|createDate      |DateTime||||
|startDate       |DateTime||||
|endDate         |String|LSP|||
|summary         |String||||





---
## /v3/loan/getLoanRequest
### Request Body

|Fields          |Type |Origin|comments|mandatory?|
|----------------|:---:|:----:|:-------|---------:|
|metadata        |Object|LSP|||
|loanId          |String|LSP|||
|requestId       |String|LSP|||






---
## /v3/loan/getLoanResponse

### Request Body

|Fields          |Type |Origin|comments|mandatory?|
|----------------|:---:|:----:|:-------|---------:|
|metadata        |Object|LSP|||
|response        |Object|Lender|||
|requestId       |String|LSP|||
|loanId          |String||||
|loanStatus      |String-enum||||
|createDate      |DateTime||||
|startDate       |DateTime||||
|endDate         |String|LSP|||
|type            |String-enum||CASHFLOW, PERSONAL, HOME, VEHICLE, BUSINESS||
|lender          |Object||||
|collateral      |List||||
|guarantors      |List||||
|applicants      |List||||
|terms           |Object||||
|disbursement    |Object||||
|repayment       |Object||||





---
## /v3/loan/loanStatementRequest

### Request Body

|Fields          |Type |Origin|comments|mandatory?|
|----------------|:---:|:----:|:-------|---------:|
|metadata        |Object|LSP|||
|loanId          |String||||
|requestId       |String|LSP|||





---
## /v3/loan/loanStatementResponse

### Request Body

|Fields          |Type |Origin|comments|mandatory?|
|----------------|:---:|:----:|:-------|---------:|
|metadata        |Object|LSP|||
|loanId          |String|LSP|||
|requestId       |String|LSP|||
|response        |Object|Lender|||
|accountStatement|Object|Lender|schema: Transaction||

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
|date            |DateTime||||
|narration       |String||Details of the transaction||
|txnRefNo        |String||||
|amount          |float||||
|type            |String-enum||DEPOSIT,WITHDRAWAL||
|closingBalance  |float||||


---
## /v3/loan/listLoansRequest

### Request Body

|Fields          |Type |Origin|comments|mandatory?|
|----------------|:---:|:----:|:-------|---------:|
|metadata        |Object|LSP|||
|borrower        |Object|LSP|||
|requestId       |String|LSP|||






---
## /v3/loan/listLoansResponse

### Request Body

|Fields          |Type |Origin|comments|mandatory?|
|----------------|:---:|:----:|:-------|---------:|
|metadata        |Object|LSP||Y|
|response        |Object|Lender||Y|
|requestId       |String|LSP||Y|
|loans           |List||Schema: loanDetail||

### loanDetail
|Fields          |Type |Origin|comments|mandatory?|
|----------------|:---:|:----:|:-------|---------:|
|loanId          |String|||
|terms           |Object|||