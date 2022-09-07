# **This module dives deep into the Create operation:**

## _Document Creation Methos:_

- MongoDB offers 4 method for creating documents:

1. **insertOne()**: this is used to create one document within the collection.
2. **insertMany()**: this is used to create multiple documents at once using an array of documents.
3. **insert()**: this was the old method for creating document and it is more flexible; it can add single or multiple documents.
4. **mongoimport**: importing data.

**note**: insertOne() & insertMany() gives better ackwolegment about the insert than insert().

## _insertMany() and ordered insert:_

- insert many can have another argument , which is the configurations object for the insert operation.

- this config object has a boolean property "ordered" which if it was set to true , while inserting multiple objects for example 3 objects , if the 2nd insertion failed then the 3rd insertion will fail also even if it has no problem so to avoid this we set the ordered property to false.

- there is no right or wrong approach here it depends on your buisiness logic weather you set this property to true or false.

## _WriteConcern:_

- another porperty in the insert configurations is "writeConcern".

- writeConcern by it self is also an object with the following properties.

  - w: 0 ro 1 value indicate weather you want to be acknowledged that the server recieved the insetion order or not. if that is set to 0 then you donot wait to recieve an acknowledgment from the storage engine.

  - j: the default is 'udefined' which means that you shouldn't use a journal, you can set this to 'true' which means use journal.

**note**: the journal is useful in the case of data insertion is interrupted with sudden close of the server, when the server is back up it uses the journal to check if any job is not done yet and complete the interrupted insertion.

- wtimeout: how much time in milliseconds wait for the operations to be finished else stop the operation.
