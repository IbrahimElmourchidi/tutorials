# **This module discuss the basic CRUD operations using mongo DB:**

## _Introduction :_

- Mongo DB Server can have multiple **Databases** , each database contains one or more **Collections** and each collection contains one or more **Documents**.
- **Collections** is the same as tables in the Sql Databases.
- **Document** is the same as records in the Sql Databases. Document max size is 16mb and it can hold nested documents up to 100 level.
- **Databases** , **Collections**, and **Documents** are created implicitly when you start insert data in them.

## _Module Cheat Sheet:_

### **1. show all databases**

```bash
    show dbs
```

### **2. create database**

```bash
    use <database name>
```

- This command set the current active database to what ever database pass to the command. If the database doesn't exist, it will be created once you start insert data.
- The current active database is accessed through the _**db**_ variable.

### **3. insert data to collections**

```bash
    db.<collection name>.insertOne(<your document object>)
```

- This command inset one document the _<collection name>_ inside the current active database, if the collections doesn't exist , it will be created implicitly.

### **4. find all data in collections**

```bash
    db.<collection name>.find(<your filtering object>)
```

- This command gets all the data that matched the the filtering object, if the filtering object is empty then all data in that collection will be returned.

  <big><ins>**Note**: the find method doesn't reutrn the data, instead it returns a **cursor object** to the first 20 matching data, using this cursor your can iterate over the collection to get the next 20 results and so on.</ins></big>

- because find return a cursor not the data you may need to use **pretty()** method to prsent the data in a more readable way.

```bash
    db.<collection name>.find(<your filtering object>).pretty()
```

### **5. Delete document from collections**

- to delete one document

```bash
    db.<collection name>.deleteOne(<your fileter object>)
```

- This command deletes the first document matches the filter object.

- to delete many documents.

```bash
    db.<collection name>.deleteMany(<your fileter object>)
```

- This command deletes all documents that matches the filter object.

  <big><ins>**Note:** to use **deleteOne()** or **deleteMany()** you must pass a filter object , if not an **exception** is thrown. </ins></big>

  <big><ins>**Note:** if the filer object is empty the the **deleteOne()** command will delete the **first** document in the collection, whereas the **deleteMany()** command will delete **all** the documents in the collection. </ins></big>

### **6. Update documents in collections**

- to update one document

```bash
    db.<collection name>.updateOne(<your fileter object>, {$set: <your update object>})
```

- This command updates the first document matches the filter object.

- to update many documents.

```bash
    db.<collection name>.updateMany(<your fileter object>, {$set:<your update object>})
```

- This command updates all documents that matches the filter object.

  <big><ins>**Note:** to use **updateOne()** or **updateMany()** you must pass a filter object , if not an **exception** is thrown. </ins></big>

  <big><ins>**Note:** the update object can contain properties that either exist or not in the original document, if the property exists the value is simply updated else the property will be created.</ins></big>

### **7. insert multiple document to collections**

```bash
    db.<collection name>.insertMany(<arry of your document objects>)
```

- This command inset Many document the _<collection name>_ inside the current active database, if the collections doesn't exist , it will be created implicitly.

### **8. find one document in the collection**

```bash
    db.<collection name>.findOne(<your filter object>)
```

- This command finds the first document matches the filter object.

  <big><ins>**Note:** unlike find() this method does return data (not cursor object) so if you try to use pretty() with is error happens.</ins></big>

### **9. Update() vs UpdateMany()**

```bash
    db.<collection name>.update(<your filter object>, <your update object>)

    db.<collection name>.updateMany(<your filter object>, {$set:{<your update object>}})
```

- both of these command update the documents matching the filter object, although update replaces the whole object if uses normal object withoud the $set object.

- In general its recommended to avoid using update() and only use updateOne() and updateMany() to avoid this sitiuation.

- If you want to replace your object you can use replaceOne().

### **10. replace documents in collections**

- to replace one document

```bash
    db.<collection name>.updateOne(<your fileter object>, {$set: <your update object>})
```

- This command replace the document that matches the filter object.
- the filter object should contain atomic property.

### **11. find and the cursor object**

- as stated above find doesn't return data, instead it returns a cursor object to the data which can be used to iterate over all the data.

- this behavior is intended to reduce the amount of data needed to be transfered in large collections (same purpose of pagination).

- but what if you need to get all the data no just the first 20? use this command:

```bash
    db.<collection name>.find().forEach(item => printjson(item))
```

- this command simply uses the forEach() method defined in the cursor object to iterate over all the data and print them with printjson().

  <big><ins>**Note:** this doesn't fetch all data the loop over them , in contrast it fetches documents on demand.</ins></big>

### **12. Projection**

```bash
    db.<collection name>.find(<your filter object>, <your projection object>)
```

- projection object contains property names with values 0 or 1.

- if the value is 1 then this property will be presented in the document else it will be excluded (same as serailization in SQL).

- this helps reduce your used bandwidth when transfering data.

- **\_id** is included by default so if you want to exclude it you need to explicitly add \_id:0 to you projection object.

- if you passed empty projection object all the properties are included by default, if you added at least one property with value 1 in the projections object then all other propeties are excluded implicitly and you need to tell mongo DB to explicitly add them if you need them , the only exception is the \_id which is always included by default.

### **13. Drop database**:

```bash
db.dropDatabase();
```

## _check points :_

- at the end of this module you must be able to:
  - create database.
  - insert data to a collection (2 methods).
  - get data from a collection ( 2 methods)
  - update data of a collection (3 methods).
  - delete data from a collection (2 method).
  - iterate over all the data in a collection (not just the first 20).
  - know the difference between update & updateAll()
  - drop database.
