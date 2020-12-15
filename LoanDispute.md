# Loan Dispute API

## Overview
The purspose of Laon Dispute API is to resolve any arising disputes

## /v3/loan/dispute/raiseDisputeRequest
Raises a new dispute
```
{
  "metadata": {
    "version": "1.0",
    "timestamp": "2018-12-06T11:39:57.153Z",
    "traceId": "e8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
    "orgId": "LSP123"
  },
  "loanId": "e8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
  "requestId": "e8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
  "dispute": {
    "id": null,
    "description": "Amount not disbursed to the account yet",
    "url": null,
    "status": null,
    "extensibleData": null
  }
}
```
|Fields   |Type |Origin|comments|mandatory?|
|---------|:---:|:----:|:------:|---------:|
|metadata |Object|LSP||Y|
|loanId   |String|LSP|The id of loan for which the dispute is being raised|Y|
|requestId|String|LSP||Y|
|dispute  |Object|LSP|The details of the dispute|Y|

### Dispute
|Fields         |Type |Origin|comments|mandatory?|
|---------------|:---:|:----:|:------:|---------:|
|id             |String|Lender||Y|
|lenderDisputeId|String|||N|
|lenderId       |String|Lender||Y|
|loanId         |String|LSP||Y|
|description    |String|LSP||Y|
|status         |String-enum|Lender|NEW, PROCESSING, NEEDMOREINFO, RESOLVED, CLOSED|Y|
|url            |String|Lender|URL where dispute progress can be tracked|N|
|extensibleData |String|||N|

---

## /v3/loan/dispute/raiseDisputeResponse
The lender responds with the required information against the dipute raised
```
{
  "metadata": {
    "version": "1.0",
    "timestamp": "2018-12-06T11:39:57.153Z",
    "traceId": "e8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
    "orgId": "FIU123"
  },
  "response": {
    "error": "0"
  },
  "requestId": "e8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
  "dispute": {
    "id": "e8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
    "description": null,
    "status": "NEED_MORE_INFO",
    "url": "URL where dispute progress can be tracked",
    "extensibleData": null
  }
}
```
|Fields   |Type |Origin|comments|mandatory?|
|---------|:---:|:----:|:------:|---------:|
|metadata |Object|Lender||Y|
|loanId   |String|LSP||Y|
|requestId|String|||Y|
|dispute  |Object|Lender||Y|

---

## /v3/loan/dispute/disputeStatusRequest
LSP request the Lender to provide the stauts of the dispute with given dispute Id
```
{
  "metadata": {
    "version": "1.0",
    "timestamp": "2018-12-06T11:39:57.153Z",
    "traceId": "e8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
    "orgId": "LSP123"
  },
  "requestId": "e8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
  "dispute": {
    "id": "e8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
    "description": null,
    "url": null,
    "status": null,
    "extensibleData": null
  }
}
```
|Fields   |Type |Origin|comments|mandatory?|
|---------|:---:|:----:|:------:|---------:|
|metadata |Object|LSP||Y|
|requestId|String|LSP||Y|
|dispute  |Object|LSP||Y|

---

## /v3/loan/dispute/disputeStatusResponse
Lender sends the status of the dispute with given dispute Id to the LSP
```
{
  "metadata": {
    "version": "1.0",
    "timestamp": "2018-12-06T11:39:57.153Z",
    "traceId": "e8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
    "orgId": "FIU123"
  },
  "response": {
    "error": "0"
  },
  "requestId": "e8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
  "dispute": {
    "id": "e8cc6822bd4bbb4eb1b9e1b4996fbff8acb",
    "description": null,
    "url": null,
    "status": "CLOSED",
    "extensibleData": null
  }
}
```
|Fields          |Type |Origin|comments|mandatory?|
|---------|:---:|:----:|:------:|---------:|
|metadata |Object|Lender||Y|
|response |Object|Lender||Y|
|requestId|String|||Y|
|dispute  |Object|LSP||Y|