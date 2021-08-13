# POTENTIAL API REWRITE
This is a document that aims to explain and provide a potential api structure that could be used for the rewrite. This is going to contain the current API request along with an updated API request and an explination and reasoning behind it


## Current Combat API

<pre>
{
    "client_name": "ajedi32",
    "sessionid": "0BD7D136-E487-11E8-9F32-F2801F1B9FD1",
    "match_type": "Echo_Arena_Private",
    "map_name": "mpl_arena_a",
    "private_match": true,
    "tournament_match": false,
    "blue_points": 9,
    "orange_points": 5,
    "sessionip": "204.74.226.94",
    "player": {
      "vr_left": [1, 0, 0],
      "vr_position": [0, 0, 0],
      "vr_forward": [0, 0, 1],
      "vr_up": [0, 1, 0]
    },
    "teams": [
      {
        "team": "BLUE TEAM"
        },
        "players": [
          {
            "name": "Bob",
            "playerid": 0,
            "userid": 9221405949665979,
            "number": 88,
            "level": 16,
            "ping": 75,
            "head": {
                "position": [1.9080001, -0.80900002, -7.9890003],
                "forward": [-0.34600002, -0.41700003, -0.84100002],
                "left": [-0.93600005, 0.21200001, 0.28],
                "up": [0.061000004, 0.88400006, -0.46300003]
            },
            "body": {
                "position": [1.9080001, -0.80900002, -7.9890003],
                "forward": [-0.208, 0.36600003, -0.90700006],
                "left": [-0.91400003, 0.257, 0.31400001],
                "up": [0.34800002, 0.89400005, 0.28100002]
            },
            "velocity": [0, 0, 0],
            "lhand": {
                "pos": [-2.7710001, 2.2950001, -6.4300003],
                "forward": [-0.61800003, 0.60500002, -0.50200003],
                "left": [0.147, 0.71600002, 0.68300003],
                "up": [0.77200001, 0.34800002, -0.53100002]
            },
            "rhand": {
                "pos": [0.21600001, -2.3150001, 78.168007],
                "forward": [-0.69100004, 0.112, -0.71400005 ],
                "left": [-0.574, -0.68500006, 0.44800001],
                "up": [-0.43900001, 0.72000003, 0.53800005]
            }
          }
          /* ...other blue players here */
        ]
      },
      {
        "team": "ORANGE TEAM"
        },
        "players": [
          /* ...orange players here; see blue players section for example */
        ]
      },
      {
        "team": "SPECTATORS",
        "possession": false,
        "players": [
          /* ...spectators here; see blue players section for example */
        ]
      }
    ]
  }
</pre>

## Issues with the current API
- It was mainly build for arena in mind
- It is lacking all combat unique stasticits
- Some of the data is invalid when using it with combat
---

In general the api was not designed to be used properly with combat

## Idea behind the new API
My general idea for the new api is to provide enough information in the api to be able to reconstrust the game with just the API information alone. So if you have a program that can save the API calls to a file and have a program that can read and process that information it would be possible to make an accurate "replay" of the game.

## New API
<pre>
{
    "client_name": "ajedi32",
    "sessionid": "0BD7D136-E487-11E8-9F32-F2801F1B9FD1",
    "match_type": "Echo_Combat_Private",
    "map_name": "mpl_combat_gauss",
    "private_match": true,
    "tournament_match": false,
    "sessionip": "204.74.226.94",

    "blue_rounds" : 1, 
    "orange_rounds" : 1,
    "capture_point_locked" : false,
    "capture_point_owner" : [1,0],
    "capture_point_contested" : true,
    "capture_point_clamed" : true,
    "capture_point_transfer" : 0,
    "orange_team_points": 65,
    "blue_team_points" : 25,

    "payload" :{
        "distance" : 0,
        "checkpoint" : 0,
        "speed" : 0,
        "contested" : false,
        "cooldown" : false,
        "object" : {
            "position" : [0,0,0], 
            "forward": [-0.208, 0.36600003, -0.90700006],
            "left": [-0.91400003, 0.257, 0.31400001],
            "up": [0.34800002, 0.89400005, 0.28100002]
        },
        "velocity" : [0,0,0]
    },
    "player": {
      "vr_left": [1, 0, 0],
      "vr_position": [0, 0, 0],
      "vr_forward": [0, 0, 1],
      "vr_up": [0, 1, 0]
    },
    "teams": [
      {
        "team": "BLUE TEAM",
        "players": [
          {
            "name": "Bob",
            "playerid": 0,
            "userid": 9221405949665979,
            "number": 88,
            "level": 16,
            "ping": 75,
            "objective" : false,
            "stunned" : false,
            "invulnerable" : false,
            "head": {
                "position": [1.9080001, -0.80900002, -7.9890003],
                "forward": [-0.34600002, -0.41700003, -0.84100002],
                "left": [-0.93600005, 0.21200001, 0.28],
                "up": [0.061000004, 0.88400006, -0.46300003]
            },
            "body": {
                "position": [1.9080001, -0.80900002, -7.9890003],
                "forward": [-0.208, 0.36600003, -0.90700006],
                "left": [-0.91400003, 0.257, 0.31400001],
                "up": [0.34800002, 0.89400005, 0.28100002]
            },
            "velocity": [0, 0, 0],
            "lhand": {
                "pos": [-2.7710001, 2.2950001, -6.4300003],
                "forward": [-0.61800003, 0.60500002, -0.50200003],
                "left": [0.147, 0.71600002, 0.68300003],
                "up": [0.77200001, 0.34800002, -0.53100002]
            },
            "rhand": {
                "pos": [0.21600001, -2.3150001, 78.168007],
                "forward": [-0.69100004, 0.112, -0.71400005 ],
                "left": [-0.574, -0.68500006, 0.44800001],
                "up": [-0.43900001, 0.72000003, 0.53800005]
            },
            "stats": {
                "eliminations": 5,
                "objective_time": 78.645569,
                "objective_eliminations" : 0,
                "objective_damage": 0,
                "deaths": 0,
                "damage": 0,
                "headshot_elimintions": 0,
                "stuns" : 0
                "assists" : 0
            },
            "loadout":{
                "weapon" : {
                    "name" : "comet",
                    "overheated" : false,
                    "heat" : 0
                },
                "ordinance":{
                    "name" : "detinator",
                    "active" : false,
                    "recharge" : 0
                },
                "tech":{
                    "name" : "threat_scanner",
                    "active" : false,
                    "recharge" : 0
                }
            },
            "health": 120

          }
          /* ...other blue players here */
        ]
      },
      {
        "team": "ORANGE TEAM",
        "players": [
          /* ...orange players here; see blue players section for example */
        ]
      },
      {
        "team": "SPECTATORS",
        "possession": false,
        "players": [
          /* ...spectators here; see blue players section for example */
        ]
      }
    ],
    "entitys": [
        {
            "name" : "detinator",
            "owner" : 2,
            "object" : {
                "position" : [0,0,0], 
                "forward": [-0.208, 0.36600003, -0.90700006],
                "left": [-0.91400003, 0.257, 0.31400001],
                "up": [0.34800002, 0.89400005, 0.28100002]
            },
            "velocity" : [-0.91400003, 0.257, 0.31400001]
        },
        {
            "name" : "comet_shot"
            /* ...other info here; see entity info above for example */
        },
        {
            "name" : "shield"
            /* ...other info here; see entity info above for example */
        }
    ]
  }
