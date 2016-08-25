# The HotSchedules Application API

The HotSchedules IoT Platform provides a new way to interact with HotSchedules Application Data through a REST API. The legacy SOAP API will be depricated and should no longer be used. 

Customers and developers have a choice when integrating with the HotSchedules Labor application. Data moves between the HotSchedules IoT platform and the HotSchedules application. You may choose to use the Platform API to get / post data but you must ensure the platform server side processes are running to ensure that data flows to the HotSchedules Application.

To understand the API, read the API [Specification](https://github.com/hotschedules/workshops/blob/master/Application/hs_api.md#specification)

## Application Services

[Employee](https://github.com/hotschedules/workshops/blob/master/Application/hs_employee.md)  
[Labour](https://github.com/hotschedules/workshops/blob/master/Application/hs_labour.md)  
[Organisation](https://github.com/hotschedules/workshops/blob/master/Application/hs_org.md)  
[Sales](https://github.com/hotschedules/workshops/blob/master/Application/hs_sales.md)  
[Schedule](https://github.com/hotschedules/workshops/blob/master/Application/hs_schedule.md)  
[Timecard](https://github.com/hotschedules/workshops/blob/master/Application/hs_timecard.md)  
[Transactions](https://github.com/hotschedules/workshops/blob/master/Application/hs_transactions.md)  



## Specification



The Application API is defined as follows


````
<HOST><NAMESPACE><RESOURCE><CONCEPT ID><STORE ID><METHOD>?<PARAMS>
````

Property | Definition | Actual value or example
------------ | ------------- | ------------
HOST | The Production instance  | <https://api.bodhi.space>
NAMESPACE | The Namespace is your account name | e.g. TifflesCakes | 
RESOURCE |  The Application API makes use of [Vert.x](http://vertx.io/) to integrate with Hotschedules Labor. The vertx resource is accessed using as "controllers/vertx/". The application is "hotschedules" |   controllers/vertx/hotschedules
CONCEPT | The ID of the concept or brand | e.g. 1
STORE ID | The ID of the store | e.g. 2
METHOD | The resource method we are calling | e.g. getEmpInfo

Example Use case

Tiffles is a two concept chain of coffee shops (concept 1) and bake shops (concept 2). We want to get information about all the active employees for our Palo Alto coffee store, Store number 2. 

The URL request would be constructed as follows:  

Property | Value 
------------ | -------------  
Host | api.bodhi.space 
Namespace |  tiffles  
Resource | controllers/vertx/hotschedules  
Concept |  1 
Store | 2  
Method | getEmpInfo  
Params | active_only=true  

The URL looks like this:

````
https://api.bodhi.space/tiffles/controllers/vertx/hotschedules/1/2/getEmpInfo?active_only=true
````

Calling this through CURL:

````
curl -X GET -H "Content-Type:application/json" -u username:password 
"https://api.bodhi.space/tiffles/controllers/vertx/hotschedules/1/2/getEmpInfo?active_only=true"
````






