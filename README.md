# connect-gzip

Middleware for [Connect](http://senchalabs.github.com/connect/) or [Express](http://expressjs.com/) that compresses static files using gzip and caches the result on disk for use in future requests.


## Installation

Install via npm (outdated version):

    $ npm install connect-gzip


## Usage

### staticGzip(root, [options])

Gzips files in a root directory, and then serves them using the [send](https://github.com/pillarjs/send) middleware. Note that options get passed through as well, so the `maxAge` and other options supported by `send` also work.

If a file under the root path (such as an image) does not have an appropriate MIME type for compression, it will still be passed through to `send` and served uncompressed. Thus, you can simply use `staticGzip` in place of `connect.static` or `express.static`.

    var connect = require('connect'),
        staticGzip = require('connect-gzip');
    
    connect.createServer(
      staticGzip(__dirname + '/public')
    ).listen(3000);
    
    
    // Only gzip javascript files:
    staticGzip(__dirname + '/public', { matchType: /javascript/ })

    // Set a maxAge in milliseconds for browsers to cache files
    var oneDay = 86400000;
    staticGzip(__dirname + '/public', { maxAge: oneDay })

    // Store all gzipped files in a directory called 'public-gzip'
    var oneDay = 86400000;
    staticGzip(__dirname + '/public', { gzipRoot: __dirname + '/public-gzip' })

Options:

- `matchType` - A regular expression tested against the file MIME type to determine whether the response should be gzipped or not. As in `connect.static`, MIME types are determined based on file extensions using [node-mime](https://github.com/bentomas/node-mime). The default value is `/text|javascript|json/`.
- `maxAge` - Maximum time in milliseconds for browsers to cache files.
- `gzipRoot` - Root directory for cached gzip files. Defaults to root if not specified.


## Tests

Run the tests with

    npm test


## License

(The MIT License)

Copyright (c) 2011 Nate Smith &lt;nate@nateps.com&gt;

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
'Software'), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.