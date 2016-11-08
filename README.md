# Data-Representation-And-Querying-PouchDB
PouchDB app and exercises. To run the PouchDB app start PouchDB Server and open the index.html file.

#### PROBLEM 1) Perform a get request on the root resource
curl http://127.0.0.1:5984/

#### PROBLEM 2) Create a new database called emails and perform a get request on it
curl -X PUT http://127.0.0.1:5984/emails
curl http://127.0.0.1:5984/emails

#### PROBLEM 3) Create a JSON file called email1.json and add it to the database
The following is the contents of the json file
{
	"email": "G00324844@gmit.ie"
}

Used cat email1.json to verify the contents

Command used to add it to the database
curl -X POST http://127.0.0.1:5984/emails -H "Content-type: application/json" -d @email1.json

#### PROBLEM 4) Add a second document called email2.json
The following is the contents of the json file
{
	"email": "G00123456@gmit.ie"
}

Command used to add it to the database (Just changed the file name at the end)
curl -X POST http://127.0.0.1:5984/emails -H "Content-type: application/json" -d @email2.json

#### PROBLEM 5) Retrieving the documents added above
Command used to retieve the ids
curl http://127.0.0.1:5984/emails/_all_docs

Command used to retrieve the documents ids and content
curl http://127.0.0.1:5984/emails/_all_docs?include_docs=true

Command used to retrive each document individually
curl http://127.0.0.1:5984/emails/[Insert ID here]?include_docs=true

For example:
curl http://127.0.0.1:5984/emails/4d6c2559-3af1-45cc-a55f-307236bfc93a?include_docs=true
Returns:
{"email":"G00123456@gmit.ie","_id":"4d6c2559-3af1-45cc-a55f-307236bfc93a","_rev":"1-4702fc23e10ffd596ab2179d2ac5f447"}

#### PROBLEM 6) Update the first document
Edited email1.json to make it the following
{
	"_id": "4d6c2559-3af1-45cc-a55f-307236bfc93a"
	"email": "G00000000@gmit.ie",
	"_rev":"1-4702fc23e10ffd596ab2179d2ac5f447"
}

Added it to the database using the command
curl -X PUT http://127.0.0.1:5984/emails/4d6c2559-3af1-45cc-a55f-307236bfc93a -H "Content-type: application/json" -d @email1.json
		
Retrieve it using
curl http://127.0.0.1:5984/emails/4d6c2559-3af1-45cc-a55f-307236bfc93a

#### PROBLEM 7) Delete the document
Use the following command to delete the document
curl -X DELETE http://127.0.0.1:5984/emails/4d6c2559-3af1-45cc-a55f-307236bfc93a

Get all documents using the following command and check if it was deleted
curl http://127.0.0.1:5984/emails/_all_docs