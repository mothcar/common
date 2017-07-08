## Start

## Step 1 : install pug module
```
npm install --save pug
```

## Step 2 : Configuring the view engine
Go to `config / views.js` and edit
```
// engine: 'ejs',
  engine: 'pug',
```

## Step 3 : Create pug file
In pug file, you will need to start with 
```
extends ../layout
block body
```
## Step 4 : Sample
In pug syntax, indent is very important!
```
h1 pug Singup
form(method='POST' action='/user')
	input(type='username' name='username')
	input(type='email' name='email')
	input(type='password' name='password')
	input(type='submit' value='submit')
```

## Step 4 : Connect view file
Open `config / routes.js`
```
'GET /' 						: {controller :'Home', action : 'homeAction', view : 'homepage'},
'GET /login'				: {view : 'login'},
'GET /signup'				: {view : 'signup'},
'/main'							: {view : 'main'}
```

