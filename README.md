# User Onboarding API

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

#  Signup Process

    [Signup Flow](images/UserProvisioning_EzyReach.png)
