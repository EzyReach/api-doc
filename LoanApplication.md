# Loan Application API

## Overview
The objective of Loan Application API is to register for a new loan application.

![alt text](https://github.com/iSPIRT/OCEN/blob/master/Sequence-Diagram/LoanApplication.PNG "Loan Application")

![alt text](https://github.com/EzyReach/api-doc/blob/loan-api/createLoanApplicationRequest.PNG "createLoanApplicationsRequest Flow Diagram")

![alt text](https://github.com/EzyReach/api-doc/blob/loan-api/loanApplication.PNG "loanApplication Fields")

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
|Fields          |Type |Origin|comments|mandatory?|
|----------------|:---:|:----:|:------:|---------:|
|error           |String|Lender||Y|
|traceId         |String|LSP|The traceId in respone is the same as the traceId sent via request payload except the first character|Y|
|timestamp       |dateTime|Lender||Y|

### Request Body
#### Request payload
```
{
  "metadata": {},
  "requestId": "e8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
  "loanApplications": [
    {
      "createdDate": "2020-03-01T00:00:00Z",
      "loanApplicationId": "e8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
      "offers": null,
      "type": "CASHFLOW",
      "borrower": {},
      "collaterals": [],
      "guarantors": [],
      "applicants": [],
      "terms": {},
      "description": null,
      "url": null,
      "extensibleData": null
    }
  ]
}
```

|Fields          |Type |Origin|comments|mandatory?|
|----------------|:---:|:----:|:------:|---------:|
|metadata        |Object|LSP||Y|
|requestId       |String|LSP||Y|
|loanApplications|List|LSP|List of each Loan Application where each of them is an object|Y|

> Note: The traceId, loanApplicationId and requestId are the same in the example. It is not sure if they are meant to be the same or not.

### metadata
```
"metadata": {
    "version": "1.0",
    "timestamp": "2018-12-06T11:39:57.153Z",
    "traceId": "e8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
    "orgId": "LSP123"
  }
 ```
|Fields   |Type |Origin|comments|mandatory?|
|------   |:---:|:-----:|:-------|---------:|
|version  |String|LSP||Y|
|timestamp|DateTime|LSP|This is the time at which loan application is created|Y|
|traceId  |String|LSP||Y|
|orgId    |String|LSP|This is the identification of the LSP|Y|


### loanApplication
|Fields           |Type |Origin|comments|mandatory?|
|------           |:---:|:----:|:-------|--------:|
|createDate       |String|LSP|The date on which the applicant applies for a new loan on LSP portal|N|
|loanApplicationId|DateTime|LSP||Y|
|offers           |List|Unknown||N|
|type             |String-enum|User|CASHFLOW, PERSONAL, HOME, VEHICLE, BUSINESS|N|
|borrower         |Object|LSP|The data  of borrower could be stored in the LSP database when the user signup|N|
|collaterals      |List|LSP|The deatils of GST invoices on which the loan is to be raised|N|
|guarantors       |List|LSP||N|
|applicants       |List|LSP|List of applicants and co-applicants|N|
|terms            |Object|LSP|schema is termDetails|N|
|description      |String|User/LSP|A short description of the loan application|N|
|url              |String|||N|
|extensibleData   |String|||N|
|loanApplicationStatus|String-enum||ROCESSING, OFFERED, GRANTED, REJECTED, ACTION_REQUIRED|N|
|lender           |Object|User|User may choose from  list of availbale lenders|N|


#### borrower
```
"borrower": {
        "primaryId": "CPAA1234A",
        "primaryIdType": "PAN",
        "secondaryId": null,
        "additionalIdentifiers": [],
        "name": "John doe",
        "category": "ORGANIZATION",
        "contactDetails": [],
        "platformData": null,
        "documents": []
      }
```
|Fields               |Type |Origin|comments|mandatory?|
|------               |:---:|:----:|:-------|---------:|
|primaryId            |String|User| of primaryIdType, eg if primaryIdType is MOBILE then primaryId would be mobile number|Y|
|primaryIdType        |String-enum|User|PAN, MOBILE, AADHAR|Y|
|secondaryId          |String|User||N|
|additionalIdentifiers|List|User|ids other than primary id|Y|
|name                 |String|User||N|
|category             |String-enum|User|ORGANIZATION, INDIVIDUAL|Y|
|contactDetails       |Object|User||Y|
|platformData         |...|LSP||N|
|documents            |List|User||Y|


#### contactDetails
```
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
        ]
```
|Fields        |Type |Origin|comments|mandatory?|
|------        |:---:|:----:|:-------|---------:|
|type          |String-enum|User|PRIMARY, OTHER|Y|
|phone         |String|User||Y|
|description   |String|User||N|
|email         |String|User||Y|
|address       |Object|||Y|
|url           |String|||N|
|extensibleData||||N|

##### address

> It is not clear whether the address would be provided by the user or would be fetched from some source document by the user (Aadhar, PAN, GSTIN etc).

|Fields   |Type |Origin|comments|mandatory?|
|------   |:---:|:----:|:-------|---------:|
|co       |String||care of||
|hba      |String||House/Building/Apartment||
|srl      |String||Street/Road/Lane||
|landmark |String||||
|als      |String||Area/Locality/Sector||
|vtc      |String||Village/Town/City||
|pinCode  |String||||
|po       |String||||
|district |String||||
|state    |String||||
|country  |String||||
|url      |String||||
|latitude |String||||
|longitude|String||||



#### documents
```
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
```
|Fields          |Type |Origin|comments|mandatory?|
|------          |:---:|:----:|:-------|---------:|
|format          |String-enum|User|DOC, IMAGE, CSV, JSON, XML|Y|
|refernece       |String|User||Y|
|source          |String-enum|User||AA, FIP, FIU, FSR, USER, GSTN|Y|
|sourceIdentifier|String|User|example: GSTN|Y|
|type            |String-enum||GSTN_B2B_INVOICE, GSTN_PROFILE, PAN, AADHAAR, DRIVING_LICENSE, PASSPORT, OTHER|Y|
|isDataInline    |boolean|User||Y|
|data            |String|LSP||Base64 encoded String|Y|


#### collateral
```
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
      ]
```

|Fields                 |Type |Origin|comments|mandatory?|
|------                 |:---:|:----:|:-------|---------:|
|collateralPrimaryId    |String|User|collateralPrimaryIdType value|Y|
|collateralPrimaryIdType|String-enum|User|GST_INVOICE, VIN, OTHER|Y|
|type                   |String|User|eg GST_INVOICE|Y|
|additionalIdentifiers  |List|User||N|
|valuation              |Object|||N|
|parties                |List|User||Y|
|documents              |List|User||Y|
|url                    |String|User||N|
|extensibleData         |String|||N|


##### valuation
|Fields        |Type |Origin|comments|mandatory?|
|------        |:---:|:----:|:-------|---------:|
|value         |String||Y|
|currency      |String||Y|
|date          |DateTime||Y|
|source        |String||Y|
|url           |String||N|
|extensibleData|String||N|


#### applicants
```
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
      ]
```
|Fields               |Type |Origin|comments|mandatory?|
|------               |:---:|:----:|:-------|---------:|
|primaryIdType        |String-enum|User|PAN, MOBILE, AADHAAR|Y|
|primaryId            |String|User|The value of primaryIdType, eg if primaryIdType is PAN then primaryId would be PAN number|Y|
|category             |String-enum||ORGANIZATION, INDIVIDUAL|Y|
|contactDetails       |Object|User||Y|
|additionalIdentifiers|List|User||Y|
|documents            |List|User||Y|
|name                 |String|User||N|
|relationshipWithBorrower|String|User||N|


### guarantors
|Fields                  |Type       |Origin|comments|mandatory?|
|------                  |:---------:|:----:|:-------|---------:|
|priamryId               |String     |LSP||Y|
|primaryIdType           |String-enum|USER|PAN, MOBILE, AADHAR|Y|
|category                |String-enum|USER|ORGANIZATION, INDIVIDUAL|Y|
|contactDetails          |Object     |User||Y|
|relationshipWithBorrower|String     |User||N|
|additionalIdentifiers   |List		 |USER|identification in addition to primary id|Y|
|documents               |List       |User||Y|
|name                    |String     |User||N|

### additionalIdentifier
|Fields                  |Type |Origin|comments|mandatory?|
|------                  |:---:|:----:|:-------|---------:|
|id                      |String|USER||Y|
|additionalIdentifierType|String-enum|USER|PAN, MOBILE, AADHAR|Y|


### termDetails (schema of terms)
```
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
      }
```
|Fields          |Type |Origin|comments|mandatory?|
|------          |:---:|:----:|:-------|---------:|
|requestedAmount |float|||Y|
|currency        |String|||Y|
|description     |String|||N|
|sanctionedAmount|float||||
|interestType    |String-enum||FIXED, FLOATING|N|
|interestAmount  |flaot|||N|
|totalAmount     |float|||N|
|tenure          |Object|||N|
|legalAgreement  |Object|||N|
|documents       |List|||N|
|charges         |Object|||N|
|url             |String|||N|
|extensibleData  |String|||N|

#### tenure
|Fields   |Type |Origin|comments|mandatory?|
|------   |:---:|:----:|:-------|---------:|
|duration |int|||Y|
|unit     |String-enum||DAY, MONTH, YEAR|Y|

#### legalAgreement
|Fields|Type |Origin|comments|mandatory?|
|------|:---:|:----:|:-------|---------:|
|type  |String-enum||TEXT, URL|Y|
|data  |String||Base64 encoded String|Y|


### offer
|Fields|Type |Origin|comments|mandatory?|
|------|:---:|:----:|:-------|---------:|
|type  |String-enum||TEXT, URL|Y|
|data  |String||Base64 encoded String|


---

## /v3/loanApplication/createLoanApplicationsResponse

### Response
### ACK
|Fields          |Type |Origin|comments|mandatory?|
|----------------|:---:|:----:|:-------|---------:|
|error           |String|LSP||
|traceId         |String|LSP||
|timestamp       |dateTime|LSP||

### Request Body
```
{
  "metadata": {
    "version": "1.0",
    "timestamp": "2018-12-06T11:39:57.153Z",
    "traceId": "e8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
    "orgId": "FIU123"
  },
  "response": {
    "error": "0"
  },
  "requestId": "e8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
  "loanApplications": [
    {
      "createdDate": null,
      "loanApplicationId": "e8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
      "offers": null,
      "type": null,
      "borrower": null,
      "collaterals": null,
      "guarantors": null,
      "applicants": null,
      "terms": null,
      "description": null,
      "url": null,
      "lender": {
        "primaryId": "AWW PA7645M",
        "primaryIdType": "PAN",
        "additionalIdentifiers": [],
        "name": "ABC Bank",
        "category": "ORGANIZATION",
        "contactDetails": [],
        "documents": []
      },
      "extensibleData": null,
      "loanApplicationStatus": "PROCESSING"
    }
  ]
}
```
|Fields          |Type |Origin|comments|mandatory?|
|----------------|:---:|:----:|:-------|---------:|
|metadata        |Object|LSP||Y|
|response        |Object|Lender||Y|
|requestId       |String|LSP||Y|
|loanApplications|List|LSP||Y|
|lender          |Object|Lender||Y|

### lender
```
"lender": {
        "primaryId": "AWW PA7645M",
        "primaryIdType": "PAN",
        "additionalIdentifiers": [],
        "name": "ABC Bank",
        "category": "ORGANIZATION",
        "contactDetails": [],
        "documents": []
      }
```
|Fields               |Type |Origin|comments|mandatory?|
|----------------     |:---:|:----:|:-------|---------:|
|primaryIdType        |String-enum|Lender|PAN, MOBILE, AADHAR|Y|
|primaryId            |String|Lender|primaryIdType value, eg if primaryIdType is PAN then primaryId would be PAN number|Y|
|category             |String-enum|Lender|ORGANIZATION, INDIVIDUAL|Y|
|contactDetails       |List|Lender||Y|
|additionalIdentifiers|List|Lender||Y|
|documents            |List|Lender||Y|
|name                 |String|Lender||N|