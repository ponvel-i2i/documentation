---
title: Tapgenes

language_tabs:
  - curl

toc_footers:
  - <a href='https://www.tapgenes.com' target="blank">Go to Site</a>

includes:
  - errors

search: true
---

# Introduction

## API reference

> API endpoint

```
https://tapgenes.com
```

Welcome to the Tapgenes API! You can use our API to access individuals and their families health and wealth endpoints, which can get person's personal information, relationship details and health details in our database.

TapGenes is designed to complement, not replace, the relationship between you and your financial advisor or physician. Our aim is to promote individual responsibility for health and wealth and not to offer financial or medical advice. The website is intended for a general audience.

# Authentication

## Login

> API Endpoint

```
POST https://tapgenes.com/ehr/v1/login
```

> Example Request

```curl
curl -X POST --header 'Content-Type: application/x-www-form-urlencoded' --header 'Accept: application/json' -d 'username=<USERNAME/EMAIL>&password=<PASSWORD>&fromsource=Tapgenes&clientId=<CLIENT_ID>&clientSecret=<CLIENT_SECRET>' 'https://tapgenes.com/ehr/v1/login'
```

> Make sure to replace the follows,

```
USERNAME/EMAIL - Valid email
PASSWORD - password
CLIENT_ID - your client id
CLIENT_SECRET - your client secret
```

> Example Response

```json
{
  "id": 1234,
  "email": "XXXXX@XXXX.com",
  "isActive": 1,
  "isAdmin": false,
  "environment": "Tapgenes",
  "accessToken": "0e4f70df-7d8b-4afc-9a35-39f72a322cf9",
  "lastAccessUTC": 1510052975657,
  "personDetailsEntity": {
    "id": 1234,
    "userId": 1234,
    "firstName": "Johny",
    "lastName": "Mamon",
    "fullName": "Johny Mamon",
    "dob": "1993-02-14",
    "isLiving": 1,
    "imgUrl": "https://graph.facebook.com/XXX/picture?type=large",
    "sex": "female",
    "relationshipStatus": "married",
    "accountCreator": 0,
    "isAdopted": 0
  },
  "fromSource": "Tapgenes",
  "isPremiumUser": false
}
```

