---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='https://www.a-boss.net'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the A-BOSS API!

# Authentication

Send a post request to our authenticate url and receive your oauth token. This will be used in all future calls to our api.



> To authentication, use this code:

```shell
curl "http://api.a-boss.net/v1/authenticate.json"
  -X POST
  -H "Content-Type: application/json"
  -d '{"user":"username", "password":"password"}'
```
> The above command returns JSON structured like this:

```json
{
  "token": "oauth_token"
}
```
# Profile

The profile endpoint returns information about the current user along with the projects and agencies he has access to.


### HTTP Request

`GET http://api.a-boss.net/v1/profile.json`

### URL Parameters

None

### Headers

`Authorization: Bearer oauth_token`

> To return the profile, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl "http://api.a-boss.net/v1/profile.json"
  -H "Authorization: Bearer oauth_token"
```

> The above command returns JSON structured like this:

```json
{
    "id": 1,
    "email": "email",
    "name": "name",
    "avatar": "https://artist.a-boss.net/images/default_profile.png",
    "projects": [
        {
            "id": 1,
            "title": "ABOSS",
            "project_code": "ABO"
        }
    ],
    "agencies": [
        {
            "id": 2,
            "title": "ABOSS Agency",
            "projects": [
                {
                    "id": 2,
                    "title": "ABOSS Agency Project",
                    "project_code": "AAP"
                }
            ]
        }
    ]
}
```

> Make sure to replace `oauth_token` with your API key.


<aside class="notice">
You must replace <code>oauth_token</code> with your personal API key.
</aside>

# Events

## Project events

This endpoint retrieves all events within a certain range for an artist.


### HTTP Request

`GET http://api.a-boss.net/v1/projects/<ID>/events.json`

### URL Parameters

Parameter | Example | Description
--------- | ------- | -----------
from | 2018-01-01 | Start of the time range for the events.
to | 2018-12-31 | End of the time range for the events.
limit | 50 | Number of events returned.
page | 5 | The page number. We calculate the offset based on the limit param.

If using only **from** parameter, the results will be sorted **ascending**.

If using **to**, results will be **descending** so that past events can also be paginated starting at that date.

### Headers

`Authorization: Bearer oauth_token`

> To return events for your project, use this code:

```shell
curl "http://api.a-boss.net/v1/projects/<ID>/events.json"
  -H "Authorization: Bearer oauth_token"
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "project_id": 2,
    "type": "event",
    "title": "Concert",
    "start": "2018-07-18T00:00:00.000+02:00",
    "end": "2018-07-18T01:00:00.000+02:00",
    "tba": true,
    "allday": null,
    "in_the_night": false,
    "event_type": null,
    "event_status": "option",
    "description": null,
    "event_website": null,
    "info": null,
    "location": {
      "id": 1,
      "title": "Royal Concertgebouw",
      "country": "Netherlands",
      "city": "Amsterdam",
      "street": "Concertgebouwplein",
      "home_number": "10",
      "postal_code": "1071 LN",
      "phone_number": "",
      "website": "",
      "region": "",
      "lat": "52.35630920000001",
      "lng": "4.879060400000071"
    },
    "availabilities": [],
    "event_color": null,
    "labels": [],
    "ticket_sales": [],
    "details": {
      "general": {
          "stage": null,
          "capacity": null,
          "timetable": null,
          "press": null,
          "set_recording": null
      },
      "deal": {
          "fee": null,
          "deal_percentage_artist": 0,
          "deal_percentage_venue": 0,
          "due_to_artist": 0,
          "due_to_booker": 0,
          "currency": "eur",
          "items": []
      },
      "travel": [
          {
            "id": 2,
            "event_type": "flight",
            "title": "Flight",
            "start": "2018-07-18T00:00:00.000+02:00",
            "end": "2018-07-18T01:00:00.000+02:00",
            "tba": false,
            "allday": null,
            "in_the_night": false
          },
          {
            "id": 3,
            "event_type": "hotel",
            "title": "Hotel stay",
            "start": "2018-07-18T00:00:00.000+02:00",
            "end": "2018-07-18T01:00:00.000+02:00",
            "tba": false,
            "allday": null,
            "in_the_night": false
          },
          {
            "id": 4,
            "event_type": "car",
            "title": "Car ride",
            "start": "2018-07-18T00:00:00.000+02:00",
            "end": "2018-07-18T01:00:00.000+02:00",
            "tba": false,
            "allday": null,
            "in_the_night": false
          },
          {
            "id": 5,
            "event_type": "train",
            "title": "Train ride",
            "start": "2018-07-18T00:00:00.000+02:00",
            "end": "2018-07-18T01:00:00.000+02:00",
            "tba": false,
            "allday": null,
            "in_the_night": false
          }
        ],
        "advancing": {
            "timeschedule": [],
            "contacts": [],
            "arrival": {
                "navigation": {
                    "street": null,
                    "home_number": null,
                    "postalcode": null,
                    "city": null,
                    "country": null
                },
                "route": null,
                "parking": null,
                "distance_parking_to_stage": null,
                "load_in": null,
                "catering": null,
                "dressing_room": null
            },
            "technical": {
                "technical": null,
                "audio": null,
                "light": null,
                "video": null,
                "sfx": null,
                "backline": null,
                "remarks": null
            },
            "other": {
                "merchandise": null,
                "clothing": null
            }
        },
        "files": [
            {
                "id": 0,
                "title": "Itinerary",
                "file_size": null,
                "url": ""
            }
        ],
        "setlist": [],
        "guestlist": []
    }
  }
]
```
## Agency Project events

