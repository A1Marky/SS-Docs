# Authentication API

## Overview

This section of the documentation covers the authentication process for accessing the system. It details how users can authenticate using their email and password.

## Endpoints

### Sign In With Email and Password

Authenticates a user with email and password.

- **URL**: `https://identitytoolkit.googleapis.com/v1/accounts:signInWithPassword`
- **Method**: `POST`
- **URL Parameters**: Requires an API key as a query parameter: `?key=[API_KEY]`
- **Headers**:
  - `Content-Type`: application/json
  - `sec-ch-ua`: A string representing the user's browser information.
  - `X-Client-Version`: Client version.
  - `sec-ch-ua-mobile`: Indicates if the request is made from a mobile device.
  - `User-Agent`: The user agent string of the user's web browser.
  - `sec-ch-ua-platform`: The platform of the user's device.

- **Data Payload**:
json
{
"returnSecureToken": true,
"email": "user@example.com",
"password": "userPassword",
"clientType": "CLIENT_TYPE_WEB"
}


- **Success Response**:
  - **Code**: 200
  - **Content**:

  json
{
"kind": "identitytoolkit#VerifyPasswordResponse",
"localId": "userLocalId",
"email": "user@example.com",
"displayName": "UserDisplayName",
"idToken": "idTokenHere",
"registered": true,
"refreshToken": "refreshTokenHere",
"expiresIn": "3600"
}


- **Error Response**:
  - **Code**: 400 BAD REQUEST
  - **Content**: `{ error : "Error message" }`

- **Notes**:
  - The `idToken` received upon successful authentication must be used for authenticating subsequent requests.
  - The `expiresIn` field denotes the time in seconds until the token expires.
  - Ensure to replace sensitive information such as email and password with placeholders when documenting.


Remember to replace `[API_KEY]` with the actual API key in your documentation if it's intended for internal use, or instruct the reader on how to obtain their API key if the documentation is public. Also, consider adding a section on how to handle and refresh tokens based on the `expiresIn` and `refreshToken` fields for completeness.



# Games API

## Overview

This section describes the endpoint to retrieve information about basketball games on a specific date, site, and slate.

## Endpoints

### Get Games Information

Retrieves information about basketball games based on the specified date, site, and slate.

- **URL**: `https://basketball-sim.appspot.com/_ah/api/nba/v1/games`
- **Method**: `GET`
- **URL Parameters**:
  - `date`: The date for which to retrieve games information (format: YYYY-MM-DD).
  - `site`: The site identifier (e.g., `fd` for FanDuel).
  - `slate`: The unique identifier for the slate of games.
  - `sport`: The sport identifier (e.g., `nba`).

- **Headers**:
  - `Accept`: application/json, text/plain, */*
  - `Authorization`: Bearer token for authentication.
  - `sec-ch-ua`: A string representing the user's browser information.
  - `sec-ch-ua-mobile`: Indicates if the request is made from a mobile device.
  - `User-Agent`: The user agent string of the user's web browser.
  - `sec-ch-ua-platform`: The platform of the user's device.

- **Success Response**:
  - **Code**: 200
  - **Content**:
  json
{
"games": [
{
"away_score": 113.484,
"away_team": "NY",
"away_team_confirmed": true,
"away_wins": 0.4693,
"gid": "unique-game-id",
"home_score": 114.6387,
"home_team": "PHI",
"home_team_confirmed": true,
"home_wins": 0.5307,
"in_slate": true,
"num_games": "1500",
"proc_id": "process-id",
"start_time_js": "2024-02-23T00:00:00Z",
"time_tuple": "timestamp"
},
{
"away_score": 116.051,
"away_team": "SAS",
"away_team_confirmed": true,
"away_wins": 0.2303,
"gid": "unique-game-id",
"home_score": 126.691,
"home_team": "SAC",
"home_team_confirmed": true,
"home_wins": 0.7697,
"in_slate": false,
"num_games": "3000",
"proc_id": "process-id",
"start_time_js": "2024-02-23T03:00:00Z",
"time_tuple": "timestamp"
}
]
}
- **Notes**:
  - The `gid` field represents the unique identifier for each game.
  - The `proc_id` is a process identifier associated with the game.
  - `start_time_js` indicates the start time of the game in ISO 8601 format.
  - `time_tuple` is a timestamp representation of the game start time.
  - Ensure to replace sensitive information such as the Authorization token with placeholders when documenting.



# Slates API

## Overview

This section describes the endpoint to retrieve information about slates of basketball games for a specific date and sport.

## Endpoints

### Get Slates Information

Retrieves information about slates of games based on the specified date and sport.

- **URL**: `https://basketball-sim.appspot.com/_ah/api/nba/v1/slates`
- **Method**: `GET`
- **URL Parameters**:
  - `date`: The date for which to retrieve slates information (format: YYYY-MM-DD).
  - `sport`: The sport identifier (e.g., `nba`).

- **Headers**:
  - `Accept`: application/json, text/plain, */*
  - `Authorization`: Bearer token for authentication.
  - `sec-ch-ua`: A string representing the user's browser information.
  - `sec-ch-ua-mobile`: Indicates if the request is made from a mobile device.
  - `User-Agent`: The user agent string of the user's web browser.
  - `sec-ch-ua-platform`: The platform of the user's device.

