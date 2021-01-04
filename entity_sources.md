# Entity Sources

There are three sources of information:
1. User - The data to be entered by the user manually
2. GST - The data that is fetched from the GST portal using user's GSTIN
3. LSP - The data that the LSP itself is providing



## 1. User Onboarding

### A. User SignUp

|Fields   |Source|Comment|
|---------|:----:|:------|
|user_id  |LSP   |UUID|
|username |USER  |username is same as user's email|
|password |USER  |Stored after hashing|
|mobile   |USER  |Optional|



### B. User profiling (Borrower's details)
User type - GSTIN based

|Fields        |Source |Comment|
|--------------|:-----:|:------|
|borrower_id   |LSP    |UUID|
|gstin         |USER   ||
|primary id    |Unknown|Either USER or GST|
|primaryIdType |Unknown|PAN, AADHAR, MOBILE - Either USER or GST|
|name          |Unknown|Either USER or GST|
|category      |LSP    |Category to be hardcoded as ORGANIZATION|
|Contact detail|Unknown|Either USER or GST|
|documents     |GST|   ||



## 2. Create Loan Application

### A. LoanApplication

|Fields           |Source|Comment|
|-----------------|:----:|:------|
|createDate       |LSP||
|loanApplicationId|LSP||
|type             |LSP|Hardcoded as CASHFLOW|
|borrower         |LSP & USER||
|collaterals      |LSP & GST||
|terms            |LSP||



### B. Collateral

|Fields                 |Source|Comment|
|-----------------------|:----:|:------|
|collateralPrimaryId    |GST   |Format: (GSTIN)_(INVOICENUM)|
|collateralPrimaryIdType|LSP   |Harcoded as GST_INVOICE|
|type                   |LSP   |Harcoded as GST_INVOICE
|documents              |GST   |B2B GST Invoice|



### C. Terms

|Fields           |Source|Comment|
|-----------------|:----:|:------|
|requestedAmount  |USER  ||
|currency         |LSP   |Hardcoded as INR|


