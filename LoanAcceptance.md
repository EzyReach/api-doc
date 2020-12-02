# Loan Acceptance API

## Overview
The Object of Laon Acceptance API is to trigger and verify loan acceptance after loan application has been sent to the lender.

![alt text](https://github.com/iSPIRT/OCEN/blob/master/Sequence-Diagram/LoanAcceptanceAPIs.PNG "Loan Acceptance")

## /v3/loan/triggerLoanAcceptanceRequest

### schema of lenderOTPRequest

|Fields            |Type |Origin|comments|mandatory?|
|----------------  |:---:|:----:|:-------|---------:|
|metadata          |Object|LSP||Y|
|requestId         |String|LSP||Y|
|loanApplicationIds|List|LSP|List of loanApplication Ids for which Loan Acceptance Request has to be triggered|Y|
|credBlock         |Object|LSP||Y|

```
"credBlock": {
    "type": "OTP",
    "data": {
      "appToken": "0aBCD7DMr7s",
      "otpSessionKey": null,
      "maskedPhoneNumber": null,
      "url": null,
      "extensibleData": null,
      "otp": null,
      "status": null
    }
  }
```
### credBlock
|Fields            |Type |Origin|comments|mandatory?|
|----------------  |:---:|:----:|:-------|---------:|
|type              |String-enum||String is "OTP"|Y|
|data              |Object||schema: OTPBlock|Y|

### OTPBlock
|Fields            |Type |Origin|comments|mandatory?|
|----------------  |:---:|:----:|:-------|---------:|
|appToken          |String|||N|
|otpSessionKey     |String|||N|
|maskedPhoneNumber |String||Phone number of the applicant|N|
|url               |String|||N|
|extensibleData    |String|||N|
|otp               |String|||N|
|status            |String-enum||SUCCESS, INCORRECT_OTP, INVALID_SESSION|N|


---
## /v3/loan/triggerLoanAcceptanceResponse

### schema of lenderOTPResponse

|Fields            |Type |Origin|comments|mandatory?|
|----------------  |:---:|:----:|:-------|---------:|
|metadata          |Object|LSP||Y|
|response          |Object|LSP|eg. {"error":"0"}|Y|
|requestId         |String|LSP||Y|
|credBlock         |Object|||Y|


```
"credBlock": {
    "type": "OTP",
    "data": {
      "appToken": null,
      "otpSessionKey": "e8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
      "maskedPhoneNumber": "xxxxxx9090",
      "url": null,
      "extensibleData": null,
      "otp": null,
      "status": null
    }
  }
```

---
## /v3/loan/verifyLoanAcceptanceRequest

### schema of VerifyLenderOTPRequest

```
"credBlock": {
    "type": "OTP",
    "data": {
      "appToken": null,
      "otpSessionKey": "e8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
      "maskedPhoneNumber": null,
      "url": null,
      "extensibleData": null,
      "otp": "689451",
      "status": null
    }
  }
```
|Fields          |Type |Origin|comments|mandatory?|
|----------------|:---:|:----:|:-------|---------:|
|metadata        |Object|LSP||Y|
|requestId       |String|LSP||Y|
|credBlock       |Object|||Y|



---
## /v3/loan/verifyLoanAcceptanceResponse

### schema of VerifyLenderOTPResponse

```
"credBlock": {
    "type": "OTP",
    "data": {
      "appToken": null,
      "otpSessionKey": "e8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
      "maskedPhoneNumber": null,
      "url": null,
      "extensibleData": null,
      "otp": null,
      "status": "SUCCESS"
    }
  }
```

|Fields          |Type |Origin|comments|mandatory?|
|----------------|:---:|:----:|:-------|---------:|
|metadata        |Object|LSP|...|Y|
|requestId       |String|LSP||Y|
|credBlock       |Object|||Y|
|response        |Object|Lender||Y|