API
===

# API

## User

<<<<<<< HEAD
*API Verbs*          | *List Parameter*     | *Function*           | *Note*
-------------------- | -------------------- | -------------------- | --------------------
user/create          | accid                | Create user          |
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
=======
*API Verbs*          | *List Parameter*     | *Function*           | *Note*               | *Example*
-------------------- | -------------------- | -------------------- | -------------------- | -------------------
user/create          | accid                | Create user          |                      | curl --data 'token=$2y$10$OqwI.xelrPKz&accid=user1&password=secret&email=user1@domain.com' https://teleponrakyat.id/api/user/create
                     | password             |                      |                      |
                     | email                |                      |                      |
                     | firstname            |                      |                      |
                     | lastname             |                      |                      |
user/remove          | accid                | Remove user          |                      | curl --data 'token=$2y$10$OqwI.xelrPKz&accid=user1&email=user1@domain.com' https://teleponrakyat.id/api/user/remove
                     | email                |                      |                      |
user/update          | accid                | Update user          |                      | curl --data 'token=$2y$10$OqwI.xelrPKz&accid=user1&password=verysecret&email=user1@domain.com' https://teleponrakyat.id/api/user/update
                     | password             |                      |                      |
                     | email                |                      |                      |
                     | firstname            |                      |                      |
                     | lastname             |                      |                      |
user/list            |                      | Get list user        |                      | curl --data 'token=$2y$10$OqwI.xelrPKz' https://teleponrakyat.id/api/user/list
>>>>>>> f1bd2314ba0312c1f2a1b66c235ce430da52de2f

Example :
curl --data 'token=$2y$10$OqwI.82kdiqyrbx61lsjandz7&accid=user1&password=secret&email=user1@domain.com' https://teleponrakyat.id/api/user/create
curl --data 'token=$2y$10$OqwI.82kdiqyrbx61lsjandz7' https://teleponrakyat.id/api/user/list

## Phone Number

*API Verbs*          | *List Parameter*     | *Function*           | *Note*               | *Example*
-------------------- | -------------------- | -------------------- | -------------------- | --------------------
phonenumber/create   | user                 | Create phone number  |                      | curl --data 'token=$2y$10$OqwI.xelrPKz&user=user1&dcp=dcp.domain.com&secret=password&desc=Phone1' https://teleponrakyat.id/api/phonenumber/create
                     | dcp                  |                      |                      |
                     | secret               |                      |                      |
                     | desc                 |                      |                      |
phonenumber/remove   | user                 | Remove phone number  |                      | curl --data 'token=$2y$10$OqwI.xelrPKz&user=user1&dcp=dcp.domain.com&phonenumber=180001' https://teleponrakyat.id/api/phonenumber/remove
                     | dcp                  |                      |                      |
                     | phonenumber          |                      |                      |
phonenumber/update   | user                 | Update phone number  |                      | curl --data 'token=$2y$10$OqwI.xelrPKz&user=user1&dcp=dcp.domain.com&secret=bestpassword&desc=Phone1' https://teleponrakyat.id/api/phonenumber/update
                     | dcp                  |                      |                      |
                     | secret               |                      |                      |
                     | desc                 |                      |                      |
phonenumber/list     | dcp                  | Get list phone number|                      | curl --data 'token=$2y$10$OqwI.xelrPKz&user=user1&dcp=dcp.domain.com' https://teleponrakyat.id/api/phonenumber/list
                     | user                 |                      |                      |

Example :
curl --data 'token=$2y$10$OqwI.82kdiqyrbx61lsjandz7&user=user1&dcp=dcp.domain.com&secret=password&desc=Phone1' https://teleponrakyat.id/api/phonenumber/create
curl --data 'token=$2y$10$OqwI.82kdiqyrbx61lsjandz7&user=user1&dcp=dcp.domain.com' https://teleponrakyat.id/api/phonenumber/list

## Domain

*API Verbs*          | *List Parameter*    | *Function*            | *Note*               | *Example* 
-------------------- | ------------------- | --------------------- | -------------------- | --------------------
domain/list          |                     | Get List Domain       |                      | curl --data 'token=$2y$10$OqwI.xelrPKz' https://teleponrakyat.id/api/domain/list

Example :
curl --data 'token=$2y$10$OqwI.82kdiqyrbx61lsjandz7' https://teleponrakyat.id/api/domain/list


Online phone
------------

*API Verbs*          | *List Parameter*    | *Function*            | *Note*               | *Example*
-------------------- | ------------------- | --------------------- | -------------------- | --------------------
onlinephone/list     |                     | Get List Online Phone |                      | curl --data 'token=$2y$10$OqwI.xelrPKz' https://teleponrakyat.id/api/onlinephone/list

Example :
curl --data 'token=$2y$10$OqwI.82kdiqyrbx61lsjandz7' https://teleponrakyat.id/api/onlinephone/list


Gateway
------------

*API Verbs*          | *List Parameter*    | *Function*            | *Note*               | *Example*
-------------------- | ------------------- | --------------------- | -------------------- | --------------------
gateway/list         |                     | Get List Gateway      |                      | curl --data 'token=$2y$10$OqwI.xelrPKz' https://teleponrakyat.id/api/gateway/list

Example :
curl --data 'token=$2y$10$OqwI.82kdiqyrbx61lsjandz7' https://teleponrakyat.id/api/gateway/list


## CDR

<<<<<<< HEAD
*API Verbs*          | *List Parameter*    | *Function*            | *Note*
-------------------- | ------------------- | --------------------- | ------------------------
cdr/list             | user                | Get CDR Data          |
                     | dcp                 |                       |
                     | from                |                       | Source number
                     | to                  |                       | Destination number
                     | startdate           |                       | Date format (dd-mm-YYYY)
                     | enddate             |                       | Date format (dd-mm-YYYY)
                     | starttime           |                       | Time format (HH:ii:ss)
                     | endtime             |                       | Time format (HH:ii:ss)
                     | maxduration         |                       | Number in seconds
                     | minduration         |                       | Number in seconds
=======
*API Verbs*          | *List Parameter*    | *Function*            | *Note*                   | *Example* 
-------------------- | ------------------- | --------------------- | ------------------------ | ---------------------
cdr/list             | user                | Get CDR Data          |                          | curl --data 'token=$2y$10$OqwI.xelrPKz&dcp=dcp.domain.com' https://teleponrakyat.id/api/cdr/list
                     | dcp                 |                       |                          |
                     | from                |                       | Source number            |
                     | to                  |                       | Destination number       |
                     | startdate           |                       | Date format (dd-mm-YYYY) |
                     | enddate             |                       | Date format (dd-mm-YYYY) |
                     | starttime           |                       | Time format (HH:ii:ss)   |
                     | endtime             |                       | Time format (HH:ii:ss)   |
                     | maxduration         |                       | Number in seconds        |
                     | minduration         |                       | Number in seconds        |
>>>>>>> f1bd2314ba0312c1f2a1b66c235ce430da52de2f

Example :
curl --data 'token=$2y$10$OqwI.82kdiqyrbx61lsjandz7&dcp=dcp.domain.com' https://teleponrakyat.id/api/cdr/list

## Return Codes

*Error Code*         | *Error String*      |
-------------------- | ------------------- |
403                  | Invalid token       |
501                  | DCP not found       |
502                  | User not found      |