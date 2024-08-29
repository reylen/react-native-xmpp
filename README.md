# react-native-xmpp-z

An XMPP library for React Native.

A simple interface for native XMPP communication. Both iOS and Android are supported.

This version of XMPP remove 'XMPPFramework.h' file,  that's confict width the framework 'XMPPFramework'. So we remove it!

# 2020.11.30  update for react-native v0.63.2   change s.dependency 'React' to s.dependency "React-Core"
# 2021.11.18  update ios project file location, modify  RNXMPP   extends RCTEventEmitter
# 2021.11.19  修复1.1.5 src 问题
# 2022.12.21  修复iOS下 CocoaAsyncSocket 后台运行问题，ios16之后禁止socket后台
## Demo

XmppDemo uses a Flux approach (check its `XmppStore`) to communicate with a sample XMPP server, where 4 accounts were registered.

![demo-3](https://cloud.githubusercontent.com/assets/1321329/10537760/406affa6-73f4-11e5-986f-81a78adf129e.gif)

## Example

```js
var XMPP = require('react-native-xmpp-z');

// optional callbacks
XMPP.on('message', (message) => console.log('MESSAGE:' + JSON.stringify(message)));
XMPP.on('iq', (message) => console.log('IQ:' + JSON.stringify(message)));
XMPP.on('presence', (message) => console.log('PRESENCE:' + JSON.stringify(message)));
XMPP.on('error', (message) => console.log('ERROR:' + message));
XMPP.on('loginError', (message) => console.log('LOGIN ERROR:' + message));
XMPP.on('login', (message) => console.log('LOGGED!'));
XMPP.on('connect', (message) => console.log('CONNECTED!'));
XMPP.on('disconnect', (message) => console.log('DISCONNECTED!'));

// trustHosts (ignore self-signed SSL issues)
// Warning: Do not use this in production (security will be compromised).
XMPP.trustHosts(['chat.google.com']);

// connect
XMPP.connect(MYJID, MYPASSWORD);

// send message
XMPP.message('Hello world!', TOJID);

// disconnect
XMPP.disconnect();

// remove all event listeners (recommended on componentWillUnmount)
XMPP.removeListeners();

// remove specific event listener (type can be 'message', 'iq', etc.)
XMPP.removeListener(TYPE);
```

## Getting started

1. `yarn add react-native-xmpp-z`

Please be sure add 'use_framework!' in your podfile

Please use pod install, no link need any more!

### iOS


### Android

If rnpm doesn't link the react-native-xmpp correct:

**android/settings.gradle**

```gradle
include ':react-native-xmpp-z'
project(':react-native-xmpp-z').projectDir = new File(rootProject.projectDir, '../node_modules/react-native-xmpp-z/android')
```

**android/app/build.gradle**

```gradle
dependencies {
   ...
   compile project(':react-native-xmpp-z')
}
```

**MainApplication.java**

On top, where imports are:

```java
import rnxmpp.RNXMPPPackage;
```

Add the `ReactVideoPackage` class to your list of exported packages.

```java
@Override
protected List<ReactPackage> getPackages() {
    return Arrays.<ReactPackage>asList(
        new MainReactPackage(),
        new RNXMPPPackage()
    );
}
```
