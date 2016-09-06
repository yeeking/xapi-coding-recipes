# xAPI Statement Recipes for Educational Coding Activity 

This repository contains statement recipes that are suitable for describing coding activiy. 

It was originally developed to support analysis of data from our CodeCircle system (http://live.codecircle.com).

## Table of contents

* [Initialise a document](#initialise-a-document)
* [Fork a document](#fork-a-document)
* [Edit a document](#edit-a-document)
* [Tag a document](#tag-a-document)


## Initialise a document
This statement is generated when a user creates a new document on codecircle. An example can be found in statement_examples/document_initialised.json.  Note this does not happen when they fork an existing document - for that we have the fork statement. 

## Open a document for editing (launch)
This statement is generated when a user loads up a pre-existing document, for editing or just for viewing. It will also be generated when the user creates or forks a document, since the new document will be opened after this event. An example can be found in statement_examples/document_launched.json.

## End a document viewing session (suspemd)
This statement is generated when a user has previously opened a document but has not generatred any system events for a certain period. The length of the period of inactivity should probably be  specified in the data. An example can be found in statement_examples/session_suspended.json.

## Fork a document
This is created when a user forks an existing document on codecircle. The context property provides information about the original document. An example can be found in statement_examples/document_forked.json. 


## Edit a document
This statement is generated for every edit that is made to a document. Since Codecircle uses an implementation of operational transformation to maintain the document content (allowing realtime, collaborative editing), it necessarily logs every edit or 'operation' that is made. The result object is used to specify the success of the edit (does the code pass through the jshint/ other code checker or not) and the raw score, which is the number of characters in the edit (often == 1, but sometimes more, when they copy paste, for example.). An example can be found in statement_examples/document_edited.json.


## Tag a document 
This statement is generated when a user tags a document. This is typically used during lessons to allow simple document sets to be created. An example can be found in statement_examples/document_annotated.json.


