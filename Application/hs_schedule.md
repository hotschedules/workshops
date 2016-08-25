# Schedules and Shifts


ScheduleService Web ServiceDescriptionThis service is intended for third parties to be able to grab scheduled shifts from HotSchedules and import theminto their POS/data warehouse/enterprise/etc. system.


## getScheduleV3

This method takes in a concept ID, store ID, start and end dates. Itreturns an array of WSScheduleItem objects, which represent onescheduled shift each, for import into the POS. This method returns alimited amount of data per shift: employee HS ID, employee POS ID,internal HS Job ID, POS Job ID, shift start date/time, shift enddate/time, work week start date/time, work week end date/time.
This method takes in a concept ID, store ID, start and end dates. It returns an array of WSScheduleItemobjects, which represent one scheduled shift each, for import into the POS. This method returns a limitedamount of data per shift: employee HS ID, employee POS ID, internal HS Job ID, POS Job ID, shift startdate/time, shift end date/time, work week start date/time, work week end date/time.

/concept/store/getSchedule?start_day=DD&start_month=MM&start_year=YYYY&end_day=DD&end_month=MM&end_year=YYYY






```
"https://api.bodhi.space/namespace/controllers/vertx/hotschedules/1/1/getSchedule?start_day=30&start_month=4&start_year=2016&end_day=5&end_month=5&end_year=2016"
```



````
curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/1/1/getScheduleV3?start_day=30&start_month=4&start_year=2016&end_day=5&end_month=5&end_year=2016"

````


## getShiftsV3


````
"https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/1/1/getShiftsV3?start_day=30&start_month=4&start_year=2016&end_day=5&end_month=5&end_year=2016"
````


````
curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/1/1/getShiftsV3?start_day=30&start_month=4&start_year=2016&end_day=5&end_month=5&end_year=2016"
````