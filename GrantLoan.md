# Grant Loan

## Overview
The objective of Grant Loan API is to approve loan and answer various queries regarding the loan application.

![alt text](https://github.com/iSPIRT/OCEN/blob/master/Sequence-Diagram/GrantLoan.PNG "Grant Loan")

## /v3/loan/grantLoanRequest

### Request Body

|Fields           |Type |Origin|comments|mandatory?|
|---------------- |:---:|:----:|-------:|---------:|
|metadata         |Object|LSP|||
|requestId        |String|LSP|||
|loanApplicationId|String|LSP|This was sent to the lender through **createLoanApplicationsRequest**||





---
## /v3/loan/grantLoanResponse

### Request Body

|Fields          |Type |Origin|comments|mandatory?|
|----------------|:---:|:----:|-------:|---------:|
|metadata        |Object|LSP|||
|response        |Object|Lender|||
|requestId       |String|LSP|||
|loanId          |String||||
|loanStatus      |String-enum|Lender|eg PROCESSING||
|terms           |Object||||
|repayment       |Object||||
|disbursement    |String|LSP|||





---
## /v3/loan/loanSummaryRequest
### Request Body

|Fields          |Type |Origin|comments|mandatory?|
|----------------|:---:|:----:|-------:|---------:|
|metadata        |Object|LSP|||
|loanId          |String|LSP|||
|requestId       |String|LSP|||





---
## /v3/loan/loanSummaryResponse

### Request Body

|Fields          |Type |Origin|comments|mandatory?|
|----------------|:---:|:----:|-------:|---------:|
|metadata        |Object|LSP|||
|response        |Object|Lender|||
|requestId       |String|LSP|||
|loanId          |String||||
|loanStatus      |String-enum||||
|createDate      |DateTime||||
|startDate       |DateTime||||
|endDate         |String|LSP|||
|summary         |String||||





---
## /v3/loan/getLoanRequest
### Request Body

|Fields          |Type |Origin|comments|mandatory?|
|----------------|:---:|:----:|-------:|---------:|
|metadata        |Object|LSP|||
|loanId          |String|LSP|||
|requestId       |String|LSP|||






---
## /v3/loan/getLoanResponse

### Request Body

|Fields          |Type |Origin|comments|mandatory?|
|----------------|:---:|:----:|-------:|---------:|
|metadata        |Object|LSP|||
|response        |Object|Lender|||
|requestId       |String|LSP|||
|loanId          |String||||
|loanStatus      |String-enum||||
|createDate      |DateTime||||
|startDate       |DateTime||||
|endDate         |String|LSP|||
|type            |String-enum||CASHFLOW, PERSONAL, HOME, VEHICLE, BUSINESS||
|lender          |Object||||
|collateral      |List||||
|guarantors      |List||||
|applicants      |List||||
|terms           |Object||||
|disbursement    |Object||||
|repayment       |Object||||





---
## /v3/loan/loanStatementRequest

### Request Body

|Fields          |Type |Origin|comments|mandatory?|
|----------------|:---:|:----:|-------:|---------:|
|metadata        |Object|LSP|||
|loanId          |String||||
|requestId       |String|LSP|||





---
## /v3/loan/loanStatementResponse

### Request Body

|Fields          |Type |Origin|comments|mandatory?|
|----------------|:---:|:----:|-------:|---------:|
|metadata        |Object|LSP|||
|loanId          |String|LSP|||
|requestId       |String|LSP|||
|response        |Object|Lender|||
|accountStatement|Object|Lender|schema: Transaction||

#### Transaction (Schema for accountStatement)

```
"accountStatement": {
    "date": "2020-03-01T00:00:00Z",
    "narration": "Repayment of Loan no : xxxxxxx9090",
    "txnRefNo": "004618602124",
    "amount": "50000.00",
    "type": "DEPOSIT",
    "closingBalance": "50000.00",
    "url": null,
    "extensibleData": null
  }
 ```

|Fields          |Type |Origin|comments|mandatory?|
|----------------|:---:|:----:|-------:|---------:|
|date            |DateTime||||
|narration       |String||Details of the transaction||
|txnRefNo        |String||||
|amount          |float||||
|type            |String-enum||DEPOSIT,WITHDRAWAL||
|closingBalance  |float||||


---
## /v3/loan/listLoansRequest

### Request Body

|Fields          |Type |Origin|comments|mandatory?|
|----------------|:---:|:----:|-------:|---------:|
|metadata        |Object|LSP|||
|borrower        |Object|LSP|||
|requestId       |String|LSP|||






---
## /v3/loan/listLoansResponse

### Request Body

|Fields          |Type |Origin|comments|mandatory?|
|----------------|:---:|:----:|-------:|---------:|
|metadata        |Object|LSP||
|response        |Object|Lender||
|requestId       |String|LSP||
|loans           |List||Schema: loanDetail|

### loanDetail
|Fields          |Type |Origin|comments|mandatory?|
|----------------|:---:|:----:|-------:|---------:|
|loanId          |String|||
|terms           |Object|||