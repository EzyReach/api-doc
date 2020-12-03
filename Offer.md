#Offer API

## Overview

![alt text](https://github.com/iSPIRT/OCEN/blob/master/Sequence-Diagram/OfferAPIs.PNG "OfferAPI")

## /v3/offer/generateOffersRequest
```
{
  "metadata": {
    "version": "1.0",
    "timestamp": "2018-12-06T11:39:57.153Z",
    "traceId": "s8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
    "orgId": "LSP123"
  },
  "requestId": "t8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
  "loanApplicationIds": [
    "t8cc6822bd4bbb4eb1b9e1b4996fbff8acb"
  ]
}
```
|Fields            |Type |Origin|comments|mandatory?|
|----------------  |:---:|:----:|:-------|---------:|
|metadata          |Object|LSP||Y|
|requestId         |String|LSP||Y|
|loanApplicationIds|List|LSP||Y|

---

## /v3/offer/generateOffersResponse
```
{
  "metadata": {
    "version": "1.0",
    "timestamp": "2018-12-06T11:39:57.153Z",
    "traceId": "w8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
    "orgId": "FIU123"
  },
  "response": {
    "error": "0"
  },
  "requestId": "x8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
  "loanApplications": [
    {
      "loanApplicationId": "x8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
      "offers": [],
      "loanApplicationStatus": "OFFERED",
      "createdDate": null,
      "type": null,
      "borrower": null,
      "collaterals": null,
      "guarantors": null,
      "applicants": null,
      "terms": null,
      "description": null,
      "url": null,
      "extensibleData": null
    }
  ]
}
```
|Fields          |Type |Origin|comments|mandatory?|
|----------------|:---:|:----:|:-------|---------:|
|metadata        |Object|Lender||Y|
|requestId       |String|LSP||Y|
|response        |Object|Lender||Y|
|loanApplications|List|||Y|


### loanApplication
|Fields           |Type |Origin|comments|mandatory?|
|------           |:---:|:----:|:-------|--------:|
|createDate       |DateTime   |LSP     |The date on which the applicant applies for a new loan on LSP portal|N|
|loanApplicationId|String     |LSP     ||Y|
|offers           |List       |Lender  ||N|
|type             |String-enum|User    |CASHFLOW, PERSONAL, HOME, VEHICLE, BUSINESS|N|
|borrower         |Object     |LSP     |The data  of borrower could be stored in the LSP database when the user signup|N|
|collaterals      |List       |LSP     |The deatils of GST invoices on which the loan is to be raised|N|
|guarantors       |List       |LSP     ||N|
|applicants       |List       |LSP     |List of applicants and co-applicants|N|
|terms            |Object     |LSP     |schema is termDetails|N|
|description      |String     |User/LSP|A short description of the loan application|N|
|url              |String     |        ||N|
|extensibleData   |String     |        ||N|
|loanApplicationStatus|String-enum|    |ROCESSING, OFFERED, GRANTED, REJECTED, ACTION_REQUIRED|N|
|lender           |Object     |User    |User may choose from  list of availbale lenders|N|

#### offer
```
"offers": [
        {
          "id": "y8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
          "description": "A short description of the offer",
          "validTill": "2018-12-06T00:00:00.000Z",
          "terms": {
            "requestedAmount": "50000.00",
            "currency": "INR",
            "sanctionedAmount": "50000.00",
            "interestType": "FIXED",
            "interestRate": "12.00",
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
            "charges": {
              "prepayment": {
                "chargeType": "RATE_BASED",
                "description": "Description of charge calculation",
                "data": {
                  "rate": "6",
                  "applicableParameter": "TOTAL_LOAN_AMOUNT"
                }
              },
              "bounce": {
                "chargeType": "FIXED_AMOUNT",
                "description": "Description of charge calculation",
                "data": {
                  "amount": "3000.00"
                }
              },
              "latePayment": {
                "chargeType": "FIXED_AMOUNT",
                "description": "Description of charge calculation",
                "data": {
                  "amount": "3000.00"
                }
              },
              "processing": {
                "chargeType": "FIXED_AMOUNT",
                "description": "Description of charge calculation",
                "data": {
                  "amount": "3000.00"
                }
              }
            }
          },
          "disbursement": {
            "plans": [
              {
                "id": "hb8c6822bd4bbb4eb1b9e1b4996fbff8acb",
                "automatic": false,
                "scheduleType": "ONE_TIME",
                "noOfInstallments": "1",
                "totalAmount": "10000.00",
                "status": "INACTIVE"
              }
            ],
            "accountDetails": [
              {
                "id": "hb8c6822bd4bbb4eb1b9e1b4996fbff8acb",
                "accountDataType": "ACCOUNT",
                "data": {
                  "accountType": "CURRENT",
                  "maskedAccountNumber": "XXXXXXXXX9090"
                }
              }
            ]
          },
          "repayment": {
            "plans": [
              {
                "id": "a8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
                "automatic": false,
                "scheduleType": "ONE_TIME",
                "payNowAllowed": false,
                "changeMethodAllowed": false,
                "noOfInstallments": "1",
                "tenure": {
                  "duration": "1",
                  "unit": "MONTH"
                },
                "title": "Title of the repayment plan",
                "shortDescription": "short description of repayment plan",
                "url": "lender url showing repayment details",
                "penalty": "0.00",
                "principal": "9000.00",
                "interestAmount": "1000.00",
                "totalAmount": "10000.00",
                "status": "INACTIVE"
              }
            ]
          }
        }
      ]
```
|Fields        |Type |Origin|comments|mandatory?|
|------        |:---:|:----:|:-------|--------:|
|id            |String|Lender||Y|
|description   |String|Lender||N|
|validTill     |DateTime|Lender||Y|
|terms         |Object|Lender||Y|
|disbursement  |Object|Lender||Y|
|repayment     |Object|Lender||Y|
|documents     |List|||Y|
|url           |String|||N|
|extensibleData|String|||N|

>The details of terms, disbursement, repayment, documents are available in LoanApplication API docs.

---

## /v3/offer/setOffersRequest
```
{
  "metadata": {
    "version": "0.1.0",
    "timestamp": "2018-12-06T11:39:57.153Z",
    "traceId": "c8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
    "orgId": "LSP123"
  },
  "requestId": "12c1ds6822bd4bbb4eb1b9e1b4996fbff8acb",
  "loanApplicationId": "d8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
  "offer": {
    "id": "y8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
    "description": null,
    "validTill": null,
    "terms": null,
    "disbursement": null,
    "repayment": null,
    "documents": null,
    "url": null,
    "extensibleData": null
  }
}
```
|Fields           |Type |Origin|comments|mandatory?|
|---------------- |:---:|:----:|:-------|---------:|
|metadata         |Object|LSP||Y|
|requestId        |String|LSP||Y|
|loanApplicationId|String|LSP||Y|
|offer            |Object|||Y|

## /v3/offer/setOffersResponse
```
{
  "metadata": {
    "version": "1.0",
    "timestamp": "2018-12-06T11:39:57.153Z",
    "traceId": "w8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
    "orgId": "FIU123"
  },
  "response": {
    "error": "0"
  },
  "requestId": "w8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
  "loanApplicationId": "w8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
  "loanApplicationStatus": "OFFER_ACCEPTED"
}
```
|Fields               |Type |Origin|comments|mandatory?|
|---------------------|:---:|:----:|:-------|---------:|
|metadata             |Object|Lender||Y|
|response             |Object|Lender||Y|
|requestId            |String|LSP||Y|
|loanApplicationId    |String|LSP||Y|
|loanApplicationStatus|sString-enum|Lender|PROCESSING, OFFERED, GRANTED, REJECTED, ACTION_REQUIRED|Y|