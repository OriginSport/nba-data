*[English](README.md) ∙ [简体中文](README-zh-Hans.md)*

## API Document

## Player API
* [1. Query Player Info] 
* [2. Query Multiple Player Info] 
* [3. Query Player Stats]
* [4. Query Player Stats in Last Five Games]
* [5. Query Multiple Player Stats in Last Five Games]
* [6. Fetch Players By Game Date]


### 1. Query player info
* METHOD: `GET`
* URL: http://api.ttnbalite.com/api/nba/player/query/?player_id=2544

| Name      | Type  | Mandatory  | Description |
| ---           | ---       | ---   | --- |
| player_id     |   int      | true  | Player id

|       | Type    | Description |
| ---           | ---         | --- |
|   number| int         | Jersey Number
|  en_name       |      str       |English Name
|avatar_uri   | str| Player avatar URL
|wt|int|Weight
|height|int|Height


* Response：
```Namejson
{
  "ok": true,
  "data": {
    "number": 23,
    "en_name": "LeBron James",
    "avatar_uri": "player_avatar/2544.png",
    "wt":250,
    "height":203,
    "current_team": {
      "id":1610612739,
    }
    "stat":{
      "ast":9,
      "pts":27.3,
      "blk":0.9,
      "reb":8.7,
      "stl":1.5,
      "tov":4.3,
      "season_fpts":43.44
    }
  }
}
```

### 2. Query Multiple Player Info
* METHOD: `GET`
* URL: http://api.ttnbalite.com/api/nba/player/bulk/query/?player_ids=203115,2544

| Name      | Type  | Mandatory  | Description |
| ---           | ---       | ---   | --- |
| player_ids     |   int      | true  | One or multiple player id

| Response      | Type    | Description |
| ---           | ---         | --- |
|   number| int         | Jersey Number
|  en_name       |      str       |English name
|avatar_uri   | str| Player avatar URL
|wt|int|Weight
|height|int|Height


* Response：
```json
{
  "ok": true,
  "data": {
    "2544":{"number": 23,
            "en_name": "LeBron James",
            "avatar_uri": "player_avatar/2544.png",
            "wt":250,
            "height":203,
            "current_team": {
              "id":1610612739,
            }
    "203115":{"number": 5,
              "en_name": "Will Barton",
              "avatar_uri": "player_avatar/203115.png",
              "wt":190,
              "height":198,
              "current_team": {
                "id":1610612743,
            }
    }
  }
}
```


### 3. Query Player Stats
* METHOD: `GET`
* URL: http://api.ttnbalite.com/api/nba/player/statistic/?category=steals&season_type=playoff

| Name      | Type  | Mandatory  | Description |
| ---           | ---       | ---   | --- |
| category     |   str      | true  | [points, rebounds, assists, steals, blocks] Choose a category
|season_type  | str |true   |[regular, playoff] Choose a season type

| Response      | Type    | Description |
| ---           | ---         | --- |
|   id| int         | id
|  val       |   float          |Value
|season   | int| Season



* Response：
```json
{
  "ok": true,
  "data": {
    "id": 1172,
    "val": "3.5",
    "season": 2016,
    "player": {
      "id": "200765",
      "en_name":"Rajon Rondo",
      "tid":1610612740,
    }
  }
}
```


### 4. Query Player Stats in Last Five Games
* METHOD: `GET`
* URL: http://api.ttnbalite.com/api/nba/player/latest/boxscore/?player_id=2544

| Name      | Type  | Mandatory  | Description |
| ---           | ---       | ---   | --- |
| player_id     |   int      | true  | Player id

| Response      | Type    | Description |
| ---           | ---         | --- |
|   reb| int         | Rebounds
|  stl       |      int       |Steals
|ast   | int| Assists
|  blk      | int  |Blocks
|pts   |int|Points
|  tov    | int  |Turnovers
|fan_pts|float|Fantasy Points（pts+1.2*reb+1.5*ast+2.0*stl+2.0*blk-tov）


* Response：
```json
{
  "ok": true,
  "data": {
    {"reb":12,
     "stl":2,
     "ast":10,
     "blk":1,
     "pts":26,
     "tov":6,
     "fan_pts":56.4,
    },
    {"reb":12,
     "stl":2,
     "ast":10,
     "blk":1,
     "pts":26,
     "tov":6,
     "fan_pts":56.4,
    },
    {"reb":13,
     "stl":1,
     "ast":12,
     "blk":2,
     "pts":33,
     "tov":6,
     "fan_pts":55.6,
    },
    {"reb":12,
     "stl":2,
     "ast":10,
     "blk":1,
     "pts":26,
     "tov":6,
     "fan_pts":56.4,
    },
    {"reb":12,
     "stl":2,
     "ast":10,
     "blk":1,
     "pts":26,
     "tov":6,
     "fan_pts":56.4,
    },
    }
  }
}
```


