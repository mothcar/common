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

## Reference  
[video](http://irlnathan.github.io/sailscasts/blog/2013/11/20/sailscasts-answers-ep4-creating-a-more-attractive-url-in-sails-with-slugs-dot-dot-dot-really/)  
