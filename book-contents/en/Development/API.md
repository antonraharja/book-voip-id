API
===

# API

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
                     | dcp                  |                      |
                     | secret               |                      |
                     | desc                 |                      |
phonenumber/remove   | user                 | Remove phone number  |
                     | dcp                  |                      |
                     | phonenumber          |                      |
phonenumber/update   | user                 | Update phone number  |
                     | dcp                  |                      |
                     | secret               |                      |
                     | desc                 |                      |
phonenumber/list     | dcp                  | Get list phone number|
                     | user                 |                      |

## Domain

*API Verbs*          | *List Parameter*    | *Function*            | *Note*
-------------------- | ------------------- | --------------------- | --------------------
domain/list          |                     | Get List Domain       |


Online phone
------------

*API Verbs*          | *List Parameter*    | *Function*            | *Note*
-------------------- | ------------------- | --------------------- | --------------------
onlinephone/list     |                     | Get List Online Phone |


Gateway
------------

*API Verbs*          | *List Parameter*    | *Function*            | *Note*
-------------------- | ------------------- | --------------------- | --------------------
gateway/list         |                     | Get List Gateway      |


## CDR

*API Verbs*          | *List Parameter*    | *Function*            | *Note*
-------------------- | ------------------- | --------------------- | --------------------
cdr/list             |                     | Get CDR Data

## Return Codes

*Error Code*         | *Error String*      |
-------------------- | ------------------- |
403                  | Invalid token       |
501                  | DCP not found       |
502                  | User not found      |