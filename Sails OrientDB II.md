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
 
 
 
 


