# Grant Loan

![alt text](https://github.com/iSPIRT/OCEN/blob/master/Sequence-Diagram/GrantLoan.PNG "Grant Loan")

## /v3/loan/grantLoanRequest

### Request Body

|Fields          |Type |Origin|comments|
|----------------|:---:|:----:|-------:|
|metadata        |...|LSP|...|
|requestId       |String|LSP|...|
|loanApplicationId|String|LSP|This was sent to the lender through **createLoanApplicationsRequest**|





---
## /v3/loan/grantLoanResponse

### Request Body

|Fields          |Type |Origin|comments|
|----------------|:---:|:----:|-------:|
|metadata        |...|LSP|...|
|response        ||Lender||
|requestId       |String|LSP|...|
|loanId          ||||
|loanStatus      ||||
|terms           ||||
|repayment       ||||
|disbursement    |String|LSP||





---
## /v3/loan/loanSummaryRequest
### Request Body

|Fields          |Type |Origin|comments|
|----------------|:---:|:----:|-------:|
|metadata        |...|LSP|...|
|loanId          |String|||
|requestId       |String|LSP|...|





---
## /v3/loan/loanSummaryResponse

### Request Body

|Fields          |Type |Origin|comments|
|----------------|:---:|:----:|-------:|
|metadata        |...|LSP|...|
|response        |Object|Lender||
|requestId       |String|LSP|...|
|loanId          |String|||
|loanStatus      |String-enum|||
|createDate      |DateTime|||
|startDate       |DateTime|||
|endDate         |String|LSP||
|summary         |String





---
## /v3/loan/getLoanRequest
### Request Body

|Fields          |Type |Origin|comments|
|----------------|:---:|:----:|-------:|
|metadata        |...|LSP|...|
|loanId          |String|||
|requestId       |String|LSP|...|






---
## /v3/loan/getLoanResponse

### Request Body

|Fields          |Type |Origin|comments|
|----------------|:---:|:----:|-------:|
|metadata        |...|LSP|...|
|response        |Object|Lender||
|requestId       |String|LSP|...|
|loanId          |String|||
|loanStatus      |String-enum|||
|createDate      |DateTime|||
|startDate       |DateTime|||
|endDate         |String|LSP||
|type            ||||
|borrower        ||||
|lender          ||||
|collateral      ||||
|guarantors      ||||
|applicants      ||||
|terms           ||||
|disbursement    ||||
|repayment       ||||





---
## /v3/loan/loanStatementRequest

### Request Body

|Fields          |Type |Origin|comments|
|----------------|:---:|:----:|-------:|
|metadata        |...|LSP|...|
|loanId          |String|||
|requestId       |String|LSP|...|





---
## /v3/loan/loanStatementResponse

### Request Body

|Fields          |Type |Origin|comments|
|----------------|:---:|:----:|-------:|
|metadata        |...|LSP|...|
|loanId          |String|||
|requestId       |String|LSP|...|
|response        ||||
|accountStatement||||




---
## /v3/loan/listLoansRequest

### Request Body

|Fields          |Type |Origin|comments|
|----------------|:---:|:----:|-------:|
|metadata        |...|LSP|...|
|borrower        |Object|||
|requestId       |String|LSP|...|






---
## /v3/loan/listLoansResponse

### Request Body

|Fields          |Type |Origin|comments|
|----------------|:---:|:----:|-------:|
|metadata        |...|LSP|...|
|response        |Object|Lender||
|requestId       |String|LSP|...|
|loans           |Array||Schema: loanDetail|

### loanDetail
|Fields          |Type |Origin|comments|
|----------------|:---:|:----:|-------:|
|loanId          ||||
|terms           ||||