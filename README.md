# AWS SDK Light

![npm](https://img.shields.io/npm/v/aws-sdk-light)
![](https://github.com/karopolopoulos/aws-sdk-light/workflows/ci/badge.svg)

This package is primarily focused at enabling Apigee users to integrate with AWS services directly from a [JavaScript Policy](https://docs.apigee.com/api-platform/reference/policies/javascript-policy). However it can certainly be used by anyone.

Although there are already many great libraries that allow integration into AWS services (including the actual [aws-sdk](https://www.npmjs.com/package/aws-sdk)!) I found that the situation I was in did not allow me to use them :sob: :rage:.

Key things about why I made this:

- Javascript Policy is the only viable option for me
- The engine used is [Rhino JavaScript engine 1.7.7.1](https://docs.apigee.com/release/supported-software.html#apigeeedgecloud-javascript)
- There are limitations with the current JS version
  - Methods cannot exceed 64kb - [generated bytecode for method exceeds 64K limit](http://www.programmersought.com/article/5394215653/)
  - ES2015 features and beyond are not supported (including Typed Array) - [Rhino ES2015 Support](https://mozilla.github.io/rhino/compat/engines.html)

## Installation

Available on [npm](https://www.npmjs.com/package/aws-sdk-light)

```shell
npm install aws-sdk-light
```

## Overview

### Importing

```js
// import entire SDK
var awsSdkLight = require('aws-sdk-light');

// import single module
var awsSdkLight = require('aws-sdk-light/clients/lambda');
```

### Usage

```js
var awsSdkLight = require('aws-sdk-light');

var options = {
  accessKeyId: '<value>',
  secretAccessKey: '<value>',
  region: '<value>'
};
var lambda = new awsSdkLight.Lambda(options);

var params = {
  FunctionName: 'hello-world',
  Payload: <string>
};
lambda.invoke(params, function(err, data) {
  if (err) {
    console.log(err);
  } else {
    console.log(data)
  }
});
```

## Documentation

- [Guides](docs/guides.md)
- [API Documentation](docs/api.md)
