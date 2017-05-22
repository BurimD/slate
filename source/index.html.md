---
title: API Reference

language_tabs:
  - json
---

# Issues
- Reduce calls

# HTTP Error Status Codes

## Internal Server Error

> Return
```json
{
    "Error": "Error code"
}
```

- CODE `500`
- REASON `Problem with a db connection or json marshaling`
- BODY `Can raise security problems. User can learn backend structure`


## Bad Request

> Return
```json
{
    "Error": "Item does not exist"
}
```

- CODE `400`
- REASON `One of the requested items does not exist`
- BODY `Can raise security problems. Info leakage`

## Unauthorized

> Return
```json
{
    "Error": "Not a manager"
}
```

- CODE `401`
- REASON `Non manager user requesting a manager view`
- BODY `Can raise security issues. Info leakage`


# Endpoints

## Profile Settings (View 11)

> Call returns
```json
{
	"TID": "b43oiie44tl41lagpvcg",
	"ID": "b43oiie44tl41lagpveg",
	"CID": "b41v1ve44tl62gbtoeug",
	"Email": "buriderveni@gmail.com",
	"Name": "Burim",
	"LastName": "Derveni",
	"Image": "Some image",
	"Status": "accepted",
	"Performance": 40,
	"Sessions": 1,
	"Manager": false
}
```

Use this endpoint to get profile settings for a user.

`GET http://dev.oraiapp.com/v1_5/sales/getUser/tid/uid/sessionid`


## Individual User Dashboard with Sessions

> Call returns
```json
{
  "LastName": "Derveni",
  "Name": "Burim",
  "Sessions": [
    {
      "UID": "b450it644tl7g9hmodsg",
      "ID": "b450it644tl7g9hmodrg",
      "Opportunity": "",
      "Module": "",
      "Date": "",
      "Duration": 0,
      "Score": 40
    }
  ]
}
```

Use this endpoint to get individual user dashboard including sessions

`GET http://sdev.tryoratio.com/v1_5/getUserSessions/tid/uid/sessionid`


## Team Settings

> Call returns
```json
{
  "Invited": [
    {
      "TID": "",
      "ID": "",
      "Email": "burimderveni@gmail.com",
      "Created": 0,
      "Company": ""
    }
  ],
  "Members": [
    {
      "TID": "",
      "ID": "",
      "CID": "",
      "Email": "tempuser@oratio.ai",
      "Name": "some-name",
      "LastName": "some-lastname",
      "Image": "",
      "Performance": 0,
      "Sessions": 0,
      "Manager": false
    }
  ],
  "Name": "selectTeam"
}
```

Use this endpoint to get team settings. Requester must be a manager.

`GET http://sdev.tryoration.com/v1_5/sales/getTeamSettings/cid/tid/uid/sessionid`


## Team Dashboard

> Call returns
```json
{
  "Members": [
    {
      "ID": "b450it644tl7g9hmodtg",
      "Image": "Some image",
      "LastName": "Gupta",
      "Name": "Paritosh",
      "Performance": "30"
    }
  ],
  "Name": "FrontEnd",
  "TID": "b450it644tl7g9hmodr0"
}
```

Use this endpoint to team results for a manager. Requester must be a manager

`GET http://sdev.tryoratio.com/sales/v1_5/getTeam/cid/tid/uid/sessionid`

## Manager Products

> Call returns
```json
{
  "Products": [
    {
      "ID": "b450it644tl7g9hmodu0",
      "Modules": [
        {
          "PID": "b450it644tl7g9hmodu0",
          "ID": "b450it644tl7g9hmodpg",
          "Name": "Development",
          "Instructions": [
            "Step 1",
            "Step 2"
          ],
          "Keywords": [
            "Word 1",
            "Word 2"
          ],
          "TargetTime": 15
        },
        {
          "PID": "b450it644tl7g9hmodu0",
          "ID": "b450it644tl7g9hmodq0",
          "Name": "PublicSpeaking",
          "Instructions": [
            "Step 1",
            "Step 2"
          ],
          "Keywords": [
            "Word 1",
            "Word 2"
          ],
          "TargetTime": 16
        }
      ],
      "Name": "Sales"
    },
    {
      "ID": "b4512m223akink066mp0",
      "Modules": [],
      "Name": "Education"
    }
  ]
}
```

Use this endpoint to get products and all corresponding modules under manager

`GET sdev.tryoration.com/v1_5/sales/getManagerProducts/cid/uid/sessionid`

## Get Session

> Call returns
```json
{
  "Final": true,
  "StartTimes": null,
  "EndTimes": null,
  "Words": null,
  "RawString": "",
  "Fillers": {
    "Summary": null,
    "Locations": null,
    "Recommendation": "Fillers distract your audience from focusing on your speech",
    "Total": 0
  },
  "Error": "",
  "WPM": {
    "WPM": null,
    "WPMRange": {
      "Blue": null,
      "Green": null,
      "Red": null
    },
    "Recommendation": "",
    "Average": 0
  },
  "Pauses": {
    "Pauses": null,
    "Recommendation": ""
  },
  "Projection": {
    "Labels": null,
    "Data": null,
    "Recommendation": "Need more data to show results",
    "Locations": null
  },
  "Energy": {
    "Values": null,
    "VocalVariation": 0,
    "Recommendation": ""
  },
  "TranscriptClarity": "",
  "Prompt": ""
}
```

Use this endpoint to get information about a session.

`GET sdev.tryoration.com/v1_5/sales/getSesion/uid/id/sessionid`

## Edit Module

> POST input
```json
{
	"PID": "product-id",
	"ID": "module-id",
	"Name ": "some - name ",
	"Instructions": ["string1", "string"],
	"Keywords": ["word1", "word2"],
	"TargetTime": "time"
}
```

