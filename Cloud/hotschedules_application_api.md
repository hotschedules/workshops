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


### getStoreEmployees

Method: getStoreEmployees
Params: active_only, boolean [true, false]


```
curl -X GET -H "Content-Type:application/json" -u U:P "https://api.bodhi.space/namespace/controllers/vertx/hotschedules/1/1/getStoreEmployees?active_only=true"
```

### getStoreJobs

concept/store/

```
curl -X GET -H "Content-Type:application/json" -u U:P
 "https://api.bodhi.space/namespace/controllers/vertx/
 hotschedules/1/1/getStoreJobs?active_only=true"
```





### getGroups

concept/store/

```
curl -X GET -H "Content-Type:application/json" -u U:P "https://api.bodhi.space/namespace/controllers/vertx/hotschedules/1/getGroups"
```



## Employee API


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

### getEmpJobs


/concept/store/getEmpJobs?active_only=true

```
curl -X GET -H "Content-Type:application/json" -u U:P "https://api.bodhi.space/namespace/controllers/vertx/hotschedules/1/1/getEmpJobs?active_only=true
```



### getDriversByInterval

/concept/store/getDriversByInterval?start_day=30&start_month=4&start_year=2016&end_day=5&end_month=5&end_year=2016&volume_type=TABLE&data_type=ACTUAL


````
curl -X GET -H "Content-Type:application/json" -u U:P "https://api.bodhi.space/namespace/controllers/vertx/hotschedules/1/1/getDriversByInterval?start_day=30&start_month=4&start_year=2016&end_day=5&end_month=5&end_year=2016&volume_type=TABLE&data_type=ACTUAL"
````

## Schedules, Shifts and Timecards


### getSchedule

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

