# Loan Acceptance API

![alt text](https://github.com/iSPIRT/OCEN/blob/master/Sequence-Diagram/LoanAcceptanceAPIs.PNG "Loan Acceptance")

## /v3/loan/triggerLoanAcceptanceRequest

### schema of lenderOTPRequest

|Fields            |Type |Origin|comments|
|----------------  |:---:|:----:|-------:|
|metadata          |...|LSP|...|
|requestId         |String|LSP|...|
|loanApplicationIds|List|LSP||
|credBlock         |Object|||


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
|maskedPhoneNumber |String|||
|url               |String|||
|extensibleData    |String|||
|otp               |String|||
|status            |String-enum|||


---
## /v3/loan/triggerLoanAcceptanceResponse

### schema of lenderOTPResponse

|Fields            |Type |Origin|comments|
|----------------  |:---:|:----:|-------:|
|metadata          |...|LSP|...|
|response          |Object|LSP|response is an object in the format {error:"string"}, eg. {"error":"0"}|
|requestId         |String|LSP||
|credBlock         |Object|||




---
## /v3/loan/verifyLoanAcceptanceRequest

### schema of VerifyLenderOTPRequest

|Fields          |Type |Origin|comments|
|----------------|:---:|:----:|-------:|
|metadata        |...|LSP|...|
|requestId       |String|LSP|...|
|credBlock       |Object|LSP|...|



---
## /v3/loan/verifyLoanAcceptanceResponse

### schema of VerifyLenderOTPResponse

|Fields          |Type |Origin|comments|
|----------------|:---:|:----:|-------:|
|metadata        |...|LSP|...|
|requestId       |String|LSP|...|
|credBlock       |Object|LSP|...|
|response        |Object|Lender||