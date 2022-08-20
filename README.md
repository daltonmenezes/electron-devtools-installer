Electron DevTools Installer
---------------------------
[![npm](https://img.shields.io/npm/v/dalonmenezes/electron-devtools-installer?style=for-the-badge&labelColor=1C1E26&color=61ffca)](https://www.npmjs.com/package/@daltonmenezes/electron-devtools-installer)
![npm](https://img.shields.io/npm/dt/@dalonmenezes/electron-devtools-installer?style=for-the-badge)
[![license](https://img.shields.io/github/license/daltonmenezes/electron-devtools-installer.svg?maxAge=2592000&style=for-the-badge&labelColor=1C1E26&color=61ffca)](https://github.com/daltonmenezes/electron-devtools-installer/blob/main/LICENSE)

This is an easy way to install DevTool extensions into Electron.  You shouldn't
have to mess around with downloading the extension, finding the right folder and
then configuring the path for everyone's machines.

## Features beyond the original repository
- Custom session partition support

## Install

```
npm i @daltonmenezes/electron-devtools-installer -D
```
or
```
yarn add @daltonmenezes/electron-devtools-installer -D
```

## Usage
All you have to do now is this in the **main** process of your application.

```js
import installExtension, { REACT_DEVELOPER_TOOLS } from '@daltonmenezes/electron-devtools-installer';

// Or if you can not use ES6 imports

/**
const { default: installExtension, REACT_DEVELOPER_TOOLS } = require('@daltonmenezes/electron-devtools-installer');
*/

const { app } = require('electron');

app.whenReady().then(() => {
  installExtension(REACT_DEVELOPER_TOOLS, {
      forceDownload: false,
      sessionId: 'persist:my-app', // custom session partition
      loadExtensionOptions: {
        allowFileAccess: true,
      },
    })
    .then((name) => console.log(`Added Extension:  ${name}`))
    .catch((err) => console.log('An error occurred: ', err));
});
```
To install multiple extensions, `installExtension` takes an array.

## What extensions can I use?

Technically you can use whatever extension you want.  Simply find the ChromeStore ID
of the extension you want to install, and call `installExtension('YOUR_ID_HERE')`.  We
offer a few extension ID's inside the package so you can easily import them to install without
having to find them yourselves.

```js
import installExtension, {
  EMBER_INSPECTOR, REACT_DEVELOPER_TOOLS,
  BACKBONE_DEBUGGER, JQUERY_DEBUGGER,
  ANGULARJS_BATARANG, VUEJS_DEVTOOLS,
  VUEJS3_DEVTOOLS, REDUX_DEVTOOLS,
  CYCLEJS_DEVTOOL, MOBX_DEVTOOLS,
  APOLLO_DEVELOPER_TOOLS,
} from '@daltonmenezes/electron-devtools-installer';
```

## How does it work?

Well, you know those steps over in the [Electron Docs](https://github.com/electron/electron/blob/master/docs/tutorial/devtools-extension.md)
that involve downloading, copying, checking paths, Etc.

This does all of that for you, it downloads the chrome extension directly from
the Chrome WebStore.  Then it extracts it to your applications `userData` directory
before loading it into Electron.

## Credits
- [Samuel Attard (author)](https://github.com/MarshallOfSound)
- [Dalton Menezes (this fork maintainer)](https://github.com/daltonmenezes)