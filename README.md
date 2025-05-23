#!/bin/bash

#Set variables
Username="my-new-user"
Password="Strong@123"
#Policy to be given for the User
Policy_ARN="arn:aws:iam::aws:policy/AdministratorAccess"

#Create IAM User
aws iam create-user --username "$Username"

#Attach Policy
aws iam attach-user-policy \--user-name "$Username" \--policy-arn "$Policy_ARN"

#Create access for Programmatic approach
aws iam create-access-key --user-name "$Username" > "${Username}_creds.json"

#Create login profile (for AWS Console access)
aws iam create-login-profile \--user-name "$Username" \--password "$Password"

#Output
echo "IAM User '$Username' created."
echo "Access keys stored in ${Username}_creds.json"
echo "Console password is '$Password'."
