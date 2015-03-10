## Apple Watch Plugin for Apache Cordova

**Not ready for production use, work in progress**

If you're interested in this plugin, please [contact me](http://ilee.co.uk/contact-me/).

## Install

```
cordova plugin add https://github.com/leecrossley/cordova-plugin-apple-watch.git
```

You **do not** need to reference any JavaScript, the Cordova plugin architecture will add a `applewatch` object to your root automatically when you build.

## Usage

### init

Initialises the Apple Watch interface, this must be called and the success handler fired before messages can be sent.

```js
applewatch.init(function successHandler(appGroupId) {}, errorHandler);
```

The `successHandler` is called with one arg `appGroupId` that was used in initialisation. The app bundleId will be used for identification by default, prefixed by "group.".

You can supply your own Application Group Id with the optional `appGroupId` argument, this should be in the format "group.com.company.app":

```js
applewatch.init(successHandler, errorHandler, appGroupId);
```

### sendMessage

Sends a message object to a specific queue (must be called after successful init).

Used to send strings or json objects to the Apple Watch extension.

```js
applewatch.sendMessage(successHandler, errorHandler, message, queueName);
```

### handleMessage

Handles a message object received on a specific queue (must be called after successful init).

Used to handle strings or json objects received from the Apple Watch extension.

```js
applewatch.handleMessage(messageHandler, queueName);
```

## Example

Basic example to send a message "test" to the "default" queue and get handled.

This example is iPhone -> iPhone.

```
var onMessageReceived = function (message) {
    alert("Message received: " + message);
};

var onInit = function (appGroupId) {
    alert(appGroupId);

    applewatch.handleMessage(onMessageReceived);

    setTimeout(function() {
        applewatch.sendMessage(null, null, "test");
    }, 1000)
};

applewatch.init(onInit);
```

## Platforms

iOS 8.2+ only.

## License

[MIT License](http://ilee.mit-license.org)
