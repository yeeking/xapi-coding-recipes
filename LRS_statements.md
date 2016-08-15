# xAPI Statement types for CodeCircle

This document describes and provides examples of xAPI statements that can be generated from CodeCircle activity. Where possible, they have been based on existing xAPI related vocab sets, e.g. [https://adl.gitbooks.io/experience-xapi-vocabulary-primer/content/search_and_query_opportunities/direct_requests_on_vocabulary_dataset_iris.html] and [search form here][http://xapi.vocab.pub:8890/fct/facet.vsp?cmd=text&sid=4013]. 

## Table of contents

* [Initialise a document](#initialise-a-document)
* [Fork a document](#fork-a-document)
* [Edit a document](#edit-a-document)
* [Tag a document](#tag-a-document)

## Initialise a document
This statement is generated when a user creates a new document on codecircle. Note this does not happen when they fork an existing document. 
```
{
    "id": "12345678-1234-5678-1234-567812345678",
    "actor":{
        "name":"Matthew", 
        "objectType":"Agent", 
        "account": {
            "homePage": "http://live.codecircle.com/s/@username",
            "name": "cc_mongo_user_id"
        }
    },
    "verb":{
    	"id":"http://adlnet.gov/expapi/verbs/initialized", 
        "display":{
            "en-GB":"initialised", 
            "en-US":"initialized"
        }, 

    },
    "object": {
    	"objectType": "Activity"
    	"id": "http://live.codecircle.com/<docId>",
	    "definition": 
	    	{"name":
	    		{"en-US":"CodeCircle Document title"},
	    "description":
	    		{"en-US":"A document in CodeCircle system"}
	    	}

}
```

## Fork a document
This is created when a user forks an existing document on codecircle. The context property provides access to the original document. 

```Javascript
{
    "id": "12345678-1234-5678-1234-567812345678",
    "actor":{
     	"name":"Matthew", 
     	"objectType":"Agent", 
        "account": {
        	"homePage": "http://live.codecircle.com/s/@username",
	        "name": "cc_mongo_user_id"
    	}
    },
    "verb":{
    	"id":"http://xapi.vocab.pub:8890/describe/?url=http%3A%2F%2Fwww.openlinksw.com%2Fschemas%2Fgithub%23forks&sid=4013&urilookup=1", 
        "display":{
            "en-GB":"forked"
        }, 

    },
    "object": {
    	"objectType": "Activity"
    	"id": "http://live.codecircle.com/<docId>",
	    "definition": {
             "name":
	    		{"en-US":"CodeCircle Document title"},
	         "description":
	    		{"en-US":"A document in CodeCircle system"}
	    }
    }
    "context": {
        "contextActivities":{
            "parent": { "id": "http://live.codecircle.com/<docId_that_was_forked>" },
        }
    }
}
```

## Edit a document
This statement is generated for every edit that is made to a document. Since Codecircle uses an implementation of operational transformation to maintain the document content (allowing realtime, collaborative editing), it necessarily logs every edit or 'operation' that is made. The result object is used to specify the success of the edit (does the code pass through the jshint/ other code checker or not) and the raw score, which is the number of characters in the edit (often == 1, but sometimes more, when they copy paste, for example.). 

```Javascript
{
    "id": "12345678-1234-5678-1234-567812345678",
    "actor":{
        "name":"Matthew", 
        "objectType":"Agent", 
        "account": {
            "homePage": "http://live.codecircle.com/s/@username",
            "name": "cc_mongo_user_id"
        }
    },
    "verb":{
    	"id":"https://w3id.org/xapi/acrossx/verbs/edited", 
        "display":{
            "en-GB":"edited"
        }, 

    },
    "object": {
    	"objectType": "Activity"
    	"id": "http://live.codecircle.com/<docId>",
	    "definition": {
	       "name":
	    		{"en-US":"CodeCircle Document"},
	       "description":
	    		{"en-US":"A document in CodeCircle system"}
	    }
    ], 
    "result": {
        "success": true,
        "score": {
            "raw": 100
        }
    }
}
```

## Tag a document 
This statement is generated when a user tags a document. This is typically used during lessons to allow simple document sets to be created. 


```Javascript
{
    "id": "12345678-1234-5678-1234-567812345678",
    "actor":{
        "name":"Matthew", 
        "objectType":"Agent", 
        "account": {
            "homePage": "http://live.codecircle.com/s/@username",
            "name": "cc_mongo_user_id"
        }
    },
    "verb":{
        "id":"https://w3id.org/xapi/adb/verbs/annotated
", 
        "display":{
            "en-GB":"annotated"
        }, 

    },
    "object": {
        "objectType": "Activity"
        "id": "http://live.codecircle.com/<docId>",
        "definition": 
            {"name":
                {"en-US":"CodeCircle Document title"},
        "description":
                {"en-US":"A document in CodeCircle system"}
            }

}
```





