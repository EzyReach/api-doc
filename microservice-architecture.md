# Proposed Microservice Archtecture

## User Onboarding
1. User Registration


#### The following points need clarification:
1. Will there be an option for login to admin? If yes, what actions will admin perform?

2. Where will user get AA id? Does he/she need to register on AA app first before registering to LSP app?

3. Format of response payload from AA?

4. Will AA directly send user details to Lender? If yes, then where would the data to be sent in createLoanApplication come from?

5. What is the "document" sent in createLoanApplication?
Base64 encoded
```
"data": "eyJzdGpDZCI6IkFQMDAzIiwibGdubSI6Ik1TIENPUlBPUkFUSU9OIiwic3RqIjoiQkNQIEtPRElLT05EQSIsImR0eSI6IlJlZ3VsYXIiLCJjeGR0IjoiIiwiZ3N0aW4iOiIwNUFCTlRZMzI5MFA4WkEiLCJuYmEiOlsiQm9uZGVkIFdhcmVob3VzZSIsIkVPVSAvIFNUUCAvIEVIVFAiLCJGYWN0b3J5IC8gTWFudWZhY3R1cmluZyIsIklucHV0IFNlcnZpY2UgRGlzdHJpYnV0b3IgKElTRCkiLCJMZWFzaW5nIEJ1c2luZXNzIl0sImxzdHVwZHQiOiIwNS8wMS8yMDE3IiwicmdkdCI6IjA1LzA1LzIwMTciLCJjdGIiOiJGb3JlaWduIExMUCIsInN0cyI6IlByb3Zpc2lvbmFsIiwiY3RqQ2QiOiJBUDAwNCIsImN0aiI6IkJDUCBUSFVNTUFLVU5UQSIsInRyYWRlTmFtIjoiQUxUT04gUExBU1RJQyBQUklWQVRFIExURCIsImFkYWRyIjpbeyJhZGRyIjp7ImJubSI6IkVMUEhJTlNUT05FIEJVSUxESU5HIiwic3QiOiIxMCwgVkVFUiBOQVJJTUFOIFJPQUQiLCJsb2MiOiJGT1JUIiwiYm5vIjoiMTAiLCJzdGNkIjoiUmFqYXN0aGFuIiwiZmxubyI6IjFTVCBGTE9PUiIsImx0IjoiNzQuMjE3OSIsImxnIjoiMjcuMDIzOCIsInBuY2QiOiI0MDAwMDEifSwibnRyIjpbIldob2xlc2FsZSBCdXNpbmVzcyJdfV0sInByYWRyIjp7ImFkZHIiOnsiYm5tIjoiS0FUR0FSQSBIT1VTRSIsInN0IjoiMTUsIEwgSkFHTU9IQU5EQVMgTUFSRyIsImxvYyI6Ik1BTEFCQVIgSElMTCIsImJubyI6IjUiLCJzdGNkIjoiTWFoYXJhc2h0cmEiLCJmbG5vIjoiNFRIIEZMT09SIiwibHQiOiI3NC4yMTc5IiwibGciOiIyNy4wMjM4IiwicG5jZCI6IjQwMDAwNiJ9LCJudHIiOlsiV2hvbGVzYWxlIEJ1c2luZXNzIl19fQ=="
```

Base64 decoded
```
{
  "stjCd":"AP003",
  "lgnm":"MS CORPORATION",
  "stj":"BCP KODIKONDA",
  "dty":"Regular",
  "cxdt":"",
  "gstin":"05ABNTY3290P8ZA",
  "nba":["Bonded Warehouse","EOU / STP / EHTP","Factory / Manufacturing","Input Service Distributor (ISD)",
  "Leasing Business"],
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
      "bnm":"KATGARA HOUSE","st":"15,L JAGMOHANDAS MARG",
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