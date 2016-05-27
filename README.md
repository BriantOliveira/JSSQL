## Install
```sh
$ npm install jssql
```
## Introduction

This is a node.js driver that makes sql easy! It doesnt matter if you're a SQl noob or export, everyone can enjoy JSSQL.

### Setting up our database
The first thing we need to do is setup a database. The code below initializes a database instance and if the database does not exist, then it will create one. 

```js
var jssql = require('jssql');

var Database = jssql.Database;
var testDatabase = new Database({
    host: '127.0.0.1',
    user: 'root',
    password: '',
    database: 'TEST_DATABASE'
});
```

### Creating our first scheme and table
Now that we have a database initilized we can go right into creating out first scheme and table. Let's start by creating our scheme. 
```js
var Scheme = jssql.Scheme;
var Table = jssql.Table;
var Structure = jssql.Structure;

var testScheme = new Scheme({
    ID: {
        type: Structure.Type.INT,
        AI: true,
        Index: Structure.Index.PRIMARY
    },
    NAME: {
        type: "VARCHAR",
        length: 100
    }
});
```
The most important part about creating a scheme is the syntax we use. Inside the project we include constant variables that can be used that describe types and indexs. You can use the constants we define or just write in the keywords yourself. The column syntax is shown below:
- type: The datatype of the column (required)
- length: The datatype length of the column
- index: The index type of the column
- ai: If the column is auto incrementing 
- null: If the column can be null

Once the Scheme is setup, we then have to create our table. A table definition only needs to contain the table name and the scheme. The most important part about creating a table is remembering to pair it with a database. Without a database pair the table will fail to work. 
```js
var testTable = new Table('TABLE_NAME', testScheme);

testDatabase.table(testTable);
```

### Placing and recieving information 
Once we have our table sorted out, we can place some information in it. Below is a quick example of how to add a row
```js
testTable.save({
    NAME: "BOB"
}, function(err){
    if(err)
        throw err;
});
```

Recieving a row is just as easy! Just use the find function and we can get all the rows with the information we want!
```js
testTable.find({
    NAME: "BOB"
}, function(err, rows){
   if(err){
       throw err;
   }

    Console.dir(rows);
});
```

There is a small window that the save function takes to actually save the new row. Because of this time, having a save and find right after each other will not show the new row. Should not be a problem unless you have the code following each other. In that case, set a timeout before you call the find. 

## Developers Note
This is my first npm project, and I am having a grand time working on this. I am adding features as I need them regarding my personal projects. If you want a feature added, submit a ticket [Here](https://github.com/FrostbyteDevelopment/JSSQL/issues). If you want to help with my project, feel free to create a pull request. I am also dislexic, so if anyone wants to help me with this README, feel free.
