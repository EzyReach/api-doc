# Authentication API

## Overview
The objective of the Authentication APIs is to establish a secure authenticated session for all subsequent interactions with the GST System
## Request Headers

| Attributes | Description | Sample |
| ---------- | -----------| --------|
| ClientId | Client Identification for authentication. This is the identifier generated in API developer portal and mapped to an application. This is also called API Key and API usage is monitored at API key level.|l7xxf9d8151153954559b5d071bbd139f610|
| ClientSecret | Secret code for the API client. This API password is generated in API developer portal. Along with clientid, client-secret needs to be included in each request to access GST API.API consumer can regenerate client-secret through API| 3c7a20b8fd79422da20f495134d8eeb0|
| state-cd | State code to which the Tax Payer belongs to|11 (e.g. for Sikkim)|
|ip-usr	| Public IP Address of end user who requested access to data will be passed by GSP application or application accessing Taxpayer services. Access System will capture IP Address of calling application.|137.232.3.35|
|txn | Unique Transaction ID associated with the request |LAPN24235325555|

## Request For OTP
User using LSP application will be authenticated asynchronously using OTP. OTP Request API is used by the LSP to initiate the issue of OTP to user.After the successful verification of request parameters, GST system sends the OTP to the users primary business credentials through Email and SMS
- POST : https://api-domain-name/taxpayerapi/v1.0/authenticate
- Content Type: application/json
- #### Request Payload
```sh
{
"action": "OTPREQUEST",
"app_key": "48Kw7zR3L9nsbBJI3BJBmg8K0cx/XoGzR6uJHcBCuEPUlBTDPLochguhJk1DTvvHYQqQwaU0yhOqfZHgalD9sGMikaEBmY7Y1YcjP5drvwhmmcqQmCLK3D1FE18ditvlqV4DWou5feLM07QwWTj/i8mDwc5YgWz0cYnr6r7wnd2nlbmMxdHOYbKjOP6SxOdD2Gb6GZDI5+RFkkfGSPKwtvXR9NfZQaLaTIY1w8O0X0NI56C9oqjcqT5+FgdpTnLYc3rodHJuEFVgqfeTpWSk3QfAcnQg9P1N9Azcx2OI+AXbLLhcLLbSpfveelhaK02uEdUDYgGHfztr//9RPfqOzg==",
"username": "testUser"
}
```
- #### Response Payload
```sh
{
  "status_cd": "1"
}
```
- ##### Error Codes
| Error Code | Description |
| ------ | ------ |
| AUTH4032 | Invalid USER|
| AUTH4033 | Invalid Session|
| AUTH4034 | Invalid OTP|
| AUTH4036 | Invalid App Key|
| AUTH4037 | API Access Denied|
| AUTH4038 | Session Expired|
| AUTH4039 | Invalid Data Object|
| AUTH4040 | Malformed Request Detected|
| AUTH4041 | Invalid State Code|
| TEC4001 | Technical Error|
| TEC4002 | Invalid Data Format|
| TEC4003 | Invalid AppKey|
| SWEB9002 | Invalid User ID or Password. Please try again.|
| SWEB9033 | Your Password has expired. Please change your password.|
| SWEB9035 | IAccount is Locked.|
| GEN5001 | Missing Mandatory Params|
| AUT4031 | Client ID is Null|
| AUT4033 | Invalid Client ID|
| AUT4032 | Client-Secret is Null|
| AUT4034 | Invalid Client-Secret|
| GEN5007 | Malformed Request|
| RET11402 | Unauthorized User!|