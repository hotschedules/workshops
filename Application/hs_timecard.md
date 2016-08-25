# Timecards


ScheduleService Web ServiceDescriptionThis service is intended for third parties to be able to grab scheduled shifts from HotSchedules and import theminto their POS/data warehouse/enterprise/etc. system.





## getTimeCards

/concept/store/getTimeCards?start_day=DD&start_month=MM&start_year=YYYy&end_day=DD&end_month=MM&end_year=YYYY

```
curl -X GET -H "Content-Type:application/json" -u U:P "https://api.bodhi.space/namespace/controllers/vertx/hotschedules/1/1/getTimeCards?start_day=30&start_month=4&start_year=2016&end_day=5&end_month=5&end_year=2016"
```






## setTimeCards

setTimeCardsV3



````
{
  "jobName": String,
  "ovtTtl": Real,
  "ovtHrs": Integer,
  "clockOut": UTC DATE TIME - "YYYY-MM-DDTHH:MM:SS-00:00",
  "regWage": Real,
  "clockIn": UTC DATE TIME - "YYYY-MM-DDTHH:MM:SS-00:00",
  "ovtWage": Real,
  "breakMinutes": Real,
  "jobId": Integer,
  "businessDate": {
    "month": Integer,
    "year": Integer,
    "day": Integer
  },
  "regHrs": Real,
  "spcTtl": Real,
  "hsId": Integer,
  "spcHrs": Integer,
  "ovtMins": Integer,
  "storeNum": Integer,
  "empPosId": Integer,
  "regTtl": Real
}
````


````
{
  "jobName": "Cook",
  "ovtTtl": 0,
  "ovtHrs": 0,
  "clockOut": "2016-07-31T22:05:00-05:00",
  "regWage": 9,
  "clockIn": "2016-07-30T15:56:00-05:00",
  "ovtWage": 13.5,
  "breakMinutes": 0,
  "jobId": 16921407,
  "businessDate": {
    "month": 7,
    "year": 2016,
    "day": 31
  },
  "regHrs": 6.15,
  "spcTtl": 0,
  "hsId": 929931334634,
  "spcHrs": 0,
  "ovtMins": 0,
  "storeNum": 1,
  "empPosId": 1052,
  "regTtl": 55.35
}
````



````
curl -X PUT -H "Content-Type:application/json" 
-u <username>:<password> 
"https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/1/1/setTimeCardsV3?
start_day=30&start_month=4&start_year=2016&end_day=5&end_month=5&end_year=2016" 
-d "[{
  "jobName": "Cook",
  "ovtTtl": 0,
  "ovtHrs": 0,
  "clockOut": "2016-07-31T22:05:00-05:00",
  "regWage": 9,
  "clockIn": "2016-07-30T15:56:00-05:00",
  "ovtWage": 13.5,
  "breakMinutes": 0,
  "jobId": 16921407,
  "businessDate": {
    "month": 7,
    "year": 2016,
    "day": 31
  },
  "regHrs": 6.15,
  "spcTtl": 0,
  "hsId": 929931334634,
  "spcHrs": 0,
  "ovtMins": 0,
  "storeNum": 1,
  "empPosId": 1052,
  "regTtl": 55.35
}]"
````

setTimeCardsDeclaredTips

curl -X PUT -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/1/1/setTimeCardsDeclaredTips?start_day=30&start_month=4&start_year=2016&end_day=5&end_month=5&end_year=2016" -d "[{json_object_1}, {json_object_2}, {json_object_3}...]"