### 5. Query Multiple Player Stats in Last Five Games
* METHOD: `GET`
* URL: http://api.ttnbalite.com/api/nba/players/latest/boxscore/?player_ids=2544,201566

| Name      | Type  | Mandatory  | Description |
| ---           | ---       | ---   | --- |
| player_ids     |   int      | true  | Player id

| Response      | Type    | Description |
| ---           | ---         | --- |
|   reb| int         | Rebounds
|  stl       |      int       |Steals
|ast   | int| Assits
|pts   |int|Points
|  blk      | int  |Blocks
|  tov    | int  |Turnovers
|fan_pts|float|Fantasy Points（pts+1.2*reb+1.5*ast+2.0*stl+2.0*blk-tov）

* Response：
```json
{
  "ok": true,
  "data":{ 
    "2544":{
      "reb":12,
      "stl":2,
      "ast":10,
      "blk":1,
      "pts":26,
      "tov":6,
      "fan_pts":56.4,
    },
    "201566":{
      "reb":13,
      "stl":2,
      "ast":14,
      "blk":0,
      "pts":37,
      "tov":5,
      "fan_pts":65.6,
   }
  }
}
```


### 6. Fetch Players By Game Date
* METHOD: `GET`
* URL: http://api.ttnbalite.com/api/nba/player/daily/list/?game_date=2018-03-22

| Name      | Type  | Mandatory  | Description |
| ---           | ---       | ---   | --- |
| game_date     |   str     | true  | Game Date

| Response      | Type    | Description |
| ---           | ---         | --- |
|   number| int         | Jersey Number
|  en_name       |      str       |English name
|avatar_uri   | str| Player avatar URL
|wt|int|Weight
|height|int|Height

* Response：
```json
{
  "ok": true,
  "data":[ 
    {
    "number": 23,
    "en_name": "LeBron James",
    "avatar_uri": "player_avatar/2544.png",
    "wt":250,
    "height":203,
    "current_team": {
      "id":1610612739,
    },
    {
    "number": 5,
    "en_name": "Will Barton",
    "avatar_uri": "player_avatar/203115.png",
    "wt":190,
    "height":198,
    "current_team": {
      "id":1610612743,
    }
 
  ]
}
```
## Team API

* [1. Query Team Info]  
* [2. Query All Team Info] 
* [3. Query League Standing] 
* [4. Query Result in Last Five Games] 


### 1. Query Team Info
* METHOD: `GET`
* URL: http://api.ttnbalite.com/api/nba/team/query/?team_id=1610612739

| Name      | Type  | Mandatory  | Description |
| ---           | ---       | ---   | --- |
| team_id     |   int      | true  | Team id

| Response      | Type    | Description |
| ---           | ---         | --- |
|  en_name       |      str       |English name
|id   | int| Team id
|division| str| Team Division


* Response：
```json
{
  "ok": true,
  "data": {
    "en_name": "Cavaliers",
    "id": 1610612739,
    "division": "中部区"
  }
}
```

### 2. Query All Team Info
* METHOD: `GET`
* URL: http://api.ttnbalite.com/api/nba/team/all/

| Name      | Type  | Mandatory  | Description |
| ---           | ---       | ---   | --- |
|  None    |         |   | 

| Response      | Type    | Description |
| ---           | ---         | --- |
|  en_name       |      str       |English name
|id   | int| Team id
|division| str| Team Division


* Response：
```json
{
  "ok": true,
  "data": [
  { 
    "en_name": "Hawks",
    "id": 1610612737,
    "division": "东南区"
  },
  { 
    "en_name": "Nuggets",
    "id": 1610612743,
    "division": "西北区"
  }
  { 
    "en_name": "Cavaliers",
    "id": 1610612739,
    "division": "中部区"
  }
  ]
}
```


### 3. Query League Standing
* METHOD: `GET`
* URL: http://api.ttnbalite.com/api/nba/team/standing/

| Name      | Type  | Mandatory  | Description |
| ---           | ---       | ---   | --- |
|  None    |         |   | 

| Response      | Type    | Description |
| ---           | ---         | --- |
|  order | int       | Rank
|  team       |      str       |Team Info
|conf   | str| Team Conference
|div| str| Team Division