This endpoint retrieves all events within a certain range for an artist belonging to an agency.


### HTTP Request

`GET http://api.a-boss.net/v1/agencies/<ID>/projects/<ID>/events.json`

### URL Parameters

Parameter | Example | Description
--------- | ------- | -----------
from | 2018-01-01 | Start of the time range for the events.
to | 2018-12-31 | End of the time range for the events.
limit | 50 | Number of events returned.
page | 5 | The page number. We calculate the offset based on the limit param.

If using only **from** parameter, the results will be sorted **ascending**.

If using **to**, results will be **descending** so that past events can also be paginated starting at that date.

### Headers

`Authorization: Bearer oauth_token`

> To return events for your project, use this code:

```shell
curl "http://api.a-boss.net/v1/agencies/<ID>/projects/<ID>/events.json"
  -H "Authorization: Bearer oauth_token"
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "project_id": 2,
    "type": "event",
    "title": "Concert",
    "start": "2018-07-18T00:00:00.000+02:00",
    "end": "2018-07-18T01:00:00.000+02:00",
    "tba": true,
    "allday": null,
    "in_the_night": false,
    "event_type": null,
    "event_status": "option",
    "description": null,
    "event_website": null,
    "info": null,
    "location": {
      "id": 1,
      "title": "Royal Concertgebouw",
      "country": "Netherlands",
      "city": "Amsterdam",
      "street": "Concertgebouwplein",
      "home_number": "10",
      "postal_code": "1071 LN",
      "phone_number": "",
      "website": "",
      "region": "",
      "lat": "52.35630920000001",
      "lng": "4.879060400000071"
    },
    "availabilities": [],
    "event_color": null,
    "labels": [],
    "ticket_sales": [],
    "details": {
      "general": {
          "stage": null,
          "capacity": null,
          "timetable": null,
          "press": null,
          "set_recording": null
      },
      "deal": {
          "fee": null,
          "deal_percentage_artist": 0,
          "deal_percentage_venue": 0,
          "due_to_artist": 0,
          "due_to_booker": 0,
          "currency": "eur",
          "items": []
      },
      "travel": [
          {
            "id": 2,
            "event_type": "flight",
            "title": "Flight",
            "start": "2018-07-18T00:00:00.000+02:00",
            "end": "2018-07-18T01:00:00.000+02:00",
            "tba": false,
            "allday": null,
            "in_the_night": false
          },
          {
            "id": 3,
            "event_type": "hotel",
            "title": "Hotel stay",
            "start": "2018-07-18T00:00:00.000+02:00",
            "end": "2018-07-18T01:00:00.000+02:00",
            "tba": false,
            "allday": null,
            "in_the_night": false
          },
          {
            "id": 4,
            "event_type": "car",
            "title": "Car ride",
            "start": "2018-07-18T00:00:00.000+02:00",
            "end": "2018-07-18T01:00:00.000+02:00",
            "tba": false,
            "allday": null,
            "in_the_night": false
          },
          {
            "id": 5,
            "event_type": "train",
            "title": "Train ride",
            "start": "2018-07-18T00:00:00.000+02:00",
            "end": "2018-07-18T01:00:00.000+02:00",
            "tba": false,
            "allday": null,
            "in_the_night": false
          }
        ],
        "advancing": {
            "timeschedule": [],
            "contacts": [],
            "arrival": {
                "navigation": {
                    "street": null,
                    "home_number": null,
                    "postalcode": null,
                    "city": null,
                    "country": null
                },
                "route": null,
                "parking": null,
                "distance_parking_to_stage": null,
                "load_in": null,
                "catering": null,
                "dressing_room": null
            },
            "technical": {
                "technical": null,
                "audio": null,
                "light": null,
                "video": null,
                "sfx": null,
                "backline": null,
                "remarks": null
            },
            "other": {
                "merchandise": null,
                "clothing": null
            }
        },
        "files": [
            {
                "id": 0,
                "title": "Itinerary",
                "file_size": null,
                "url": ""
            }
        ],
        "setlist": [],
        "guestlist": []
    }
  }
]
```
