# operator-directory

## API References
###Lookup phone number
#####- GET /api/v/1/lookup/@phonenumber
**@phonenumber**
the number have to start with:
- **+** for any numbers
- **0** for local Filipino numbers

**Result**

| name | type | example |
|--------|--------|--------|
|country|String|Philippines|
|telco|String|SMART|
|subtype|String|BUDDY|
|code|String|BDY|
|phone_number|String (E164 Format)|+639479352566|
|black_list|Boolean|true|

**Exemples**

/api/v/1/lookup/09479356522
```json
{
   "country":"Philippines",
   "telco":"SMART",
   "subtype":"BUDDY",
   "code":"BDY",
   "phone_number":"+639479352566",
   "black_list":false
}
```
/api/v/1/lookup/+33683122296
```json
{
   "country":"France",
   "telco":"Orange France",
   "subtype":"None",
   "code":"None",
   "phone_number":"+33683122296",
   "black_list":false
}
```
###PhPrefix API
#####- GET /api/v/1/phprefix

**Parameters**

| name | type | example |default value|
|--------|--------|--------|--------|
|nationalNumber|String|9475000000|*required*|

**Result**

| name | type | example |
|--------|--------|--------|
|prefix|Int|947|
|from|Long|5000000|
|to|Long|8999999|
|telco|String|SMART|
|subtype|String|BUDDY|
|code|String|BDY|
|id|String|54fd3d8aae05b4de67d73bd3|

**Exemples**

/api/v/1/phprefix?nationalNumber=9479352566
```json
{
    "subtype": "BUDDY",
    "telco": "SMART",
    "code": "BDY",
    "prefix": 947, 
    "from": 9200000,
    "to": 9899999,
	"id": "54fd3d8aae05b4de67d73bd3"
}
```

#####- POST /api/v/1/phprefix

**Parameters**

| name | type | example |default value|
|--------|--------|--------|--------|
|**prefix**|Int|947|*required*|
|**from**|Long|5000000|*required*|
|to|Long|8999999|from|
|telco|String|SMART|*required*|
|subtype|String|BUDDY|*required*|
|code|String|BDY|*required*|
|id|String|54fd3d8aae05b4de67d73bd3|an ObjectId will be generate|


**Result**

| code | description |
|--------|--------|
|201|created|

#####- DELETE /api/v/1/phprefix

**Parameters**

| name | type | example |default value|
|--------|--------|--------|--------|
|id|String|54fd3d8aae05b4de67d73bd3|*required*|

**Result**

| code | description |
|--------|--------|
|202|PhPrefix deleted|

###BlackList API
#####- GET /api/v/1/blacklist

**Parameters**

| name | type | example |default value|
|--------|--------|--------|--------|
|countryCode|Int|33|*required*|
|nationalNumber|Long|683233395|*required*|

Or

| name | type | example |default value|
|--------|--------|--------|--------|
|id|String|54fd3d8aae05b4de67d73bd3|*required*|

**Result**

| name | type | example |
|--------|--------|--------|
|countryCode|Int|33|
|from|Long|200000000|
|to|Long|399999999|
|status|Boolean|true|
|country|String|France|
|firstName|String|Renaud|
|lastName|String|Jollet|
|description|String|Spamer|
|id|String|54fd3d8aae05b4de67d73bd3|

**Exemples**

/api/v/1/blacklist?countryCode=33&nationalNumber=283948273
```json
{
    "countryCode": 33,
    "from": 200000000,
    "to": 399999999,
    "status": true,
    "country": "France",
    "firstName": "Renaud",
    "lastName": "Jollet",
    "description": "Spamer",
	"id": "54fd3d8aae05b4de67d73bd3"
}
```

#####- POST /api/v/1/blacklist

**Parameters**

| name | type | example |default value|
|--------|--------|--------|--------|
|**countryCode**|Int|33|*required*|
|**from**|Long|200000000|*required*|
|to|Long|399999999|from|
|status|Boolean|true|true|
|country|String|France|will return the English country name of the number "+{countyCode}{from}"|
|firstName|String|Renaud|""|
|lastName|String|Jollet|""|
|description|String|Spamer|""|
|id|String|54fd3d8aae05b4de67d73bd3|An ObjectId will be generate|

**Result**

| code | description |
|--------|--------|
|201|BlackList item created|

#####- DELETE /api/v/1/blacklist

**Parameters**

| name | type | example |default value|
|--------|--------|--------|--------|
|id|String|54fd3d8aae05b4de67d73bd3|*required*|

**Result**

| code | description |
|--------|--------|
|202|BlackList item deleted|

#####- DELETE /api/v/1/blacklist

**Parameters**

| name | type | example |default value|
|--------|--------|--------|--------|
|id|String|54fd3d8aae05b4de67d73bd3|*required*|
|status|Boolean|true|*required*|

**Result**

| code | description |
|--------|--------|
|202|BlackList status Update to {status}|

## Status code

| status | description |
|--------|--------|
| 200  | OK |
|201 | Created |
|202 | Accepted |
|204|No Content|
|400| Bad Request|
|404| not found|