* Response：
```json
{
  "ok": true,
  "data": {
      "East":[
        {"order":1,
        "team":{
          "id":1610612739,
      }
        "conf":"East",
        "div":"Central"},
        {"order":2,
        "team":{
          "id":1610612745,
      }
        "conf":"East",
        "div":"Atlantic"
          
      }
      ]
      
       "West":[
        {"order":1,
        "team":{
          "id":1610612745,
      }
        "conf":"West",
        "div":"Southwest"},
       {"order":2,
        "team":{
          "id":1610612744,
      }
        "conf":"West",
        "div":"Pacific"
      }
      ]
      
  }
}
```


### 4. Query Result in Last Five Games
* METHOD: `GET`
* URL: http://api.ttnbalite.com/api/nba/team/latest/boxscore/?team_id=1610612739

| Name      | Type  | Mandatory  | Description |
| ---           | ---       | ---   | --- |
| team_id     |   int      | true  | Team id

| Response      | Type    | Description |
| ---           | ---         | --- |
|   date| str        | Game Date
|  result       |      str       |Result
|home_team_boxscore   | str| Home Team Box Score
|away_team_boxscore| str|Away Team Box Score


* Response：
```json
{
  "ok": true,
  "data": {
    "date": "2018-03-20",
    "result": "117-124",
    "home_team_boxscore":{
        "ast":24,
        "pts":124,
        "blk":6,
        "reb":42,
        "team":1610612739,
        "game": "0021701050",
        }
    "away_team_boxscore": {
        "ast":26,
        "pts":117,
        "blk":7,
        "reb":32,
        "team":1610612749,
        "game": "0021701050",
        }
        }
 
}
}
```


## Game API

* [1. Query Game Status] 
* [2. Query Game Info] 
* [3. Query Game By Date] 
* [4. Query Multiple Game Info] 


### 1. Query Game Status
* METHOD: `GET`
* URL: http://api.ttnbalite.com/api/nba/game/state/

| Name      | Type  | Mandatory  | Description |
| ---           | ---       | ---   | --- |
|  None    |         |   | 

| Response      | Type    | Description |
| ---           | ---         | --- |
|  game_state | str       | Game Status
|previous_game_dates   | str| Previous Game Day
|next_game_dates| str| Next Game Day
|game_date|str| Current Game Day


* Response：
```json
{
  "ok": true,
  "data": {
    "game_state":"PRE",
    "can_play_live_betting":true,
    "previous_game_dates":["2018-03-20"],
    "next_game_dates": ["2018-03-22"],
    "game_date":"2018-03-21"
  }
}
```

### 2. Query Game Info
* METHOD: `GET`
* URL: http://api.ttnbalite.com/api/nba/game/detail/?game_id=0011600017

| Name      | Type  | Mandatory  | Description |
| ---           | ---       | ---   | --- |
|  game_id    |    int     | true  | Game id

| Response      | Type    | Description |
| ---           | ---         | --- |
|  date | str       | Game Date
|  result     | str      |Game Result
|home_team_boxscore   | str| Home Team Box Score
|away_team_boxscore| str| Away Team Box Score



* Response：
```json
{
  "ok": true,
  "data": {
    "date":"2016-10-06",
    "result":"102-117",
    "home_team_boxscore":{
        "ast":30,
        "blk":4,
        "reb":42,
        "stl":10,
        "pts":117,
        "game":"0011600017",
    },
    "away_team_boxscore":{
        "ast":23,
        "blk":3,
        "reb":37,
        "stl":8,
        "pts":102,
        "game":"0011600017",
    },
  }
}
```

### 3. Query Game By Date
* METHOD: `GET`
* URL: http://api.ttnbalite.com/api/nba/game/list/by/date/?date=2018-03-20

| Name      | Type  | Mandatory  | Description |
| ---           | ---       | ---   | --- |
|  date    |    str     | true  | Game Date

| Response      | Type    | Description |
| ---           | ---         | --- |
|  date | str       | Game Date
|  result     | str      |Game Result
|home_team_boxscore   | str| Home Team Box Score
|away_team_boxscore| str| Away Team Box Score



* Response：
```json
{
  "ok": true,
  "data": [
  {
    "date":"2018-03-20",
    "result":"117-124",
    "home_team_boxscore":{
        "ast":24,
        "blk":6,
        "reb":42,
        "stl":4,
        "pts":124,
        "game":"0021701050",
    },
    "away_team_boxscore":{
        "ast":26,
        "blk":7,
        "reb":32,
        "stl":11,
        "pts":117,
        "game":"0021701050",
    },
    {
    "date":"2018-03-20",
    "result":"100-110",
    "home_team_boxscore":{
        "ast":24,
        "blk":8,
        "reb":44,
        "stl":9,
        "pts":110,
        "game":"0021701051",
    },
    "away_team_boxscore":{
        "ast":20,
        "blk":3,
        "reb":47,
        "stl":4,
        "pts":100,
        "game":"0021701051",
    },
    ]
  }
}
```

