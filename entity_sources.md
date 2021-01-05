# Entity Sources

There are four sources of information:
1. USER - The data to be entered by the user manually
2. GST - The data that is fetched from the GST portal using user's GSTIN
3. LSP - The data that the LSP itself is providing
4. LENDER - The data received from lenders



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
|gstin         |USER   |15 character GST identification number|
|primary id    |Unknown|Either USER or GST|
|primaryIdType |Unknown|PAN, AADHAR, MOBILE - Either USER or GST|
|name          |Unknown|Either USER or GST|
|category      |LSP    |Category to be hardcoded as ORGANIZATION|
|contact detail|GST    |Details received from GST would be mapped according to ContactDetail schema (as per OCEN's specification)|
|documents     |GST|   ||


### C. User Action History
|Fields    |Source|Comment|
|----------|:----:|:------|
|session_id|LSP   |UUID|
|user_id   |LSP   ||
|device_id |LSP   ||
|start_time|LSP   ||
|end_time  |LSP   ||
|mode      |LSP   |APP or WEB|


### D. Device
|Fields        |Source|Comment|
|--------------|:----:|:------|
|device_id     |LSP   |UUID
|device_type   |LSP   |MOBILE, COMPUTER, TAB|
|device_address|LSP   |MAC address|




## 2. Loan Lending

### I. Create Loan Application

#### A. LoanApplication

|Fields           |Source|Comment|
|-----------------|:----:|:------|
|createDate       |LSP||
|loanApplicationId|LSP||
|type             |LSP|Hardcoded as CASHFLOW|
|borrower         |LSP & USER||
|collaterals      |LSP & GST||
|terms            |LSP||
|offer            |LENDER||



#### B. Collateral

|Fields                 |Source|Comment|
|-----------------------|:----:|:------|
|collateralPrimaryId    |GST   |Format: (GSTIN)_(INVOICENUM)|
|collateralPrimaryIdType|LSP   |Harcoded as GST_INVOICE|
|type                   |LSP   |Harcoded as GST_INVOICE
|documents              |GST   |B2B GST Invoice|



#### C. Terms

|Fields           |Source|Comment|
|-----------------|:----:|:------|
|requestedAmount  |USER  ||
|currency         |LSP   |Hardcoded as INR|


#### D. Document

|Fields          |Source|Comment|
|----------------|:----:|:------|
|format          |LSP   |Hardcoded as JSON|Y|
|reference       |LSP   |35 characters alphanumeric string|
|source          |LSP   |Hardcoded as GSTN|
|sourceIdentifier|LSP   |Hardcoded as GSTN|Y|
|type            |LSP   |Hardcoded as GSTN_PROFILE|
|isDataInline    |LSP   |Hardcoded as true|
|data            |GST   |Base64 encoded fetched from GST Search Taxpayer API|


### II. Loan Offers

### III. Loan Acceptance

### IV. Grant Loan




## Consent Handling




## Post Loan