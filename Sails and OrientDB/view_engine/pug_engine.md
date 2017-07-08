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

## Step 5 : Connect view file
Open `config / routes.js`
```
'GET /' 	: {controller :'Home', action : 'homeAction', view : 'homepage'},
'GET /login'	: {view : 'login'},
'GET /signup'	: {view : 'signup'},
'/main'		: {view : 'main'}
```


## Tutorial :: [LINK](https://codepen.io/mimoduo/post/learn-pug-js-with-pugs)

## import file
```
link(href='/styles/styles.css', rel='stylesheet')
script(src='/js/somejs.js')
script(type='text/javascript').  
	var myVar = 'Hello world ';
	var sum = myVar+somevar;
	console.log(sum);
h1 This is pub Homepage
h2 Welcome
```

