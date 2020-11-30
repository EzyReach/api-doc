# Loan Application API


![alt text](https://github.com/iSPIRT/OCEN/blob/master/Sequence-Diagram/LoanApplication.PNG "Loan Application")

![alt text](https://github.com/nirmal3047/OCEN-Documentation/blob/master/createLoanApplicationRequest.PNG "createLoanApplicationsRequest Flow Diagram")

![alt text](https://github.com/nirmal3047/OCEN-Documentation/blob/master/loanApplication.PNG "loanApplication Fields")

## /v3/loanApplication/createLoanApplicationsRequest

### Response

### ACK
|Fields          |Type |Origin|comments|
|----------------|:---:|:----:|-------:|
|error           |String|Lender|...|
|traceId         |String|Lender|...|
|timestamp       |dateTime|Lender|...|

### Request Body

|Fields          |Type |Origin|comments|
|----------------|:---:|:----:|-------:|
|metadata        |...|LSP|...|
|requestId       |String|LSP|...|
|loanApplications|Array|LSP|Array of each Loan Application where each of them is an object|


### metadata
|Fields|Type |Origin|comments|
|------|:---:|-----:|-------:|
|version|String|...|...|
|timestamp|DateTime|LSP|...|
|traceId|String|Unknown|...|
|orgId|String|LSP|...|


### loanApplication
|Fields           |Type |Origin|comments|
|------           |:---:|-----:|-------:|
|createDate       |String|LSP|...|
|loanApplicationId|DateTime|LSP|...|
|offers           |String|Unknown|...|
|type             |String-enum|LSP|...|...|
|borrower         |Object|LSP|The data  of borrower could be stored in the LSP database when the signup|
|collaterals      |Array|LSP|...|
|guarantors       |Array|LSP|...|
|applicants       |Array|LSP|...|
|terms            |Object|LSP|...|


#### borrower
|Fields               |Type |Origin|comments|
|------               |:---:|-----:|-------:|
|primaryId            |String|...||
|primaryIdType        |String-enum|...||
|secondaryId          |String|||
|additionalIdentifiers|Array|||
|name                 |String|||
|category             |String-enum|||
|contactDetails       |Object|||
|platformData         |...|||
|documents            |Array|||

#### collateral
|Fields                 |Type |Origin|comments|
|------                 |:---:|-----:|-------:|
|collateralPrimaryId    |String|||
|collateralPrimaryIdType|String-menu|||
|type                   |String|||
|additionalIdentifiers  |Array|||
|valuation              |Object|||
|parties                |Array|||
|documents              |Array|||

#### applicants
|Fields               |Type |Origin|comments|
|------               |:---:|-----:|-------:|
|primaryIdType        |String-enum|||
|primaryId            |String|||
|category             |String-enum|||
|contactDetails       |Object|||
|additionalIdentifiers|Array|||
|documents            |Array|||

### guarantors
|Fields                  |Type |Origin|comments|
|------                  |:---:|-----:|-------:|
|priamryId               |String|||
|primaryIdType           |String-enum|||
|category                |String-enum|||
|contactDetails          |Object|||
|relationshipWithBorrowe |String|||
|additionalIdentifiers   |Array|||
|documents               |Array|||

---

## /v3/loanApplication/createLoanApplicationsResponse

### ACK
|Fields          |Type |Origin|comments|
|----------------|:---:|:----:|-------:|
|error           |String|LSp|...|
|traceId         |String|LSP|...|
|timestamp       |dateTime|LSP|...|

### Request Body
|Fields          |Type |Origin|comments|
|----------------|:---:|:----:|-------:|
|metadata        |...|LSP|...|
|response        |Lender|||
|requestId       |String|LSP|...|
|loanApplications|Array|LSP|...|
|lender          |Object|Lender||

### lender
|Fields               |Type |Origin|comments|
|----------------     |:---:|:----:|-------:|
|primaryIdType        |String-enum|||
|primaryId            |String|||
|category             |String-enum|||
|contactDetails       |Object|||
|additionalIdentifiers|Array|||
|documents            |Array|||