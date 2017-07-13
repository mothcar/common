## client image.pug
```pug
p select a image from your pc
	form(action="/imageup", method="post", enctype="multipart/form-data")
		input(type="text", name="title")
		input(type="file", multiple, name="image")
		button(type="submit", value="Upload") Upload File
```

## create FileController.js
```javascript
/**
 * FileController
 *
 * @description :: Server-side logic for managing files
 * @help        :: See http://links.sailsjs.org/docs/controllers
 */

module.exports = {
    upload: function(req, res, next) {
        // body...
        var uploadFile= req.file('image');
        console.log();
        var uploadPath = process.cwd()+'/assets/images';
        uploadFile.upload({
            dirname: uploadPath
        }, function onUploadComplete(err, files) {

            if (err)
                return res.serverError(err);

            return res.json({
                message: files.length + ' file(s) uploaded successfully!',
                path: uploadPath,
                file: files
            });
        });
    }
};
```


## Reference
[image upload Git](https://github.com/ReyesMagos/images-upload-test-sails)

## Beginning S3 : connection with IAM
[LINK](http://docs.aws.amazon.com/sdk-for-javascript/v2/developer-guide/getting-started-nodejs.html#getting-started-nodejs-download)



