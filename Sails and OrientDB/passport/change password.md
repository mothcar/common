
## Step 1 : Prepare
> Prepare Auth : look [LINK](https://github.com/mothcar/common/blob/master/Sails%20and%20OrientDB/passport/login.md)

## Step 2 : Create View page that could change password
```
<h1>This is Main</h1>
<h2>Get user ID</h2>
  <form method="POST" action="/newpassword">
  <input type="password" name="newpassword">
  <input type="submit" value="submit">
</form>
```

## Step 3 : configuring the routes
Go `config / routes.js` and insert this.
```
'POST /newpassword' : {controller : 'User', action : 'changepasswordAction'},
```

## Step 4 : Configuring the Controller
Go `controller / UserController.js` and insert this lines.
```
changepasswordAction : function(req, res){
		let p_newpassword = req.param('newpassword');
		let user_id = req.user.id;
		
		console.log('new password is : ', user_id);

		User.update({id : user_id},{ password : p_newpassword}).exec(function afterwards(err, updated){
			if (err) {
				// handle error here- e.g. `res.serverError(err);`
				console.log('ERROR OCCURed ' + err);
				return;
			}
			console.log('*** UserController.js ***')
			console.log('Updated user to have name : ' , req.user);
		});

		res.send('Response done')
	}
  ```
  
  ## Step 5 : Configuring the Model
  go `models / User.js` insert this lines after `beforeCreate` function block.
  ```
  beforeUpdate: function(user, cb) {
		console.log('*** User.js ***')
		console.log('User.js - this user profile :: ', user)
		bcrypt.genSalt(10, function(err, salt) {
			bcrypt.hash(user.password, salt, function(err, hash) {
				if (err) {
					console.log(err);
					cb(err);
				} else {
					user.password = hash;
					cb();
				}
			});
		});
	}
  ```
  
## Done!
