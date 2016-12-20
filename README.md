# gulp-s3 [![NPM version][npm-image]][npm-url]

> s3 plugin for [gulp](https://github.com/wearefractal/gulp)

## Usage

First, install `gulp-ams3` as a development dependency:

```shell
npm install --save-dev gulp-ams3
```

Setup your aws.json file
```javascript
{
  "key": "AKIAI3Z34347CUAFHG53DMJA",
  "secret": "acYxWRu5RRa6CwzQfdfsdfuhdXEfTpbQA+1XQJ7Z1bGTCx",
  "bucket": "dev.example.com",
  "region": "eu-west-1"
}
```

Then, use it in your `gulpfile.js`:
```javascript
var s3 = require("gulp-ams3");
aws = JSON.parse(fs.readFileSync('./aws.json'));
var Client = s3(aws);
gulp.src('./dist/**')
    .pipe(Client.upload({
         uploadPath: "example/test/"
    }));
```

## API


#### options.headers

Type: `Array`          
Default: `[]`

Headers to set to each file uploaded to S3

```javascript
var options = { headers: {'Cache-Control': 'max-age=315360000, no-transform, public'} }
gulp.src('./dist/**', {read: false})
    .pipe(Client.upload(options));
```

#### options.gzippedOnly

Type: `Boolean`          
Default: `false`

Only upload files with .gz extension, additionally it will remove the .gz suffix on destination filename and set appropriate Content-Type and Content-Encoding headers.

```javascript
var gulp = require("gulp");
var s3 = require("gulp-ams3");
var gzip = require("gulp-gzip");
var options = { gzippedOnly: true };
var Client = s3(aws);
gulp.src('./dist/**')
.pipe(gzip())
.pipe(Client.upload(options));

});
```

## License

[MIT License](http://en.wikipedia.org/wiki/MIT_License)

[npm-url]: https://npmjs.org/package/gulp-ams3