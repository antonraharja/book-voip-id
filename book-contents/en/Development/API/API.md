This Document for VoIP ID API

## User

*API Verbs*          | *List Parameter*     | *Function*           | *Note*
-------------------- | -------------------- | -------------------- | --------------------
user/create          | accid                | Create user          |
                     | password             |                      |
                     | email                |                      |
                     | firstname            |                      |
                     | lastname             |                      | 
user/remove          | accid                | Remove user          |
                     | email                |                      |
user/update          | accid                | Update user          |
                     | password             |                      |
                     | email                |                      |
                     | firstname            |                      |
                     | lastname             |                      |
user/list            |                      | Get list user        |


## Phone Number

*API Verbs*          | *List Parameter*     | *Function*           | *Note*
-------------------- | -------------------- | -------------------- | --------------------
phonenumber/create   | user                 | Create phone number  |
                     | dss                  |                      |
                     | secret               |                      |
                     | desc                 |                      |
phonenumber/remove   | user                 | Remove phone number  |
                     | dss                  |                      |
                     | phonenumber          |                      |
phonenumber/update   | user                 | Update phone number  |
                     | dss                  |                      |
                     | secret               |                      |
                     | desc                 |                      |
phonenumber/list     | dcp                  | Get list phone number|
                     | user                 |                      |

## Domain

*API Verbs*          | *List Parameter*    | *Function*            | *Note*
-------------------- | ------------------- | --------------------- | --------------------
domain/list          |                     | Get List Domain       |


## Online phone

*API Verbs*          | *List Parameter*    | *Function*            | *Note*
-------------------- | ------------------- | --------------------- | --------------------
onlinephone/list     |                     | Get List Online Phone |


## CDR
*API Verbs*          | *List Parameter*    | *Function*            | *Note*
-------------------- | ------------------- | --------------------- | --------------------
cdr/list             |                     | Get CDR Data
