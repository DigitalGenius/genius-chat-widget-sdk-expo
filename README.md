# genius-chat-expo

Digital Genius Chat Expo Module

# Installation in managed Expo projects

For [managed](https://docs.expo.dev/archive/managed-vs-bare/) Expo projects, please follow the installation instructions in the [API documentation for the latest stable release](#api-documentation). If you follow the link and there is no documentation available then this library is not yet usable within managed projects &mdash; it is likely to be included in an upcoming Expo SDK release.

# Installation in bare React Native projects

For bare React Native projects, you must ensure that you have [installed and configured the `expo` package](https://docs.expo.dev/bare/installing-expo-modules/) before continuing.

### Add the package to your npm dependencies

```
npm install genius-chat-expo
```

### Configure for iOS

Run `npx pod-install` after installing the npm package.


### Configure for Android


No additional setup necessary.

### Example

```JavaScript
export default function App() {
  useEffect(() => {
    const onWidgetEmbedded = DGChatModule.addOnWidgetEmbeddedListener(()=>{
      DGChatModule.launchWidget();
    });

    return () => onWidgetEmbedded.remove();
  }, []);

  DGChatModule.showDGChatView(
    "your_widget_id",
    "your_environment",
    {"generalSettings":{ "isChatLauncherEnabled" : true}, "locale" : "en-US"}, // optional custom configs
    "crm_platform", // optional
    "crm_version", // optional
  );
  return (
    <View style={styles.container}>
      <Text>Hello</Text>
    </View>
  );
}
```

### Additional Methods

You can use a set of additional methods to interact directly with Chat Widget. These methods are lised as a part of ``DGChatModule``.

The `sendMessage` method allows the customer to programmatically send a message on the user behalf. This method is not available once the user is handed over to a crm:

```JavaScript
function sendMessage(message: string)
```

The sendSystemMessage method allows the customer to programmatically send a system message to system. This method is only available after the chat has been embeded:

```JavaScript
function sendSystemMessage(payload: object)
```
For example:
```JavaScript
sendSystemMessage({
    "name" : "auth_token",
    "payload" : "your_jwt_token",
})
```
The `launchWidget` method allows the customer to programmatically launch the widget:

```JavaScript
function launchWidget()
```

The `initProactiveButtons` method allows the customer to programmatically trigger the proactive buttons to display:

```JavaScript
function initProactiveButtons(questions: Array<string>, answers: Array<string>)
```

The `hideDGChatView` method allows customer to hide the chat view:

```JavaScript
function hideDGChatView()
```

See [full methods list](https://docs.digitalgenius.com/docs/methods) for more details.



Contributions are very welcome! Please refer to guidelines described in the [contributing guide]( https://github.com/expo/expo#contributing).
