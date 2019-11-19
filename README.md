# Pinch 👌

Callback and promise based HTTP client that supports SSL pinning for React Native.

## Installation

Using NPM:
```
npm install react-native-pinch
```

Using Yarn:
```
yarn add react-native-pinch
```

## Automatically link

#### With React Native 0.60+

```shell
cd ios
pod install
```

## Adding certificates

Before you can make requests using SSL pinning, you first need to add your `.cer` files to your project's assets.

### Android

 - Place your `.cer` files under `android/src/main/assets/`. (You may have to create this directory in your project.)

### iOS

 - Place your `.cer` files in your iOS Project. Don't forget to add them in your `Build Phases > Copy Bundle Resources`, in Xcode.


## Example
*Examples are using the ES6 standard*

Requests can be made by using the `fetch(url[, config, [callback]])` method of Pinch.

### Using Promises
```javascript
import pinch from 'react-native-pinch';

pinch.fetch('https://my-api.com/v1/endpoint', {
  method: 'post',
  headers: { customHeader: 'customValue' },
  body: '{"firstName": "Jake", "lastName": "Moxey"}',
  timeoutInterval: 10000 // timeout after 10 seconds
  sslPinning: {
    cert: 'cert-file-name', // cert file name without the `.cer`
    certs: ['cert-file-name-1', 'cert-file-name-2'], // optionally specify multiple certificates
  }
})
  .then(res => console.log(`We got your response! Response - ${res}`))
  .catch(err => console.log(`Whoopsy doodle! Error - ${err}`))
```

### Using Callbacks
```javascript
import pinch from 'react-native-pinch';

pinch.fetch('https://my-api.com/v1/endpoint', {
  method: 'post',
  headers: { customHeader: 'customValue' },
  body: '{"firstName": "Jake", "lastName": "Moxey"}',
  timeoutInterval: 10000 // timeout after 10 seconds
  sslPinning: {
    cert: 'cert-file-name', // cert file name without the `.cer`
    certs: ['cert-file-name-1', 'cert-file-name-2'], // optionally specify multiple certificates
  }
}, (err, res) => {
  if (err) {
    console.error(`Whoopsy doodle! Error - ${err}`);
    return null;
  }
  console.log(`We got your response! Response - ${res}`);
})
```

### Skipping validation

```javascript
import pinch from 'react-native-pinch';

pinch.fetch('https://my-api.com/v1/endpoint', {
  method: 'post',
  headers: { customHeader: 'customValue' },
  body: '{"firstName": "Jake", "lastName": "Moxey"}',
  timeoutInterval: 10000 // timeout after 10 seconds
  sslPinning: {} // omit the `cert` or `certs` key, `sslPinning` can be ommited as well
})
```

## Response Schema
```javascript
{
  bodyString: '',

  headers: {},

  status: 200,

  statusText: 'OK'
}
```
