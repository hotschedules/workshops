# The HotSchedules Application API

The HotSchedules IoT Platform provides a new way to interact with HotSchedules Application Data through a REST API. The legacy SOAP API will be depricated and should no longer be used. 

Customers and developers have a choice when integrating with the HotSchedules Labor application. Data moves between the HotSchedules IoT platform and the HotSchedules application. You may choose to use the Platform API to get / post data but you must ensure the platform server side processes are running to ensure that data flows to the HotSchedules Application.


## API Specification


The Application API is defined as follows


````
<HOST><NAMESPACE><RESOURCE><CONCEPT ID><STORE ID><METHOD>?<PARAMS>
````

The Production Host Is : <https://api.bodhi.space>  
The Namespace is your Platform account name.  
The Application API makes use of [Vert.x](http://vertx.io/) for hotschedules. The vertx resource is accessed using as "controllers/vertx/". The application is "hotschedules"   

Example. We want information about all the active employees for a store with ID: 2 belonging to Concept 1. Our account name is 'bladerunner'. 
The URL request would be constructed as follows:  


Host: api.bodhi.space  
Namespace: bladerunner  
Resource: controllers/vertx/hotschedules  
Concept: 1  
Store: 2  
Method: getEmpInfo  
Params: active_only=true  


````
https://api.bodhi.space/bladerunner/controllers/vertx/hotschedules/1/2/getEmpInfo?active_only=true
````

Calling this through CURL:

````
curl -X GET -H "Content-Type:application/json" -u username:password 
"https://api.bodhi.space/namespace/controllers/vertx/hotschedules/1/2/getEmpInfo?active_only=true"
````


For all API requests assume "https://api.bodhi.space/namespace/controllers/vertx/hotschedules/" prefix.


## Stores and Concepts



### getConcept


Method: getConcept
Params: None

```
curl -X GET -H "Content-Type:application/json" -u U:P 
"https://api.bodhi.space/namespace/controllers/vertx/hotschedules/getConcept"
```


### getStores

Method: getStores
Params: group_id, integer

````
https://api.bodhi.space/namespace/controllers/vertx/hotschedules/1/getStores?group_id=0
````


```
curl -X GET -H "Content-Type:application/json" -u U:P "https://api.bodhi.space/namespace/controllers/vertx/hotschedules/1/getStores?group_id=0"
```








### getGroups

concept/store/

```
curl -X GET -H "Content-Type:application/json" -u U:P "https://api.bodhi.space/namespace/controllers/vertx/hotschedules/1/getGroups"
```



## Employee Service
This service provides operations for a third party to push or request employee and employee job data into HotSchedules.


### getEmpJobs

Get a list of all jobs assigned to all employees for a store.
Takes a concept ID and a store ID and returns anarray of objects. 

/concept/store/getEmpJobs?active_only=true


concept Int 1..1 The identifier for the location's concept. Mustbe unique within the company. ContactHotSchedules if you're not sure about thisvalue.storeNum Int 1..1 Numeric (integer) identifier for the store. Mustbe unique within the concept.


```
curl -X GET -H "Content-Type:application/json" -u U:P "https://api.bodhi.space/namespace/controllers/vertx/hotschedules/1/1/getEmpJobs?active_only=true
```


### getStoreEmployees

This method takes in a concept ID, store ID, a flag to determine ifonly active employees are returned, and returns an array of objects.

Method: getStoreEmployees
Params: active_only, boolean [true, false]


```
curl -X GET -H "Content-Type:application/json" -u U:P "https://api.bodhi.space/namespace/controllers/vertx/hotschedules/1/1/getStoreEmployees?active_only=true"
```


### getStoreJobs

This method takes in a concept ID and a store ID, and returns anarray of all jobs currently defined in HotSchedules for the givenconcept/store.

concept/store/

```
curl -X GET -H "Content-Type:application/json" -u U:P
 "https://api.bodhi.space/namespace/controllers/vertx/
 hotschedules/1/1/getStoreJobs?active_only=true"
```



setEmpJobs

This method takes in a concept ID, store ID, and an array ofWSEmpJob objects to assign jobs to individual employees. Thismethod returns a WSReturn object.
setEmps
This method takes in a concept ID, store ID and an array ofWSEmployee objects. Using the authentication from the usernametoken and the conecpt and store IDs, the server will resolve whichHotSchedules client this sync is for. The array of employees will beparsed on the server side to employees who need to be inserted orupdated in the HS database. This method returns a WSReturnobject.








### getEmpInfo

concept/store/getEmpInfo?active_only=true



```
curl -X GET -H "Content-Type:application/json" -u U:P 

"https://api.bodhi.space/namespace/controllers/vertx/hotschedules/1/1/
getEmpInfo?active_only=true"

```

### getEmpAvailability


/concept/store/getEmpAvailability?active_only=true

```
curl -X GET -H "Content-Type:application/json" -u U:P "https://api.bodhi.space/namespace/controllers/vertx/hotschedules/1/1/getEmpAvailability?active_only=true"
```





### getDriversByInterval

/concept/store/getDriversByInterval?start_day=30&start_month=4&start_year=2016&end_day=5&end_month=5&end_year=2016&volume_type=TABLE&data_type=ACTUAL


````
curl -X GET -H "Content-Type:application/json" -u U:P "https://api.bodhi.space/namespace/controllers/vertx/hotschedules/1/1/getDriversByInterval?start_day=30&start_month=4&start_year=2016&end_day=5&end_month=5&end_year=2016&volume_type=TABLE&data_type=ACTUAL"
````

## Schedules, Shifts and Timecards


ScheduleService Web ServiceDescriptionThis service is intended for third parties to be able to grab scheduled shifts from HotSchedules and import theminto their POS/data warehouse/enterprise/etc. system.


### getSchedule

This method takes in a concept ID, store ID, start and end dates. Itreturns an array of WSScheduleItem objects, which represent onescheduled shift each, for import into the POS. This method returns alimited amount of data per shift: employee HS ID, employee POS ID,internal HS Job ID, POS Job ID, shift start date/time, shift enddate/time, work week start date/time, work week end date/time.
This method takes in a concept ID, store ID, start and end dates. It returns an array of WSScheduleItemobjects, which represent one scheduled shift each, for import into the POS. This method returns a limitedamount of data per shift: employee HS ID, employee POS ID, internal HS Job ID, POS Job ID, shift startdate/time, shift end date/time, work week start date/time, work week end date/time.

/concept/store/getSchedule?start_day=DD&start_month=MM&start_year=YYYY&end_day=DD&end_month=MM&end_year=YYYY






```
curl -X GET -H "Content-Type:application/json" -u U:P "https://api.bodhi.space/namespace/controllers/vertx/hotschedules/1/1/getSchedule?start_day=30&start_month=4&start_year=2016&end_day=5&end_month=5&end_year=2016"
```




### getTimeCards

/concept/store/getTimeCards?start_day=DD&start_month=MM&start_year=YYYy&end_day=DD&end_month=MM&end_year=YYYY

```
curl -X GET -H "Content-Type:application/json" -u U:P "https://api.bodhi.space/namespace/controllers/vertx/hotschedules/1/1/getTimeCards?start_day=30&start_month=4&start_year=2016&end_day=5&end_month=5&end_year=2016"
```


### getLaborByBusDay

/concept/store/getLaborByBusDay?start_day=DD&start_month=MM&start_year=YYYY&end_day=DD&end_month=MM&end_year=YYYY&labor_type=optimal


```
curl -X GET -H "Content-Type:application/json" -u U:P "https://api.bodhi.space/namespace/controllers/vertx/hotschedules/1/1/getLaborByBusDay?start_day=30&start_month=1&start_year=2016&end_day=5&end_month=5&end_year=2016&labor_type=optimal"
```

### getLaborByJobAndInterval

/concept/store/getLaborByJobAndInterval?start_day=DD&start_month=MM&start_year=YYY&end_day=DD&end_month=MM&end_year=YYYY&labor_type=optimal


```
curl -X GET -H "Content-Type:application/json" -u U:P "https://api.bodhi.space/namespace/controllers/vertx/hotschedules/1/1/getLaborByJobAndInterval?start_day=30&start_month=1&start_year=2016&end_day=5&end_month=5&end_year=2016&labor_type=optimal"
```



## Sales



### getGuestCounts

/concept/store/getGuestCounts?start_date=YYYY-MM-DDT00:00:00&end_date=YYYY-MM-DDT00:00:00"

```
curl -X GET -H "Content-Type:application/json" -u U:P "https://api.bodhi.space/namespace/controllers/vertx/hotschedules/1/1/getGuestCounts?start_date=2016-04-30T00:00:00&end_date=2016-05-03T00:00:00"
```

### getRCV

/concept/store/getRCV

```
curl -X GET -H "Content-Type:application/json" -u U:P "https://api.bodhi.space/namespace/controllers/vertx/hotschedules/1/1/getRCV"
```

### getSalesCats

/concept/store/getSalesCats

```
curl -X GET -H "Content-Type:application/json" -u U:P "https://api.bodhi.space/namespace/controllers/vertx/hotschedules/1/1/getSalesCats"
```

### getProjectedSales

/concept/store/getProjectedSales?start_day=DD&start_month=MM&start_year=YYY&end_day=DD&end_month=MM&end_year=YYYY

```
curl -X GET -H "Content-Type:application/json" -u U:P "https://api.bodhi.space/namespace/controllers/vertx/hotschedules/1/1/getProjectedSales?start_day=30&start_month=4&start_year=2016&end_day=5&end_month=5&end_year=2016"
```


### getVolumeCounts

/concept/store/getVolumeCounts?start_date=YYYY-MM-DDT00:00:00&end_date=YYYY-MM-DDT00:00:00&volume_type=TABLE

```
curl -X GET -H "Content-Type:application/json" -u U:P "https://api.bodhi.space/namespace/controllers/vertx/hotschedules/1/1/getVolumeCounts?start_date=2015-04-30T00:00:00&end_date=2016-05-03T00:00:00&volume_type=TABLE"
```

