# Loan Acceptance API

## Overview
The Object of Laon Acceptance API is to trigger and verify loan acceptance after loan application has been sent to the lender.

![alt text](https://github.com/iSPIRT/OCEN/blob/master/Sequence-Diagram/LoanAcceptanceAPIs.PNG "Loan Acceptance")

## /v3/loan/triggerLoanAcceptanceRequest

### schema of lenderOTPRequest

|Fields            |Type |Origin|comments|
|----------------  |:---:|:----:|-------:|
|metadata          |Object|LSP||
|requestId         |String|LSP||
|loanApplicationIds|List|LSP|List of loanApplication Ids for which Loan Acceptance Request has to be triggered|
|credBlock         |Object|LSP||

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
|Fields            |Type |Origin|comments|
|----------------  |:---:|:----:|-------:|
|type              |String-enum||String is "OTP"|
|data              |Object||object is of type OTPBlock|

### OTPBlock
|Fields            |Type |Origin|comments|
|----------------  |:---:|:----:|-------:|
|appToken          |String|||
|otpSessionKey     |String|||
|maskedPhoneNumber |String||Phone number of the applicant|
|url               |String|||
|extensibleData    |String|||
|otp               |String|||
|status            |String-enum|||


---
## /v3/loan/triggerLoanAcceptanceResponse

### schema of lenderOTPResponse

|Fields            |Type |Origin|comments|
|----------------  |:---:|:----:|-------:|
|metadata          |Object|LSP||
|response          |Object|LSP|response is an object in the format {error:"string"}, eg. {"error":"0"}|
|requestId         |String|LSP||
|credBlock         |Object|||


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
|Fields          |Type |Origin|comments|
|----------------|:---:|:----:|-------:|
|metadata        |Object|LSP|...|
|requestId       |String|LSP||
|credBlock       |Object|LSP||



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

|Fields          |Type |Origin|comments|
|----------------|:---:|:----:|-------:|
|metadata        |Object|LSP|...|
|requestId       |String|LSP||
|credBlock       |Object|LSP||
|response        |Object|Lender||