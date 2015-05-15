This Document for VoIP ID API :

*API Verbs* | *List Parameter* | *Function* | *Note*
--- | --- | --- | --- 
 **User :**  |
user/create | accid | Create user
 | password 
 | email 
 | firstname
 | lastname 
user/remove | accid | Remove user 
 | email 
user/update | accid | Update user
 | password
 | email
 | firstname
 | lastname
user/list : | | Get list user
| | 
**Phone Number :** |
phonenumber/create | user | Create phone number
 | dss
 | secret
 | desc
phonenumber/remove | user | Remove phone number
 | dss
 | phonenumber
phonenumber/update | user | Update phone number
 | dss 
 | secret
 | desc
phonenumber/list | user | Get list phone number
|
**Online phone :** |
onlinephone/list | | Get List Online Phone Number
|
**CDR :** |
cdr/list | | Get CDR Data