> Call returns
```json
{
	"PID": "product-id",
	"ID": "module-id",
	"Name ": "some - name ",
	"Instructions": ["string1", "string"],
	"Keywords": ["word1", "word2"],
	"TargetTime": "time"
}
```

Use this endpoint to edit a module. Make sure to fill all the fields of the module. This will remove the old module and replace it

`POST http:/sdev.tryoration.com/sales/v1_5/postModule/uid/sessionid`


## Individual Session Performance

> Call returns
``` json
{

}'
```

Use this endpoint to get individual user performance.

`GET http://tryoration.com/sales/v1_5/getsession/uid/sid/sessionid`


## Create Company

> POST Input
```json
{
	"Name": "some-name",
	"Location": "some-location",
	"Image": "some-image"
}
```

> Call returns
```json
{
	"ID": "generated id",
	"Name": "some-name",
	"Location": "some-location",
	"Image": "some-image"
}
```

Use this endpoint to create a new company.

`GET http://sdev.tryoration.com/v1_5/sales/putCompany/sessionid`

## Create Team

> POST input
```json
{
	"CID": "companyID",
	"Name": "some-name",
	"ManagerID": "some-id"
}
```

> Call returns
```json
{
	"CID": "companyID",
	"ID": "generated ID",
	"Name": "some-name",
	"ManagerID": "some-id"
}
```

Use this endpoint to create a new team.

`GET http://sdev.tryoration.com/v1_5/sales/putTeam/sessionid`


## Create, Update User

> Post input
```json
{
	"TID": "team ID",
	"CID": "CompanyID",
	"Email": "some email",
	"Name": "some-name",
	"LastName": "some-lastname",
	"Image": "some-image",
	"Performance": 0,
	"Sessions": 0,
}
```

> Call returns
```json
{
	"TID": "team ID",
	"CID": "company ID",
	"ID": "generated ID",
	"Email": "some email",
	"Name": "some-name",
	"LastName": "some-lastname",
	"Image": "some-image",
	"Performance": "int perf",
	"Sessions": "some sessions",
	"Manager": "bool manager"
}
```

Use this endpoint to create or update a new user. Empty ID fields creates a new user. No user created if invite does not exist. Invite deleted. iid=man user is a manager.

`GET http://sdev.tryoration.com/v1_5/sales/putUser/iid/sessionid`

## Create Product

> POST input
```json
{
	"TID": "team ID",
	"Name": "some-name",
	"Image": "some-image"
}
```

> Call returns
```json
{
	"ID": "generated ID",
  "TID": "team ID",
	"Name": "some-name",
	"Image": "some-image"
}
```

Use this endpoint to create new product.

`GET http://sdev.tryoration.com/v1_5/sales/putProduct/sessionid`

## Create, Update Module

> POST input
```json
{
	"PID": "some-id",
	"Name ": "some-name",
	"Instructions": ["string1", "string"],
	"Keywords": ["word1", "word2"],
	"TargetTime": "time"
}
```

> Call returns
```json
{
	"PID": "some-id",
	"ID": "module-id",
	"Name ": "some - name ",
	"Instructions": ["string1", "string"],
	"Keywords": ["word1", "word2"],
	"TargetTime": "time"
}
```

Use this endpoint to create or update a new module. Empty ID fields creates a new module. Requester must e manager.

`GET http://sdev.tryoration.com/v1_5/sales/putModule/cid/tid/sessionid`

## Send Invite

> POST Input
```json
[
    {
      "TID": "someteamID",
      "Email": "someEmail@host.com",
      "TeamName": "Orai",
      "CID": "some id",
      "ManagerName": "someName",
    }
]
```

> Call returns
```json

```

Use this endpoint to send invitation to new user. Requester must be a manager

`GET http://sdev.tryoration.com/v1_5/sales/sendInvite/sessionid`

## Get Invite

> Call returns
```json
{
  "TID": "teamID",
  "ID": "generatedID",
  "Email": "email",
  "Created": 0,
  "TeamName": "team",
  "CID": "some id"
}
```

```json
{
"Error": "Not found"
}
```

```json
{
"Error": "Invitation expired"
}
```

Use this endpoint to handle an invitation accepted by a user.

`GET http://sdev.tryoration.com/v1_5/sales/getInvite/tid/id`

## Put Session

> Input
```json
{
  "Date": "some-date",
  "Duration": 7,
  "Module": "some-name",
  "Opportunity": "some-opportunity",
  "Score": 10,
  "UID": "userID",
  "MID": "module ID",
  "PID": "product ID",
}
```

Use this endpoint to put a new session. This is an internal package funciton.

## Put Image

> POST input
```json
{
  "body": "[]byte",
  "type": "image/jpeg|image/png|image/bmp",
}
```

Enter an image for a user. user must enter an image for each team he joins.

`GET http://sdev.tryoration.com/v1_5/sales/getInvite/tid/uid`

## Delete Product

Use this endpoint to delete product. All modules under product removed.

`GET http://dev.oraiapp.com/v1_5/sales/deleteProduct/cid/tid/pid/uid/sessionid`

## Delete Module

Use this endpoint to delete a module.

`GET http://dev.oraiapp.com/v1_5/sales/deleteModule/cid/tid/pid/mid/uid/sessionid`

## Delete Member

Use this endpoint to delete a module. All sessions under member removed.

`GET http://dev.oraiapp.com/v1_5/sales/deleteMember/cid/tid/uid/mid/sessionid`

## Delete Session

Use this endpoint to delete a session

`GET dev.oraiapp.com/v1_5/sales/deleteSession/sid/uid/sessionid`
