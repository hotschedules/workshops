
# Employee Service Methods
This service provides operations for a third party to push or request employee and employee job data into HotSchedules.


## Get All Employee Jobs for a Store

**Method Name:** getEmpJobs

Get a list of all jobs assigned to all employees for a store.  
Takes a concept ID and a store ID and returns an array of Employee Job objects. 

**URL**

````
/concept/store/getEmpJobs?active_only=BOOLEAN
````



concept Int 1..1 The identifier for the location's concept. Mustbe unique within the company. ContactHotSchedules if you're not sure about thisvalue.storeNum Int 1..1 Numeric (integer) identifier for the store. Mustbe unique within the concept.


```
curl -X GET -H "Content-Type:application/json" -u U:P "https://api.bodhi.space/namespace/controllers/vertx/hotschedules/1/1/getEmpJobs?active_only=true
```


## getStoreEmployees

This method takes in a concept ID, store ID, a flag to determine ifonly active employees are returned, and returns an array of objects.

Method: getStoreEmployees
Params: active_only, boolean [true, false]


```
curl -X GET -H "Content-Type:application/json" -u U:P "https://api.bodhi.space/namespace/controllers/vertx/hotschedules/1/1/getStoreEmployees?active_only=true"
```


## getStoreJobs

This method takes in a concept ID and a store ID, and returns anarray of all jobs currently defined in HotSchedules for the givenconcept/store.

concept/store/

```
curl -X GET -H "Content-Type:application/json" -u U:P
 "https://api.bodhi.space/namespace/controllers/vertx/
 hotschedules/1/1/getStoreJobs?active_only=true"
```



## setEmpJobs

This method takes in a concept ID, store ID, and an array ofWSEmpJob objects to assign jobs to individual employees. Thismethod returns a WSReturn object.


````
curl -X PUT -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/1/1/setEmpJobs?start_day=30&start_month=4&start_year=2016&end_day=5&end_month=5&end_year=2016" -d "[{json_object_1}, {json_object_2}, {json_object_3}...]"````
## setEmps
This method takes in a concept ID, store ID and an array ofWSEmployee objects. Using the authentication from the usernametoken and the conecpt and store IDs, the server will resolve whichHotSchedules client this sync is for. The array of employees will beparsed on the server side to employees who need to be inserted orupdated in the HS database. This method returns a WSReturnobject.


````
https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/1/1/setEmps?start_day=30&start_month=4&start_year=2016&end_day=5&end_month=5&end_year=2016" -d "[{json_object_1}, {json_object_2}, {json_object_3}...]
````



````
curl -X PUT -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/1/1/setEmps?start_day=30&start_month=4&start_year=2016&end_day=5&end_month=5&end_year=2016" -d "[{json_object_1}, {json_object_2}, {json_object_3}...]"
````






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


