[![npm](https://img.shields.io/npm/dm/express-sanitizer.svg?style=flat-square)](https://github.com/markau/express-sanitizer)
[![Build Status](https://github.com/markau/express-sanitizer/workflows/build/badge.svg?branch=master)](https://github.com/markau/express-sanitizer)
[![npm](https://img.shields.io/npm/l/express.svg?style=flat-square)](https://github.com/markau/express-sanitizer)
[![dependencies](https://david-dm.org/markau/express-sanitizer.svg?style=flat-square)](https://david-dm.org/markau/express-sanitizer)
[![Known Vulnerabilities](https://snyk.io/test/github/markau/express-sanitizer/badge.svg?targetFile=package.json)](https://snyk.io/test/github/markau/express-sanitizer?targetFile=package.json)

**Notice**: The primary dependency for this library hasn't been updated in 5 years. Before using this library, consider other options such as [express-validator](https://express-validator.github.io/docs/). 

# express-sanitizer

An express middleware for [Caja-HTML-Sanitizer](https://github.com/theSmaw/Caja-HTML-Sanitizer), which wraps [Google Caja sanitizer](https://code.google.com/p/google-caja/wiki/JsHtmlSanitizer).

A useful complement to the [express-validator](https://github.com/ctavan/express-validator) -- to fill a gap now that XSS sanitization support has been removed from that module's parent [node-validator](https://github.com/chriso/node-validator).

## Installation

```
yarn add express-sanitizer
```

or

```
npm install --save express-sanitizer
```

## Usage

Import the module

```javascript
const expressSanitizer = require('express-sanitizer');
```

Mount the middleware *below* the `express.json()` (or, prior to express v4.16, `bodyParser()`) instantiation and *above* mounting of your routes

```javascript
app.use(express.json());

// Mount express-sanitizer middleware here
app.use(expressSanitizer());

app.post('/', function(req, res, next) {
  // replace an HTTP posted body property with the sanitized string
  const sanitizedString = req.sanitize(req.body.propertyToSanitize);
  // send the response -- res.body.sanitized = " world"
  res.send({ sanitized: sanitizedString });
});
```

## Output

The string
```javascript
'<script>hello</script> world'
```
will be sanitized to ' world'.

## Limitations

This is a basic implementation of [Caja-HTML-Sanitizer](https://github.com/theSmaw/Caja-HTML-Sanitizer) with the specific purpose of mitigating against persistent XSS risks (<b>note the borderline abandonware comments in that repo!</b>).

## Caveats

This module trusts the dependencies to provide basic persistent XSS risk mitigation. A user of this package should review all packages and make their own decision on security and fitness for purpose.

## Changelog
### v1.0.6
- Removed unused dependency

### v1.0.5
- Unit tests (better late than never)

### v1.0.4
- Merged PR #3 from Brian M. Jemilo II

### v1.0.3
- Updated README to base example on an express-generator scaffolded application

### v1.0.2
- Updated sanitizer dependency to 0.1.3
- Merged PR #4 from @ScottRamsden

### v1.0.1
- Updated sanitizer dependency to 0.1.2

### v1.0.0
- Update to v1

### v0.1.1
- Merged PR removing unused dependency

### v0.1.0
- Initial release

## Contributors

- Mark Andrews <20metresbelow@gmail.com>
- Patrick Hogan <patrick@callinize.com>
- Scott Ramsden @ScottRamsden
- Brian M. Jemilo II <jemiloii@jemiloii.com>

## License

Copyright (c) 2021 Mark Andrews <20metresbelow@gmail.com>, MIT License

