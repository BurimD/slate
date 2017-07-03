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
    "Error": "Not a manager || Not authenticated"
}
```

- CODE `401`
- REASON `Non manager user requesting a manager view`
- BODY `Can raise security issues. Info leakage`


# Endpoints

## Login

> Call returns

```json
{
  "sessionID": "generated sessionID"
}
```

Login/authenticate against backend Server. User browser must support cookies. If user is autheticated through firebase a session is started in login. beegoSessionID cookie created using sha256. This cookie is used as key for redis. A random sessionID is generated and returned to user. This sessionID is stored within the redis object whose key is the session cookie. It is stored as the key for:
    sessionID -> beegoSessionID
The final mapping:
    beegoSessionID -> sessionID -> beegoSessionID||uid
SessionID and cookie need to be included in all future requests. validateSession checks if the above mapping is still valid in memory and returns true or false.

`GET http://dev.oraiapp.com/v1_5/sales/login/`

## Logout

> Call returns

```json
{
  "msg": "Session destroyed"
}
```

Delete session, and redis key-value pair. Cookie no longer sent to user browser.

## User Settings

> Call returns

```json
{
  "TID": "b4ko2l2a081gv2vfaitg",
  "ID": "KIhl1ZKGkNgEnfpELm50kpPMoNf1",
  "CID": "b4ko2kqa081gv2vfait0",
  "Email": "email",
  "Name": "John",
  "LastName": "Doe",
  "Image": "imgUrl",
  "Performance": 0,
  "Sessions": 0,
  "Manager": true,
  "TeamName": "OraiDemo"
}
```

Get user profile.

`GET http://dev.oraiapp.com/v1_5/sales/getUser/tid/uid/sessionid`


## User Sessions

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

Get user sessions.

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

Get team settings. Requester must be team manager.

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

Get team results. User must be team manager.

`GET http://sdev.tryoratio.com/sales/v1_5/getTeam/cid/tid/uid/sessionid`

## Products

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

Get products and modules. Requester must be a manager.

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

Get session.

`GET sdev.tryoration.com/v1_5/sales/getSesion/uid/id/sessionid`


## Individual Session Performance

> Call returns

``` json
{

}
```

Get session information for user.

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

Create company. Name, Location required.

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

Create new team. CID, Name, ManagerID required.

`GET http://sdev.tryoration.com/v1_5/sales/putTeam/sessionid`


## Create User

> Post input

```json
{
	"TID": "team ID",
	"CID": "CompanyID",
	"Email": "some email. Do not send for current user. Will get 400",
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

Create new user. TID, CID, Email, Name, LastName reuqired. Use this endpoint to create new user. No user created if invite does not exist. Invite deleted. iid=man user is a manager.

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

Create new product. TID, Name required.

`GET http://sdev.tryoration.com/v1_5/sales/putProduct/sessionid`

## Create Module

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

Create module. All but ID field required.

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

Send invitation to new user. TID, Email, TeamName, CID, ManagerName required. User must be a manager.

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

Handle invitations accepted by user.

`GET http://sdev.tryoration.com/v1_5/sales/getInvite/tid/id`

## Put Session

> POST Input

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

Create new session. Internal library function.

## Put Image

> POST input

```json
{
  "body": "[]byte",
  "type": "image/jpeg|image/png|image/bmp",
}
```

Enter image for user. Image needed for each team.

`GET http://sdev.tryoration.com/v1_5/sales/putImage/tid/uid`

## Update Company

> POST input

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
	"ID": "gcomapny ID",
	"Name": "some-name",
	"Location": "some-location",
	"Image": "some-image"
}
```

Update Company. Name, Location, WatsonID required. Old object replaced.

`POST http:/sdev.tryoration.com/sales/updateCompany/sessionid`

## Update Team

> POST input

```json
{
	"CID": "companyID",
	"Name": "some-name",
	"ManagerID": "some-id",
  "ID": "some-id"
}
```

> Call returns

```json
{
	"CID": "companyID",
	"ID": "team ID",
	"Name": "some-name",
	"ManagerID": "some-id"
}
```

Update Team. All attributes required. Old object replaced.

`POST http:/sdev.tryoration.com/sales/updateTeam/sessionid`

## Update User

> POST input

```json
{
	"TID": "team ID",
	"CID": "CompanyID",
  "ID": "userID",
	"Email": "some email. Do not send for current user. Will get 400",
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
	"ID": "user ID",
	"Email": "some email",
	"Name": "some-name",
	"LastName": "some-lastname",
	"Image": "some-image",
	"Performance": "int perf",
	"Sessions": "some sessions",
	"Manager": "bool manager"
}
```

Update User. TID, ID, CID, Name, LastName required. Old object replaced.

`POST http:/sdev.tryoration.com/sales/updateUser/sessionid`

## Update Product

> POST input

```json
{
	"TID": "team ID",
  "ID": "product ID",
	"Name": "some-name",
	"Image": "some-image"
}
```

> Call returns
```json
{
	"ID": "product ID",
  "TID": "team ID",
	"Name": "some-name",
	"Image": "some-image"
}
```


Update Product. TID, ID Name required. Old object replaced.

`POST http:/sdev.tryoration.com/sales/updateProduct/sessionid`

## Update Module

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

Update module. All fields required.

`POST http:/sdev.tryoration.com/sales/updateModule/cid/tid/sessionid`

## Delete Product

Delete product. All modules under product removed.

`DELETE http://dev.oraiapp.com/v1_5/sales/deleteProduct/cid/tid/pid/uid/sessionid`

## Delete Module

Delete module.

`DELETE http://dev.oraiapp.com/v1_5/sales/deleteModule/cid/tid/pid/mid/uid/sessionid`

## Delete Member

Delete member. All sessions under member removed.

`DELETE http://dev.oraiapp.com/v1_5/sales/deleteMember/cid/tid/uid/mid/sessionid`

## Delete Session

Delete session.

`DELETE dev.oraiapp.com/v1_5/sales/deleteSession/sid/uid/sessionid`

## Delete Invite

Delete invite.

`DELETE http://dev.oraiapp.com/v1_5/sales/deleteInvite/cid/tid/iid/mid/sessionid`
