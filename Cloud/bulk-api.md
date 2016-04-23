
# Bulk API

The Bulk API is the prescribed method to post large data files to the platform. The API call is asynchronous and returns a key that the user must use to check the status of the import. 

Note: The size limitation for the data file is 17 MB in one bulk post.



## Use Case

You want to POST a large amount of data to the platform API. 
You have a JSON formatted file. Use the Platform /bulk API to POST the data.


##Prerequisites


* Write access to the data object you want to POST data to
* A text editor that can handle JSON files
* CURL or some other means to POST to the API


## API definition


The bulk API is defined as follows:

````
https://<host>/<namespace>/bulk --data @jsonfile
````

Example

````
https://api.bodhi.space/mynamespace/bulk --data @myjsonfile.json
````




## JSON file format 

The JSON file consists of two tags 

* configuration for import
* the data payload

The configuration section specifies 

* the operation required - insert, update, upsert. ()Delete is not supported)
* whether a report is required - boolean
* the target data type


````
{
	"config": {
		"op": "insert" or "update" or "upsert"
		 "report": true,			<- optional, need a report? (default: false) 
		 "target": "target_name”	<- the name of the type
	},
	"payload": [
	{
		"name1": "value",
		"name2": "value"
	}, {
		"name1": "value",
		"name2": "value"
	}]
}
 
````




````
{
	"config": {
		"op": "insert",
		"report": true,
		"target":  "Store"
	},
	"payload": [
		{
		"store_name": "Food Sales",
		"store_number": "SalesItem",
		"store_city": "DAS-Food-Sales"
	    }
		]
}
````




## CURL

````
curl -is -X POST -H 'Content-type:application/json' -u u:p https://api.bodhi.space/ns/bulk --data @kpidef.json
````



The payload varies depending on the type of operation.

 Returns 202 with header bulk_id:<the bulk id>



For errors or feedback with any of these labs please contact support@hotschedules.com






