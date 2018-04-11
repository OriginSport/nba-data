## API接口文档

## Player API
* [1. 查询球员信息] 
* [2. 查询多个球员信息] 
* [3. 查询球员数据]
* [4. 查询球员最近五场比赛数据]
* [5. 查询多个球员最近五场比赛数据]
* [6. 根据日期查询参赛球员]


### 1. 查询球员信息
* 方法: `GET`
* URL: http://api.ttnbalite.com/api/nba/player/query/?player_id=2544

| 输入参数      | 参数类型  | 必填  | 参数说明 |
| ---           | ---       | ---   | --- |
| player_id     |   int      | true  | 球员 id

| 输出参数      | 参数类型    | 参数说明 |
| ---           | ---         | --- |
|   number| int         | 球衣号码
|  en_name       |      str       |英文名字
|avatar_uri   | str| 球员头像URL
|cn_name| str| 中文名字
|wt|int|体重
|height|int|身高


* 结果示例：
```json
{
  "ok": true,
  "data": {
    "number": 23,
    "en_name": "LeBron James",
    "avatar_uri": "player_avatar/2544.png",
    "cn_name":"勒布朗-詹姆斯",
    "wt":250,
    "height":203,
    "current_team": {
      "cn_name": "骑士",
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

### 2. 查询多个球员信息
* 方法: `GET`
* URL: 'http://api.ttnbalite.com/api/nba/player/bulk/query/?player_ids=203115,2544'

| 输入参数      | 参数类型  | 必填  | 参数说明 |
| ---           | ---       | ---   | --- |
| player_ids     |   int      | true  | 一个或多个球员 id

| 输出参数      | 参数类型    | 参数说明 |
| ---           | ---         | --- |
|   number| int         | 球衣号码
|  en_name       |      str       |英文名字
|avatar_uri   | str| 球员头像URL
|cn_name| str| 中文名字
|wt|int|体重
|height|int|身高


* 结果示例：
```json
{
  "ok": true,
  "data": {
    "2544":{"number": 23,
            "en_name": "LeBron James",
            "avatar_uri": "player_avatar/2544.png",
            "cn_name":"勒布朗-詹姆斯",
            "wt":250,
            "height":203,
            "current_team": {
              "cn_name": "骑士",
              "id":1610612739,
            }
    "203115":{"number": 5,
              "en_name": "Will Barton",
              "avatar_uri": "player_avatar/203115.png",
              "cn_name":"威尔-巴顿",
              "wt":190,
              "height":198,
              "current_team": {
                "cn_name": "掘金",
                "id":1610612743,
            }
    }
  }
}
```


### 3. 查询球员数据
* 方法: `GET`
* URL: 'http://api.ttnbalite.com/api/nba/player/statistic/?category=steals&season_type=playoff'

| 输入参数      | 参数类型  | 必填  | 参数说明 |
| ---           | ---       | ---   | --- |
| category     |   str      | true  | points,rebounds,assists,steals,blocks 任意一项
|season_type  | str |true   |regular,playoff 任意一项

| 输出参数      | 参数类型    | 参数说明 |
| ---           | ---         | --- |
|   id| int         | id
|  val       |   float          |球员数据
|season   | int| 赛季数据时间



* 结果示例：
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


### 4. 查询球员最近五场比赛数据及范特西评分
* 方法: `GET`
* URL: 'http://api.ttnbalite.com/api/nba/player/latest/boxscore/?player_id=2544'

| 输入参数      | 参数类型  | 必填  | 参数说明 |
| ---           | ---       | ---   | --- |
| player_id     |   int      | true  | 球员 id

| 输出参数      | 参数类型    | 参数说明 |
| ---           | ---         | --- |
|   reb| int         | 篮板
|  stl       |      int       |抢断
|ast   | int| 助攻
|  blk      | int  |盖帽
|pts   |int|得分
|  tov    | int  |失误
|fan_pts|float|范特西评分（pts+1.2*reb+1.5*ast+2.0*stl+2.0*blk-tov）


* 结果示例：
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

### 5. 查询多个球员最近一场比赛数据及范特西评分
* 方法: `GET`
* URL: 'http://api.ttnbalite.com/api/nba/players/latest/boxscore/?player_ids=2544,201566'

| 输入参数      | 参数类型  | 必填  | 参数说明 |
| ---           | ---       | ---   | --- |
| player_ids     |   int      | true  | 球员 id

| 输出参数      | 参数类型    | 参数说明 |
| ---           | ---         | --- |
|   reb| int         | 篮板
|  stl       |      int       |抢断
|ast   | int| 助攻
|pts   |int|得分
|  blk      | int  |盖帽
|  tov    | int  |失误
|fan_pts|float|范特西评分（pts+1.2*reb+1.5*ast+2.0*stl+2.0*blk-tov）

* 结果示例：
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



### 6. 根据日期查询参赛球员
* 方法: `GET`
* URL: 'http://api.ttnbalite.com/api/nba/player/daily/list/?game_date=2018-03-22'

| 输入参数      | 参数类型  | 必填  | 参数说明 |
| ---           | ---       | ---   | --- |
| game_date     |   str     | true  | 比赛日期

| 输出参数      | 参数类型    | 参数说明 |
| ---           | ---         | --- |
|   number| int         | 球衣号码
|  en_name       |      str       |英文名字
|avatar_uri   | str| 球员头像URL
|cn_name| str| 中文名字
|wt|int|体重
|height|int|身高

* 结果示例：
```json
{
  "ok": true,
  "data":[ 
    {
    "number": 23,
    "en_name": "LeBron James",
    "avatar_uri": "player_avatar/2544.png",
    "cn_name":"勒布朗-詹姆斯",
    "wt":250,
    "height":203,
    "current_team": {
      "cn_name": "骑士",
      "id":1610612739,
    },
    {
    "number": 5,
    "en_name": "Will Barton",
    "avatar_uri": "player_avatar/203115.png",
    "cn_name":"威尔-巴顿",
    "wt":190,
    "height":198,
    "current_team": {
      "cn_name": "掘金",
      "id":1610612743,
    }
 
  ]
}
```
## Team API

* [1. 查询球队信息]  
* [2. 查询所有球队信息] 
* [3. 查询东西部球队排名] 
* [4. 查询球队最近五场比赛结果] 


### 1. 查询球队信息
* 方法: `GET`
* URL: 'http://api.ttnbalite.com/api/nba/team/query/?team_id=1610612739'

| 输入参数      | 参数类型  | 必填  | 参数说明 |
| ---           | ---       | ---   | --- |
| team_id     |   int      | true  | 球队 id

| 输出参数      | 参数类型    | 参数说明 |
| ---           | ---         | --- |
|   cn_name| str        | 中文名字
|  en_name       |      str       |英文名字
|id   | int| 球队 id
|division| str| 球队分区


* 结果示例：
```json
{
  "ok": true,
  "data": {
    "cn_name": "骑士",
    "en_name": "Cavaliers",
    "id": 1610612739,
    "division": "中部区"
  }
}
```

### 2. 查询所有球队信息
* 方法: `GET`
* URL: 'http://api.ttnbalite.com/api/nba/team/all/'

| 输入参数      | 参数类型  | 必填  | 参数说明 |
| ---           | ---       | ---   | --- |
|  无    |         |   | 

| 输出参数      | 参数类型    | 参数说明 |
| ---           | ---         | --- |
|   cn_name| str        | 中文名字
|  en_name       |      str       |英文名字
|id   | int| 球队 id
|division| str| 球队分区


* 结果示例：
```json
{
  "ok": true,
  "data": [
  { "cn_name": "老鹰",
    "en_name": "Hawks",
    "id": 1610612737,
    "division": "东南区"
  },
  { "cn_name": "掘金",
    "en_name": "Nuggets",
    "id": 1610612743,
    "division": "西北区"
  }
  { "cn_name": "骑士",
    "en_name": "Cavaliers",
    "id": 1610612739,
    "division": "中部区"
  }
  ]
}
```


### 3. 查询东西部球队排名
* 方法: `GET`
* URL: 'http://api.ttnbalite.com/api/nba/team/standing/'

| 输入参数      | 参数类型  | 必填  | 参数说明 |
| ---           | ---       | ---   | --- |
|  无    |         |   | 

| 输出参数      | 参数类型    | 参数说明 |
| ---           | ---         | --- |
|  order | int       | 排名
|  team       |      str       |球队信息
|conf   | str| 球队东西部分区
|div| str| 球队分区


* 结果示例：
```json
{
  "ok": true,
  "data": {
      "East":[
        {"order":1,
        "team":{
          "cn_name":'骑士'，
          "id":1610612739,
      }
        "conf":"East",
        "div":"Central"},
        {"order":2,
        "team":{
          "cn_name":'凯尔特人'，
          "id":1610612745,
      }
        "conf":"East",
        "div":"Atlantic"
          
      }
      ]
      
       "West":[
        {"order":1,
        "team":{
          "cn_name":'火箭'，
          "id":1610612745,
      }
        "conf":"West",
        "div":"Southwest"},
       {"order":2,
        "team":{
          "cn_name":'勇士'，
          "id":1610612744,
      }
        "conf":"West",
        "div":"Pacific"
      }
      ]
      
  }
}
```


### 4. 查询球队最近五场比赛结果
* 方法: `GET`
* URL: 'http://api.ttnbalite.com/api/nba/team/latest/boxscore/?team_id=1610612739'

| 输入参数      | 参数类型  | 必填  | 参数说明 |
| ---           | ---       | ---   | --- |
| team_id     |   int      | true  | 球队 id

| 输出参数      | 参数类型    | 参数说明 |
| ---           | ---         | --- |
|   date| str        | 比赛日期
|  result       |      str       |比分
|home_team_boxscore   | str| 主队比赛数据详情
|away_team_boxscore| str|客队比赛数据详情


* 结果示例：
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

* [1. 查询比赛状态] 
* [2. 查询比赛信息] 
* [3. 根据日期查询比赛] 
* [4. 查询多个比赛信息] 



### 1. 查询比赛状态
* 方法: `GET`
* URL: 'http://api.ttnbalite.com/api/nba/game/state/'

| 输入参数      | 参数类型  | 必填  | 参数说明 |
| ---           | ---       | ---   | --- |
|  无    |         |   | 

| 输出参数      | 参数类型    | 参数说明 |
| ---           | ---         | --- |
|  game_state | str       | 比赛状态
|  can_play_live_betting      |      bool       |是否可以开即时竞猜
|previous_game_dates   | str| 前一个比赛日
|next_game_dates| str| 下一个比赛日
|game_date|str|当前比赛日


* 结果示例：
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

### 2. 查询比赛信息
* 方法: `GET`
* URL: 'http://api.ttnbalite.com/api/nba/game/detail/?game_id=0011600017'

| 输入参数      | 参数类型  | 必填  | 参数说明 |
| ---           | ---       | ---   | --- |
|  game_id    |    int     | true  | 比赛 id

| 输出参数      | 参数类型    | 参数说明 |
| ---           | ---         | --- |
|  date | str       | 比赛日期
|  result     | str      |比赛结果
|home_team_boxscore   | str| 主队数据统计
|away_team_boxscore| str| 客队数据统计



* 结果示例：
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

### 3. 根据日期查询比赛
* 方法: `GET`
* URL: 'http://api.ttnbalite.com/api/nba/game/list/by/date/?date=2018-03-20'

| 输入参数      | 参数类型  | 必填  | 参数说明 |
| ---           | ---       | ---   | --- |
|  date    |    str     | true  | 比赛日期

| 输出参数      | 参数类型    | 参数说明 |
| ---           | ---         | --- |
|  date | str       | 比赛日期
|  result     | str      |比赛结果
|home_team_boxscore   | str| 主队数据统计
|away_team_boxscore| str| 客队数据统计



* 结果示例：
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

### 4. 查询多个比赛信息
* 方法: `GET`
* URL: 'http://api.ttnbalite.com/api/nba/game/bulk/query/?game_ids=0011600001'

| 输入参数      | 参数类型  | 必填  | 参数说明 |
| ---           | ---       | ---   | --- |
|  game_ids    |    int     | true  | 比赛 id

| 输出参数      | 参数类型    | 参数说明 |
| ---           | ---         | --- |
|  date | str       | 比赛日期
|  result     | str      |比赛结果
|home_team_boxscore   | str| 主队数据统计
|away_team_boxscore| str| 客队数据统计



* 结果示例：
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

* [1. 查询季后赛信息] 

### 1. 查询季后赛信息
* 方法: `GET`
* URL: 'http://api.ttnbalite.com/api/nba/playoff/series/'

| 输入参数      | 参数类型  | 必填  | 参数说明 |
| ---           | ---       | ---   | --- |
|  无    |         |   | 

| 输出参数      | 参数类型    | 参数说明 |
| ---           | ---         | --- |
|  round | int      | 回合
| tid1      |    int      |队伍1 id
|tid2   | int| 队伍2 id
|conference| str| 分区
|season|str|赛季
|series|str|系列赛数据


* 结果示例：
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
* [1. 查询新闻] 

### 1. 查询新闻
* 方法: `GET`
* URL: 'http://api.ttnbalite.com/api/nba/playoff/series/'

| 输入参数      | 参数类型  | 必填  | 参数说明 |
| ---           | ---       | ---   | --- |
|  无    |         |   | 

| 输出参数      | 参数类型    | 参数说明 |
| ---           | ---         | --- |
|  date | str      | 日期
| cn_name      |    str      |中文名字
|   player| int| 球员 id



* 结果示例：
```json
{
  "ok": true,
  "data": {
    "date":'2018-03-20',
    "black_list": [
      {"cn_name":"以赛亚-托马斯",
       "player": "202738",
      }
    ]
    "red_list": [
      {"cn_name":"勒布朗-詹姆斯",
       "player": "2544",
      }
    ]
  }
}
```



## Injury API

* [1. 根据球队查询伤病信息] 
* [2. 查询所有伤病信息] 

### 1. 查询伤病信息
* 方法: `GET`
* URL: 'http://api.ttnbalite.com/api/injury/query/team/'

| 输入参数      | 参数类型  | 必填  | 参数说明 |
| ---           | ---       | ---   | --- |
|  无    |         |   | 

| 输出参数      | 参数类型    | 参数说明 |
| ---           | ---         | --- |
|  date | str      | 日期
| en_enjury      |    str      |中文名字
|   en_ex_return| str| 预计上场时间
|name|str|球员名字



* 结果示例：
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


### 2. 查询所有伤病信息
* 方法: `GET`
* URL: 'http://api.ttnbalite.com/api/injury/list/all/'

| 输入参数      | 参数类型  | 必填  | 参数说明 |
| ---           | ---       | ---   | --- |
|  无    |         |   | 

| 输出参数      | 参数类型    | 参数说明 |
| ---           | ---         | --- |
|  date | str      | 日期
| en_enjury      |    str      |中文名字
|   en_ex_return| str| 预计上场时间
|name|str|球员名字



* 结果示例：
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