### 4. Query Multiple Game Info
* METHOD: `GET`
* URL: http://api.ttnbalite.com/api/nba/game/bulk/query/?game_ids=0011600001

| Name      | Type  | Mandatory  | Description |
| ---           | ---       | ---   | --- |
|  game_ids    |    int     | true  | Game id

| Response      | Type    | Description |
| ---           | ---         | --- |
|  date | str       | Game Date
|  result     | str      |Game Result
|home_team_boxscore   | str| Home Team Box Score
|away_team_boxscore| str| Away Team Box Score



* Response：
```json
{
  "ok": true,
  "data": 
    "0011600001":{
      "date":"2016-10-02
      "result":"93-97"
      "home_team_boxscore":{
        "ast":14,
        "blk":7,
        "reb":58,
        "stl":4,
        "pts":97,
        "game":"0011600001",
    },
      "away_team_boxscore":{
        "ast":19,
        "blk":7,
        "reb":42,
        "stl":15,
        "pts":93,
        "game":"0011600001",
    },
    
  }
}
```

## Playoff API

* [1. Query Playoff Info] 

### 1. Query Playoff Info
* METHOD: `GET`
* URL: http://api.ttnbalite.com/api/nba/playoff/series/

| Name      | Type  | Mandatory  | Description |
| ---           | ---       | ---   | --- |
|  None    |         |   | 

| Response      | Type    | Description |
| ---           | ---         | --- |
|  round | int      | Round
| tid1      |    int      |Team1 id
|tid2   | int| Team2 id
|conference| str| Conference
|season|str|Season
|series|str|Series Stats


* Response：
```json
{
  "ok": true,
  "data": {
    "west":[{
      "round":1,
      "series":[{
        "tid1":1610612744,
        "tid2":1610612757,
        "conference":"West",
        "season":"2016-17"}]
    }]
    "east":[{
      "round":1,
      "series":[{
        "tid1":1610612738,
        "tid2":1610612741,
        "conference":"East",
        "season":"2016-17"}]
    }]
  }
}
```

## News API
* [1. Query News] 

### 1. Query News
* METHOD: `GET`
* URL: http://api.ttnbalite.com/api/nba/playoff/series/

| Name      | Type  | Mandatory  | Description |
| ---           | ---       | ---   | --- |
|  None    |         |   | 

| Response      | Type    | Description |
| ---           | ---         | --- |
|  date | str      | Date
|   player| int| Player id



* Response：
```json
{
  "ok": true,
  "data": {
    "date":'2018-03-20',
    "black_list": [
      {
       "player": "202738",
      }
    ]
    "red_list": [
      {
       "player": "2544",
      }
    ]
  }
}
```



## Injury API

* [1. Query Injury Player By Team] 
* [2. Query All Injury Players] 

### 1. Query Injury Player By Team
* METHOD: `GET`
* URL: http://api.ttnbalite.com/api/injury/query/team/

| Name      | Type  | Mandatory  | Description |
| ---           | ---       | ---   | --- |
|  None    |         |   | 

| Response      | Type    | Description |
| ---           | ---         | --- |
|  date | str      | Date
|   en_ex_return| str| Expected Return Time
|name|str|Player Name



* Response：
```json
{
  "ok": true,
  "data": [{
    "date":'12/23/17',
    "name":"Nikola Vucevic",
    "en_injury":"Hand",
    "en_ex_return":"Expected to be out until at least Feb 3"
  },
  { "date":'12/14/17',
    "name":"Mirza Teletovic",
    "en_injury":"Illness",
    "en_ex_return":"Expected to be out until at least Feb 1"
  }]
}
```

### 2. Query All Injury Players
* METHOD: `GET`
* URL: http://api.ttnbalite.com/api/injury/list/all/

| Name      | Type  | Mandatory  | Description |
| ---           | ---       | ---   | --- |
|  None    |         |   | 

| Response      | Type    | Description |
| ---           | ---         | --- |
|  date | str      | Date
|   en_ex_return| str| Expected Return Time
|name|str|Player Name



* Response：
```json
{
  "ok": true,
  "data": [{
    "date":'12/23/17',
    "name":"Nikola Vucevic",
    "en_injury":"Hand",
    "en_ex_return":"Expected to be out until at least Feb 3"
  },
  { "date":'12/14/17',
    "name":"Mirza Teletovic",
    "en_injury":"Illness",
    "en_ex_return":"Expected to be out until at least Feb 1"
  }]
}
```
