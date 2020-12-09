# Disbursement

## Overview

## /v3/disbursement/setDisbursementPlanRequest
```
{
  "metadata": {
    "version": "1.0",
    "timestamp": "2018-12-06T11:39:57.153Z",
    "traceId": "e8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
    "orgId": "LSP123"
  },
  "requestId": "e8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
  "loanApplicationId": "e8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
  "loanId": null,
  "plan": {}
}
```
|Fields           |Type |Origin|comments|mandatory?|
|-----------------|:---:|:----:|:------:|---------:|
|metadata         |Object|LSP||Y|
|requestId        |String|LSP||Y|
|loanApplicationId|String|LSP||Y|
|loanId           |String|LSP||N|
|plan             |Object||schema: PaymentPlan|Y|


### PaymentPlan
```
"plan": {
    "id": "e8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
    "title": null,
    "shortDescription": null,
    "description": null,
    "paymentUrl": null,
    "automatic": "false",
    "payNowAllowed": null,
    "editPlanAllowed": null,
    "changeMethodAllowed": null,
    "scheduleType": "ONE_TIME",
    "frequency": null,
    "noOfInstallments": "1",
    "tenure": {
      "duration": null,
      "unit": null
    },
    "principal": null,
    "interestAmount": null,
    "penalty": null,
    "startDate": null,
    "status": null,
    "totalAmount": "10000.00",
    "url": null,
    "extensibleData": null
  }
```
|Fields             |Type    |Origin|comments|mandatory?|
|-------------------|:------:|:----:|:-------|---------:|
|id                 |String|||Y|
|automatic          |boolean|||Y|
|scheduleType       |String-enum||ONE_TIME, RECURRING, AS_PRESENTED|Y|
|noOfInstallments   |integer    |||Y|
|totalAmount        |float |||Y|
|title              |String|||N|
|shortDescription   |String|||N|
|description        |String|||N|
|paymentUrl         |String|||N|
|payNotAllowed      |boolean|||N|
|editPlanAllpwed    |boolean|||N|
|changeMethodAllowed|boolean|||N|
|frequency          |String-enum||WEEKLY, MONTHLY, QUARTERLY, HALF_YEARLY, YEARLY|N|
|tenure             |Object|||N|
|principal          |float |||N|
|interestAmount     |float |||N|
|penalty            |float |||N|
|startDate          |DateTime|||N|
|status             |String-enum||ACTIVE, INACTIVE, PENDING_AUTH|N|
|url                |String|||N|
|extensibleData     |String|||N|


---

## /v3/disbursement/setDisbursementPlanResponse
|Fields          |Type |Origin|comments|mandatory?|
|----------------|:---:|:----:|:------:|---------:|
|metadata        |Object|LSP||Y|
|requestId       |String|LSP||Y|
|response        |String|Lender||Y|
|plan            |Object|||Y|


---

## /v3/disbursement/setDisbursementAccountRequest
```
{
  "metadata": {
    "version": "1.0",
    "timestamp": "2018-12-06T11:39:57.153Z",
    "traceId": "e8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
    "orgId": "LSP123"
  },
  "requestId": "e8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
  "loanApplicationId": "e8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
  "loanID": null,
  "account": {}
}
```
|Fields           |Type |Origin|comments|mandatory?|
|-----------------|:---:|:----:|:------:|---------:|
|metadata         |Object|LSP||Y|
|requestId        |String|LSP||Y|
|loanApplicationId|String|LSP||N|
|loanId           |String|LSP||N|
|account          |Object||schema: AccountDetails|Y|


