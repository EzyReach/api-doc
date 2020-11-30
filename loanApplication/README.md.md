# Loan Application API

## Overview
The objective of Loan Application API is to register for a new loan application.

![alt text](https://github.com/iSPIRT/OCEN/blob/master/Sequence-Diagram/LoanApplication.PNG "Loan Application")

![alt text](https://github.com/nirmal3047/OCEN-Documentation/blob/master/createLoanApplicationRequest.PNG "createLoanApplicationsRequest Flow Diagram")

![alt text](https://github.com/nirmal3047/OCEN-Documentation/blob/master/loanApplication.PNG "loanApplication Fields")

## /v3/loanApplication/createLoanApplicationsRequest

### Response
### ACK
#### Response payload
```
{
  "ack": {
    "error": "0",
    "traceId": "d8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
    "timestamp": "2018-12-06T11:39:57.153Z"
  }
}
```
|Fields          |Type |Origin|comments|
|----------------|:---:|:----:|-------:|
|error           |String|Lender||
|traceId         |String||The traceId in respone is the same as the traceId sent via request payload except the first character|
|timestamp       |dateTime|Lender||

### Request Body
#### Request payload
```
{
  "metadata": {
    "version": "1.0",
    "timestamp": "2018-12-06T11:39:57.153Z",
    "traceId": "e8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
    "orgId": "LSP123"
  },
  "requestId": "e8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
  "loanApplications": [
    {
      "createdDate": "2020-03-01T00:00:00Z",
      "loanApplicationId": "e8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
      "offers": null,
      "type": "CASHFLOW",
      "borrower": {
        "primaryId": "CPAA1234A",
        "primaryIdType": "PAN",
        "secondaryId": null,
        "additionalIdentifiers": [],
        "name": "John doe",
        "category": "ORGANIZATION",
        "contactDetails": [
          {
            "type": "PRIMARY",
            "phone": "7777777777",
            "description": null,
            "email": "johndoe@defenterprises",
            "address": {
              "co": "<care of>",
              "hba": "<House/Building/Apartment>",
              "srl": "<Street/Road/Lane>",
              "landmark": "",
              "als": "<Area/Locality/Sector>",
              "vtc": "<Village/Town/City>",
              "pincode": "",
              "po": "",
              "district": "",
              "state": "",
              "country": "",
              "url": "<digital address>",
              "latitude": "",
              "longitude": "",
              "extensibleData": null
            },
            "url": null,
            "extensibleData": null
          }
        ],
        "platformData": null,
        "documents": [
          {
            "format": "JSON",
            "reference": "b8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
            "source": "GSTN",
            "sourceIdentifier": "GSTN",
            "type": "GSTN_PROFILE",
            "isDataInline": true,
            "data": "eyJzdGpDZCI6IkFQMDAzIiwibGdubSI6Ik1TIENPUlBPUkFUSU9OIiwic3RqIjoiQkNQIEtPRElLT05EQSIsImR0eSI6IlJlZ3VsYXIiLCJjeGR0IjoiIiwiZ3N0aW4iOiIwNUFCTlRZMzI5MFA4WkEiLCJuYmEiOlsiQm9uZGVkIFdhcmVob3VzZSIsIkVPVSAvIFNUUCAvIEVIVFAiLCJGYWN0b3J5IC8gTWFudWZhY3R1cmluZyIsIklucHV0IFNlcnZpY2UgRGlzdHJpYnV0b3IgKElTRCkiLCJMZWFzaW5nIEJ1c2luZXNzIl0sImxzdHVwZHQiOiIwNS8wMS8yMDE3IiwicmdkdCI6IjA1LzA1LzIwMTciLCJjdGIiOiJGb3JlaWduIExMUCIsInN0cyI6IlByb3Zpc2lvbmFsIiwiY3RqQ2QiOiJBUDAwNCIsImN0aiI6IkJDUCBUSFVNTUFLVU5UQSIsInRyYWRlTmFtIjoiQUxUT04gUExBU1RJQyBQUklWQVRFIExURCIsImFkYWRyIjpbeyJhZGRyIjp7ImJubSI6IkVMUEhJTlNUT05FIEJVSUxESU5HIiwic3QiOiIxMCwgVkVFUiBOQVJJTUFOIFJPQUQiLCJsb2MiOiJGT1JUIiwiYm5vIjoiMTAiLCJzdGNkIjoiUmFqYXN0aGFuIiwiZmxubyI6IjFTVCBGTE9PUiIsImx0IjoiNzQuMjE3OSIsImxnIjoiMjcuMDIzOCIsInBuY2QiOiI0MDAwMDEifSwibnRyIjpbIldob2xlc2FsZSBCdXNpbmVzcyJdfV0sInByYWRyIjp7ImFkZHIiOnsiYm5tIjoiS0FUR0FSQSBIT1VTRSIsInN0IjoiMTUsIEwgSkFHTU9IQU5EQVMgTUFSRyIsImxvYyI6Ik1BTEFCQVIgSElMTCIsImJubyI6IjUiLCJzdGNkIjoiTWFoYXJhc2h0cmEiLCJmbG5vIjoiNFRIIEZMT09SIiwibHQiOiI3NC4yMTc5IiwibGciOiIyNy4wMjM4IiwicG5jZCI6IjQwMDAwNiJ9LCJudHIiOlsiV2hvbGVzYWxlIEJ1c2luZXNzIl19fQ=="
          }
        ]
      },
      "collaterals": [
        {
          "collateralPrimaryId": "<GSTIN>_<INVOICENUM>",
          "collateralPrimaryIdType": "GST_INVOICE",
          "type": "GST_INVOICE",
          "additionalIdentifiers": [],
          "valuation": {
            "value": "",
            "description": null,
            "currency": "",
            "date": "",
            "source": "GSTN",
            "url": null,
            "extensibleData": null
          },
          "parties": [],
          "documents": [
            {
              "format": "JSON",
              "reference": "e8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
              "source": "GSTN",
              "sourceIdentifier": "GSTN",
              "type": "GSTN_B2B_INVOICE",
              "isDataInline": true,
              "data": "eyJjdGluIjoiMDFBQUJDRTIyMDdSMVo1IiwiY2ZzIjoiWSIsImludiI6W3siY2hrc3VtIjoiQkJVSUJVSVVJSktLQkpLR1VZRlRGR1VZIiwidXBkYnkiOiJTIiwiaW51bSI6IlMwMDg0MDAiLCJpZHQiOiIyNC0xMS0yMDE2IiwidmFsIjo3MjkyNDguMTYsInBvcyI6IjA2IiwicmNocmciOiJOIiwiZXRpbiI6IjAxQUFCQ0U1NTA3UjFaNCIsImludl90eXAiOiJSIiwiY2ZsYWciOiJOIiwiZGlmZl9wZXJjZW50IjowLjY1LCJvcGQiOiIyMDE2LTEyIiwiaXRtcyI6W3sibnVtIjoxLCJpdG1fZGV0Ijp7InJ0Ijo1LCJ0eHZhbCI6MTAwMDAsImlhbXQiOjMyNSwiY2FtdCI6MCwic2FtdCI6MCwiY3NhbXQiOjEwfX1dfV19"
            }
          ]
        }
      ],
      "guarantors": [],
      "applicants": [
        {
          "primaryId": "9898989898",
          "primaryIdType": "MOBILE",
          "category": null,
          "name": null,
          "relationshipWithBorrower": null,
          "contactDetails": null,
          "additionalIdentifiers": null,
          "documents": null,
          "url": null,
          "extensibleData": null
        }
      ],
      "terms": {
        "requestedAmount": "50000.00",
        "currency": "INR",
        "description": null,
        "sanctionedAmount": null,
        "interestType": null,
        "interestRate": null,
        "interestAmount": null,
        "totalAmount": null,
        "tenure": null,
        "legalAgreement": null,
        "documents": null,
        "charges": null,
        "url": null,
        "extensibleData": null
      },
      "description": null,
      "url": null,
      "extensibleData": null
    }
  ]
}
```

|Fields          |Type |Origin|comments|
|----------------|:---:|:----:|-------:|
|metadata        |Object|LSP||
|requestId       |String|LSP||
|loanApplications|List|LSP|List of each Loan Application where each of them is an object|

> Note: The traceId, loanApplicationId and requestId are the same in the example. It is not sure if they are meant to be the same or not.

### metadata
|Fields|Type |Origin|comments|
|------|:---:|-----:|-------:|
|version|String|LSP||
|timestamp|DateTime|LSP|This is the time at which loan application is created|
|traceId|String|Unknown||
|orgId|String|LSP|This is the identification of the LSP|


### loanApplication
|Fields           |Type |Origin|comments|
|------           |:---:|-----:|-------:|
|createDate       |String|LSP|The date on which the applicant applies for a new loan on LSP portal|
|loanApplicationId|DateTime|LSP||
|offers           |String|Unknown||
|type             |String-enum|LSP||
|borrower         |Object|LSP|The data  of borrower could be stored in the LSP database when the signup|
|collaterals      |List|LSP||
|guarantors       |List|LSP||
|applicants       |List|LSP||
|terms            |Object|LSP||


#### borrower
|Fields               |Type |Origin|comments|
|------               |:---:|-----:|-------:|
|primaryId            |String|LSP||
|primaryIdType        |String-enum|LSP||
|secondaryId          |String|LSP||
|additionalIdentifiers|List|LSP||
|name                 |String|User||
|category             |String-enum|LSP||
|contactDetails       |Object|User||
|platformData         |...|LSP||
|documents            |List|User||

#### collateral
|Fields                 |Type |Origin|comments|
|------                 |:---:|-----:|-------:|
|collateralPrimaryId    |String|||
|collateralPrimaryIdType|String-menu|||
|type                   |String|||
|additionalIdentifiers  |List|||
|valuation              |Object|User||
|parties                |List|||
|documents              |List|User||

#### applicants
|Fields               |Type |Origin|comments|
|------               |:---:|-----:|-------:|
|primaryIdType        |String-enum|||
|primaryId            |String|||
|category             |String-enum|||
|contactDetails       |Object|User||
|additionalIdentifiers|List|||
|documents            |List|User||

### guarantors
|Fields                  |Type |Origin|comments|
|------                  |:---:|-----:|-------:|
|priamryId               |String|LSP||
|primaryIdType           |String-enum|LSP||
|category                |String-enum|LSP||
|contactDetails          |Object|User||
|relationshipWithBorrower|String|User||
|additionalIdentifiers   |List|USER||
|documents               |List|User||

### additionalIdentifier
|Fields                  |Type |Origin|comments|
|------                  |:---:|-----:|-------:|
|id                      |String|||
|additionalIdentifierType|String-enum||PAN, MOBILE, AADHAR|

---

## /v3/loanApplication/createLoanApplicationsResponse

### Response
### ACK
|Fields          |Type |Origin|comments|
|----------------|:---:|:----:|-------:|
|error           |String|LSP|...|
|traceId         |String|LSP|...|
|timestamp       |dateTime|LSP|...|

### Request Body
|Fields          |Type |Origin|comments|
|----------------|:---:|:----:|-------:|
|metadata        |Object|LSP||
|response        |Object|Lender||
|requestId       |String|LSP||
|loanApplications|List|LSP||
|lender          |Object|Lender||

### lender
|Fields               |Type |Origin|comments|
|----------------     |:---:|:----:|-------:|
|primaryIdType        |String-enum|Lender|eg "PAN"|
|primaryId            |String|Lender||
|category             |String-enum|Lender||
|contactDetails       |List|Lender||
|additionalIdentifiers|List|||
|documents            |List|Lender||