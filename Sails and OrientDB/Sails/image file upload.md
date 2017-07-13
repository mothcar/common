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
        var uploadFile= req.file('userPhoto');
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

