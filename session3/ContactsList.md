
# Building a Contacts List

To introduce Performance and Complexity when building Web Apps, we will use an example of building out a Contacts List (similiar to Facebook Messenger) to discuss what will need to be considered when optimizing for performance.

### Server side
In this example, we have a server that provides us with an JSON array to our client app that is to display a React App Contact List. Let's say by making the request to GET https://exampleserver.com/v1/contacts/list will return the follow:


```
let contacts : [{
		"name": "Fry",
		"date_added": "2017-03-27",
		"group": "human",
		"gender": "male",
		"born" : "earth",
		"status" : "online"
	},{
		"name": "Leela",
		"date_added": "2017-03-27",
		"group": "human",
		"gender": "female",
		"born" : "earth",
		"status" : "online"
	},
...
	{
		"name": "Hermes",
		"date_added": "2017-03-27",
		"group": "human",
		"gender": "male",
		"born" : "earth",
		"status" : "offline"
	},
	{
		"name": "Zoidberg",
		"date_added": "2017-03-27",
		"group": "lobster",
		"gender": "male",
		"born" : "unknown",
		"status" : "offline"
	}]

```

### Client Side
Given the array above we can create a list that can look like:
![Unsorted Contacts List](images/unsorted.png "Unsorted Contacts List")

As we are building this, what are some things to consider in terms of performance?

### Cost of operations

Firstly, network calls are expensive. Making an API call to another server takes signficiantly more time than making queries on your local device. If you can do operations locally it will be much more perfomant than relying on network calls.

### Limit the number of operations 
Do what is only necessary. If we have a search feature for this contact list and the server also provides GET https://exampleserver.com/v1/contacts/search?q= 
Should we use this API call whenever the user types in a query into the search box.

This is the first step of thinking about performance when building apps. In the next section, we dig deeper to determine how we analyze performance when working with data structures.