</pre>

## Additions



### Capture point speficics
---
#### `blue_rounds`
How many rounds the blue team has won in capture point

#### `orange_rounds`
How many rounds the orange team has won in capture point

#### `capture_point_locked`
If the capture point is locked. Ex.in the beggining of the game or once a team reached 100%

#### `capture_point_owner`
Who is in current possession of the capture point. Regardless of if its contested or in the process of being transfered
#### `capture_point_contested`
If the capture point is being contested and there are no point gains for either team

#### `capture_point_clamed`
If the capture point has an active member of the team in the point. otherwise that team gains points at half value

#### `capture_point_transfer`
The time of the transfer. Ex. when a team is capturing the point first, When possession is transfering from one team to another.

#### `orange_team_points`
The points that the orange team has in the current round. this is in terms of the points not percentage

#### `blue_team_points`
The points that the blue team has in the current round. this is in terms of the points not percentage

### Payload information
---
#### `distance`
The distance the payload is from the start

#### `checkpoint`
What checkpoint the payload is at
Possible values:
- `0`
- `1`
- `2`

#### `speed`
The travel speed of the payload

#### `contested`
Whether the point is being activly contested by the defending team. this only happend if both team are activly on the payload

#### `cooldown`
If the payload is in cooldown from gaining a checkpoint.

#### `object.position` 
The position of the payload

#### `object.forward` 
The forward direction of the payload

#### `object.left` 
The left direction of the payload

#### `object.up` 
The up direction of the payload

#### `velocity`
The velocity of the payload in terms of x,y,z
### Player information
---

#### `objective`
Weather the player is activly on the objective or not. If the player is in the capture point or is grabbing the payload

#### `stunned` 
If the player is stunned by an arc-mine or a stunfield

#### `health`
The health value of the player

#### `stats`
A list of player stats

#### `invulnerable`
If the player is phased and invulnerable to damage

#### `stats.eliminations`
The number of eliminations a player has

#### `stats.objective_time`
The objective time the player has

#### `stats.objective_eliminations`
The number of eliminations a player has while on objective

#### `stats.objective_damage`
The objective damage the player has

#### `stats.deaths`
The number of deaths the player has

#### `stats.damage`
The total amount of damage the player has

#### `stats.headshot_elimintions`
The number of headshot eliminations

#### `stats.assists`
The number of assists

#### `stats.stuns`
The number of stuns a player has

#### `loadout`
The loadout a player has

#### `loadout.weapon`
The weapon the player has

#### `loadout.weapon.name`
The name of the weapon

#### `loadout.weapon.overheat`
If the weapon is overheated

#### `loadout.weapon.heat`
The current "heat" value of the weapon

#### `loadout.ordinance`
The ordinance the player has

#### `loadout.ordinance.name`
The name of the ordinance

#### `loadout.ordinance.active`
If the ordinance is currently active and in the map. Ex. in a players hand, planted down, or thrown

#### `loadout.ordinance.cooldown`
The cooldown of the ordinance

#### `loadout.tech`
The techmod the player has

#### `loadout.tech.name`
The name of the techmod

#### `loadout.tech.active`
If the Techmod is active

#### `loadout.tech.cooldown`
The techmod cooldown

### Entitys
---
#### `entitys`
A list of entitys in the map

#### `name`
The name of tne entity
Possible values:
- `comet_shot`
- `pulsar_shot`
- `meator_shot`
- `nova_shot`
- `detinator`
- `instant_heal`
- `arc_mine`
- `stunfield`
- `shield`

#### `owner`
The playerID of the owner/sender of this entity

#### `object.position` 
The position of the entity

#### `object.forward` 
The forward direction of the entity

#### `object.left` 
The left direction of the entity

#### `object.up` 
The up direction of the entity

#### `object.velocity` 
The velocity of the entity
