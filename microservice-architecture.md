# Proposed Microservice Archtecture
The documents lists all the steps required for an user to avail loan through EzyReach and tries to purpose an structure for the microservices required 


## User Onboarding
The first step in the process of availing loan through an LCP would be user registration.

![alt text](https://github.com/EzyReach/api-doc/blob/microservices-architecture/Onboarding.png "User Onboarding")

1. User Registration
* Username and password
* Username would be same as user's email id, which will be verified using OTP or verification link. This will help the user to recover his/her account in case he/she forgets the password.

Steps for user registraion:
* User will enter username (email) and password.
* The application will verify if the username entered is unique or not. If the username already exists in the system, it will throw an error. If it is unique, a temperory user_entity will be created (this object will not be stored in the database). The user will be requested to check their email
* Upon clicking on the verification link, or entering the OTP, the user will be verified and the details will be stored in the database

2. User Login
* Use JWT token for verifying user sessions

3. User profiling (Borrower's details)
After successful login, the user will input his/her GSTIN. User's getails would be fetched from GST portal and would be mapped according to Borrower's attributes in OCEN specifications

Mapping between data fetched from GST and data required for Borrower's profiling

|Field from GST|Type |Description|Field in Borrower's address|Type |Description|
|---------------|:---:|:---------:|:----------------------|:---:|:---------:|
|bnm |String|building name|hba      |String|House/Building/Apartment|
|st  |String|street       |srl      |String|Street/Road/Lane        |
|loc |String|location     |als      |String|Area/Locality/Sector    |
|bno |String|door number  |         |String||
|stcd|String|state name   |state    |String||
|flno|String|floor number |         |String||
|lt  |String|lattitude    |lattitude|String||
|lg  |String|longitude    |longitude|String||
|pncd|String|pincode      |pincode  |String||
|    |      |             |co       |String|care of                  |
|    |      |             |landmark |String||
|    |      |             |vtc      |String|Village/Town/City        |
|    |      |             |po       |String||
|    |      |             |district |String||
|    |      |             |         |String|country                  |
|    |      |             |url      |String|digital address          |



3. Fetching GST invoices
* After successful login, upon user's request eligible invoices will be fetched from GSTIN.

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

```
{
  "gstin": "01AABCE2207R1Z5",
  "fp": "052020",
  "b2b": [
    {
      "ctin": "01AABCE2207R1Z5",
      "trdname": "E-Invoicer",
      "inv": [
        {
          "chksum": "BBUIBUIUIJKKBJKGUYFTFGUY",
          "inum": "S008400",
          "idt": "24-11-2016",
          "val": 729248.16,
          "pos": "06",
          "rchrg": "N",
          "etin": "01AABCE5507R1C4",
          "inv_typ": "R",
          "srctyp": "e-Invoice",
          "irn": "897ADG56RTY78956HYUG90BNHHIJK453GFTD99845672FDHHHSHGFH4567FG56TR",
          "irngendate": "24-12-2019",
          "einvstatus": "ACT",
          "autodft": "Auto-populated",
          "autodftdt": "24-12-2019",
          "errorCd": "null",
          "errorMsg": "null",
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
  ],
  "cdnur": [
    {
      "chksum": "ASDFGJKLPTBBJKBJKBBJKBB",
      "typ": "B2CL",
      "ntty": "C",
      "nt_num": "533515",
      "nt_dt": "23-09-2016",
      "val": 123123,
      "pos": "03",
      "srctyp": "e-Invoice",
      "irn": "897ADG56RTY78956HYUG90BNHHIJK453GFTD99845672FDHHHSHGFH4567FG56TR",
      "irngendate": "24-12-2019",
      "einvstatus": "ACT",
      "autodft": "Auto-population failed",
      "autodftdt": "24-12-2019",
      "errorCd": "RT123",
      "errorMsg": "Error in AutoDraft",
      "itms": [
        {
          "num": 1,
          "itm_det": {
            "rt": 10,
            "txval": 5225.28,
            "iamt": 845.22,
            "csamt": 789.52
          }
        }
      ]
    }
  ],
  "exp": [
    {
      "exp_typ": "WPAY",
      "inv": [
        {
          "chksum": "ASDFGJKLPTBBJKBJKBBJKBB",
          "inum": "81542",
          "idt": "12-02-2016",
          "val": 995048.36,
          "sbpcode": "ASB991",
          "sbnum": "7896542",
          "sbdt": "04-10-2016",
          "srctyp": "e-Invoice",
          "irn": "897ADG56RTY78956HYUG90BNHHIJK453GFTD99845672FDHHHSHGFH4567FG56TR",
          "irngendate": "24-12-2019",
          "einvstatus": "ACT",
          "autodft": "Auto-population failed",
          "autodftdt": "24-12-2019",
          "errorCd": "RT123",
          "errorMsg": "Error in AutoDraft",
          "itms": [
            {
              "txval": 10000,
              "rt": 5,
              "iamt": 833.33,
              "csamt": 100
            }
          ]
        }
      ]
    },
    {
      "exp_typ": "WOPAY",
      "inv": [
        {
          "chksum": "ASDFGJKLPTBBJKBJKBBJKBB",
          "inum": "81542",
          "idt": "12-02-2016",
          "val": 995048.36,
          "sbpcode": "ASB881",
          "sbnum": "7896542",
          "sbdt": "04-10-2016",
          "srctyp": "e-Invoice",
          "irn": "897ADG56RTY78956HYUG90BNHHIJK453GFTD99845672FDHHHSHGFH4567FG56TR",
          "irngendate": "24-12-2019",
          "einvstatus": "ACT",
          "autodft": "Auto-population failed",
          "autodftdt": "24-12-2019",
          "errorCd": "null",
          "errorMsg": "null",
          "itms": [
            {
              "txval": 10000,
              "rt": 5,
              "iamt": 325,
              "csamt": 100
            }
          ]
        }
      ]
    }
  ],
  "cdnr": [
    {
      "ctin": "01AAAAP1208Q1ZS",
      "trdname": "E-Invoicer",
      "nt": [
        {
          "chksum": "adsdsfsjskssssq",
          "ntty": "C",
          "nt_num": "533515",
          "nt_dt": "23-09-2016",
          "val": 123123,
          "pos": "03",
          "rchrg": "Y",
          "inv_typ": "DE",
          "srctyp": "e-Invoice",
          "irn": "897ADG56RTY78956HYUG90BNHHIJK453GFTD99845672FDHHHSHGFH4567FG56TR",
          "irngendate": "24-12-2019",
          "einvstatus": "ACT",
          "autodft": "Auto-population failed",
          "autodftdt": "24-12-2019",
          "errorCd": "RT123",
          "errorMsg": "Error in AutoDraft",
          "itms": [
            {
              "num": 1,
              "itm_det": {
                "rt": 10,
                "txval": 5225.28,
                "iamt": 845.22,
                "camt": 0,
                "samt": 0,
                "csamt": 789.52
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

The above response is same as the response recieved from the folllowing: 

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