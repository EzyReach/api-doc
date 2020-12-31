# Entity Sources

There are three sources of information:
1. User - The data to be entered by the user manually
2. GST - The data that is fetched from the GST portal using user's GSTIN
3. LSP - The data that the LSP itself is providing



## 1. User Onboarding

|Fields   |Source|Comment|
|---------|:----:|:------|
|username |USER  |username is same as user's email|
|password |USER  |
|mobile   |USER  |



## 2. User profiling (Borrower)

|Fields        |Source|Comment|
|--------------|:----:|:------|
|gstin         |USER  ||
|primary id    |Unknown|Either USER or GST|
|primaryIdType |Unknown|PAN, AADHAR, MOBILE - Either USER or GST|
|name          |Unknown|Either USER or GST
|category      |LSP    |Category to be hardcoded as ORGANIZATION|
|Contact detail|Unknown|Either USER or GST|
|documents     |GST|   ||



## 3. Loan Application

|Fields           |Source|Comment|
|-----------------|:----:|:------|
|createDate       |LSP||
|loanApplicationId|LSP||
|type             |LSP|Hardcoded as CASHFLOW|
|borrower         |LSP & USER||
|collaterals      |LSP & GST||
|terms            |LSP||



## 4. Collateral

|Fields                 |Source|Comment|
|-----------------------|:----:|:------|
|collateralPrimaryId    |GST   |Format: <GSTIN>_<INVOICENUM>|
|collateralPrimaryIdType|LSP   |Harcoded as GST_INVOICE|
|type                   |LSP   |Harcoded as GST_INVOICE
|documents              |GST   |B2B GST Invoice|



## Terms

|Fields           |Source|Comment|
|-----------------|:----:|:------|
|requestedAmount  |USER  ||
|currency         |LSP   |Hardcoded as INR|