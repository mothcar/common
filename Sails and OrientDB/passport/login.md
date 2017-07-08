## Step 1 : create Project
```
$ sails new yourProject
```


## Step 2 : dependencies
Add these dependencies to your package.json
```
"dependencies": {
    ...
    "bcrypt": "~0.8.0",
    "passport": "~0.2.1",
    "passport-local": "~1.0.0",
    ...
}
```
## Step 3 : install dependencies
```
$ npm install
```

## Step 4 : create user model
```
$sails generate api user
```
and then let's make User.js look like this:
```
var bcrypt = require('bcrypt');

module.exports = {
    attributes: {
        email: {
            type: 'email',
            required: true,
            unique: true
        },
        password: {
            type: 'string',
            minLength: 6,
            required: true
        },
        toJSON: function() {
            var obj = this.toObject();
            delete obj.password;
            return obj;
        }
    },
    beforeCreate: function(user, cb) {
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
};
```

## Step 5 : create auth controller
```
$ sails generate controller auth
```
and then let's make AuthController.js to make look like this too.
```
var passport = require('passport');

module.exports = {

    _config: {
        actions: false,
        shortcuts: false,
        rest: false
    },

    login: function(req, res) {

        passport.authenticate('local', function(err, user, info) {
            if ((err) || (!user)) {
                return res.send({
                    message: info.message,
                    user: user
                });
            }
            req.logIn(user, function(err) {
                if (err) res.send(err);
                return res.send({
                    message: info.message,
                    user: user
                });
            });

        })(req, res);
    },

    logout: function(req, res) {
        req.logout();
        res.redirect('/');
    }
};
```
## Step 6 : Create Singup.ejs and Login.ejs Views 
```
<h1>Signup</h1>
<form method="POST" action="/user">
  <input type="email" name="email">
  <input type="password" name="password">
  <input type="submit" value="submit">
</form>
```
and  
```
<h1>Login</h1>
  <form method="POST" action="/login">
  <input type="email" name="email">
  <input type="password" name="password">
  <input type="submit" value="submit">
</form>
```
## Step 7 : Configuring the routes.js
```
module.exports.routes = {
  '/': {
    view: 'homepage'
  },

  'get /login': {
       view: 'login'
  },

  'post /login': 'AuthController.login',

  '/logout': 'AuthController.logout',

  'get /signup': {
    view: 'signup'
  }
};
```
## Step 8 : Configuring the http.js on /config/http.js
```
module.exports.http = {
   middleware: {

    passportInit    : require('passport').initialize(),
    passportSession : require('passport').session(),

     order: [
            'startRequestTimer',
            'cookieParser',
            'session',
            'passportInit',     
            'passportSession', 
            'myRequestLogger',
            'bodyParser',
            'handleBodyParserError',
            'compress',
            'methodOverride',
            'poweredBy',
            'router',
            'www',
            'favicon',
            '404',
            '500'
          ],
     }
};
```
Into the order array we added passportInit and passportSession after the session element. The name of this array is quite self-explanatory, the elements must be ordered this way.  

## Step 9 : define Passport local strategy for authentication
create a new file called **passport.js**

```
var passport = require('passport'),
LocalStrategy = require('passport-local').Strategy,
bcrypt = require('bcrypt');

passport.serializeUser(function(user, done) {
    done(null, user.id);
});

passport.deserializeUser(function(id, done) {
    User.findOne({ id: id } , function (err, user) {
        done(err, user);
    });
});

passport.use(new LocalStrategy({
    usernameField: 'email',
    passwordField: 'password'
  },
  function(email, password, done) {

    User.findOne({ email: email }, function (err, user) {
      if (err) { return done(err); }
      if (!user) {
        return done(null, false, { message: 'Incorrect email.' });
      }

      bcrypt.compare(password, user.password, function (err, res) {
          if (!res)
            return done(null, false, {
              message: 'Invalid Password'
            });
          var returnUser = {
            email: user.email,
            createdAt: user.createdAt,
            id: user.id
          };
          return done(null, returnUser, {
            message: 'Logged In Successfully'
          });
        });
    });
  }
));
```

## Step 10 : Step 8: add a new policy  
create `isAuthenticated.js` into the `/api/policies/` folder
```
module.exports = function(req, res, next) {
   if (req.isAuthenticated()) {
        return next();
    }
    else{
        return res.redirect('/login');
    }
};
```
Briefly, we are telling Sails what to do if a user is not authenticated, then we can bind this policy to any of the controllers in the app.  

## Step 11 : bind the policy to a controller
Let's create a controller and a model just for testing what we have done.  
I am going to call this api post.
```
$ sails generate api post
```
Then let's bind the policy to the PostController by updating yourproject/config/policies.js:  
```
module.exports.policies = {

   '*': true,

  'PostController': {
    '*': 'isAuthenticated'
  },

};
```

## Step 12 : run a test
Lift your application  
```
$ sails lift
```


## Refernce
http://iliketomatoes.com/implement-passport-js-authentication-with-sails-js-0-10-2/




