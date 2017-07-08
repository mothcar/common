## Start

## Step 1 : install pug module
```console
$ npm install --save pug
```

## Step 2 : Configuring the view engine
Go to `config / views.js` and edit
```javascript
// engine: 'ejs',
  engine: 'pug',
```
## Step 3 : Sample pug
In pug syntax, indent is very important!
```pug
h1 pug Singup
form(method='POST' action='/user')
	input(type='username' name='username')
	input(type='email' name='email')
	input(type='password' name='password')
	input(type='submit' value='submit')
```


## Step 4 : update page (extends)
If you want to update page, you will need to start with 
```pug
extends ../layout
block body
```

## Step 5 : Connect view file
Open `config / routes.js`
```javascript
'GET /' 	: {controller :'Home', action : 'homeAction', view : 'homepage'},
'GET /login'	: {view : 'login'},
'GET /signup'	: {view : 'signup'},
'/main'		: {view : 'main'}
```


## Basic Tutorial :: [LINK](https://codepen.io/mimoduo/post/learn-pug-js-with-pugs)
## Syntax :: [LINK](https://medium.com/@antonioregadas/getting-started-with-pug-template-engine-e49cfa291e33)

## import file
```pug
link(href='/styles/styles.css', rel='stylesheet')
script(src='/js/somejs.js')
script(type='text/javascript').  
	var myVar = 'Hello world ';
	var sum = myVar+somevar;
	console.log(sum);
h1 This is pub Homepage
h2 Welcome
```
## Useful technique
> include
>> make part `parts/in_login_form.pug`
```pug
form(method='POST' action='/login')
	div.form-group
		label(for='email') Email : 
		input#email.form-control(type='email' name='email' placeholder='your@gmail.com')
	div.form-group
		label(for='pwd') password : 
		input#pwd.form-control(type='password' name='password' placeholder='6자리 이상')
	button.btn.btn-primary(type='submit') Log in

```
>> insert part into view pug file
```pug
div.col-md-4.column
	include parts/in_login_form.pug
```

## form :: [LINK](https://teamtreehouse.com/library/creating-a-registration-form-with-pug-jade-2)