### AccountDetails
```
"account": {
    "id": "e8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
    "description": null,
    "status": null,
    "accountDataType": "ACCOUNT",
    "data": {
      "accountType": null,
      "accountIFSC": null,
      "accountNumber": null,
      "vpa": null,
      "maskedAccountNumber": null
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

#### AccountDetailsData (schema of data)
|Fields             |Type |Origin|comments|mandatory?|
|-------------------|:---:|:----:|:-------|---------:|
|accountType        |String-enum||SAVINGS, CURRENT, OVERDRAFT|N|
|accountIFSC        |String|||N|
|accountNumber      |String|||N|
|vpa                |String||virtual payment address|N|
|maskedAccountNumber|String||eg. XXXXXXXXX9090|N|




---

## /v3/disbursement/setDisbursementAccountResponse
|Fields           |Type |Origin|comments|mandatory?|
|-----------------|:---:|:----:|:------:|---------:|
|metadata         |Object|LSP||Y|
|requestId        |String|LSP||Y|
|response         |String|Lender||N|
|account          |Object||schema: AccountDetails|Y|




---

## /v3/disbursement/triggerDisbursementRequest
```
{
  "metadata": {
    "version": "1.0",
    "timestamp": "2018-12-06T11:39:57.153Z",
    "traceId": "e8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
    "orgId": "LSP123"
  },
  "loanId": "e8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
  "requestId": "e8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
  "payment": {}
}
```
|Fields    |Type |Origin|comments|mandatory?|
|----------|:---:|:----:|:------:|---------:|
|metadata  |Object|LSP||Y|
|loanId    |String|LSP||Y|
|requestId |String|LSP||Y|
|payment   |Object|LSP||Y|


### Payment
```
"payment": {
    "id": "e8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
    "description": null,
    "date": null,
    "principal": null,
    "interestAmount": null,
    "fee": null,
    "penalty": null,
    "totalAmount": null,
    "installmentNumber": null,
    "status": null,
    "useSavedPaymentOption": null,
    "paymentMethodType": null,
    "paymentUrl": null,
    "txnRefNo": null,
    "url": null,
    "extensibleData": null
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





---

## /v3/disbursement/triggerDisbursementResponse
|Fields    |Type |Origin|comments|mandatory?|
|----------|:---:|:----:|:------:|---------:|
|metadata  |Object|||Y|
|response  |Object|||Y|
|requestId |String|||Y|
|payment   |Object|||Y|




---

## /v3/disbursement/triggerDisbursementStatusRequest
|Fields    |Type |Origin|comments|mandatory?|
|----------|:---:|:----:|:------:|---------:|
|metadata  |Object|LSP||Y|
|loanId    |String|LSP||Y|
|requestId |String|LSP||Y|
|payment   |Object|||Y|




---

## /v3/disbursement/triggerDisbursementStatusResponse
```
{
  "metadata": {
    "version": "1.0",
    "timestamp": "2018-12-06T11:39:57.153Z",
    "traceId": "e8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
    "orgId": "LSP123"
  },
  "loanId": "e8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
  "requestId": "e8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
  "payment": {}
}
```
|Fields    |Type |Origin|comments|mandatory?|
|----------|:---:|:----:|:------:|---------:|
|metadata  |Object|||Y|
|response  |Object|||Y|
|requestId |String|||Y|
|payment   |Object|||Y|



---

## /v3/disbursement/getDisbursementPlansRequest
```
{
  "metadata": {
    "version": "1.0",
    "timestamp": "2018-12-06T11:39:57.153Z",
    "traceId": "e8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
    "orgId": "LSP123"
  },
  "requestId": "e8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
  "loanId": "e8cc6822bd4bbb4eb1b9e1b4996fbff8acb"
}
```
|Fields    |Type |Origin|comments|mandatory?|
|----------|:---:|:----:|:------:|---------:|
|metadata  |Object|LSP||Y|
|requestId |String|LSP||Y|
|loanId    |String|LSP||Y|




---

## /v3/disbursement/getDisbursementPlansResponse
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
  "plans": [
    {
      "id": "a8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
      "title": null,
      "shortDescription": null,
      "description": null,
      "paymentUrl": null,
      "automatic": "false",
      "payNowAllowed": null,
      "editPlanAllowed": null,
      "changeMethodAllowed": null,
      "scheduleType": "ONE_TIME",
      "frequency": null,
      "noOfInstallments": "1",
      "tenure": {
        "duration": null,
        "unit": null
      },
      "principal": null,
      "interestAmount": null,
      "penalty": null,
      "startDate": null,
      "status": null,
      "totalAmount": "10000.00",
      "url": null,
      "extensibleData": null
    },
    {
      "id": "hb8c6822bd4bbb4eb1b9e1b4996fbff8acb",
      "title": null,
      "shortDescription": null,
      "description": null,
      "paymentUrl": null,
      "automatic": "false",
      "payNowAllowed": null,
      "editPlanAllowed": null,
      "changeMethodAllowed": null,
      "scheduleType": "ONE_TIME",
      "frequency": null,
      "noOfInstallments": "1",
      "tenure": {
        "duration": null,
        "unit": null
      },
      "principal": null,
      "interestAmount": null,
      "penalty": null,
      "startDate": null,
      "status": null,
      "totalAmount": "10000.00",
      "url": null,
      "extensibleData": null
    }
  ]
}
```
|Fields    |Type |Origin|comments|mandatory?|
|----------|:---:|:----:|:------:|---------:|
|metadata  |Object|||Y|
|response  |Object|Lender||Y|
|requestId |String|||Y|
|plans     |List<Object>||List of payment plans|Y|



---

## /v3/disbursement/getDisbursementAccountsRequest
```
{
  "metadata": {
    "version": "1.0",
    "timestamp": "2018-12-06T11:39:57.153Z",
    "traceId": "e8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
    "orgId": "LSP123"
  },
  "loanId": "e8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
  "requestId": "e8cc6822bd4bbb4eb1b9e1b4996fbff8acb"
}
```
|Fields    |Type |Origin|comments|mandatory?|
|----------|:---:|:----:|:------:|---------:|
|metadata  |Object|LSP||Y|
|loanId    |String|LSP||Y|
|requestId |String|LSP||Y|


---

## /v3/disbursement/getDisbursementAccountsResponse
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
  "accountList": [
    {
      "id": "hb8c6822bd4bbb4eb1b9e1b4996fbff8acb",
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
  ],
  "requestId": "e8cc6822bd4bbb4eb1b9e1b4996fbff8acb"
}
```
|Fields      |Type |Origin|comments|mandatory?|
|------------|:---:|:----:|:------:|---------:|
|metadata    |Object|||Y|
|response    |Object|||Y|
|accountList |List<Object>|||Y|
|requestId   |String|||Y|


### AccountDetails
|Fields         |Type |Origin|comments|mandatory?|
|---------------|:---:|:----:|:-------|---------:|
|id             |String|||N|
|description    |String|||N|
|status         |String-enum||ACTIVE, INACTIVE|N|
|accountDataType|String-enum||ACCOUNT, VPA|Y|
|data           |Object||schema: AccountDetailsData|Y|
|url            |String|||N|
|extensibleData |String|||N|