- **Success Response**:
  - **Code**: 200
  - **Content**:
  json
{
"slates": [
{
"date": "2024-02-22",
"id": "unique-slate-id",
"name": "Slate Name",
"num_games": "Number of Games",
"provider_id": "Provider ID",
"site": "Site Identifier",
"start_time": "Slate Start Time"
}
// Additional slates here
]
}

- **Notes**:
  - The `id` field represents the unique identifier for each slate.
  - `date` indicates the date of the slate.
  - `name` provides a descriptive name for the slate.
  - `num_games` shows the number of games included in the slate.
  - `provider_id` is an identifier for the provider of the slate.
  - `site` indicates the site identifier (e.g., `fd` for FanDuel, `dk` for DraftKings).
  - `start_time` specifies the start time of the slate.
  - Ensure to replace sensitive information such as the Authorization token with placeholders when documenting.



  # Player Projections API

## Overview

This section describes the endpoint to retrieve player projections for basketball games on a specific date, site, and slate.

## Endpoints

### Get Player Projections

Retrieves projections for players based on the specified date, site, slate, and sport.

- **URL**: `https://basketball-sim.appspot.com/endpoints/get_player_projections`
- **Method**: `POST`
- **Headers**:
  - `Content-Type`: application/json
  - `Accept`: application/json, text/plain, */*
  - `Authorization`: Bearer token for authentication.
  - `sec-ch-ua`: A string representing the user's browser information.
  - `sec-ch-ua-mobile`: Indicates if the request is made from a mobile device.
  - `User-Agent`: The user agent string of the user's web browser.
  - `sec-ch-ua-platform`: The platform of the user's device.

- **Data Payload**:
json
{
"conditionals": [],
"date": "YYYY-MM-DD",
"percentile": "0",
"site": "Site Identifier",
"slate": "Slate Identifier",
"sport": "Sport Identifier"
}


- **Success Response**:
  - **Code**: 200
  - **Content**:

  json
{
"players": [
{
"name": "Player Name",
"team": "Team Identifier",
"position": "Player Position",
"projection": 33.4587,
"price": 7800,
"minutes": 35.3464,
"points": 14.2013,
"rebounds": 3.575,
"assists": 6.90467,
"steals": 1.20767,
"blocks": 0.711,
"turnovers": 1.14567,
"site": "Site Identifier",
"slate": "Slate Identifier",
"date": "YYYYMMDD",
// Additional player stats and projection details
}
// Additional players here
]
}


- **Notes**:
  - The response includes detailed projections for each player, including statistical categories like points, rebounds, assists, steals, and blocks.
  - The `site` and `slate` fields in the request payload specify the fantasy sports site and the specific slate of games for which projections are being requested.
  - Ensure to replace sensitive information such as the Authorization token with placeholders when documenting.



