# Proposed Microservice Archtecture
The documents lists all the steps required for an user to avail loan through EzyReach and tries to purpose an structure for the microservices required 


## User Onboarding
The first step in the process of availing loan through an LCP would be user registration.

![alt text](https://github.com/EzyReach/api-doc/blob/microservices-architecture/Onboarding.png "User Onboarding")

1. User Registration
* Username and password
* Preferably, username should be same as user's email id, which can be verified using OTP or verification link. This will help the user to recover his/her account in case he/she forgets the password.

2. User Login
* Use JWT token for verifying user sessions

3. Fetching GST invoices
* After successful login, the user will input his/her GSTIN to fetch the eligible invoices.

> Will user's GSTIN be stored in the LSP's database Or has it to be entered every time the user wants to apply for a new loan?

Inputs required
* GSTIN
* Start date
* End date

**GET** https://<domain-name>/taxpayerapi/v2.1/returns/gstr1
**URL Parameters**  action_required="Y/N", gstin={}, ret_period={},ctin={}, from_time={}
[Get Challan History API](https://developer.gst.gov.in/apiportal/taxpayer/returns/apilist/v2.1 "GST Develpoer Portal")

```
{
  "b2b": [
    {
      "ctin": "01AABCE2207R1Z5",
      "cfs": "Y",
      "inv": [
        {
          "chksum": "BBUIBUIUIJKKBJKGUYFTFGUY",
          "updby": "S",
          "inum": "S008400",
          "idt": "24-11-2016",
          "val": 729248.16,
          "pos": "06",
          "rchrg": "N",
          "etin": "01AABCE5507R1Z4",
          "inv_typ": "R",
          "cflag": "N",
          "diff_percent": 0.65,
          "opd": "2016-12",
          "srctyp": "EInvoice",
          "irn": "897ADG56RTY78956HYUG90BNHHIJK453GFTD99845672FDHHHSHGFH4567FG56TR",
          "irngendate": "24-12-2019",
          "itms": [
            {
              "num": 1,
              "itm_det": {
                "rt": 5,
                "txval": 10000,
                "iamt": 325,
                "camt": 0,
                "samt": 0,
                "csamt": 10
              }
            }
          ]
        }
      ]
    }
  ]
}
```

### b2b invoice
|Fields |Type |Origin|Description|mandatory?|
|-------|:---:|:----:|:----------|---------:|
|ctin   |Alphanumeric with 15 characters||GSTIN/UID of the Receiver taxpayer/UN, Govt Bodies||
|cfs    |Character (Y/N)||GSTR2 filing status of counter party||
|inv    |List<Object>||Invoice Details||

### invoice
|Fields      |Type       |Origin|Description|mandatory?|
|------------|:---------:|:----:|:----------|---------:|
|chksum      |String (Max length:64)||Invoice Check sum value ||
|updby       |Character||Uploaded by||
|inum        |String (Max length:16)||Supplier Invoice Number||
|idt         |Datetime||Supplier Invoice Date||
|val         |Decimal(15,2)||Supplier Invoice Value||
|pos         |String(Max length:2)||Place of supply||
|rchrg       |Character||Reverse Charge||
|etin        |Alphanumeric with 15 characters||EcomOperator||
|inv_type    |String (Max length: 5) (R/SEWP/SEWOP/DE/CBW)||Invoice type||
|cflag       |Two Character(A/R/M/N/U/P/DF/FR)||Counter Party Flag||
|diff_percent|Decimal (3,2)||Differential percentage||
|opd         |YYYY-MM||Original Period||
|items       |List<Object>||Items||

### itm
|Fields      |Type |Origin|Description|mandatory?|
|------------|:---:|:----:|:----------|---------:|
|num         |int||Serial no||
|itm_det     |Object||Item Details||

### ite_det
|Fields|Type         |Origin|Description|mandatory?|
|------|:-----------:|:----:|:----------|---------:|
|rt    |Decimal(3,2) ||rate||
|txval |Decimal(11,2)||Taxable value of Goods or Service as per invoice||
|iamt  |Decimal(11,2)||IGST Amount as per invoice||
|camt  |Decimal(11,2)||SGST Amount as per invoice||
|csamt |Decimal(11,2)||cess Amount as per invoice||


## Domain Object Relationships

![alt text](https://github.com/EzyReach/api-doc/blob/microservices-architecture/User_er.PNG "User Entity Relationship")

![alt text](https://github.com/EzyReach/api-doc/blob/microservices-architecture/DomainObjects.PNG "Domain Objects")


#### The following points need clarification:


1. Will there be an option for login to admin? If yes, what actions will admin perform?

2. Where will user get AA id? Does he/she need to register on AA app first before registering to LSP app?
Also note that AA id is not reusable across multiple AA
[Reference](https://sahamati.org.in/faq/ "Sahamati FAQ")


3. Format of response payload from AA?

4. Will AA directly send user details to Lender? If yes, then where would the data to be sent in createLoanApplication come from?

5. What is the "document" sent in createLoanApplication as a field of Borrower?

> Base64 encoded
```
"data": "eyJzdGpDZCI6IkFQMDAzIiwibGdubSI6Ik1TIENPUlBPUkFUSU9OIiwic3RqIjoiQkNQIEtPRElLT05EQSIsImR0eSI6IlJlZ3VsYXIiLCJjeGR0IjoiIiwiZ3N0aW4iOiIwNUFCTlRZMzI5MFA4WkEiLCJuYmEiOlsiQm9uZGVkIFdhcmVob3VzZSIsIkVPVSAvIFNUUCAvIEVIVFAiLCJGYWN0b3J5IC8gTWFudWZhY3R1cmluZyIsIklucHV0IFNlcnZpY2UgRGlzdHJpYnV0b3IgKElTRCkiLCJMZWFzaW5nIEJ1c2luZXNzIl0sImxzdHVwZHQiOiIwNS8wMS8yMDE3IiwicmdkdCI6IjA1LzA1LzIwMTciLCJjdGIiOiJGb3JlaWduIExMUCIsInN0cyI6IlByb3Zpc2lvbmFsIiwiY3RqQ2QiOiJBUDAwNCIsImN0aiI6IkJDUCBUSFVNTUFLVU5UQSIsInRyYWRlTmFtIjoiQUxUT04gUExBU1RJQyBQUklWQVRFIExURCIsImFkYWRyIjpbeyJhZGRyIjp7ImJubSI6IkVMUEhJTlNUT05FIEJVSUxESU5HIiwic3QiOiIxMCwgVkVFUiBOQVJJTUFOIFJPQUQiLCJsb2MiOiJGT1JUIiwiYm5vIjoiMTAiLCJzdGNkIjoiUmFqYXN0aGFuIiwiZmxubyI6IjFTVCBGTE9PUiIsImx0IjoiNzQuMjE3OSIsImxnIjoiMjcuMDIzOCIsInBuY2QiOiI0MDAwMDEifSwibnRyIjpbIldob2xlc2FsZSBCdXNpbmVzcyJdfV0sInByYWRyIjp7ImFkZHIiOnsiYm5tIjoiS0FUR0FSQSBIT1VTRSIsInN0IjoiMTUsIEwgSkFHTU9IQU5EQVMgTUFSRyIsImxvYyI6Ik1BTEFCQVIgSElMTCIsImJubyI6IjUiLCJzdGNkIjoiTWFoYXJhc2h0cmEiLCJmbG5vIjoiNFRIIEZMT09SIiwibHQiOiI3NC4yMTc5IiwibGciOiIyNy4wMjM4IiwicG5jZCI6IjQwMDAwNiJ9LCJudHIiOlsiV2hvbGVzYWxlIEJ1c2luZXNzIl19fQ=="
```

> Base64 decoded
```
{
  "stjCd":"AP003",
  "lgnm":"MS CORPORATION",
  "stj":"BCP KODIKONDA",
  "dty":"Regular",
  "cxdt":"",
  "gstin":"05ABNTY3290P8ZA",
  "nba":[
    "Bonded Warehouse",
    "EOU / STP / EHTP",
    "Factory / Manufacturing",
    "Input Service Distributor (ISD)",
    "Leasing Business"
  ],
  "lstupdt":"05/01/2017",
  "rgdt":"05/05/2017",
  "ctb":"Foreign LLP",
  "sts":"Provisional",
  "ctjCd":"AP004",
  "ctj":"BCP THUMMAKUNTA",
  "tradeNam":"ALTON PLASTIC PRIVATE LTD",
  "adadr":[
    {
      "addr":{
        "bnm":"ELPHINSTONE BUILDING",
        "st":"10, VEER NARIMAN ROAD",
        "loc":"FORT",
        "bno":"10",
        "stcd":"Rajasthan",
        "flno":"1ST FLOOR",
        "lt":"74.2179",
        "lg":"27.0238",
        "pncd":"400001"
        },
      "ntr":["Wholesale Business"]
    }
  ],
  "pradr":{
    "addr":{
      "bnm":"KATGARA HOUSE",
      "st":"15,L JAGMOHANDAS MARG",
      "loc":"MALABAR HILL",
      "bno":"5",
      "stcd":"Maharashtra",
      "flno":"4TH FLOOR",
      "lt":"74.2179",
      "lg":"27.0238",
      "pncd":"400006"
     },
     "ntr":["Wholesale Business"]
  }
}
```
The above response sample is actually the same as response sample returned from the following url:
**GET** https://api-domain-name/commonapi/v1.1/search
[GST Search Taxpayer API](https://developer.gst.gov.in/apiportal/taxpayer/other/apilist/v1.1 "GST Develpoer Portal")

|Error codes |Error Description|
|------      |:----------------|
|FO8001      |Malformed Request|
|FO8007      |Invalid GSTIN/UIN|

|Fields  |Type |Origin|comments|mandatory?|
|------  |:---:|:----:|:-------|---------:|
|stjCd   |String||State Jurisdiction Code||
|lgnm    |String||Legal Name of Business||
|stj     |String||State Jurisdiction||
|dty     |String||Taxpayer type||
|cxdt    |Date||Date Of Cancellation||
|gstin   |String||GSTIN of the Tax Payer||
|nba     |String||Nature of Business Activity ||
|lstupdt |Date||Last Updated Date||
|rgdt    |Date||Date of Registration||
|ctb     |String||Constitution of Business||
|sts     |String||GSTN status||
|ctjCd   |String||Centre Jurisdiction Code||
|ctj     |String||Centre Jurisdiction||
|tradeNam|String||Trade Name||
|adadr   |Object||Additional Place of Business Fields||
|pradr   |Object||Pricipal Place of Business fields||

6. Borrower details fetched from GST invoices do not match to the details to be sent with createLoanApplication (contact details etc). Does the borrow manually need to enter these details?


7. What is document sent as a part of collateral?

> Base64 decoded
```
{
  "ctin":"01AABCE2207R1Z5",
  "cfs":"Y",
  "inv":[
    {
      "chksum":"BBUIBUIUIJKKBJKGUYFTFGUY",
      "updby":"S",
      "inum":"S008400",
      "idt":"24-11-2016",
      "val":729248.16,
      "pos":"06",
      "rchrg":"N",
      "etin":"01AABCE5507R1Z4",
      "inv_typ":"R",
      "cflag":"N",
      "diff_percent":0.65,
      "opd":"2016-12",
      "itms":[
        {
          "num":1,
          "itm_det":{
            "rt":5,
            "txval":10000,
            "iamt":325,
            "camt":0,
            "samt":0,
            "csamt":10
          }
        }
      ]
    }
  ]
}
```

