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


## Success Reference : 
[LINK](https://github.com/sails101/file-uploads/blob/master/api/controllers/FileController.js#L15)

# Show image
It doesn't have to do with CORS, it's the S3 bucket configuration on Amazon Web Services.  

If you are comfortable with the entire bucket being public-read, here's the official AWS guide, and my rough steps:  

enable web hosting, add index/error document defaults.
1. add the public-read policy (below; only need to change BUCKETNAME)  
2. policy:  
```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AddPerm",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::yourBucketName/*"
        }
    ]
}
```
![policy](https://github.com/mothcar/common/blob/master/images/policy.png)
