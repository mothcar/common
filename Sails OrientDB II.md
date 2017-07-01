# contents
## 1. Setting Sails.js
## 2. Connect OrientDB

# Setting Sails.js

1. Sails new Project

~~~~
$ sails new <projectName>
~~~~

 http://next.sailsjs.com/get-started
 
 2. Create Controller
 ```
 $ sails create controller foo
 ```
 ![](https://github.com/mothcar/common/blob/master/images/controller.jpg)
 
 3. Edit Action on api/controllers.js
 ```
 module.exports = {
	myGoAction : function(req, res){
		res.send("Hello World");
	}
};
```

 4. Edit Route on config/routes.js
 ```
 '/': {view: 'homepage'},
	'GET /foo/bar' : {controller :'Foo', action : 'myGoAction'}
 ```
 
 # Connect OrientDB 
 
 1. Define properies on config/connections.js
 ```
 myLocalOrient: {
        adapter: 'sails-orientdb',
        host: 'localhost',
        port: 2424,
        user: 'root',
        password: 'your_password',
        database: 'o2',
        schema : true,

        // Additional options
        options: {

          // DB/Oriento Options
          //
          // database type: graph | document
          databaseType : 'graph',
          //
          // storage type: memory | plocal
          storage : 'plocal',

          // Useful in REST APIs
          //
          // If `id` is URI encoded, decode it with `decodeURIComponent()` (useful when `id` comes from an URL)
          decodeURIComponent : true,
          //
          // Replaces circular references with `id` after populate operations (useful when results will be JSONfied)
          removeCircularReferences : false,

          // migrations
          //
          // Drop tables without deleting edges/vertexes hence not ensuring graph consistency
          // Will speed up drop operations. Only works with migration: 'alter' or 'drop'
          unsafeDrop : false,

          // other
          //
          // Turn parameterized queries on
          parameterized : true
        }
	}
```

2. Create Model on api/models/<SomeName : Post.js>

```
module.exports = {

    schema: true,
    tableName: 'topic',
    attributes: {
        id: {
            type: 'string',
            primaryKey: true,
            columnName: '@rid'
        },
        name: {
            type: 'string',
            unique: false,
			columnName: 'title'
        },
        firstName: {
            type: 'string',
            unique: false,
			columnName: 'some'
        }
    }
};
```
3. Connect DB adapter on config/models.js
```
module.exports.models = {

  // connection: 'localDiskDb',
  connection: 'myLocalOrient',

  migrate: 'safe'

};
```
*must be migrate: 'safe'*

4. 


 
 
 


