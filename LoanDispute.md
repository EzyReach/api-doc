# Loan Dispute API

## Overview
The purspose of Laon Dispute API is to resolve any arising disputes

## /v3/loan/dispute/raiseDisputeRequest
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
|metadata |Object|||Y|
|loanId   |String|||Y|
|requestId|String|||Y|
|dispute  |Object|||Y|

### dispute
|Fields         |Type |Origin|comments|mandatory?|
|---------------|:---:|:----:|:------:|---------:|
|id             |String|||Y|
|lenderDisputeId|String|||N|
|lenderId       |String|||Y|
|loanId         |String|||Y|
|description    |String|||Y|
|status         |String-enum||NEW, PROCESSING, NEEDMOREINFO, RESOLVED, CLOSED|Y|
|url            |String|||N|
|extensibleData |String|||N|

---

## /v3/loan/dispute/raiseDisputeResponse
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
|metadata |Object|||Y|
|loanId   |String|||Y|
|requestId|String|||Y|
|dispute  |Object|||Y|

---

## /v3/loan/dispute/disputeStatusRequest
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
|metadata |Object|||Y|
|requestId|String|||Y|
|dispute  |Object|||Y|

---

## /v3/loan/dispute/disputeStatusResponse
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
|metadata |Object|||Y|
|response |Object|||Y|
|requestId|String|||Y|
|dispute  |Object|||Y|