Tapgenes use API keys (client id & client secret) to allow access to this API. You can login with your client credentials at our [site](https://www.tapgenes.com).

Tapgenes expects for the Access Token to be included in all API requests to the server in a header.

Parameter    | Description
------------ | -----------
username     | username/email which is used during registration
password     | password
source       | Tapgenes
clientId     | client ID
clientSecret | client secret

# User

## Create User

> API Endpoint

```
POST https://tapgenes.com/ehr/v1/user
```

> Example Request

```curl
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{
  "password": <PASSWORD>,
  "email": <USERNAME/EMAIL>,
  "isNewsLetterAccepted": true,
  "others": {"fromsource":"Tapgenes"},
  "clientId": <CLIENT_ID>,
  "clientSecret": <CLIENT_SECRET>
}' 'https://tapgenes.com/ehr/v1/user'
```
> Make sure to replace the follows,

```
USERNAME/EMAIL - Valid email
PASSWORD - password
CLIENT_ID - your client id
CLIENT_SECRET - your client secret
```

> Example Response

```json
{
  "id": 1234,
  "email": "XXXXX@XXXX.com",
  "isActive": 1,
  "environment": "Tapgenes",
  "accessToken": "0e4f70df-7d8b-4afc-9a35-39f72a322cf9",
  "lastAccessUTC": 1510052975657,
  "personDetailsEntity": {
    "id": 1234,
    "userId": 1234,
    "firstName": "XXXX",
    "isLiving": 1,
    "accountCreator": 0,
    "isAdopted": 0
  },
  "fromSource": "Tapgenes",
  "isPremiumUser": false
}
```

This endpoint is used to create or register new user.

Parameter    | Description
------------ | -----------
email     | username/email
password     | password
isNewsLetterAccepted | if you wants to receive Tapgenes news letter, set to true
others | It should be JSON object
clientId     | client ID
clientSecret | client secret

## Forgot Password

> API Endpoint

```
POST https://tapgenes.com/ehr/v1/user/forgotPassword
```

> Example Request

```curl
curl -X POST --header 'Content-Type: application/x-www-form-urlencoded' --header 'Accept: application/json' -d 'emailId=<USERNAME/EMAIL>' 'https://tapgenes.com/ehr/v1/user/forgotPassword'
```
> Make sure to replace the follows,

```
USERNAME/EMAIL - Valid email
```

> Example Response

```json
{
  "message": "Password Reset Link Sent"
}
```

This endpoint used to get the reset password link to the registered email.

Parameter    | Description
------------ | -----------
emailId     | email which was used during registration

## Reset Password

> API Endpoint

```
POST https://tapgenes.com/ehr/v1/user/resetPassword
```

> Example Request

```curl
curl -X POST --header 'Content-Type: application/x-www-form-urlencoded' --header 'Accept: application/json' -d 'newPassword=<PASSWORD>&confirmPassword=<CONFIRM_PASSWORD>&activationKey=<KEY>' 'https://tapgenes.com/ehr/v1/user/resetPassword'
```
> Make sure to replace the follows,

```
PASSWORD - new password
CONFIRM_PASSWORD - confirm password
KEY - key to reset password
```

> Example Response

```json
{
  "message": "Password Reset Completed"
}
```

This endpoint used to reset your password.

Parameter    | Description
------------ | -----------
newPassword     | New password
confirmPassword | Confirm password
activationKey | The activation key which was got in the mail during forgot password request

## Update Password

> API Endpoint

```
POST https://tapgenes.com/ehr/v1/user/updatePassword
```

> Example Request

```curl
curl -X POST --header 'Content-Type: application/x-www-form-urlencoded' --header 'Accept: text/plain' --header 'Authorization: OAuth2 <ACCESS_TOKEN>' -d 'oldPassword=<OLD_PASSWORD>&newPassword=<NEW_PASSWORD>&confirmPassword=<CONFIRM_PASSWORD>' 'https://tapgenes.com/ehr/v1/user/updatePassword'
```
> Make sure to replace the follows,

```
ACCESS_TOKEN - access token
NEW_PASSWORD - new password
CONFIRM_PASSWORD - confirm password
```

> Example Response

```json
{
  "message": "Password Updated"
}
```

This endpoint used to update your password.

Parameter    | Description
------------ | -----------
newPassword     | New password
confirmPassword | Confirm password

<aside class="notice">
You must replace `ACCESS_TOKEN` with your API request.
</aside>

# Person

## Get Person

> API Endpoint

```
GET https://tapgenes.com/ehr/v1/person/{personId}
```

> Example Request

```curl
curl -X GET --header 'Accept: application/json' --header 'Authorization: OAuth2 <ACESS_TOKEN>' 'https://tapgenes.com/ehr/v1/person/<PERSON_ID>'
```

> Make sure to replace the follows,

```
PERSON_ID - the person Id
```

> Example Response

```json
{
  "id": 1234,
  "email": "XXXX@XXXX.com",
  "fbId": "XXXXX",
  "fsId": "XXXX",
  "isActive": 1,
  "isAdmin": false,
  "environment": "Tapgenes",
  "personDetailsEntity": {
    "id": XXXX,
    "userId": XXXX,
    "firstName": "Johny",
    "lastName": "Mamon",
    "fullName": "Johny Mamon",
    "dob": "1993-02-14",
    "isLiving": 1,
    "imgUrl": "https://graph.facebook.com/XXXX/picture?type=large",
    "address": "",
    "deathCause": "",
    "sex": "female",
    "relationshipStatus": "married",
    "accountCreator": 0,
    "isAdopted": 0
  },
  "isPremiumUser": false
}
```
This endpoint used to get the person.

Parameter    | Description
------------ | -----------
personId     | person Id

<aside class="notice">
You must replace `ACCESS_TOKEN` with your API request.
</aside>

## Get Current Person

> API Endpoint

```
GET https://tapgenes.com/ehr/v1/person/current
```

> Example Request

```curl
curl -X GET --header 'Accept: application/json' --header 'Authorization: OAuth2 <ACCESS_TOKEN>' 'https://tapgenes.com/ehr/v1/person/current'
```

> Example Response

```json
{
  "id": 1234,
  "email": "XXXX@XXXX.com",
  "fbId": "XXXXX",
  "fsId": "XXXX",
  "isActive": 1,
  "isAdmin": false,
  "environment": "Tapgenes",
  "personDetailsEntity": {
    "id": XXXX,
    "userId": XXXX,
    "firstName": "Johny",
    "lastName": "Mamon",
    "fullName": "Johny Mamon",
    "dob": "1993-02-14",
    "isLiving": 1,
    "imgUrl": "https://graph.facebook.com/XXXX/picture?type=large",
    "address": "",
    "deathCause": "",
    "sex": "female",
    "relationshipStatus": "married",
    "accountCreator": 0,
    "isAdopted": 0
  },
  "isPremiumUser": false
}
```
This endpoint used to get current person who logged in.

<aside class="notice">
You must replace `ACCESS_TOKEN` with your API request.
</aside>

## Update Person

> API Endpoint

```
PUT https://tapgenes.com/ehr/v1/person
```

> Example Request

```curl
curl -X PUT --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'Authorization: OAuth2 <ACCESS_TOKEN>' -d '{
  "id": 1234,
  "email": "XXXX@XXXXX.com",
  "personDetailsEntity": {
    "firstName": "Johny",
    "lastName": "Memone",
    "fullName": "Johny Memone",
    "dob": "2017-11-08",
    "telephone": "XXXXXXXXXX",
    "isLiving": 1,
    "hometown": "",
    "imgUrl": "",
    "language": "",
    "address": "",
    "religion": "",
    "lastupdate": "2017-11-08",
    "ancestry": "",
    "doe": "2017-11-08",
    "deathCause": "",
    "sex": "female",
    "isAdopted": 0,
    "bloodType": "string",
    "ageOfDeath": 0
  }
}' 'https://tapgenes.com/ehr/v1/person'
```

> Example Response

```json
{
  "id": 1234,
  "email": "XXXX@XXXX.com",
  "fbId": "XXXXX",
  "fsId": "XXXX",
  "isActive": 1,
  "isAdmin": false,
  "environment": "Tapgenes",
  "personDetailsEntity": {
    "id": XXXX,
    "userId": XXXX,
    "firstName": "Johny",
    "lastName": "Mamon",
    "fullName": "Johny Mamon",
    "dob": "1993-02-14",
    "isLiving": 1,
    "imgUrl": "https://graph.facebook.com/XXXX/picture?type=large",
    "address": "",
    "deathCause": "",
    "sex": "female",
    "relationshipStatus": "married",
    "accountCreator": 0,
    "isAdopted": 0
  },
  "isPremiumUser": false
}
```
This endpoint used to update the person.

<aside class="notice">
You must replace `ACCESS_TOKEN` with your API request.
</aside>

## Update List of Persons

> API Endpoint

```
PUT https://tapgenes.com/ehr/v1/person/list
```

> Example Request

```curl
curl -X PUT --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'Authorization: OAuth2 <ACCESS_TOKEN>' -d '[{
  "id": 1234,
  "email": "XXXX@XXXXX.com",
  "personDetailsEntity": {
    "firstName": "Johny",
    "lastName": "Memone",
    "fullName": "Johny Memone",
    "dob": "2017-11-08",
    "telephone": "XXXXXXXXXX",
    "isLiving": 1,
    "hometown": "",
    "imgUrl": "",
    "language": "",
    "address": "",
    "religion": "",
    "lastupdate": "2017-11-08",
    "ancestry": "",
    "doe": "2017-11-08",
    "deathCause": "",
    "sex": "female",
    "isAdopted": 0,
    "bloodType": "string",
    "ageOfDeath": 0
  },
  "fromSource": "Tapgenes"
}]' 'https://tapgenes.com/ehr/v1/person/list'
```

> Example Response

```json
[{
  "id": 1234,
  "email": "XXXX@XXXX.com",
  "fbId": "XXXXX",
  "fsId": "XXXX",
  "isActive": 1,
  "isAdmin": false,
  "environment": "Tapgenes",
  "personDetailsEntity": {
    "id": XXXX,
    "userId": XXXX,
    "firstName": "Johny",
    "lastName": "Mamon",
    "fullName": "Johny Mamon",
    "dob": "1993-02-14",
    "isLiving": 1,
    "imgUrl": "https://graph.facebook.com/XXXX/picture?type=large",
    "address": "",
    "deathCause": "",
    "sex": "female",
    "relationshipStatus": "married",
    "accountCreator": 0,
    "isAdopted": 0
  },
  "isPremiumUser": false
}]
```
This endpoint used to update list of persons.

<aside class="notice">
You must replace `ACCESS_TOKEN` with your API request.
</aside>

## Delete Person

> API Endpoint

```
DELETE https://tapgenes.com/ehr/v1/person?deletePersonId={deletedPersonId}&centerPersonId={centerPersonId}
```

> Example Request

```curl
curl -X DELETE --header 'Accept: application/json' --header 'Authorization: OAuth2 <ACCESS_TOKEN>' 'https://tapgenes.com/ehr/v1/person?deletePersonId=XXXX&centerPersonId=XXXX'
```

> Example Response

```json
{
  "message": "Password Reset Completed"
}
```

This endpoint used to delete the person who logged in.

<aside class="notice">
You must replace `ACCESS_TOKEN` with your API request.
</aside>

## User Exists

> API Endpoint

```
POST https://tapgenes.com/ehr/v1/person/userExists
```

> Example Request

```curl
curl -X POST --header 'Content-Type: application/json' --header 'Accept: text/plain' --header 'Authorization: OAuth2 <ACCESS_TOKEN>' -d '<EMAIL>' 'https://tapgenes.com/ehr/v1/person/userExists'
```

> Make sure to replace the follows,

```
EMAIL - the email which is you want to check if exist
```

> Example Response

```json
{
  "message": true
}
```

This endpoint is used to check the email is already exists

<aside class="notice">
You must replace `ACCESS_TOKEN` with your API request.
</aside>

# PHR

## Create PHR

> API Endpoint

```
POST https://tapgenes.com/ehr/v1/phr
```

> Example Request

```
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'Authorization: OAuth2 <ACCESS_TOKEN>' -d '{
  "personId": 1234,
  "document": {
        "lifeEvent": [],
        "allergy": [],
        "healthCondition": [],
        "geneticInformation": [],
        "medication": [],
        "vital": [],
        "immunization": [],
        "wellness": [],
        "note": [],
        "emergencyContact": [],
        "insuranceAdvDirective": [],
        "document": [],
        "riskModels":{}
    }
}' 'https://tapgenes.com/ehr/v1/phr'
```

> Example Response

```json
{
  "personId": 1234,
  "document": { "XXXXXXXXXX": {
        "lifeEvent": [],
        "allergy": [],
        "healthCondition": [],
        "geneticInformation": [],
        "medication": [],
        "vital": [],
        "immunization": [],
        "wellness": [],
        "note": [],
        "emergencyContact": [],
        "insuranceAdvDirective": [],
        "document": [],
        "riskModels":{}
        }
    }
}
```

This endpoint is used to create new PHR data. PHR is a Personal Health Record for the individual person stored in the database as a encrypted format.

<aside class="notice">
You must replace `ACCESS_TOKEN` with your API request.
</aside>

## Update PHR

> API Endpoint

```
PUT https://tapgenes.com/ehr/v1/phr
```

> Example Request

```
curl -X PUT --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'Authorization: OAuth2 <ACCESS_TOKEN>' -d '{
  "personId": 1234,
  "document": {
        "lifeEvent": [],
        "allergy": [],
        "healthCondition": [],
        "geneticInformation": [],
        "medication": [],
        "vital": [],
        "immunization": [],
        "wellness": [],
        "note": [],
        "emergencyContact": [],
        "insuranceAdvDirective": [],
        "document": [],
        "riskModels":{}
    }
}' 'https://tapgenes.com/ehr/v1/phr'
```

> Example Response

```json
{
  "personId": 1234,
  "document": { "XXXXXXXXXX": {
        "lifeEvent": [],
        "allergy": [],
        "healthCondition": [],
        "geneticInformation": [],
        "medication": [],
        "vital": [],
        "immunization": [],
        "wellness": [],
        "note": [],
        "emergencyContact": [],
        "insuranceAdvDirective": [],
        "document": [],
        "riskModels":{}
        }
    }
}
```

This endpoint is used to update PHR data.

<aside class="notice">
You must replace `ACCESS_TOKEN` with your API request.
</aside>

## Update List of PHRs

> API Endpoint

```
PUT https://tapgenes.com/ehr/v1/phr/list
```

> Example Request

```
curl -X PUT --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'Authorization: OAuth2 <ACCESS_TOKEN>' -d '{
  "personId": 1234,
  "document": [{
        "lifeEvent": [],
        "allergy": [],
        "healthCondition": [],
        "geneticInformation": [],
        "medication": [],
        "vital": [],
        "immunization": [],
        "wellness": [],
        "note": [],
        "emergencyContact": [],
        "insuranceAdvDirective": [],
        "document": [],
        "riskModels":{}
    }
}]' 'https://tapgenes.com/ehr/v1/phr/list'
```

> Example Response

```json
[{
  "personId": 1234,
  "document": { "XXXXXXXXXX": {
        "lifeEvent": [],
        "allergy": [],
        "healthCondition": [],
        "geneticInformation": [],
        "medication": [],
        "vital": [],
        "immunization": [],
        "wellness": [],
        "note": [],
        "emergencyContact": [],
        "insuranceAdvDirective": [],
        "document": [],
        "riskModels":{}
        }
    }
}]
```

This endpoint is used to update list of person's PHR data.

<aside class="notice">
You must replace `ACCESS_TOKEN` with your API request.
</aside>

## Get PHR

> API Endpoint

```
GET https://tapgenes.com/ehr/v1/phr/{personId}
```

> Example Request

```curl
curl -X GET --header 'Accept: text/plain' --header 'Authorization: OAuth2 <ACCESS_TOKEN>' 'https://tapgenes.com/ehr/v1/phr/<PERSON_ID>'
```

> Example Response

```json
{
  "personId": 1234,
  "document": { "XXXXXXXXXX": {
        "lifeEvent": [],
        "allergy": [],
        "healthCondition": [],
        "geneticInformation": [],
        "medication": [],
        "vital": [],
        "immunization": [],
        "wellness": [],
        "note": [],
        "emergencyContact": [],
        "insuranceAdvDirective": [],
        "document": [],
        "riskModels":{}
        }
    }
}
```

This endpoint is used to get the PHR data for a particular person using person id.

<aside class="notice">
You must replace `ACCESS_TOKEN` with your API request.
</aside>

## Get Family Member's PHR

> API Endpoint

```
GET https://tapgenes.com/ehr/v1/phr/{personId}/all
```

> Example Request

```curl
curl -X GET --header 'Accept: text/plain' --header 'Authorization: OAuth2 <ACCESS_TOKEN>' 'https://tapgenes.com/ehr/v1/phr/<PERSON_ID>/all'
```

> Example Response

```json
[{
  "personId": 1234,
  "document": { "XXXXXXXXXX": {
        "lifeEvent": [],
        "allergy": [],
        "healthCondition": [],
        "geneticInformation": [],
        "medication": [],
        "vital": [],
        "immunization": [],
        "wellness": [],
        "note": [],
        "emergencyContact": [],
        "insuranceAdvDirective": [],
        "document": [],
        "riskModels":{}
        }
    }
},
{
  "personId": 4567,
  "document": { "XXXXXXXXXX": {
        "lifeEvent": [],
        "allergy": [],
        "healthCondition": [],
        "geneticInformation": [],
        "medication": [],
        "vital": [],
        "immunization": [],
        "wellness": [],
        "note": [],
        "emergencyContact": [],
        "insuranceAdvDirective": [],
        "document": [],
        "riskModels":{}
        }
    }
}]
```

This endpoint is used to get the PHR data for all the family members in the tree.

<aside class="notice">
You must replace `ACCESS_TOKEN` with your API request.
</aside>

## Delete PHR

> API Endpoint

```
DELETE https://tapgenes.com/ehr/v1/phr/{personId}
```

> Example Request

```curl
curl -X DELETE --header 'Accept: text/plain' --header 'Authorization: OAuth2 <ACCESS_TOKEN>' 'https://tapgenes.com/ehr/v1/phr/<PERSON_ID>'
```

> Example Response

```json
{
"message":"Deleted Successfully"
}
```

This endpoint is used to delete the particular person's PHR data.

<aside class="notice">
You must replace `ACCESS_TOKEN` with your API request.
</aside>

## Upload a File

> API Endpoint

```
POST https://tapgenes.com/ehr/v1/phr/file/upload
```

> Example Request

```curl
curl -X POST --header 'Content-Type: multipart/form-data' --header 'Accept: text/plain' --header 'Authorization: OAuth2 <ACCESS_TOKEN>' 'https://tapgenes.com/ehr/v1/phr/file/upload'
```

> Example Response

```json
{
"fileId": "XXXXXXXXXXXXXXXXXX",
"fileName": "example.txt"
}
```

This endpoint is used to upload a file.

<aside class="notice">
You must replace `ACCESS_TOKEN` with your API request.
</aside>

## Download a File

> API Endpoint

```
GET https://tapgenes.com/ehr/v1/phr/file/{fileId}
```

> Example Request

```curl
curl -X GET --header 'Accept: text/plain' --header 'Authorization: OAuth2 <ACCESS_TOKEN>' 'https://tapgenes.com/ehr/v1/phr/file/{fileId}'
```

This endpoint is used to download a file.

<aside class="notice">
You must replace `ACCESS_TOKEN` with your API request.
</aside>

## Delete a File

> API Endpoint

```
DELETE https://tapgenes.com/ehr/v1/phr/file/{fileId}
```

> Example Request

```curl
curl -X DELETE --header 'Accept: text/plain' --header 'Authorization: OAuth2 <ACCESS_TOKEN>' 'https://tapgenes.com/ehr/v1/phr/file/<FILE_ID>'
```

> Example Response

```json
{
"message":"Success"
}
```

This endpoint is used to delete a file.

<aside class="notice">
You must replace `ACCESS_TOKEN` with your API request.
</aside>

## Genetic Age

> API Endpoint

```
GET https://tapgenes.com/ehr/v1/phr/geneticage
```

> Example Request

```curl
curl -X GET --header 'Accept: application/json' --header 'Authorization: OAuth2 <ACCESS_TOKEN>' 'https://tapgenes.com/ehr/v1/phr/geneticage'
```

> Example Response

```json
{
  "age": 24,
  "sex": "female",
  "geneticAge": 20,
  "result": "4 Years Younger",
  "diseaseExcept": [
    "Stroke",
    "Lung Cancer",
    "Type 2 Diabetes",
    "Colorectal Cancer",
    "Bladder Cancer",
    "Rectal Cancer",
    "Pancreatic Cancer",
    "Breast Cancer",
    "Heart Disease",
    "Ovarian Cancer",
    "Alzheimers Disease",
    "Colon Cancer",
    "Kidney Cancer",
    "Melanoma Skin Cancer"
  ],
  "diseaseFound": [
    "Alcholism(AA)",
    "Alcoholism",
    "Amyloidosis",
    "Granddaughter",
    "Heart attack",
    "Alpha thalassemia",
    "Asthma"
  ],
  "diseaseRecommendation": [],
  "familyHealthScore": 0.0079,
  "loggedInPersonBucket": "six"
}
```

This endpoint is used to calculate the Genetic Age for the person who logged in.

The Genetic Age is calculated based on the person's age gender and list of diseases presence for the person's first degree relatives. The first degree relatives are known as blood relatives like parents, siblings, children.

Response Params | Description
--------------- | -----------
age | The person's current age which is get it from family tree
sex | The person's gender which is get it from family tree
geneticAge | The genetic age is calculated based on the Age, Gender and the disease presence for the person's first degree relatives
result | The result is a difference between the age and geneticAge
diseaseExpect | The list of diseases which are already defined by the Tapgenes to calculate the Genetic Age
diseaseFound | The list of diseases which are found for the person's first degree relatives
diseaseRecommendation | Tips to reduce the disease risk. It should be available for already defined diseases
familyHealthScore | The family health score is described how healthy your family from list of families available in our database
loggedInPersonBucket | The string text represents the logged in person's bucket from predefined 10 bucket

<aside class="notice">
You must replace `ACCESS_TOKEN` with your API request.
</aside>

# Invite

## Create Invite

> API Endpoint

```
POST https://tapgenes.com/ehr/v1/invite
```

> Example Request

```curl
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'Authorization: OAuth2 <ACCESS_TOKEN>' -d '{
  "familyMembers": [
    {
      "personId": 1234,
      "emailId": "XXXX@XXXXX.com",
      "privacyId": 1,
      "relation": "son",
      "fbId": "XXXX",
      "fbName": "XXXX"
    }
  ],
  "nonFamilyMembers": [
    {
      "personId": null,
      "emailId": "XXXX@XXXXX.com",
      "privacyId": 1,
      "relation": null,
      "fbId": null,
      "fbName": null
    }
  ],
  "inviteMsg": "Hi, I want to share my Tapgenes family health tree with you. - Johny Memone"
}' 'https://tapgenes.com/ehr/v1/invite'
```

> Example Response

```json
{
"errorPerson": {},
"invitedPerson": {},
"notifiedPerson": {}
}
```

This endipoint is used to create invite for both family members (Tapgenes members) and non-family members (Non-Tapgenes members).

Response Params | Description
--------------- | -----------
errorPerson | The persons who all are getting error while creating invite
invitedPerson | The persons who all successfully invited
notifiedPerson | The person who all already invited

<aside class="notice">
You must replace `ACCESS_TOKEN` with your API request.
</aside>

## Get My Invites

> API Endpoint

```
GET https://tapgenes.com/ehr/v1/invite?page=1
```

> Example Request

```curl
curl -X GET --header 'Accept: application/json' --header 'Authorization: OAuth2 <ACCESS_TOKEN>' 'https://tapgenes.com/ehr/v1/invite?page=1'
```

> Example Response

```json
{
  "pageCount": 1,
  "inviteCount": 20,
  "invites": [
    {
      "id": 123,
      "personId": 1234,
      "relativeId": 5678,
      "relativeEmailId": "XXX@XXXXX.com",
      "inviteStatus": "accepted",
      "invitedDate": 1467722475000,
      "firstName": "Johny",
      "lastName": "Mamone",
      "imgUrl": "https://graph.facebook.com/XXXXXXXXX/picture?type=large",
      "isRelationActive": 1,
      "relativeSex": "female",
      "environment": "Tapgenes"
    }
  ]
}
```

This endipoint is used to get all the invites for logged in person.

<aside class="notice">
You must replace `ACCESS_TOKEN` with your API request.
</aside>

## Get My Active Invites

> API Endpoint

```
GET https://tapgenes.com/ehr/v1/invite/active
```

> Example Request

```curl
curl -X GET --header 'Accept: application/json' --header 'Authorization: OAuth2 ACCESS_TOKEN' 'https://tapgenes.com/ehr/v1/invite/active'
```

> Example Response

```json
{
  "pageCount": 1,
  "inviteCount": 20,
  "invites": [
    {
      "id": 123,
      "personId": 1234,
      "relativeId": 5678,
      "relativeEmailId": "XXX@XXXXX.com",
      "inviteStatus": "accepted",
      "invitedDate": 1467722475000,
      "firstName": "Johny",
      "lastName": "Mamone",
      "imgUrl": "https://graph.facebook.com/XXXXXXXXX/picture?type=large",
      "isRelationActive": 1,
      "relativeSex": "female",
      "environment": "Tapgenes"
    }
  ]
}
```

This endipoint is used to get active invites for logged in person.

<aside class="notice">
You must replace `ACCESS_TOKEN` with your API request.
</aside>

## Get Family Invites

> API Endpoint

```
GET https://tapgenes.com/ehr/v1/invite/family?page=1
```

> Example Request

```curl
curl -X GET --header 'Accept: text/plain' --header 'Authorization: OAuth2 <ACCESS_TOKEN>' 'https://tapgenes.com/ehr/v1/invite/family?page=1'
```

> Example Response

```json
{
  "pageCount": 1,
  "inviteCount": 20,
  "invites": [
    {
      "id": 123,
      "personId": 1234,
      "relativeId": 5678,
      "relativeEmailId": "XXX@XXXXX.com",
      "inviteStatus": "accepted",
      "invitedDate": 1467722475000,
      "firstName": "Johny",
      "lastName": "Mamone",
      "imgUrl": "https://graph.facebook.com/XXXXXXXXX/picture?type=large",
      "isRelationActive": 1,
      "relativeSex": "female",
      "environment": "Tapgenes"
    }
  ]
}
```

This endipoint is used to get all the family invites.

<aside class="notice">
You must replace `ACCESS_TOKEN` with your API request.
</aside>

## Get Friends Invites

> API Endpoint

```
GET https://tapgenes.com/ehr/v1/invite/friends?page=1
```

> Example Request

```curl
curl -X GET --header 'Accept: text/plain' --header 'Authorization: OAuth2 <ACCESS_TOKEN>' 'https://tapgenes.com/ehr/v1/invite/friends?page=1'
```

> Example Response

```json
{
  "pageCount": 1,
  "inviteCount": 20,
  "invites": [
    {
      "id": 123,
      "personId": 1234,
      "relativeId": 5678,
      "relativeEmailId": "XXX@XXXXX.com",
      "inviteStatus": "accepted",
      "invitedDate": 1467722475000,
      "firstName": "Johny",
      "lastName": "Mamone",
      "imgUrl": "https://graph.facebook.com/XXXXXXXXX/picture?type=large",
      "isRelationActive": 1,
      "relativeSex": "female",
      "environment": "Tapgenes"
    }
  ]
}
```

This endipoint is used to get all the friends invite

<aside class="notice">
You must replace `ACCESS_TOKEN` with your API request.
</aside>

## Accept Invite

> API Endpoint

```
POST https://tapgenes.com/ehr/v1/invite/accept/{inviteId}
```

> Example Request

```curl
curl -X POST --header 'Content-Type: application/json' --header 'Accept: text/plain' --header 'Authorization: OAuth2 <INVITE_ID>' 'https://tapgenes.com/ehr/v1/invite/accept/<INVITE_ID>'
```

> Example Response

```json
{
"person": {
  "id": 1234,
  "email": "XXXXX@XXXX.com",
  "isActive": 1,
  "isAdmin": false,
  "environment": "Tapgenes",
  "accessToken": "0e4f70df-7d8b-4afc-9a35-39f72a322cf9",
  "lastAccessUTC": 1510052975657,
  "personDetailsEntity": {
    "id": 1234,
    "userId": 1234,
    "firstName": "Johny",
    "lastName": "Mamon",
    "fullName": "Johny Mamon",
    "dob": "1993-02-14",
    "isLiving": 1,
    "imgUrl": "https://graph.facebook.com/XXX/picture?type=large",
    "sex": "female",
    "relationshipStatus": "married",
    "accountCreator": 0,
    "isAdopted": 0
  },
  "fromSource": "Tapgenes",
  "isPremiumUser": false
},
"accessToken": "XXXXXXXXXXXXXXXXX"
}
```

This endpoint is used to accept the invite. It will return the accepted person's object and access token.

<aside class="notice">
You must replace `ACCESS_TOKEN` with your API request.
</aside>

## Reject Invite

> API Endpoint

```
POST https://tapgenes.com/ehr/v1/invite/reject/{inviteId}
```

> Example Request

```curl
curl -X POST --header 'Content-Type: application/json' --header 'Accept: text/plain' --header 'Authorization: OAuth2 <ACCESS_TOKEN>' 'https://tapgenes.com/ehr/v1/invite/reject/<INVITE_ID>'
```

> Example Response

```json
{
"person": {
  "id": 1234,
  "email": "XXXXX@XXXX.com",
  "isActive": 1,
  "isAdmin": false,
  "environment": "Tapgenes",
  "accessToken": "0e4f70df-7d8b-4afc-9a35-39f72a322cf9",
  "lastAccessUTC": 1510052975657,
  "personDetailsEntity": {
    "id": 1234,
    "userId": 1234,
    "firstName": "Johny",
    "lastName": "Mamon",
    "fullName": "Johny Mamon",
    "dob": "1993-02-14",
    "isLiving": 1,
    "imgUrl": "https://graph.facebook.com/XXX/picture?type=large",
    "sex": "female",
    "relationshipStatus": "married",
    "accountCreator": 0,
    "isAdopted": 0
  },
  "fromSource": "Tapgenes",
  "isPremiumUser": false
},
"accessToken": "XXXXXXXXXXXXXXXXX"
}
```

This endpoint is used to reject the invite. It will return the rejected person's object and access token.

<aside class="notice">
You must replace `ACCESS_TOKEN` with your API request.
</aside>

# Risk Assessment

## Get List of Assessments

> API Endpoint

```
GET https://tapgenes.com/ehr/v1/meta/questionWidget
```

> Example Request

```curl
curl -X GET --header 'Accept: application/json' --header 'Authorization: OAuth2 <ACCESS_TOKEN>' 'https://tapgenes.com/ehr/v1/meta/questionWidget'
```

> Example Response

```json
[
  {
    "id": 1,
    "name": "Breast Cancer",
    "isDeleted": 0,
    "phrKey": "breastCancer",
    "sheet": "breast_cancer_live",
  },
  {
    "id": 2,
    "name": "Lung Cancer",
    "isDeleted": 0,
    "phrKey": "lungCancer",
    "sheet": "lung_cancer_live",
  },
  {
    "id": 3,
    "name": "Heart Disease",
    "isDeleted": 0,
    "phrKey": "heartDisease",
    "sheet": "heart_disease_live",
  },
  {
    "id": 4,
    "name": "Colon Cancer",
    "isDeleted": 0,
    "phrKey": "colonCancer",
    "sheet": "colon_cancer_live",
  }
]
```

This endpoint is used to get all the assessments. The assessment id is used to get the individual assessment.

<aside class="notice">
You must replace `ACCESS_TOKEN` with your API request.
</aside>

## Get Assessment

> API Endpoint

```
POST https://tapgenes.com/ehr/v1/assessment/{questionWizardId}/{slideNo}?isBack=false
```

> Example Request

```curl
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'Authorization: OAuth2 <ACCESS_TOKEN>' -d '{}' 'https://tapgenes.com/ehr/v1/assessment/<QUESTION_WIZARD_ID>/<SLIDE_NO>?isBack=false'
```

> Example Response

```json
{
  "slideNo": "3",
  "question": "Gender: Female",
  "questionInfo": "Just being a woman means that you are at higher risk compared to the men in your life.",
  "template": "Info",
  "image": "yes",
  "data": {
    "sex": "female"
  },
  "type": "Info"
}
```

This endpoint is used to process the individual assessment.

<aside class="notice">
You must replace `ACCESS_TOKEN` with your API request.
</aside>

# Family Health Tree

## Get FHT

> API Endpoint

```
GET https://tapgenes.com/fht/v1/tree/{personId}?isNonfamilyMemeber=false
```
> Example Request

```curl
curl -X GET --header 'Accept: application/json' --header 'Authorization: OAuth2 <ACCESS_TOKEN>' 'https://tapgenes.com/fht/v1/tree/<PERSON_ID>?isNonfamilyMemeber=false'
```

> Example Response

```json
[
    []
    [
    {
        "id": "XXXXX",
        "firstName": "Peter",
        "lastName": "Memone",
        "name": "Peter Memone",
        "relation": "father",
        "x": 9.5,
        "y": 3,
        "gender": "male",
        "dob": "1957-06-20",
        "doe": "",
        "email": "XXXX@XXXXX.com",
        "fatherId": 39441,
        "motherId": 39451,
        "parentX": 8.5,
        "hasPartner": true,
        "currentPartner": "XXXXX",
        "hasParent": true,
        "hasBothParent": true,
        "imageUrl": "/XXXX/XXXX/XXXX.jpg",
        "connectToBothParents": true,
        "sourcePersonId": "XXXXX",
        "isActive": "0"
    },
    {
        "id": "XXXXXX",
        "firstName": "Nancy",
        "lastName": "Memone",
        "name": "Nancy Memone",
        "relation": "mother",
        "x": 10.5,
        "y": 3,
        "gender": "female",
        "dob": "1967-10-25",
        "doe": "2016-10-10",
        "email": "XXXXX@XXXXX.com",
        "fatherId": "XXXXX",
        "motherId": "XXXX",
        "parentX": 10.5,
        "hasPartner": true,
        "currentPartner": "XXXXX",
        "hasParent": true,
        "hasBothParent": true,
        "imageUrl": "https://graph.facebook.com/XXXXXXXXXXX/picture?type=large",
        "connectToBothParents": true,
        "showSpouseLine": "left",
        "sourcePersonId": "XXXXX",
        "isActive": "1"
    }
    ]
    [
    {
        "id": "XXXXX",
        "firstName": "Johny",
        "lastName": "Mamon",
        "name": "Johny Mamon",
        "relation": "self",
        "x": 2,
        "y": 2,
        "gender": "female",
        "dob": "1993-02-14",
        "doe": "",
        "email": "XXXX@XXXXXX.com",
        "fatherId": "XXXX",
        "motherId": "XXXXX",
        "parentX": 9.5,
        "hasPartner": true,
        "currentPartner": "XXXXX",
        "hasParent": true,
        "hasBothParent": true,
        "imageUrl": "https://graph.facebook.com/XXXXXXXXXXX/picture?type=large",
        "connectToBothParents": true,
        "showSpouseLine": "left",
        "isActive": "1"
    }
    ]
    []
    []
]
```

This endpoint is used to get the Family Health tree.

<aside class="notice">
You must replace `ACCESS_TOKEN` with your API request.
</aside>

# Relation

## Add Relation

> API Endpoint

```
POST https://tapgenes.com/fht/v1/relation
```

> Example Request

```curl
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'Authorization: OAuth2 <ACCESS_TOKEN>' -d '{
  "sourcePersonId": "XXXX",
  "loggedInPersonId": "XXXX",
  "relation": "string",
  "sex": "string",
  "firstName": "string",
  "lastName": "string",
  "dob": "2017-11-10T06:14:31.227Z",
  "fbId": "string",
  "homeTown": "string",
  "imgUrl": "string",
  "fsId": "string",
  "childrenIds": [],
  "marriageDate": "2017-11-10T06:14:31.227Z",
  "isAdopted": false,
  "isLiving": false,
  "address": "string",
  "telephone": "string",
  "email": "string",
  "ancestry": "string",
  "religion": "string",
  "language": "string"
}' 'https://tapgenes.com/fht/v1/relation'
```

> Example Response

```json
{
  "id": 1234,
  "email": "XXXX@XXXX.com",
  "fbId": "XXXXX",
  "fsId": "XXXX",
  "isActive": 1,
  "isAdmin": false,
  "environment": "Tapgenes",
  "personDetailsEntity": {
    "id": XXXX,
    "userId": XXXX,
    "firstName": "Johny",
    "lastName": "Mamon",
    "fullName": "Johny Mamon",
    "dob": "1993-02-14",
    "isLiving": 1,
    "imgUrl": "https://graph.facebook.com/XXXX/picture?type=large",
    "address": "",
    "deathCause": "",
    "sex": "female",
    "relationshipStatus": "married",
    "accountCreator": 0,
    "isAdopted": 0
  }
```

This endpoint is used to create or add a new relation.

Request Params | Description
-------------- | -----------
sourcePersonId | The person who needs to be add the relation
loggedInPersonId | The person who actually logged in.
relation | The relationship which needs to be add
sex | The gender of the new person
firstName | The first name of the new person
lastName | The last name of the new person
dob | The DOB of the new person
homeTown | The home town of the new person
fsId | The family search Id, if the person imported from family search
fbId | The facebook id, if the person imported from Facebook
childrenIds | The list of child ids to add a parent relationship, if the person has a children in the tree
marriageDate | The Date of Marriage, if the new person added as a spouse relationship
isAdopted | set to true, if the new person is Adopted
isLiving | set to false, if the new person is deseased
address | The address of the new person
telephone | The telephone of the new person
email | The email of the new person
ancestry | The ancestry of the new person
religion | The religion of the new person
langulage | The language of the new person

<aside class="notice">
You must replace `ACCESS_TOKEN` with your API request.
</aside>

## Add List of Relations

> API Endpoint

```
POST https://tapgenes.com/fht/v1/relation/list
```

> Example Request

```curl
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'Authorization: OAuth2 <ACCESS_TOKEN>' -d '[{
  "sourcePersonId": "XXXX",
  "loggedInPersonId": "XXXX",
  "relation": "string",
  "sex": "string",
  "firstName": "string",
  "lastName": "string",
  "dob": "2017-11-10T06:14:31.227Z",
  "fbId": "string",
  "homeTown": "string",
  "imgUrl": "string",
  "fsId": "string",
  "childrenIds": [],
  "marriageDate": "2017-11-10T06:14:31.227Z",
  "isAdopted": false,
  "isLiving": false,
  "address": "string",
  "telephone": "string",
  "email": "string",
  "ancestry": "string",
  "religion": "string",
  "language": "string"
}]' 'https://tapgenes.com/fht/v1/relation/list'
```

> Example Response

```json
[{
  "id": 1234,
  "email": "XXXX@XXXX.com",
  "fbId": "XXXXX",
  "fsId": "XXXX",
  "isActive": 1,
  "isAdmin": false,
  "environment": "Tapgenes",
  "personDetailsEntity": {
    "id": XXXX,
    "userId": XXXX,
    "firstName": "Johny",
    "lastName": "Mamon",
    "fullName": "Johny Mamon",
    "dob": "1993-02-14",
    "isLiving": 1,
    "imgUrl": "https://graph.facebook.com/XXXX/picture?type=large",
    "address": "",
    "deathCause": "",
    "sex": "female",
    "relationshipStatus": "married",
    "accountCreator": 0,
    "isAdopted": 0
  }]
```

This endpoint is used to create or add list of relations.

Request Params | Description
-------------- | -----------
sourcePersonId | The person who needs to be add the relation
loggedInPersonId | The person who actually logged in.
relation | The relationship which needs to be add
sex | The gender of the new person
firstName | The first name of the new person
lastName | The last name of the new person
dob | The DOB of the new person
homeTown | The home town of the new person
fsId | The family search Id, if the person imported from family search
fbId | The facebook id, if the person imported from Facebook
childrenIds | The list of child ids to add a parent relationship, if the person has a children in the tree
marriageDate | The Date of Marriage, if the new person added as a spouse relationship
isAdopted | set to true, if the new person is Adopted
isLiving | set to false, if the new person is deseased
address | The address of the new person
telephone | The telephone of the new person
email | The email of the new person
ancestry | The ancestry of the new person
religion | The religion of the new person
langulage | The language of the new person

<aside class="notice">
You must replace `ACCESS_TOKEN` with your API request.
</aside>

## Get Relationship Status

> API Endpoint

```
POST https://tapgenes.com/fht/v1/relation/marriedStatus
```

> Example Request

```curl
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'Authorization: OAuth2 <ACCESS_TOKEN>' -d '{
  "personId": "XXXX",
  "relativeId": "XXXX",
  "divorced": false
}' 'https://tapgenes.com/fht/v1/relation/marriedStatus'
```

> Example Response

```json
{
  "personId": "XXXX",
  "relativeId": "XXXX",
  "divorced": false
}
```

This endpoint is used to get the relationship status of the person.

Response Params | Description
-------------- | -----------
personId | The source person id
relativeId | The spouse of the source person id
divorced | if it is true, the source person and the spouse are in divorced status

<aside class="notice">
You must replace `ACCESS_TOKEN` with your API request.
</aside>

## Update Relationship Status

> API Endpoint

```
PUT https://tapgenes.com/fht/v1/relation/updateRelation
```

> Example Request

```curl
curl -X PUT --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'Authorization: OAuth2 <ACCESS_TOKEN>' -d '{
  "personId": "XXXX",
  "relativeId": "XXXX",
  "divorced": false
}' 'https://tapgenes.com/fht/v1/relation/updateRelation'
```

> Example Response

```json
{
  "personId": "XXXX",
  "relativeId": "XXXX",
  "divorced": false
}
```

This endpoint is used to update the relationship status of the person.

Request Params | Description
-------------- | -----------
personId | The source person id
relativeId | The spouse of the source person id
divorced | if it is true, the relationship status has changed as divorced

<aside class="notice">
You must replace `ACCESS_TOKEN` with your API request.
</aside>

## Get All Relations

> API Endpoint

```
GET https://tapgenes.com/fht/v1/relation/{personId}
```

> Example Request

```curl
curl -X GET --header 'Accept: application/json' --header 'Authorization: OAuth2 <ACCESS_TOKEN>' 'https://tapgenes.com/fht/v1/relation/{PERSON_ID}'
```

> Example Response

```json
{
  "grandson": [
    {
      "lastName": "XXXXX",
      "isLiving": "1",
      "sex": "male",
      "father": "XXXXX",
      "firstLevelMember": "0",
      "isActive": "0",
      "generatedMail": "XXXXX@XXXXX.com",
      "sourcePersonId": "XXXX",
      "firstName": "XXXXXX",
      "dob": "",
      "imageUrl": "",
      "id": "XXXX",
      "doe": "",
      "email": "XXXXXX@XXXXX.com"
    }
  ],
  "grandmother": [
    {
      "lastName": "XXXXX",
      "isLiving": "1",
      "sex": "female",
      "firstLevelMember": "0",
      "husband": "XXXXX",
      "isActive": "0",
      "generatedMail": "XXXXX@XXXXX.com",
      "sourcePersonId": "XXXX",
      "firstName": "XXXXX",
      "dob": "",
      "imageUrl": "",
      "id": "XXXX",
      "doe": "",
      "email": "XXXX@XXXXX.com"
    },
    {
      "lastName": "XXXXX",
      "isLiving": "1",
      "sex": "female",
      "firstLevelMember": "0",
      "husband": "XXXX",
      "isActive": "0",
      "generatedMail": "XXXXX@XXXXX.com",
      "sourcePersonId": "XXXX",
      "firstName": "XXXXX",
      "dob": "1947-08-02",
      "imageUrl": "",
      "id": "XXXX",
      "doe": "",
      "email": "XXXXX@XXXXX.com"
    }
  ],
  "father": [
    {
      "lastName": "XXXXX",
      "isLiving": "1",
      "wife": "XXXX",
      "sex": "male",
      "father": "XXXX",
      "firstLevelMember": "1",
      "isActive": "0",
      "generatedMail": "XXXXX@XXXXX.com",
      "sourcePersonId": "XXXX",
      "firstName": "XXXXX",
      "mother": "XXXX",
      "dob": "1957-06-20",
      "imageUrl": "",
      "id": "XXXX",
      "doe": "",
      "email": "XXXXX@XXXXX.com"
    }
  ],
  "husband": [
    {
      "lastName": "XXXXX",
      "isLiving": "1",
      "wife": "XXXX",
      "sex": "male",
      "firstLevelMember": "1",
      "isActive": "0",
      "generatedMail": "XXXXX@XXXXX.com",
      "sourcePersonId": "XXXX",
      "firstName": "murugan",
      "dob": "",
      "imageUrl": "",
      "id": "XXXX",
      "doe": "",
      "email": "XXXXX@XXXXX.com"
    }
  ],
  "mother": [
    {
      "lastName": "XXXXX",
      "isLiving": "0",
      "sex": "female",
      "father": "XXXX",
      "firstLevelMember": "1",
      "husband": "XXXX",
      "isActive": "1",
      "generatedMail": "XXXXX@XXXXX.com",
      "sourcePersonId": "XXXX",
      "firstName": "Selvi",
      "mother": "XXXX",
      "dob": "1967-10-25",
      "imageUrl": "https://graph.facebook.com/XXXXX/picture?type=large",
      "id": "XXXX",
      "doe": "2016-10-10",
      "email": "XXXXX@XXXXX.com"
    }
  ],
  "son": [
    {
      "lastName": "XXXXX",
      "isLiving": "1",
      "sex": "male",
      "father": "XXXX",
      "firstLevelMember": "1",
      "isActive": "0",
      "generatedMail": "XXXXX@XXXXX.com",
      "sourcePersonId": "XXXX",
      "firstName": "XXXXXX",
      "mother": "XXXX",
      "dob": "",
      "imageUrl": "https://graph.facebook.com/XXXXX/picture?type=large",
      "id": "XXXX",
      "doe": "",
      "email": "XXXXX@XXXXX.com"
    },
    {
      "lastName": "XXXXX",
      "isLiving": "1",
      "sex": "male",
      "father": "XXXX",
      "firstLevelMember": "1",
      "isActive": "0",
      "generatedMail": "XXXXX@XXXXX.com",
      "sourcePersonId": "XXXX",
      "firstName": "XXXXX",
      "mother": "XXXX",
      "dob": "",
      "imageUrl": "",
      "id": "XXXX",
      "doe": "",
      "email": "XXXXX@XXXXX.com"
    },
    {
      "lastName": "XXXXX",
      "isLiving": "1",
      "sex": "male",
      "father": "XXXX",
      "firstLevelMember": "1",
      "isActive": "0",
      "generatedMail": "XXXXX@XXXXX.com",
      "sourcePersonId": "XXXX",
      "firstName": "XXXXX",
      "mother": "XXXX",
      "dob": "",
      "imageUrl": "",
      "id": "XXXX",
      "doe": "",
      "email": "XXXXX@XXXXX.com"
    },
    {
      "lastName": "XXXXX",
      "isLiving": "1",
      "sex": "male",
      "father": "XXXX",
      "firstLevelMember": "1",
      "isActive": "0",
      "generatedMail": "XXXXX@XXXXX.com",
      "sourcePersonId": "XXXX",
      "firstName": "XXXXX",
      "mother": "XXXX",
      "dob": "",
      "imageUrl": "",
      "id": "XXXX",
      "doe": "",
      "email": "XXXXX@XXXXX.com"
    }
  ],
  "ex-husband": [
    {
      "lastName": "XXXXX",
      "isLiving": "1",
      "sex": "male",
      "firstLevelMember": "1",
      "isActive": "0",
      "generatedMail": "XXXXX@XXXXX.com",
      "sourcePersonId": "XXXX",
      "firstName": "XXXXX",
      "dob": "",
      "imageUrl": "",
      "id": "XXXX",
      "doe": "",
      "email": "XXXXX@XXXXX.com"
    }
  ],
  "grandfather": [
    {
      "lastName": "XXXXX",
      "isLiving": "1",
      "wife": "XXXX",
      "sex": "male",
      "firstLevelMember": "0",
      "isActive": "0",
      "generatedMail": "XXXXX@XXXXX.com",
      "sourcePersonId": "XXXX",
      "firstName": "XXXXX",
      "dob": "1945-10-09",
      "imageUrl": "",
      "id": "XXXX",
      "doe": "",
      "email": "XXXXX@XXXXX.com"
    },
    {
      "lastName": "XXXXX",
      "isLiving": "0",
      "wife": "XXXX",
      "sex": "male",
      "firstLevelMember": "0",
      "isActive": "0",
      "generatedMail": "XXXXX@XXXXX.com",
      "sourcePersonId": "XXXX",
      "firstName": "XXXXX",
      "dob": "1989-01-01",
      "imageUrl": "",
      "id": "XXXX",
      "doe": "2016-01-05",
      "email": "XXXXX@XXXXX.com"
    }
  ],
  "daughter": [
    {
      "lastName": "XXXXX",
      "isLiving": "1",
      "sex": "female",
      "father": "XXXX",
      "firstLevelMember": "1",
      "isActive": "0",
      "generatedMail": "XXXXX@XXXXX.com",
      "sourcePersonId": "XXXX",
      "firstName": "XXXXX",
      "mother": "XXXX",
      "dob": "",
      "imageUrl": "https://graph.facebook.com/XXXXX/picture?type=large",
      "id": "XXXX",
      "doe": "",
      "email": "XXXXX@XXXXX.com"
    }
  ],
  "brother": [
    {
      "lastName": "XXXXX",
      "isLiving": "1",
      "sex": "male",
      "father": "XXXX",
      "firstLevelMember": "1",
      "isActive": "1",
      "generatedMail": "XXXXX@XXXXX.com",
      "sourcePersonId": "XXXX",
      "firstName": "XXXXX",
      "mother": "XXXX",
      "dob": "",
      "imageUrl": "",
      "id": "XXXX",
      "doe": "",
      "email": "XXXXX@XXXXX.com"
    }
  ],
  "sister": [
    {
      "lastName": "XXXXX",
      "isLiving": "1",
      "sex": "female",
      "father": "XXXX",
      "firstLevelMember": "1",
      "isActive": "0",
      "generatedMail": "XXXXX@XXXXX.com",
      "sourcePersonId": "XXXX",
      "firstName": "XXXXXX",
      "mother": "XXXX",
      "dob": "",
      "imageUrl": "",
      "id": "XXXX",
      "doe": "",
      "email": "XXXXX@XXXXX.com"
    }
  ]
}
```

This endpoint is used to get all the relations for the person.

<aside class="notice">
You must replace `ACCESS_TOKEN` with your API request.
</aside>

# Privacy

## Get Privacy Types

The privacy is a term is used to set the access control for the data.

> API Endpoint

```
GET https://tapgenes.com/ehr/v1/privacy/types
```

> Example Request

```curl
curl -X GET --header 'Accept: application/json' --header 'Authorization: OAuth2 <ACCESS_TOKEN>' 'https://tapgenes.com/ehr/v1/privacy/types'
```

> Example Response

```json
[
  {
    "id": 1,
    "privacyName": "NONE",
    "privacyWeight": "1"
  },
  {
    "id": 2,
    "privacyName": "VIEW",
    "privacyWeight": "2"
  },
  {
    "id": 3,
    "privacyName": "EDIT",
    "privacyWeight": "3"
  },
  {
    "id": 4,
    "privacyName": "ADMIN",
    "privacyWeight": "4"
  }
]
```

This endpoint is used to get the predefined privacy and weight.

<aside class="notice">
You must replace `ACCESS_TOKEN` with your API request.
</aside>

## Create Privacy

> API Endpoint

```
POST https://tapgenes.com/ehr/v1/privacy
```

> Example Request

```curl
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'Authorization: OAuth2 <ACCESS_TOKEN>' -d '{
  "personId": "XXXXX",
  "familyPrivacy": {
    "<FAMILY_MEMBER_ID>": {
      "basicInfo": 3,
      "lifeEvent": 3,
      "allergy": 3,
      "healthCondition": 3,
      "medication": 3,
      "vital": 3,
      "immunization": 3,
      "wellness": 3,
      "note": 3,
      "emergencyContact": 3,
      "insuranceAdvDirective": 3,
      "document": 2
    },
    "<FAMILY_MEMBER_ID>": {
      "basicInfo": 3,
      "lifeEvent": 3,
      "allergy": 3,
      "healthCondition": 3,
      "medication": 3,
      "vital": 3,
      "immunization": 3,
      "wellness": 3,
      "note": 3,
      "emergencyContact": 3,
      "insuranceAdvDirective": 3,
      "document": 3
    }
   },
  "nonFamilyPrivacy": {}
}' 'https://tapgenes.com/ehr/v1/privacy'
```

> Example Response

```json
{
  "personId": "XXXXX",
  "familyPrivacy": {
    "<FAMILY_MEMBER_ID>": {
      "basicInfo": 3,
      "lifeEvent": 3,
      "allergy": 3,
      "healthCondition": 3,
      "medication": 3,
      "vital": 3,
      "immunization": 3,
      "wellness": 3,
      "note": 3,
      "emergencyContact": 3,
      "insuranceAdvDirective": 3,
      "document": 2
    },
    "<FAMILY_MEMBER_ID>": {
      "basicInfo": 3,
      "lifeEvent": 3,
      "allergy": 3,
      "healthCondition": 3,
      "medication": 3,
      "vital": 3,
      "immunization": 3,
      "wellness": 3,
      "note": 3,
      "emergencyContact": 3,
      "insuranceAdvDirective": 3,
      "document": 3
    }
}
```

This endpoint is used to create a family and non-family privacy for the person

<aside class="notice">
You must replace `ACCESS_TOKEN` with your API request.
</aside>

## Update Privacy

> API Endpoint

```
PUT https://tapgenes.com/ehr/v1/privacy
```

> Example Request

```curl
curl -X PUT --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'Authorization: OAuth2 <ACCESS_TOKEN>' -d '{
  "personId": "XXXXX",
  "familyPrivacy": {
    "<FAMILY_MEMBER_ID>": {
      "basicInfo": 3,
      "lifeEvent": 3,
      "allergy": 3,
      "healthCondition": 3,
      "medication": 3,
      "vital": 3,
      "immunization": 3,
      "wellness": 3,
      "note": 3,
      "emergencyContact": 3,
      "insuranceAdvDirective": 3,
      "document": 2
    },
    "<FAMILY_MEMBER_ID>": {
      "basicInfo": 3,
      "lifeEvent": 3,
      "allergy": 3,
      "healthCondition": 3,
      "medication": 3,
      "vital": 3,
      "immunization": 3,
      "wellness": 3,
      "note": 3,
      "emergencyContact": 3,
      "insuranceAdvDirective": 3,
      "document": 3
    }
   },
  "nonFamilyPrivacy": {}
}' 'https://tapgenes.com/ehr/v1/privacy'
```

> Example Response

```json
{
  "personId": "XXXXX",
  "familyPrivacy": {
    "<FAMILY_MEMBER_ID>": {
      "basicInfo": 3,
      "lifeEvent": 3,
      "allergy": 3,
      "healthCondition": 3,
      "medication": 3,
      "vital": 3,
      "immunization": 3,
      "wellness": 3,
      "note": 3,
      "emergencyContact": 3,
      "insuranceAdvDirective": 3,
      "document": 2
    },
    "<FAMILY_MEMBER_ID>": {
      "basicInfo": 3,
      "lifeEvent": 3,
      "allergy": 3,
      "healthCondition": 3,
      "medication": 3,
      "vital": 3,
      "immunization": 3,
      "wellness": 3,
      "note": 3,
      "emergencyContact": 3,
      "insuranceAdvDirective": 3,
      "document": 3
    }
}
```

This endpoint is used to update a family and non-family privacy for the person

<aside class="notice">
You must replace `ACCESS_TOKEN` with your API request.
</aside>

## Get All Family Members Privacy

> API Endpoint

```
GET https://tapgenes.com/ehr/v1/privacy/{personId}
```

> Example Request

```curl
curl -X GET --header 'Accept: application/json' --header 'Authorization: OAuth2 <ACCESS_TOKEN>' 'https://tapgenes.com/ehr/v1/privacy/<PERSON_ID>'
```

> Example Response

```json
{
  "personId": "XXXXX",
  "familyPrivacy": {
    "<FAMILY_MEMBER_ID>": {
      "basicInfo": 3,
      "lifeEvent": 3,
      "allergy": 3,
      "healthCondition": 3,
      "medication": 3,
      "vital": 3,
      "immunization": 3,
      "wellness": 3,
      "note": 3,
      "emergencyContact": 3,
      "insuranceAdvDirective": 3,
      "document": 2
    },
    "<FAMILY_MEMBER_ID>": {
      "basicInfo": 3,
      "lifeEvent": 3,
      "allergy": 3,
      "healthCondition": 3,
      "medication": 3,
      "vital": 3,
      "immunization": 3,
      "wellness": 3,
      "note": 3,
      "emergencyContact": 3,
      "insuranceAdvDirective": 3,
      "document": 3
    },
    "<FAMILY_MEMBER_ID>": {
      "basicInfo": 3,
      "lifeEvent": 3,
      "allergy": 3,
      "healthCondition": 3,
      "medication": 3,
      "vital": 3,
      "immunization": 3,
      "wellness": 3,
      "note": 3,
      "emergencyContact": 3,
      "insuranceAdvDirective": 3,
      "document": 3
    },
    "<FAMILY_MEMBER_ID>": {
      "basicInfo": 3,
      "lifeEvent": 2,
      "allergy": 3,
      "healthCondition": 3,
      "medication": 3,
      "vital": 3,
      "immunization": 3,
      "wellness": 3,
      "note": 3,
      "emergencyContact": 3,
      "insuranceAdvDirective": 3,
      "document": 3
    },
    "<FAMILY_MEMBER_ID>": {
      "basicInfo": 3,
      "lifeEvent": 3,
      "allergy": 3,
      "healthCondition": 3,
      "medication": 3,
      "vital": 3,
      "immunization": 3,
      "wellness": 3,
      "note": 3,
      "emergencyContact": 3,
      "insuranceAdvDirective": 3,
      "document": 3
    }
  },
  "nonFamilyPrivacy": {}
}
```

This endpoint is used to get all the family member's privacy.

<aside class="notice">
You must replace `ACCESS_TOKEN` with your API request.
</aside>

## Get Family Members Privacy

> API Endpoint

```
POST https://tapgenes.com/ehr/v1/privacy/familyMembers
```

> Example Request

```curl
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'Authorization: OAuth2 <ACCESS_TOKEN>' -d '[XXXX]' 'https://tapgenes.com/ehr/v1/privacy/familyMembers'
```

> Example Response

```json
[
  {
    "personId": "XXXX",
    "familyPrivacy": {
      "XXXX": {
        "basicInfo": 3,
        "lifeEvent": 3,
        "allergy": 3,
        "healthCondition": 3,
        "medication": 3,
        "vital": 3,
        "immunization": 3,
        "wellness": 3,
        "note": 3,
        "emergencyContact": 3,
        "insuranceAdvDirective": 3,
        "document": 2
      },
      "XXXX": {
        "basicInfo": 3,
        "lifeEvent": 3,
        "allergy": 3,
        "healthCondition": 3,
        "medication": 3,
        "vital": 3,
        "immunization": 3,
        "wellness": 3,
        "note": 3,
        "emergencyContact": 3,
        "insuranceAdvDirective": 3,
        "document": 3
      },
      "XXXX": {
        "basicInfo": 3,
        "lifeEvent": 3,
        "allergy": 3,
        "healthCondition": 3,
        "medication": 3,
        "vital": 3,
        "immunization": 3,
        "wellness": 3,
        "note": 3,
        "emergencyContact": 3,
        "insuranceAdvDirective": 3,
        "document": 3
      },
      "XXXX": {
        "basicInfo": 3,
        "lifeEvent": 2,
        "allergy": 3,
        "healthCondition": 3,
        "medication": 3,
        "vital": 3,
        "immunization": 3,
        "wellness": 3,
        "note": 3,
        "emergencyContact": 3,
        "insuranceAdvDirective": 3,
        "document": 3
      },
      "XXXX": {
        "basicInfo": 3,
        "lifeEvent": 3,
        "allergy": 3,
        "healthCondition": 3,
        "medication": 3,
        "vital": 3,
        "immunization": 3,
        "wellness": 3,
        "note": 3,
        "emergencyContact": 3,
        "insuranceAdvDirective": 3,
        "document": 3
      }
    },
    "nonFamilyPrivacy": {}
  }
]
```

This endpoint is used to get the family members privacy based on the family member id.

<aside class="notice">
You must replace `ACCESS_TOKEN` with your API request.
</aside>

# Paywall

## Get All Premium Plans

> API Endpoint

```
GET https://tapgenes.com/ehr/v1/paywall/plans/all
```

> Example Request

```curl
curl -X GET --header 'Accept: application/json' --header 'Authorization: OAuth2 <ACCESS_TOKEN>' 'https://tapgenes.com/ehr/v1/paywall/plans/all'
```

> Example Response

```json
[
  {
    "id": "XXX",
    "planId": "XXXXXX",
    "planName": "XXXXXX",
    "price": 79,
    "trialPeriod": 0,
    "trialPeriodUnit": "month",
    "period": 1,
    "periodUnit": "year",
    "chargeModel": "flat_fee",
    "freeQuantity": 0,
    "setupCost": 0,
    "status": "active",
    "billingCycles": 0,
    "currencyCode": "USD",
    "planType": "Tapgenes",
    "createdDate": "2016-12-08",
    "modifiedDate": "2016-12-08",
    "isEnabledHostedPages": true
  },
  {
    "id": "XXX",
    "planId": "XXXXXXX",
    "planName": "XXXXXXXX",
    "description": "",
    "price": 200,
    "trialPeriod": 0,
    "trialPeriodUnit": "",
    "period": 1,
    "periodUnit": "year",
    "chargeModel": "flat_fee",
    "freeQuantity": 0,
    "setupCost": 0,
    "status": "active",
    "billingCycles": 0,
    "currencyCode": "USD",
    "inviteLimit": 0,
    "createdDate": "2017-05-30",
    "modifiedDate": "2017-05-30",
    "isEnabledHostedPages": true
  }
]
```

This endpoint is used to get all the premium plans.

<aside class="notice">
You must replace `ACCESS_TOKEN` with your API request.
</aside>

## Validate Coupon Code

> API Endpoint

POST https://tapgenes.com/ehr/v1/paywall/couponcode/validate

> Example Request

```curl
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'Authorization: OAuth2 <ACCESS_TOKEN>' -d '<COUPON_CODE>' 'https://tapgenes.com/ehr/v1/paywall/couponcode/validate'
```

> Example Response

```json
{
"response":"success"
}
```

This endpoint is used to validate the coupon code.

<aside class="notice">
You must replace `ACCESS_TOKEN` with your API request.
</aside>

## Create Subscription

> API Endpoint

POST https://tapgenes.com/ehr/v1/paywall/subscription/create

> Example Request

```curl
curl -X POST --header 'Content-Type: application/json' --header 'Accept: text/plain' --header 'Authorization: OAuth2 <ACCESS_TOKEN>' -d '{
  "couponCode": "string",
  "planId": "string",
  "name": "string",
  "discountType": "string",
  "discountPercentage": 0,
  "discountAmount": 0
}' 'https://tapgenes.com/ehr/v1/paywall/subscription/create'
```

> Example Response

```json
{
"message":"Subscription Created Successfully"
}
```

This endpoint is used to create a subscription with or without coupon code. If you have a coupon code, use this endpoint after validate the coupon code.

<aside class="notice">
You must replace `ACCESS_TOKEN` with your API request.
</aside>

## Update Subscription

> API Endpoint

POST https://tapgenes.com/ehr/v1/paywall/subscription/update

> Example Request

```curl
curl -X POST --header 'Content-Type: application/json' --header 'Accept: text/plain' --header 'Authorization: OAuth2 <ACCESS_TOKEN>' -d '{
  "couponCode": "string",
  "planId": "string",
  "name": "string",
  "discountType": "string",
  "discountPercentage": 0,
  "discountAmount": 0
}' 'https://tapgenes.com/ehr/v1/paywall/subscription/update'
```

> Example Response

```json
{
"message":"Subscription Updated Successfully"
}
```

This endpoint is used to update a subscription with or without coupon code. If you have a coupon code, use this endpoint after validate the coupon code.

<aside class="notice">
You must replace `ACCESS_TOKEN` with your API request.
</aside>

# Logout

> API Endpoint

```
POST https://tapgenes.com/ehr/v1/logout
```

> Example Request

```curl
https://tapgenes.com/ehr/v1/logout
```

This endpoint is used to logged out person session.

<aside class="notice">
You must replace `ACCESS_TOKEN` with your API request.
</aside>