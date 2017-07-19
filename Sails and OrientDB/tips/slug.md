# More Attractive Url in Sails With slugs
## Using Slug
```terminal
$ sails new slugsville --linker
```

## add `slug` into Model
```javascript
slug: {

          type: 'string',
      },
```
## add function into Model too  
Next to attribute  

```javascript
beforeCreate: function(values, next) {
		if(!values.title){
			return next({ err : ['Must have a some title!']})
		}
		values.slug = values.title.replace(/\s+/g, '').toLowerCase();
		next();
	}
```

## To get one post, create routes
```javascript
'GET	/:slug'		: { controller : 'Post', action : 'singlePost'},
'GET	/post/:slug'	: { controller : 'Post', action : 'singlePost'},
```
## implement controller
```javascript
singlePost : function(req, res, next){
		var slug = req.param('slug');
		if(slug.match(/\..+$/)) return next();

		Post
		.findOneBySlug(slug)
		.exec(function(err, post){
			if(err) return res.serverError(err);
			if(!post) return next();
			// res.view({post : post});

			res.view('components/one_post', post);
		});
	},
```

## View  
create Pug view file following model properties
```pug
extends ../layout

block body
	h2 #{area}
	h2 #{fileName}
	h2 #{content}

```



## Reference  
[video](http://irlnathan.github.io/sailscasts/blog/2013/11/20/sailscasts-answers-ep4-creating-a-more-attractive-url-in-sails-with-slugs-dot-dot-dot-really/)  
