
# Building a ContactsList
## Cost of operations

Network calls are expensive
Call per search query? No need.

So what it takes to do a search.

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

