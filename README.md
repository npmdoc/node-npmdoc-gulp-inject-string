# api documentation for  [gulp-inject-string (v1.1.0)](https://github.com/Schmicko/gulp-inject-string)  [![npm package](https://img.shields.io/npm/v/npmdoc-gulp-inject-string.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-gulp-inject-string) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-gulp-inject-string.svg)](https://travis-ci.org/npmdoc/node-npmdoc-gulp-inject-string)
#### Inject snippets in build

[![NPM](https://nodei.co/npm/gulp-inject-string.png?downloads=true)](https://www.npmjs.com/package/gulp-inject-string)

[![apidoc](https://npmdoc.github.io/node-npmdoc-gulp-inject-string/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-gulp-inject-string_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-gulp-inject-string/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-gulp-inject-string/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-gulp-inject-string/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Michael Hazell"
    },
    "bugs": {
        "url": "https://github.com/Schmicko/gulp-inject-string/issues"
    },
    "dependencies": {
        "event-stream": "^3.1.7",
        "gulp-util": "^3.0.0"
    },
    "description": "Inject snippets in build",
    "devDependencies": {
        "chai": "^3.4.1",
        "gulp": "^3.8.6",
        "gulp-rename": "^1.2.0",
        "istanbul": "^0.4.0",
        "mocha": "^2.3.4"
    },
    "directories": {},
    "dist": {
        "shasum": "f02ddedb0f7518dfbad548f7d2df05bae2ed1f64",
        "tarball": "https://registry.npmjs.org/gulp-inject-string/-/gulp-inject-string-1.1.0.tgz"
    },
    "gitHead": "79f76b196bfa852996fb9b15e9ec59fec17a8493",
    "homepage": "https://github.com/Schmicko/gulp-inject-string",
    "keywords": [
        "gulpplugin",
        "inject",
        "insert",
        "html",
        "snippet"
    ],
    "license": "MIT",
    "main": "index.js",
    "maintainers": [
        {
            "name": "schmicko",
            "email": "mike.hazell@gmail.com"
        }
    ],
    "name": "gulp-inject-string",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git+https://github.com/Schmicko/gulp-inject-string.git"
    },
    "scripts": {
        "coverage": "istanbul cover _mocha -- tests/test.js -R spec",
        "test": "mocha tests/test.js"
    },
    "version": "1.1.0"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module gulp-inject-string](#apidoc.module.gulp-inject-string)
1.  [function <span class="apidocSignatureSpan">gulp-inject-string.</span>_stream (injectMethod)](#apidoc.element.gulp-inject-string._stream)
1.  [function <span class="apidocSignatureSpan">gulp-inject-string.</span>after (search, str)](#apidoc.element.gulp-inject-string.after)
1.  [function <span class="apidocSignatureSpan">gulp-inject-string.</span>afterEach (search, str)](#apidoc.element.gulp-inject-string.afterEach)
1.  [function <span class="apidocSignatureSpan">gulp-inject-string.</span>append (str)](#apidoc.element.gulp-inject-string.append)
1.  [function <span class="apidocSignatureSpan">gulp-inject-string.</span>before (search, str)](#apidoc.element.gulp-inject-string.before)
1.  [function <span class="apidocSignatureSpan">gulp-inject-string.</span>beforeEach (search, str)](#apidoc.element.gulp-inject-string.beforeEach)
1.  [function <span class="apidocSignatureSpan">gulp-inject-string.</span>prepend (str)](#apidoc.element.gulp-inject-string.prepend)
1.  [function <span class="apidocSignatureSpan">gulp-inject-string.</span>replace (search, str)](#apidoc.element.gulp-inject-string.replace)
1.  [function <span class="apidocSignatureSpan">gulp-inject-string.</span>wrap (start, end)](#apidoc.element.gulp-inject-string.wrap)



# <a name="apidoc.module.gulp-inject-string"></a>[module gulp-inject-string](#apidoc.module.gulp-inject-string)

#### <a name="apidoc.element.gulp-inject-string._stream"></a>[function <span class="apidocSignatureSpan">gulp-inject-string.</span>_stream (injectMethod)](#apidoc.element.gulp-inject-string._stream)
- description and source-code
```javascript
_stream = function (injectMethod){
    return es.map(function (file, cb) {
        try {
            file.contents = new Buffer( injectMethod( String(file.contents) ));
        } catch (err) {
            return cb(new gutil.PluginError('gulp-inject-string', err));
        }
        cb(null, file);
    });
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.gulp-inject-string.after"></a>[function <span class="apidocSignatureSpan">gulp-inject-string.</span>after (search, str)](#apidoc.element.gulp-inject-string.after)
- description and source-code
```javascript
after = function (search, str){
    return stream(function(fileContents){
        var index, start, end;
        index = fileContents.indexOf(search);
        if(index > -1){
            start = fileContents.substr(0, index + search.length);
            end = fileContents.substr(index + search.length);
            return start + str + end;
        } else {
            return fileContents;
        }
    });
}
```
- example usage
```shell
...
    .pipe(inject.before('<script', '<script src="http://code.jquery.com/jquery-2.1.1.min.js"></script>\n'))
    .pipe(rename('before.html'))
    .pipe(gulp.dest('build'));
});

gulp.task('inject:after', function(){
gulp.src('src/example.html')
    .pipe(inject.after('</title>', '\n<link rel="stylesheet" href="test.css">\n'))
    .pipe(rename('after.html'))
    .pipe(gulp.dest('build'));
});

gulp.task('inject:beforeEach', function(){
gulp.src('src/example.html')
    .pipe(inject.beforeEach('</p', ' Finis.'))
...
```

#### <a name="apidoc.element.gulp-inject-string.afterEach"></a>[function <span class="apidocSignatureSpan">gulp-inject-string.</span>afterEach (search, str)](#apidoc.element.gulp-inject-string.afterEach)
- description and source-code
```javascript
afterEach = function (search, str) {
    return stream(function(fileContents) {
        return fileContents.split(search).join(search + str);
    });
}
```
- example usage
```shell
...
    .pipe(inject.beforeEach('</p', ' Finis.'))
    .pipe(rename('beforeEach.html'))
    .pipe(gulp.dest('build'));
});

gulp.task('inject:afterEach', function(){
gulp.src('src/example.html')
    .pipe(inject.afterEach('<p', ' class="bold"'))
    .pipe(rename('afterEach.html'))
    .pipe(gulp.dest('build'));
});

gulp.task('inject:replace', function(){
gulp.src('src/example.html')
    .pipe(inject.replace('test.js', 'test.min.js'))
...
```

#### <a name="apidoc.element.gulp-inject-string.append"></a>[function <span class="apidocSignatureSpan">gulp-inject-string.</span>append (str)](#apidoc.element.gulp-inject-string.append)
- description and source-code
```javascript
append = function (str){
    return stream(function(fileContents){
        // assume str is a string for now
        return fileContents + String(str);
    });
}
```
- example usage
```shell
...

var gulp = require('gulp'),
rename = require('gulp-rename'),
inject = require('gulp-inject-string');

gulp.task('inject:append', function(){
gulp.src('src/example.html')
    .pipe(inject.append('\n<!-- Created: ' + Date() + ' -->'))
    .pipe(rename('append.html'))
    .pipe(gulp.dest('build'));
});

gulp.task('inject:prepend', function(){
gulp.src('src/example.html')
    .pipe(inject.prepend('<!-- Created: ' + Date() + ' -->\n'))
...
```

#### <a name="apidoc.element.gulp-inject-string.before"></a>[function <span class="apidocSignatureSpan">gulp-inject-string.</span>before (search, str)](#apidoc.element.gulp-inject-string.before)
- description and source-code
```javascript
before = function (search, str){
    return stream(function(fileContents){
        var index, start, end;
        // the simplest thing ...
        index = fileContents.indexOf(search);
        if(index > -1){
            start = fileContents.substr(0, index);
            end = fileContents.substr(index);
            return start + str + end;
        } else {
            return fileContents;
        }
    });
}
```
- example usage
```shell
...
    .pipe(inject.wrap('<!-- Created: ' + Date() + ' -->\n', '<!-- Author: Mike Hazell -->'))
    .pipe(rename('wrap.html'))
    .pipe(gulp.dest('build'));
});

gulp.task('inject:before', function(){
gulp.src('src/example.html')
    .pipe(inject.before('<script', '<script src="http://code.jquery.com/jquery-2.1.1.min.js"></script>\n'))
    .pipe(rename('before.html'))
    .pipe(gulp.dest('build'));
});

gulp.task('inject:after', function(){
gulp.src('src/example.html')
    .pipe(inject.after('</title>', '\n<link rel="stylesheet" href="test.css">\n'))
...
```

#### <a name="apidoc.element.gulp-inject-string.beforeEach"></a>[function <span class="apidocSignatureSpan">gulp-inject-string.</span>beforeEach (search, str)](#apidoc.element.gulp-inject-string.beforeEach)
- description and source-code
```javascript
beforeEach = function (search, str) {
    return stream(function(fileContents) {
        return fileContents.split(search).join(str + search);
    });
}
```
- example usage
```shell
...
    .pipe(inject.after('</title>', '\n<link rel="stylesheet" href="test.css">\n'))
    .pipe(rename('after.html'))
    .pipe(gulp.dest('build'));
});

gulp.task('inject:beforeEach', function(){
gulp.src('src/example.html')
    .pipe(inject.beforeEach('</p', ' Finis.'))
    .pipe(rename('beforeEach.html'))
    .pipe(gulp.dest('build'));
});

gulp.task('inject:afterEach', function(){
gulp.src('src/example.html')
    .pipe(inject.afterEach('<p', ' class="bold"'))
...
```

#### <a name="apidoc.element.gulp-inject-string.prepend"></a>[function <span class="apidocSignatureSpan">gulp-inject-string.</span>prepend (str)](#apidoc.element.gulp-inject-string.prepend)
- description and source-code
```javascript
prepend = function (str){
    return stream(function(fileContents){
        // assume str is a string for now
        return String(str) + fileContents;
    });
}
```
- example usage
```shell
...
    .pipe(inject.append('\n<!-- Created: ' + Date() + ' -->'))
    .pipe(rename('append.html'))
    .pipe(gulp.dest('build'));
});

gulp.task('inject:prepend', function(){
gulp.src('src/example.html')
    .pipe(inject.prepend('<!-- Created: ' + Date() + ' -->\n'))
    .pipe(rename('prepend.html'))
    .pipe(gulp.dest('build'));
});

gulp.task('inject:wrap', function(){
gulp.src('src/example.html')
    .pipe(inject.wrap('<!-- Created: ' + Date() + ' -->\n', '<!-- Author: Mike Hazell -->'))
...
```

#### <a name="apidoc.element.gulp-inject-string.replace"></a>[function <span class="apidocSignatureSpan">gulp-inject-string.</span>replace (search, str)](#apidoc.element.gulp-inject-string.replace)
- description and source-code
```javascript
replace = function (search, str) {
  return stream(function(fileContents) {
    return fileContents.replace(new RegExp(search, 'g'), str);
  });
}
```
- example usage
```shell
...
    .pipe(inject.afterEach('<p', ' class="bold"'))
    .pipe(rename('afterEach.html'))
    .pipe(gulp.dest('build'));
});

gulp.task('inject:replace', function(){
gulp.src('src/example.html')
    .pipe(inject.replace('test.js', 'test.min.js'))
    .pipe(rename('replace.html'))
    .pipe(gulp.dest('build'));
});

gulp.task('default', [
'inject:append',
'inject:prepend',
...
```

#### <a name="apidoc.element.gulp-inject-string.wrap"></a>[function <span class="apidocSignatureSpan">gulp-inject-string.</span>wrap (start, end)](#apidoc.element.gulp-inject-string.wrap)
- description and source-code
```javascript
wrap = function (start, end){
    return stream(function(fileContents){
        // assume start and end are strings
        return String(start) + fileContents + String(end);
    });
}
```
- example usage
```shell
...
    .pipe(inject.prepend('<!-- Created: ' + Date() + ' -->\n'))
    .pipe(rename('prepend.html'))
    .pipe(gulp.dest('build'));
});

gulp.task('inject:wrap', function(){
gulp.src('src/example.html')
    .pipe(inject.wrap('<!-- Created: ' + Date() + ' -->\n', '<!-- Author: Mike Hazell -->'))
    .pipe(rename('wrap.html'))
    .pipe(gulp.dest('build'));
});

gulp.task('inject:before', function(){
gulp.src('src/example.html')
    .pipe(inject.before('<script', '<script src="http://code.jquery.com/jquery-2.1.1.min.js"></script>\n'))
...
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
