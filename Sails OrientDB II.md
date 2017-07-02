# contents
## 1. Setting Sails.js
## 2. Connect OrientDB

# Setting Sails.js

1. Sails new Project

~~~~
$ sails new <projectName>
~~~~

cf) http://next.sailsjs.com/get-started
 
 2. Create Controller
 ```
 $ cd <projectName>
 $ sails generate controller foo
 ```
 ![](https://github.com/mothcar/common/blob/master/images/new_foo.png)
 
 3. Edit Action on **api/controllers/FooController.js**
 ```
 module.exports = {
	myGoAction : function(req, res){
		res.send("Hello World");
	}
};
```

 4. Edit Route on **config/routes.js**
 ```
'/': {view: 'homepage'},
'GET /foo/bar' : {controller :'Foo', action : 'myGoAction'}
 ```
 
 # Connect OrientDB 
 
 1. install sails-orientdb module by npm 
 ```
 $ npm install appscot/sails-orientdb --save
 ```
 cf) https://www.npmjs.com/package/sails-orientdb
 
 
 2. Define properies on **config/connections.js**
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

3. Create Model on **api/models/<SomeName : Post.js>**  
create new file : **Post.js**

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
4. Connect DB adapter on **config/models.js**
```
module.exports.models = {

  // connection: 'localDiskDb',
  connection: 'myLocalOrient',

  migrate: 'safe'

};
```
must be **migrate: 'safe'**

5. Activate your Orientdb on your Terminal
![](https://github.com/mothcar/common/blob/master/images/orientdb.jpg)

6. Test your sql on **api/controllers/FooController.js**
```
module.exports = {
	myGoAction : function(req, res){
		Post.query("SELECT FROM topic", function(err, retrievedUsers){
			// console.log(retrievedUsers);
			// result = retrievedUsers;
		}).then(function(result){
			res.json(result);
		});
	}

};
```

7. Run Sails
```
$ sails lift
```

8. Route api 
```
http://localhost:1337/
```

9. Done : The result view on browser like this as your database.
![](https://github.com/mothcar/common/blob/master/images/new_result.jpg)

## if get Errors

### case : "Cant send headers after they are sent."
: use just once ```res.json(<some result>);```

## References : Appreciate
https://github.com/gauravdhiman/sailsjs-angularjs-orientdb-poc/tree/master/api

 
 


