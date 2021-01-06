# User Onboarding API
#  Signup process

![Signup Flow](/images/UserProvisioning_EzyReach.png)


## Overview
  The objective of Onboarding process is to create user in the user pool using AWS Cognito, verify the primary mode of the authentication and subsequently enriching user profile.
  In the current scenario:
    - Email address is used to handle the auth challenge.
    -  Profile enrichment is done via integrating with GST API
  The onboarding of the user can be categorised into three parts:
   - User Registration
       - User provides user information such as email address, Phone no, password
   - User Identity verify & User Creation
       - AWS Cognito will verify the email address
   - User Profile Update
       - Update user profile (In case of OCEN, it will talk to GST API)


## User Registration
-   User provides user information which includes:
    -   email address, Phone no, password
-   API Getway signup proxy will delegate the request to Cognito to validate the user email.
-   Cognito will use AWS Simple Email Service(SES) to send a code to the user email account
## User Identity verify & User Creation
-   Once user confirms the email code via API Gateway proxy (/signup/confirm),Cognito will create the user
-   Once done , user will be redirected to login page and thus obtailing id_token and access_token

## User Profile Create
-   User now can enter his GSTN no.This will be handled by API Gateway proxy /user/profile
-   The proxy will first verify the access token via cognito
-   It will fetch user details such as userName, email,phoneNo and will connect to provisioning microservice.
-   The Provisioning MS will request data from the GSTN API
-   Once user data is obtained a new record will be created in the user_profile record

See below sequence flow for above:

![Sequence Flow](/images/User_Provisioning _sequence.png)
