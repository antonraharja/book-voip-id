API
===

# API

## User

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

Example :
curl --data 'token=$2y$10$OqwI.82kdiqyrbx61lsjandz7&accid=user1&password=secret&email=user1@domain.com' https://teleponrakyat.id/api/user/create
curl --data 'token=$2y$10$OqwI.82kdiqyrbx61lsjandz7' https://teleponrakyat.id/api/user/list

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

Example :
curl --data 'token=$2y$10$OqwI.82kdiqyrbx61lsjandz7&user=user1&dcp=dcp.domain.com&secret=password&desc=Phone1' https://teleponrakyat.id/api/phonenumber/create
curl --data 'token=$2y$10$OqwI.82kdiqyrbx61lsjandz7&user=user1&dcp=dcp.domain.com' https://teleponrakyat.id/api/phonenumber/list

## Domain

*API Verbs*          | *List Parameter*    | *Function*            | *Note*
-------------------- | ------------------- | --------------------- | --------------------
domain/list          |                     | Get List Domain       |

Example :
curl --data 'token=$2y$10$OqwI.82kdiqyrbx61lsjandz7' https://teleponrakyat.id/api/domain/list

## Online phone

*API Verbs*          | *List Parameter*    | *Function*            | *Note*
-------------------- | ------------------- | --------------------- | --------------------
onlinephone/list     |                     | Get List Online Phone |

Example :
curl --data 'token=$2y$10$OqwI.82kdiqyrbx61lsjandz7' https://teleponrakyat.id/api/onlinephone/list

## Gateway

*API Verbs*          | *List Parameter*    | *Function*            | *Note*
-------------------- | ------------------- | --------------------- | --------------------
gateway/list         |                     | Get List Gateway      |

Example :
curl --data 'token=$2y$10$OqwI.82kdiqyrbx61lsjandz7' https://teleponrakyat.id/api/gateway/list

## CDR

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

Example :
curl --data 'token=$2y$10$OqwI.82kdiqyrbx61lsjandz7&dcp=dcp.domain.com' https://teleponrakyat.id/api/cdr/list

## Return Codes

*Error Code*         | *Error String*      |
-------------------- | ------------------- |
403                  | Invalid token       |
501                  | DCP not found       |
502                  | User not found      |